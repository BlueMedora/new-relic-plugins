# New Relic Plugin for F5 BIG-IP

The **Blue Medora New Relic Plugin for F5 BIG-IP** allows you to monitor your F5 BIG-IP performance data from within the New Relic platform by pulling metrics in from the system and displaying them in a set of intuitive, graph-based monitoring dashboards.
				
This guide includes instructions for installing and configuring the Blue Medora New Relic Plugin for F5 BIG-IP.
If you’re having a bad experience with one of our plugins, please get in touch and we’ll be happy to help you out.

----

## System Requirements

The F5 BIG-IP plugin connects to the supported F5 BIG-IP System via a management IP address. Before installing and configuring the plugin, ensure your system meets the following requirements:

**New Relic Requirements**

- A New Relic account (Sign up for a free account [here](http://newrelic.com).)

**F5 BIG-IP Plugin Requirements**

- The plugin supports **F5 BIG-IP Version 11.5.0+** through REST
- Java 1.7 or higher
- **A Blue Medora License.** A trial license will ship with the plugin that is valid for 14 days. To obtain a production license or get pricing information for the plugin, please contact sales@bluemedora.com.

----

## Installing the Plugin

We recommend using the New Relic Platform Installer for installing and running your Blue Medora plugins for New Relic.

The New Relic Platform Installer (NPI) is a command line tool that helps you easily download, configure, and manage New Relic Platform Plugins.  For more information, refer to the [Installing an NPI-compatible plugin documentation](https://docs.newrelic.com/docs/plugins/plugins-new-relic/installing-plugins/installing-npi-compatible-plugin).

Once the NPI tool has been installed, run the following command:

```
  ./npi install com.bluemedora.f5.bigip
``` 

**Note:** This command will take care of the creation of `newrelic.json` and `plugin.json` files described in the [Configuring the Plugin](#Configuring-the-Plugin) section.

###### [Download Plugin for Manual Installation](https://newrelic-bluemedora.s3.amazonaws.com/com-bluemedora-f5bigip/newrelic_f5_bigip_plugin-2.1.1_20170817_152932.tar.gz)

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

**NOTE** You can add multiple objects to the “agents” array to monitor multiple F5 BIG-IP instances.

**NOTE:** Each object in the "agents" array should have a unique "instance_name".

**Fields**

| Field Name  |  Description |
|:------------- |:-------------|
| polling_interval_seconds | The number of seconds between each data collection. |
| downtime_tracking_minutes | The number of minutes into the past that will be considered when calculating downtime |
| instance_name | Alias for the name of your F5 BIG-IP instance that will appear in the User Interface |
| host | IP address or hostname of F5 BIG-IP Management IP |
| port | Port used to connect to the F5 BIG-IP REST API. Default is `443` |
| username | User Name for F5 BIG-IP login. |
| password | Password for F5 BIG-IP login. |
| exclude_nodes_and_pool_members | Indicates whether or not to collect node and pool member data. |
| exclude_relationships | Indicates whether or not to collect relationship data. |
| timeout | Length of time in seconds to attempt data collection at a given resource. |
| send_to_plugin | Indicates whether or not to send data to New Relic Plugins. See [Blue Medora's New Relic Knobs and Levers Readme](https://github.com/BlueMedora/new-relic-plugins/blob/master/configuration-variants/readme.md) for more details |
| send_to_insights | Indicates whether or not to send data to New Relic Insights. See [Blue Medora's New Relic Knobs and Levers Readme](https://github.com/BlueMedora/new-relic-plugins/blob/master/configuration-variants/readme.md) for more details |

**Examples**
```
{
  "polling_interval_seconds": 60,
  "downtime_tracking_minutes": 60,
  "agents": [
    {
      "instance_name": "your_value_here",
      "host": "your_value_here",
      "port": 443,
      "username": "your_value_here",
      "password": "your_value_here",
      "exclude_nodes_and_pool_members": "false" // Valid values: true, false ,
      "exclude_relationships": "false" //Valid values: true, false ,
      "timeout": 30,
      "send_to_plugin": {
        "big_ip_system": true,
        "disk": true,
        "module": true,
        "node": true,
        "pool": true,
        "pool_member": true,
        "virtual_server": true,
        "application": true,
        "device": true,
        "device_group": true
      },
      "send_to_insights": {
        "big_ip_system": true,
        "disk": true,
        "module": true,
        "node": true,
        "pool": true,
        "pool_member": true,
        "virtual_server": true,
        "application": true,
        "device": true,
        "device_group": true,
        "ssl-certificate": true,
        "relationships": true,
        "notifications": "INFO" //true, false, ERROR, WARNING, INFO, DEBUG
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
For questions or issues regarding the F5 BIG-IP Plugin for New Relic, visit http://support.bluemedora.com. 

----

## Metrics Source Documentation

**System Overview**

| Metric Name  |  Description |
|:------------- |:-------------|
| Memory (GB) |  The Used and Total memory of the F5 BIG-IP system |
| Node Received Throughput (MB/sec) |  Received throughput for Nodes |
| Node Transmitted Throughput (MB/sec) |  Transmitted throughput for Nodes  |
| Node Received Packets (packets/sec) |  Received packets for Nodes  |
| Node Transmitted Packets (packets/sec) |  Transmitted packets for Nodes  |
| Disk Total Space (GB)  |  Total space across disks in system  |
| Disk Used Space (GB)  |  Total used space across disks in system  |

**Disks**

| Metric Name  |  Description |
|:------------- |:-------------|
| Total Space (GB)  |  Total space across disks in system  |
| Used Space (GB)  |  Total used space across disks in system  |
| Free Space (GB)  |  Total free space across disks in system  |
| Reserved Space (GB)  |  Total reserved space across disks in system  |

**Modules**

| Metric Name  |  Description |
|:------------- |:-------------|
| Provisioned CPU (%)  |  Provisioned CPU across modules |
| Provisioned Disk Space (GB) |  Provisioned disk space across modules  |
| Provisioned Memory (GB)  |  Provisioned memory across modules |
| Provisioned Host Memory (GB) |  Provisioned host memory across modules  |

**Virtual Servers**

| Metric Name | Description |
|:------------- |:-------------|
| Requests (requests/sec) | Requests over time |
| Connections (connections) | Connections per virtual server |
| Received Throughput (MB/sec) | Received Throughput for virtual server |
| Transmitted Throughput (MB/sec) | Transmitted Throughput for virtual server |
| Received Packets (packets/sec) | Received Packets for virtual server |
| Transmitted Packets (packets/sec) | Transmitted Packets for virtual server |

**Nodes**

| Metric Name | Description |
|:------------- |:-------------|
| Requests (Requests/sec) | Requests over time |
| Connections (connections) | Connections per node |
| Received Throughput (MB/sec) | Received Throughput for node |
| Transmitted Throughput (MB/sec) | Transmitted Throughput for node |
| Received Packets (Packets/sec) | Received Packets for node |
| Transmitted Packets (Packets/sec) | Transmitted Packets for node |

**Pools**

| Metric Name | Description |
|:------------- |:-------------|
| Requests (requests/sec) | Requests over time |
| Active Members (members) | Currently active members |
| Connections (connections) | Connections per pools |
| Received Throughput (MB/sec) | Received Throughput for pools |
| Transmitted Throughput (MB/sec) | Transmitted Throughput for pools |
| Received Packets (packets/sec) | Received Packets for pools |
| Transmitted Packets (packets/sec) | Transmitted Packets for pools |

**Pools Members**

| Metric Name | Description |
|:------------- |:-------------|
| Requests (requests/sec) | Requests over time |
| Connections (connections) | Connections per pool members |
| Sessions (sessions) | Currently active session |
| Received Throughput (MB/sec) | Received Throughput for pool members |
| Transmitted Throughput (MB/sec) | Transmitted Throughput for pool members |
| Received Packets (packets/sec) | Received Packets for pool members |
| Transmitted Packets (packets/sec) | Transmitted Packets for pool members |

**Summary**

| Metric Name | Description |
|:------------- |:-------------|
| Total Received Throughput (bytes/sec) | Total received throughput across BIG-IP System |
| Total Transmitted Throughput (bytes/sec) | Total transmitted throughput across BIG-IP System |
| Average Connections per Node | The average number of current connections per node | 
| Average Connections per Pool | The average number of connections per pool |
| Downtime (%) | The percentage of times during the downtime tracking window during which the system has been unavailable |

