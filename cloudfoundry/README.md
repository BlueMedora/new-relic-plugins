# Blue Medora Cloud Foundry Plugin for New Relic

The **Blue Medora Cloud Foundry Plugin for New Relic** allows you to monitor your Cloud Foundry performance data from within the New Relic platform by pulling metrics in from the system and displaying them in a set of intuitive, graph-based monitoring dashboards.                       

This guide includes instructions for installing and configuring the Blue Medora Cloud Foundry Plugin for New Relic.
If you’re having a bad experience with one of our plugins, please get in touch and we’ll be happy to help you out.

----

## System Requirements

The Cloud Foundry plugin collects data by making requests to the Blue Medora Cloud Foundry Nozzle. Before installing and configuring the plugin, ensure your system meets the following requirements:

**New Relic Requirements**

- A New Relic account (Sign up for a free account [here](http://newrelic.com).)

**Cloud Foundry Plugin Requirements**

- Cloud Foundry
- Blue Medora Nozzle
- Java 1.7 or higher (NOTE: Java 1.8 is required if using Pivotal Cloud Foundry version 1.10 and deploying the Blue Medora Nozzle for PCF using version 1.2.1 of the Tile. See: https://docs.pivotal.io/partners/blue-medora/index.html.)
- **A Blue Medora License.** A trial license will ship with the plugin that is valid for 14 days. To obtain a production license or get pricing information for the plugin, please contact sales@bluemedora.com.

# Configuring the Blue Medora Firehose Nozzle
The Blue Medora Firehose Nozzle is a Cloud Foundry component that collects metrics from the Loggregator Firehose  and exposes them via a RESTful API. Before the nozzle can be configured, it must be deployed.

There are multiple ways to deploy the nozzle:

- Blue Medora Nozzle for PCF Tile method (requires Pivotal Cloud Foundry)
- Installing the nozzle via the Cloud Foundry Command Line Interface (cf-cli)
- Cloning the nozzle from the github repo and running it on any box that can connect to the Traffic Controller
- Installing the nozzle via the BOSH Command Line Interface (CLI)

**Prerequisites Blue Medora Nozzle for PCF Tile method**

- Download the Blue Medora Nozzle for PCF Tile from the Pivotal Network at: https://network.pivotal.io/, then follow the instructions for installing, configuring, and using the nozzle as documented on the Pivotal web site at: https://docs.pivotal.io/blue-medora/index.html

**Prerequisites CF App method**

- Install the Cloud Foundry Command Line Interface (cf-cli) available at: https://github.com/cloudfoundry/cli
- To deploy the nozzle, configure manifest.yml and run cf push to install the cf app as described  here: https://github.com/BlueMedora/bluemedora-firehose-nozzle#deploying-as-cf-app

**Cloning Deployment Method**

- Install the Go programming language (version 1.6+) on a box that can connect to the Traffic Controller
- To deploy the nozzle, run the following command, which clones the nozzle files and dependencies from the github repository and sets them up them in your Go environment:
```
go get github.com/BlueMedora/bluemedora-firehose-nozzle
```

**BOSH CLI Deployment Method**

- Install the BOSH Command Line Interface (CLI) using the BOSH release available at: https://github.com/BlueMedora/bluemedora-firehose-nozzle-release
- Deploy the nozzle as instructed in the following tutorial: https://docs.cloudfoundry.org/loggregator/nozzle-tutorial.html

**Procedure**
The following sections describe how to configure the nozzle once it has been deployed using one of the  methods mentioned above. For additional support, refer to the following reference material:

- For information on managing UAA users within Cloud Foundry, refer to the following guide: https://docs.cloudfoundry.org/adminguide/uaa-user-management.html
- For more information on setting up a nozzle user with BOSH, refer to the following tutorial: https://docs.cloudfoundry.org/loggregator/nozzle-tutorial.html
- For more information on setting up the BOSH manifest, refer to the following guide: https://bosh.io/docs/deployment-manifest.html
NOTE: For more information on how metrics are pulled from the Blue Medora Firehose Nozzle, refer to section 
“Webserver”.

**Configuring the UAA User**
Ensure the Cloud Foundry UAA user you plan to use is authorized to access the loggregator firehose and has doppler.firehose permissions. An example of one way to modify the UAA user involves editing your Cloud Foundry BOSH manifest under the properties.uaa.clients section.

An example configuration would look similar to the following:
```
properties:
    uaa:
        clients:
            bluemedora-firehose-nozzle:
                access-token-validity: 1209600
                authorized-grant-types: authorization_code,client_credentials,refresh_token
                override: true
                secret: <password>
                scope: openid,oauth.approvals,doppler.firehose
                authorities: oauth.login,doppler.firehose
```

**Configuring the Nozzle**
To configure the nozzle itself, which connects to the Cloud Foundry firehose and exposes a RESTful API, modify and re-save the configuration file, bluemedora-firehose-nozzle.json, located in the config folder of the nozzle files as follows:

**Blue Medora Firehose Nozzle Configuration Fields**

| Field Name | Description |
|:------------- |:-------------|
| UAAURL | The UAA login URL of the Cloud Foundry deployment. |
| UAAUsername | The UAA username that has access to read from Loggregator Firehose. |
| UAAPassword | Password for the UAA Username. |
| TrafficControllerURL | The URL for the Traffic Controller. To find the URL, follow the  instructions outlined here: https://docs.cloudfoundry.org/loggregator/architecture.html#firehose |
| SubscriptionID | The subscription ID of the nozzle. For more information about  subscription IDs and nozzle scaling, refer to: https://docs.cloudfoundry.org/loggregator/log-ops-guide.html#scaling-nozzles
| DisableAccessControl | If true, disables authentication with UAA. Used in lattice deployments. |
| InsecureSSLSkipVerify | If true, allows insecure connections to the UAA and Traffic Controller endpoints. |
| IdleTimeoutSeconds | The amount of time, in seconds, the connection to the Firehose can be  idle before disconnecting. |
| MetricCacheDurationSeconds | The amount of time, in seconds, the RESTful API web server will cache  metric data. The higher this duration, the less likely the data will be  correct for a certain metric as it could hold stale data. |
| WebServerPort | Port to connect to the RESTful API (default: 8081). |

An example configuration would look similar to the following:
```
{
    “UAAURL”: “https://uaa.pcf.envrioment.com”,     
    “UAAUsername”: “apps_metrics_processing”,     
    “UAAPassword”: “password”,     
    “TrafficControllerURL”: “wss://doppler.pcf.envrionment.com:443”,     
    “SubscriptionID”: “bluemedora-nozzle-id”,     
    “DisableAccessControl”: false,     
    “InsecureSSLSkipVerify”: true,     
    “IdleTimeoutSeconds”: 30,     
    “MetricCacheDurationSeconds”: 60,     
    “WebServerPort”: 8081
}
```

**Generating SSL Certificates**

The Blue Medora Nozzle uses SSL for its REST webserver. In order to generate these certificates, run the  following command answer the questions at the prompts:
```
openssl req -x509 -nodes -days 3650 -newkey rsa:2048 -keyout certs/key.pem -out certs/cert.pem
```

**Running the Nozzle**
Once you have deployed and configured the nozzle, you can run it using the following command:

```
go run main.go
```

**Webserver**
The webserver is how metrics are pulled out of the Blue Medora Firehose Nozzle. It provides a RESTful API that  requires an authentication token.

**Token Request**
A token can be requested from the /token endpoint. A token times out after 60 seconds. In order to request a  token, send a GET request with the two header pairs username and password with values that correspond to the  UAA user in the bluemedora-firehose-nozzle.json config file. If a successful login occurs, the response will  contain a header pair of token and the value will be your token. 
Metric Endpoints

Once a valid token is acquired, a GET request with the header pair token and value of your token can be sent to  one of the following endpoints:

- /metron_agents 
- /syslog_drains 
- /tps_watchers 
- /tps_listeners 
- /stagers 
- /ssh_proxies 
- /senders 
- /route_emitters 
- /reps 
- /receptors 
- /nsync_listeners 
- /nsync_bulkers 
- /garden_linuxs 
- /file_servers 
- /fetchers 
- /convergers 
- /cc_uploaders 
- /bbs 
- /auctioneers 
- /etcds 
- /doppler_servers 
- /cloud_controllers 
- /traffic_controllers
- /gorouters

A JSON response will be sent in the following form:
```
[    
    {
      “Deployment”:”deployment_name”,       
      “Job”:”job_name”,       
      “Index”:”0”,       
      “IP”:”X.X.X.X”,       
      “ValueMetrics”:{          
        “MetricName”:integer_value,          
        “MetricName”:integer_value       
        },       
        “CounterMetrics”:{          
            “MetricName”:integer_value,          
            “MetricName”:integer_value
        }    
    }
]
```

----

## Installing the Plugin

We recommend using the New Relic Platform Installer for installing and running your Blue Medora plugins for New Relic.

The New Relic Platform Installer (NPI) is a command line tool that helps you easily download, configure, and manage New Relic Platform Plugins.  For more information, refer to the [Installing an NPI-compatible plugin documentation](https://docs.newrelic.com/docs/plugins/plugins-new-relic/installing-plugins/installing-npi-compatible-plugin).

Once the NPI tool has been installed, run the following command:

```
    ./npi install com.bluemedora.cloudfoundry
``` 

**Note:** This command will take care of the creation of `newrelic.json` and `plugin.json` files described in the [Configuring the Plugin](#Configuring-the-Plugin) section.

###### [Download Plugin for Manual Installation](https://newrelic-bluemedora.s3.amazonaws.com/com-bluemedora-cloudfoundry/newrelic_cloudfoundry_plugin-2.0.2_20170727_151026.tar.gz)

----
    
## Configuring the Plugin
From the extracted plugin folder you receive when downloading your plugin, you will find the following files: 

```
  plugin.jar
  eula.txt
  oss_attribution.txt
  [config folder]
    newrelic.template.json
    plugin.template.json 
    plugin_license.json
```

The "template" .json files found in the config folder must be modified (i.e., customized) and renamed prior to setting up the plugin for monitoring.

### Configuring the `newrelic.template.json` file

The first file, `newrelic.template.json`, contains configurations used by all Platform plugins (e.g., license key, logging information, proxy settings) and can be shared across your plugins.
Make a copy of this template and rename it to `newrelic.json`. Listed below are the configurable fields within the newrelic.json file:

**New Relic License Key** - The only required field in the `newrelic.json` file is the License Key. This unique identifier informs New Relic about the specific account tied to the plugin. For more information on the License Key, [refer to the New Relic License key documentation](https://docs.newrelic.com/docs/accounts-partnerships/accounts/account-setup/license-key).

**Example:**

```
{
   “license_key”: “YOUR LICENSE KEY”
}
```

**Insights Configuration** - Blue Medora plugins support reporting events to New Relic Insights. 
In order to achieve this you need to supply your `insights_api_key` and `insights_account_id`. 
You can find these fields in on [your New Relic API Keys page](https://rpm.newrelic.com/apikeys). 
For more information, [refer to the New Relic Insights documentation](https://docs.newrelic.com/docs/insights/new-relic-insights/adding-querying-data/insert-custom-events-insights-api#register).

Below are the fields needed to configure Insights access.

`insights_api_key` - The api key associated with your Insights account.

`insights_account_id` - The ID associated with your Insights account.

`insights_use_ssl` - Signals whether to connect to Insights via SSL. Acceptable values are `true` or `false`.

**Example:**

```
{
    "license_key": "YOUR LICENSE KEY",
    "insights_api_key": "YOUR INSIGHTS API KEY",
    "insights_account_id": "YOUR INSIGHTS ACCOUNT ID",
    "insights_use_ssl": true
}
```

**Logging Configuration** - By default Platform plugins will have their logging turned on; however, you can modify these settings with the following configurations:

`log_level` - The log level. Valid values: [debug, info, warn, error, fatal]. Defaults to info.

`log_file_name` - The log file name. Defaults to newrelic_plugin.log.

`log_file_path` - The log file path. Defaults to logs.

`log_limit_in_kbytes` - The log file limit in kilobytes. Defaults to 25600 (25 MB). If limit is set to 0, the log file size would not be limited.

**Example:**

```
{
    "license_key": "YOUR LICENSE KEY",
    "log_level": "info",
    "log_file_name": "newrelic_plugin.log",
    "log_file_path": "logs",
}
```

**Proxy Configuration** - If you are running your plugin from a machine that runs outbound traffic through a proxy, you can use the following optional configurations in your `newrelic.json` file:

`proxy_host` - The proxy host (e.g. webcache.example.com)

`proxy_port` - The proxy port (e.g. 8080). Defaults to 80 if a proxy_host is set

`proxy_username` - The proxy username

`proxy_password` - The proxy password

**Example:**

```
{
  "license_key": "YOUR LICENSE KEY",
  "proxy_host": "proxy.mycompany.com",
  "proxy_port": 9000
}
```

### Configuring the `plugin.template.json` file: 

The second file, `plugin.template.json`, contains data specific to each plugin (e.g., a list of hosts and port combinations for what you are monitoring). Templates for both of these files should be located in the ‘config’ directory in your extracted plugin folder.

Make a copy of this template and rename it to `plugin.json`. Shown below is an example of the `plugin.json` file’s contents.


**NOTE:** Each object in the "agents" array should have a unique "instance_name".

**Fields**

| Field Name | Description |
|:------------- |:-------------|
| polling_interval_seconds | The number of seconds between each data collection. |
| instance_name | The name of your New Relic Cloud Foundry instance that will appear in the user interface |
| username | User name to log into the Blue Medora Nozzle |
| password | Password to log into the Blue Medora Nozzle |
| host | The hostname or ip address of the Blue Medora Nozzle |
| validate_certificate_against_truststore | whether or not to Validate The Certificate Against the Trust Store, `true` or `false`. |
| port | Optional parameter, port to connect to. Defaults to `443` if not present |
| send_to_plugin | Indicates whether or not to send data to New Relic Plugins. See [Blue Medora's New Relic Knobs and Levers Readme](https://github.com/BlueMedora/new-relic-plugins/blob/master/configuration-variants/readme.md) for more details |
| send_to_insights | Indicates whether or not to send data to New Relic Insights. See [Blue Medora's New Relic Knobs and Levers Readme](https://github.com/BlueMedora/new-relic-plugins/blob/master/configuration-variants/readme.md) for more details |

**Example**

```
{
  "polling_interval_seconds": 60,
  "agents": [
    {
      "instance_name": "your_value_here",
      "username": "your_value_here",
      "password": "your_value_here",
      "host": "your_value_here",
      "port": 443,
      "validate_certificate_against_truststore": true,
      "send_to_plugin": {
        "access": true,
        "brain": true,
        "cell": true,
        "cloud_controller": true,
        "ccbridge": true,
        "consul": true,
        "database": true,
        "doppler_server": true,
        "gorouter": true,
        "syslog_drain_binder": true,
        "traffic_controller": true
      },
      "send_to_insights": {
        "access": true,
        "brain": true,
        "cell": true,
        "cloud_controller": true,
        "ccbridge": true,
        "consul": true,
        "database": true,
        "doppler_server": true,
        "gorouter": true,
        "syslog_drain_binder": true,
        "traffic_controller": true,
        "relationships": true,
        "notifications": "INFO"
      }
    }
  ]
}
```

## Using the Plugin
For more information about navigating New Relic’s user interface, refer to their [Using a plugin documentation](https://docs.newrelic.com/docs/plugins/plugins-new-relic/using-plugins/using-plugin) section.

## Troubleshooting/Known Issues
#### java.lang.OutOfMemoryError

When running a plugin, a `java.lang.OutOfMemoryError` may occur if too much data is being processed for the system to handle. If that issues arises, you will need to modify the `java_args` field of the “master” `newrelic.json` file located in the npi base `config` directory.

`java_args` - `-Xmx128m` (-Xmxn specifies the maximum size, in bytes, of the memory allocation pool. This value must a multiple of 1024 greater than 2 MB. Append the letter k or K to indicate kilobytes, or m or M to indicate megabytes. The default value is chosen at runtime based on system configuration.)

- **Examples:**

- `-Xmx83886080`

- `-Xmx81920k`

- `-Xmx80m`



#### FATAL ERROR: JS Allocation failed - process out of memory

If you see `FATAL ERROR: JS Allocation failed - process out of memory` during installation, edit newrelic-npi/npi replacing `bin/node npi.js "$@"` with `bin/node --max-old-space-size=4096 npi.js "$@" #modified for 4gb memory`

----

## Support Resources
For questions or issues regarding the Blue Medora Cloud Foundry Plugin for New Relic, visit http://support.bluemedora.com. 

----     

## Metrics Source Documentation

**Overview**

| Metric Name  |  Description |
|:------------- |:-------------|
| GoRouter Request Rates (requests/second) | The Requests Rate for each monitored GoRouter |
| Diego Brain Auction Rates (auctions/second) | All auction rates associated with the Diego Brain resources |
| Diego Cell Used Memory (GB) | All Used Memory data associated with the Diego Cell resource |
| Diego Cell Active Goroutines (GB) | All Active Goroutine data associated with the Diego Cell resource |

**Access**

| Metric Name  |  Description |
|:------------- |:-------------|
| File Server Used Memory (MB) | The File Server Used Memory for each monitored Access |
| SSH Proxy Used Memory (MB) | The SSH Proxy Used Memory for each monitored Access |
| File Server Active Goroutines (routines) | The File Server Active Goroutines for each monitored Access |
| SSH Proxy Active Goroutines (routines) | The SSH Proxy Active Goroutines for each monitored Access |
| File Server Memory Allocation Rates (allocations/second) | The File Server Memory Allocation Rates for each monitored Access |
| SSH Proxy Memory Allocation Rates (allocations/second) | The SSH Proxy Memory Allocation Rates for each monitored Access |
| File Server Active Memory Deallocation Rates (deallocations/second) | The File Server Memory Deallocation Rates for each monitored Access |
| SSH Proxy Active Memory Deallocation Rates (deallocations/second) | The SSH Proxy Memory Deallocation Rates for each monitored Access |

**Cloud Controllers**

| Metric Name  |  Description |
|:------------- |:-------------|
| Used Memory (%) | The Used Memory for each monitored Cloud Controller |
| CPU Usage (%) | The CPU Usage for each monitored Cloud Controller |
| Outstanding Requests Rates (requests/second) | The Outstanding Requests Rate for each monitored Cloud Controller |
| Completed Requests Rates (requests/second) | The Completed Requests Rate for each monitored Cloud Controller |
| Thread Result Scheduled Tasks (tasks) | The Thread Result Scheduled Tasks for each monitored Cloud Controller |
| Thread Result Unscheduled Tasks (tasks) | The Thread Result Unscheduled Tasks for each monitored Cloud Controller |
| Thread Scheduled Tasks (tasks) | The Thread Scheduled Tasks for each monitored Cloud Controller |
| Thread Unscheduled Tasks (tasks) | The Thread Unscheduled Tasks for each monitored Cloud Controller |
| Running Tasks (tasks) | The Running Tasks for each monitored Cloud Controller |
| Delayed Jobs (jobs) | The Delayed Jobs for each monitored Cloud Controller |
| Failed Jobs (jobs) | The Failed Jobs for each monitored Cloud Controller |

**Diego Brain**

| Metric Name  |  Description |
|:------------- |:-------------|
| Auctioneer Used Memory (MB) | The Auctioneer Used Memory for each monitored Diego Brain |
| Converger Used Memory (MB) | The Converger Used Memory for each monitored Diego Brain |
| Route Emitter Used Memory (MB) | The Route Emitter Used Memory for each monitored Diego Brain |
| Auctioneer Active Goroutines (routines) | The Auctioneer Active Goroutines for each monitored Diego Brain |
| Converger Active Goroutines (routines) | The Converger Active Goroutines for each monitored Diego Brain |
| Route Emitter Active Goroutines (routines) | The Route Emitter Active Goroutines for each monitored Diego Brain |
| Auctioneer Memory Allocation Rates (allocations/second) | The Auctioneer Memory Allocation Rates for each monitored Diego Brain |
| Converger Memory Allocation Rates (allocations/second) | The Converger Memory Allocation Rates for each monitored Diego Brain |
| Route Emitter Memory Allocation Rates (allocations/second) | The Route Emitter Memory Allocation Rates for each monitored Diego Brain |
| Auctioneer Memory Deallocation Rates (deallocations/second) | The Auctioneer Memory Deallocation Rates for each monitored Diego Brain |
| Converger Memory Deallocation Rates (deallocations/second) | The Converger Memory Deallocation Rates for each monitored Diego Brain |
| Route Emitter Memory Deallocation Rates (deallocations/second) | The Route Emitter Memory Deallocation Rates for each monitored Diego Brain |
| Route Emitter Registered Route Rates (routes/second) | The Route Emitter Registered Route Rates for each monitored Diego Brain |
| Route Emitter Synced Route Rates (routes/second) | The Route Emitter Synced Route Rates for each monitored Diego Brain |
| Route Emitter Total Route Rates (routes/second) | The Route Emitter Total Route Rates for each monitored Diego Brain |
| Route Emitter Unregistered Route Rates (routes/second) | The Route Emitter Unregistered Route Rates for each monitored Diego Brain |
| Auctioneer Cumulative LRP Auctions Failed Rate (auctions/second) | The Auctioneer Cumulative LRP Auctions Failed Rate for each monitored Diego Brain |
| Auctioneer Cumulative LRP Auctions Started Rate (auctions/second) | The Auctioneer Cumulative LRP Auctions Started Rate for each monitored Diego Brain |
| Auctioneer Cumulative Task Auctions Failed Rate (auctions/second) | The Auctioneer Cumulative Task Auctions Failed Rate for each monitored Diego Brain |
| Auctioneer Cumulative Task Auctions Started Rate (auctions/second) | The Auctioneer Cumulative Task Auctions Started Rate for each monitored Diego Brain |

**Diego Cell**

| Metric Name  |  Description |
|:------------- |:-------------|
| REP Disk Usage (%) | The REP Disk Usage for each monitored Diego Cell |
| Used Memory (MB) | The Used Memory for each monitored Diego Cell |
| Active Goroutines (routines) | The Active Goroutines for each monitored Diego Cell |
| Memory Allocation Rates (allocations/second) | The Memory Allocation Rates for each monitored Diego Cell |
| Memory Deallocation Rates (deallocations/second) | The Memory Deallocation Rates for each monitored Diego Cell |
| REP Used Memory (MB) | The REP Used Memory for each monitored Diego Cell |
| Garden Used Memory (MB) | The Garden Used Memory for each monitored Diego Cell |
| REP Active Goroutines (routines) | The REP Active Goroutines for each monitored Diego Cell |
| Garden Active Goroutines (routines) | The Garden Active Goroutines for each monitored Diego Cell |
| REP Memory Allocation Rates (allocations/second) | The REP Memory Allocation Rates for each monitored Diego Cell |
| Garden Memory Allocation Rates (allocations/second) | The Garden Memory Allocation Rates for each monitored Diego Cell |
| REP Memory Deallocation Rates (deallocations/second) | The REP Memory Deallocation Rates for each monitored Diego Cell |
| Garden Memory Deallocation Rates (deallocations/second) | The Garden Memory Deallocation Rates for each monitored Diego Cell |


**Gorouters**

| Metric Name  |  Description |
|:------------- |:-------------|
| Used Memory (MB) | The Used Memory for each monitored Gorouter |
| Active Goroutines (routines) | The Active Goroutines for each monitored Gorouter |
| Memory Allocation Rates (allocations/second) | The Memory Allocation Rates for each monitored Gorouter |
| Memory Deallocation Rates (deallocations/second) | The Memory Deallocation Rates for each monitored Gorouter |
| Requests Rates (requests/second) | The Requests Rate for each monitored GoRouter |
| HTTP Responses Rates (responses/second) | The HTTP Responses Rate for each monitored GoRouter |
