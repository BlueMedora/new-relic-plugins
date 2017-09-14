# Blue Medora MongoDB Plugin for New Relic

The **Blue Medora MongoDB Plugin for New Relic** allows you to monitor your MongoDB performance data from within the New Relic platform by pulling metrics in from the system and displaying them in a set of intuitive, graph-based monitoring dashboards.                       

This guide includes instructions for installing and configuring the Blue Medora MongoDB Plugin for New Relic.
If you’re having a bad experience with one of our plugins, please get in touch and we’ll be happy to help you out.

----

## System Requirements

The MongoDB plugin collects data by connecting to the Java MongoDB Driver. Before installing and configuring the plugin, ensure your system meets the following requirements:

**New Relic Requirements**

- A New Relic account (Sign up for a free account [here](http://newrelic.com).)

**MongoDB Plugin Requirements**

- MongoDB 3.0+ (3.0, 3.2)
- Java 1.7 or higher
- **A Blue Medora License.** A trial license will ship with the plugin that is valid for 14 days. To obtain a production license or get pricing information for the plugin, please contact sales@bluemedora.com.

----
## Access Rights
**Connection information**
- The plugin collects data from **MongoDB database** via the **Mongo Client**.

- Your **MongoDB hostname** (or IP address) is required.
A comma-seperated list of multiple hosts (mongos/mongod instances) in an environment is supported.

- In addition, **if using a port other than the default of 27017**, you can append the non-standard port number to the hostname. 
**NOTE:** Internet Protocol version 4 (IPv4) is supported for IP addresses.

**User Privileges**
- **MongoDB User Name/Password** for the admin database.

- The **same User Name/Password** must exist for all mongos/mongods in your environment.

- Ensure a least privileged MongoDB user account of **read-only**.

-----
## Installing the Plugin

We recommend using the New Relic Platform Installer for installing and running your Blue Medora plugins for New Relic.

The New Relic Platform Installer (NPI) is a command line tool that helps you easily download, configure, and manage New Relic Platform Plugins.  For more information, refer to the [Installing an NPI-compatible plugin documentation](https://docs.newrelic.com/docs/plugins/plugins-new-relic/installing-plugins/installing-npi-compatible-plugin).

Once the NPI tool has been installed, run the following command:

```
    ./npi install com.bluemedora.mongo.mongodb
``` 

**Note:** This command will take care of the creation of `newrelic.json` and `plugin.json` files described in the [Configuring the Plugin](#Configuring-the-Plugin) section.

###### [Download Plugin for Manual Installation](https://newrelic-bluemedora.s3.amazonaws.com/com-bluemedora-mongo/newrelic_mongo_mongodb_plugin-2.1.4_20170801_140528.tar.gz)

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
| downtime_tracking_minutes | The number of minutes into the past that will be considered when calculating downtime |
| instance_name | The name of your New Relic MongoDB instance that will appear in the user interface |
| validate_certificate_against_truststore | Specifies whether or not to Validate The Certificate Against the Trust Store, `true` or `false`. |
| host | The hostname(s) or ip address(es) of the Java MongoDB Driver, for example, `host` or `host1,host2:443` |
| connecting_to | Specifies whether the connection is to a mongod or mongos, for example `mongos`, `mongod` |
| ssl_mongos | Optional parameter, whether or not to use SSL for Mongos, `true` or `false`. |
| auth_mongos | Optional parameter, Authentication Type `default` or `LDAP SASL`.|
| username_mongos | Optional parameter, User name to log into the Mongos |
| password_mongos | Optional parameter, Password to log into the Mongos |
| ssl_mongod | Optional parameter, whether or not to use SSL for Mongod, `true` or `false`. |
| auth_mongod | Optional parameter, Authentication Type `default` or `LDAP SASL`.|
| username_mongod | Optional parameter, User name to log into the Mongod |
| password_mongod | Optional parameter, Password to log into the Mongod |
| send_to_plugin | Indicates whether or not to send data to New Relic Plugins. See [Blue Medora's New Relic Knobs and Levers Readme](https://github.com/BlueMedora/new-relic-plugins/blob/master/configuration-variants/readme.md) for more details |
| send_to_insights | Indicates whether or not to send data to New Relic Insights. See [Blue Medora's New Relic Knobs and Levers Readme](https://github.com/BlueMedora/new-relic-plugins/blob/master/configuration-variants/readme.md) for more details |

**Example**

```
{
  "polling_interval_seconds": 60,
  "downtime_tracking_minutes": 60,
  "agents": [
    {
      "instance_name": "your_value_here",
      "host": "your_value_here",
      "connecting_to": "mongos",
      "validate_certificate_against_truststore": false,
      "ssl_mongos": false,
      "auth_mongos": "your_value_here",
      "username_mongos": "your_value_here",
      "password_mongos": "your_value_here",
      "ssl_mongod": true,
      "auth_mongod": "default",
      "username_mongod": "your_value_here",
      "password_mongod": "your_value_here",
      "send_to_plugin": {
        "mongo_summary": true,
        "mongo_database": true,
        "mongod": true,
        "mongos": true
      },
      "send_to_insights": {
        "mongo_summary": true,
        "mongo_database": true,
        "mongod": true,
        "mongos": true,
        "cluster": true,
        "config_server": true,
        "replica_set": true,
        "shard": true,
        "relationships": true,
        "notifications": "INFO"
      }
    },
    {
      "instance_name": "your_value_here",
      "host": "host1,host2:443",
      "connecting_to": "mongod",
      "validate_certificate_against_truststore": false,
      "ssl_mongos": false,
      "auth_mongos": "",
      "username_mongos": "",
      "password_mongos": "",
      "ssl_mongod": true,
      "auth_mongod": "ldap sasl",
      "username_mongod": "your_value_here",
      "password_mongod": "your_value_here",
      "send_to_plugin": {
        "mongo_summary": true,
        "mongo_database": true,
        "mongod": true,
        "mongos": true
      },
      "send_to_insights": {
        "mongo_summary": true,
        "mongo_database": true,
        "mongod": true,
        "mongos": true,
        "cluster": true,
        "config_server": true,
        "replica_set": true,
        "shard": true,
        "relationships": true,
        "notifications": false
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
For questions or issues regarding the Blue Medora MongoDB Plugin for New Relic, visit http://support.bluemedora.com. 

----     

## Metrics Source Documentation

**Mongo Databases**

| Metric Name  |  Description |
|:------------- |:-------------|
| Average Object Size (bytes)  | The Average Object Size for each monitored Mongo Database |
| Collection Size (MB)  | The Collection Size for each monitored Mongo Database |
| Number of Extents (extents) | The Number of Extents for each monitored Mongo Database |
| Number of Indexes (indexes) | The Number of Indexes for each monitored Mongo Database |


**Mongo Mongods**

| Metric Name  |  Description |
|:------------- |:-------------|
| Current Connections (connections)  | The Number of Current Connections for each monitored Mongo Mongod |
| Network Request Rate (requests/second)  | The Network Request Rate for each monitored Mongo Mongod |
| Inbound Network Throughput (bytes/second) | The Inbound Network Throughput for each monitored Mongo Mongod |
| Outbound Network Throughput (bytes/second) | The Outbound Network Throughput for each monitored Mongo Mongod |
| Resident Memory (MB) | The Resident Memory for each monitored Mongo Mongod |
| Virtual Memory (MB) | The Virtual Memory for each monitored Mongo Mongod |
| Cache Size (MB) | The Cache Size for each monitored Mongo Mongod |
| Page Faults (faults/second) | The Page Faults for each monitored Mongo Mongod |

**Mongos Instances**

| Metric Name  |  Description |
|:------------- |:-------------|
| Inbound Network Throughput (bytes/second) | The Inbound Network Throughput for each monitored Mongo Mongos |
| Outbound Network Throughput (bytes/second) | The Outbound Network Throughput for each monitored Mongo Mongos |
| Network Request Rate (requests/second)  | The Network Request Rate for each monitored Mongo Mongos |
| Page Faults (faults/second) | The Page Faults for each monitored Mongo Mongos |
| Resident Memory (MB) | The Resident Memory for each monitored Mongo Mongos |
| Virtual Memory (MB) | The Virtual Memory for each monitored Mongo Mongos |
| Current Connections (connections)  | The Number of Current Connections for each monitored Mongo Mongos |
| Available Connections (connections)  | The Number of Available Connections for each monitored Mongo Mongos |


**Summary**

| Metric Name  |  Description |
|:------------- |:-------------|
| Downtime (%) | The percentage of times during the downtime tracking window during which the system has been unavailable |
| Average Uptime | The average up time across all mongods |
| Total Current Connections | The total number of current connections |
| Total Extents | The total number of Extents across all mongo databases | 
| Total Indexes | The total number of Indexes across all mongo databases | 
