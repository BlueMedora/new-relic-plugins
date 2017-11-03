# New Relic Plugin for Microsoft Azure SQL Database

The **Blue Medora New Relic Plugin for Microsoft Azure SQL Database** allows you to monitor your Microsoft Azure SQL Database performance data from within the New Relic platform by pulling metrics in from the system and displaying them in a set of intuitive, graph-based monitoring dashboards.
				
This guide includes instructions for installing and configuring the Blue Medora Microsoft Azure SQL Database Plugin for New Relic. 
If you’re having a bad experience with one of our plugins, please get in touch and we’ll be happy to help you out.

----

## System Requirements

The Microsoft Azure SQL Database plugin connects to a Azure SQL Database via account access keys and JDBC. Before installing and configuring the plugin, ensure your system meets the following requirements:

**New Relic Requirements**

- A New Relic account. (Sign up for a free account [here](http://newrelic.com).)

**Microsoft Azure SQL Database Plugin Requirements**

- Java 1.7 or higher
- **A Blue Medora License.** A trial license will ship with the plugin that is valid for 14 days. To obtain a production license or get pricing information for the plugin, please contact sales@bluemedora.com.

----

## Installing the Plugin

We recommend using the New Relic Platform Installer for installing and running your Blue Medora plugins for New Relic.

The New Relic Platform Installer (NPI) is a command line tool that helps you easily download, configure, and manage New Relic Platform Plugins.  For more information, refer to the [Installing an NPI-compatible plugin documentation](https://docs.newrelic.com/docs/plugins/plugins-new-relic/installing-plugins/installing-npi-compatible-plugin).

Once the NPI tool has been installed, run the following command:

```
  ./npi install com.bluemedora.microsoft.azure.database
``` 

**NOTE:** This command will take care of the creation of `newrelic.json` and `plugin.json` files described in the [Configuring the Plugin](#Configuring-the-Plugin) section.

###### [Download Plugin for Manual Installation]()

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

The second file, `plugin.template.json`, contains data specific to each plugin (e.g., a list of hosts and port combinations for what you are monitoring). Templates for both of these files should be located in the `config` directory in your extracted plugin folder.

Make a copy of this template and rename it to `plugin.json`. Shown below is an example of the `plugin.json` file’s contents.

**NOTE** You can add multiple objects to the “agents” array to monitor multiple Microsoft Azure SQL Database instances.

**NOTE:** Each object in the "agents" array should have a unique `instance_name`.

**NOTE:** In order to gather all metrics, you need to have one `azure_jdbc` and one `azure` component setup for **EACH** `instance_name`.

**NOTE:** Do not change `component_type` or `component_name`, no matter the number of instances that you have.

**Fields For Azure JDBC**

| Field Name  |  Description |
|:------------- |:-------------|
| instance_name | Alias for the name of your Microsoft Azure SQL Database instance that will appear in the User Interface |
| username | The username being used to connect to your SQL Database |
| host | The hostname or IP Address of the SQL Database you are connecting to |
| password | The password of the username specified above |
| query_count_per_database | The number of queries you would like to retrieve during collection per database |
| exclude_events | Set to True if you do not want Azure SQL Database events returned as part of the data collection |
| send_to_plugin | Indicates whether or not to send data to New Relic Plugins. See [Blue Medora's New Relic Knobs and Levers Readme](https://github.com/BlueMedora/new-relic-plugins/blob/master/configuration-variants/readme.md) for more details |
| send_to_insights | Indicates whether or not to send data to New Relic Insights. See [Blue Medora's New Relic Knobs and Levers Readme](https://github.com/BlueMedora/new-relic-plugins/blob/master/configuration-variants/readme.md) for more details |

**Fields For Azure**

| Field Name  |  Description |
|:------------- |:-------------|
| instance_name | Alias for the name of your Microsoft Azure SQL Database instance that will appear in the User Interface |
| subscription_id | Your Microsoft Azure GUID Subscription ID |
| tenant_id | Your Microsoft Azure Tenant ID |
| client_id | Your Microsoft Azure Client ID |
| max_threads | Used to specify the maximum number of threads to return per collection cycle. |
| send_to_plugin | Indicates whether or not to send data to New Relic Plugins. See [Blue Medora's New Relic Knobs and Levers Readme](https://github.com/BlueMedora/new-relic-plugins/blob/master/configuration-variants/readme.md) for more details |
| send_to_insights | Indicates whether or not to send data to New Relic Insights. See [Blue Medora's New Relic Knobs and Levers Readme](https://github.com/BlueMedora/new-relic-plugins/blob/master/configuration-variants/readme.md) for more details |

**Example**

```
{
  "polling_interval_seconds": 300,
  "downtime_tracking_minutes": 60, 
  "agents": [
    {
      "instance_name": "your_value_here",
      "component_type": "azure_jdbc",
      "component_name": "Azure SQL Database",
      "username": "your_value_here",
      "host": "your_value_here",
      "password": "your_value_here",
      "query_count_per_database": 10,
      "exclude_events": false,
      "send_to_plugin": {
        "database": true,
        "geo_replication_database": false,
        "object": true,
        "query": true,
        "server": true
      },
      "send_to_insights": {
        "server": true,
        "relationships": true,
        "query": true,
        "notifications": "true or false or ERROR or WARNING or INFO or DEBUG",
        "object": true,
        "geo_replication_database": true,
        "database": true
      }
    },
    {
      "instance_name": "your_value_here",
      "component_type": "azure",
      "component_name": "Azure",
      "subscription_id": "your_value_here",
      "tenant_id": "your_value_here",
      "client_id": "your_value_here",
      "secret": "your_value_here",
      "max_threads": "1",
      "send_to_plugin": {
        "elastic_pool": true,
        "resource_group": false,
        "sql_data_warehouse": false,
        "sql_database": true,
        "sql_server": true,
        "virtual_machine": true
      },
      "send_to_insights": {
        "elastic_pool": true,
        "resource_group": true,
        "sql_data_warehouse": true,
        "sql_database": true,
        "sql_server": true,
        "virtual_machine": true,
        "relationships": true,
        "notifications": "true or false or ERROR or WARNING or INFO or DEBUG"
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
For questions or issues regarding the Microsoft Azure SQL Database Plugin for New Relic, visit http://support.bluemedora.com. 

----

## Metrics Source Documentation     

**Overview**

| Metric Name  |  Description |
|:------------- |:------------|
| Active Server Connections (connections) | The total number of active connections across databases on the server |
| Query Top 10 Execution (executions/min) | Number of times that the plan has been executed since it was last compiled |

**Elastic Pools**

| Metric Name  |  Description |
|:------------- |:------------|
| CPU Usage (%) | Percentage of CPU in use by the Elastic Pool |
| DTU Consumption (%) | Percentage of Database Transaction Units consumed by the Elastic Pool |
| Dato I/O (%) | Physical data read percentage of the Elastic Pool |
| Database Count (databases) | Number of databases used by the Elastic Pool |
| Active Session Usage (%) | Percentage of concurrent sessions in use. The maximum is determined by the service tier |
| Storage Size (bytes) | Storage size, in bytes, of the Elastic Pool |


**Virtual Machines**

| Metric Name  |  Description |
|:------------- |:------------|
| CPU Usage (%) | Percentage of CPU in use by the Virtual Machine |
| Network In (bytes/sec) | Bytes per second received by the Virtual Machine |
| Network Out (bytes/sec) | Bytes per second sent by the Virtual Machine |
| Data Read (bytes/sec) | Bytes per second read from disk by the Virtual Machine |
| Data Written (bytes/sec) | Bytes per second written to disk by the Virtual Machine | 
| Disk Reads (operations/sec) | Rate of disk read operations performed by the Virtual Machine |
| Disk Writes (operations/sec) | Rate of disk write operations performed by the Virtual Machine |

**SQL Servers**

| Metric Name  |  Description |
|:------------- |:------------|
| Average CPU Usage (%) | Average CPU usage by databases on the SQL Server |
| Average DTUs (units) | Average Database Transaction Units used by databases on the SQL Server |
| Average Database Size (bytes) | Average size in bytes of databases on the SQL Server |
| Average Concurrent Sessions (%) | Percentage of concurrent sessions in use. The maximum is determined by the service tier |
| Average Concurrent Requests (%) | Percentage of concurrent workers (requests) which are running. The maximum is determined by the service tier |
| Average Data I/O Usage (%) | Average physical data read percentage of databases on the SQL Server |
| Average Log I/O Usage (%) | Average log write percentage of databases on the SQL Server |

**SQL Databases**

| Metric Name  |  Description |
|:------------- |:------------|
| Buffer Pool Size (bytes) | Total size of the buffer pool for a database |
| Active Connections (connections) | The number of active connections to the database |
| Storage Usage (%) | Percentage of storage being used by the SQL Database |
| Database Size (bytes) | Size, in bytes, of the SQL Database |
| DTU Usage (%) | Percentage of Database Transaction Units consumed by the SQL Database |
| Failed Connections (connections) | Number of failed connections to the SQL Database  |
| Deadlocks (deadlocks) | Number of deadlocks in the SQL Database |

**Queries**

| Metric Name  |  Description |
|:------------- |:-------------|
| Average Execution Time (seconds) | The average execution time for the query |
| Execution Time (seconds/min) | Total amount of CPU time consumed by executions of this plan since it was compiled |
| Execution Count (executions/min) | Number of times that the plan has been executed since it was last compiled |

**Database Locks**

| Metric Name  |  Description |
|:------------- |:-------------|
| Top 10 Average Page Lock Wait Duration (seconds) | Average number of milliseconds the Database Engine waited on a page lock |
| Top 10 Page Locks (locks/sec) | Cumulative number of page locks requested |
| Top 10 Average Row Lock Wait Duration (seconds) | Average number of milliseconds the Database Engine waited on a row lock |
| Top 10 Row Locks (locks/sec) | Cumulative number of row locks requested |

**Summary**

| Metric Name  |  Description |
|:------------- |:-------------|
| Plugin Downtime (%) | The percentage of times during the downtime tracking window during which the system has been unavailable |
| Average Storage Utilized (%) | Average percentage of storage being used across all the SQL Databases within your instance |
| Average Buffer Pool Size (bytes) | Average total size of the buffer pools for your databases within your instance |
| Average DTU Consumption (%) | Average percentage of Database Transaction Units consumed by the Elastic Pools in your instance |


