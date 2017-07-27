# Blue Medora IBM DB2 Plugin for New Relic

The **Blue Medora IBM DB2 Plugin for New Relic** allows you to monitor your DB2 performance data from within the New Relic platform by pulling metrics in from the system and displaying them in a set of intuitive, graph-based monitoring dashboards.						

This guide includes instructions for installing and configuring the Blue Medora IBM DB2 Plugin for New Relic.
If you’re having a bad experience with one of our plugins, please get in touch and we’ll be happy to help you out.

----

## System Requirements

The IBM DB2 Plugin connects to a DB2 database using a JDBC connection. Before installing and configuring the plugin, ensure your system meets the following requirements:

**New Relic Requirements**

- A New Relic account (Sign up for a free account [here](http://newrelic.com).)

**IBM DB2 Plugin Requirements**

- **IBM DB2 Version:** This plugin requires IBM DB2 versions 9.5+
- Java 1.7 or higher
- **A Blue Medora License.** A trial license will ship with the plugin that is valid for 14 days. To obtain a production license or get pricing information for the plugin, please contact sales@bluemedora.com.

----

## Installing the Plugin

We recommend using the New Relic Platform Installer for installing and running your Blue Medora plugins for New Relic.

The New Relic Platform Installer (NPI) is a command line tool that helps you easily download, configure, and manage New Relic Platform Plugins.  For more information, refer to the [Installing an NPI-compatible plugin documentation](https://docs.newrelic.com/docs/plugins/plugins-new-relic/installing-plugins/installing-npi-compatible-plugin).

Once the NPI tool has been installed, run the following command:

```
	./npi install com.bluemedora.ibm.db2
```	

**Note:** This command will take care of the creation of `newrelic.json` and `plugin.json` files described in the [Configuring the Plugin](#Configuring-the-Plugin) section.

###### [Download Plugin for Manual Installation](https://newrelic-bluemedora.s3.amazonaws.com/com-bluemedora-ibm-db2/newrelic_ibm_db2_plugin-2.2.0_20170727_135346.tar.gz)

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

**Fields**

| Field Name  |  Description |
|:------------- |:-------------|
| polling_interval_seconds | The number of seconds between each data collection |
| downtime_tracking_minutes | The number of minutes into the past that will be considered when calculating downtime |
| instance_name | Alias for the name of your IBM DB2 instance that will appear in the User Interface |
| username | User name to log into DB2 instance |
| password | Password to log into DB2 instance |
| host | The hostname or ip address of DB2 instance |
| port | Port to connect to DB2 instance |
| database_name | Name of DB2 database to monitor |
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
      "username": "your_value_here",
      "password": "your_value_here",
      "port": 50000,
      "host": "your_value_here",
      "database_name": "your_value_here",
      "send_to_plugin": {
        "db2_bufferpool": true,
        "db2_database": true,
        "db2_memory_pool": true,
        "db2_tablespace": true
      },
      "send_to_insights": {
        "db2_instance": true,
        "db2_bufferpool": true,
        "db2_database": true,
        "db2_memory_pool": true,
        "db2_tablespace": true,
        "db2_top_n": true,
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
For questions or issues regarding the Blue Medora IBM DB2 plugin for New Relic, visit http://support.bluemedora.com. 

----     

## Metrics Source Documentation

**System Overview**

| Metric Name  |  Description |
|:------------- |:-------------|
| Database Buffer Pool Hit Ratio (%)  | The buffer pool hit percentage on the database |
| Memory Pool Utilization (%) | The utilization percentage of a memory pool |
| Database Average Direct Read Rate (ms) | The average direct read rate of the database |
| Database Average Direct Write Rate (ms) | The average direct write rate of the database |
| Database Read Time (ms) | The time of a read from the database |
| Database Write Time (ms) | The time of a write from the database |
| Buffer Pool Read Time (ms) | The time of a read per buffer pool |
| Buffer Pool Write Time (ms) | The time of a write per buffer pool |
| Tablespace Utilization (%) | The utilization percentage per tablespace |
| Tablespace Free Pages (pages) | The number of free pages per tablespace |

**Database**

| Metric Name  |  Description |
|:------------- |:-------------|
| Active Connections (connections)  | The number of active connections on the database |
| Applications (applications)  | The number of active connections on the database |
| Allocated Sort Heap Memory (pages)  | The sort heap memory allocated to the database |
| Applications Waiting on Locks (%)  | The percentage of applications on the database that are waiting on locks |
| Deadlocks (deadlocks/minute)  | The deadlocks per minute on the database |
| Lock Waits (waits)  | The number of waits for a lock on the database |
| Catalog Cache Inserts (inserts)  | The number of catalog cache inserts on the database |
| Package Cache Inserts (inserts)  | The number of package cache inserts on the database |
| Catalog Cache Lookups (lookups)  | The number of catalog cache lookups on the database |
| Package Cache Lookups (lookups)  | The number of package cache lookups on the database |
| Catalog Cache Overflows (overflows)  | The number of catalog cache overflows on the database |
| Package Cache Overflows (overflows)  | The number of package cache overflows on the database |

**Database IO**

| Metric Name  |  Description |
|:------------- |:-------------|
| Buffer Pool Hit Ratio (%)  | The buffer pool hit percentage on the database |
| Read Time (ms) | The time of a read from the database |
| Write Time (ms) | The time of a write from the database |
| Average Direct Read Rate (ms) | The average direct read rate of the database |
| Average Direct Write Rate (ms) | The average direct write rate of the database |
| Direct Reads (reads) | The number of direct reads from the database |
| Direct Writes (writes) | The number of direct writes to the database |
| Direct Reads Requests (requests) | The number of direct read requests from the database |
| Direct Writes Requests (requests) | The number of direct write requests to the database |
| Physical Data Reads (reads/minute) | The number of physical data reads from per minute the database |
| Physical Index Reads (reads/minute) | The number of physical index reads from per minute the database |
| Logical Data Reads (reads/minute) | The number of logical data reads from per minute the database |
| Logical Index Reads (reads/minute) | The number of logical index reads from per minute the database |

**Database Log**

| Metric Name  |  Description |
|:------------- |:-------------|
| Utilization (%)  | The utilization percentage of the database log |
| Used Space (KB)  | The used space of the database log |
| Reads (reads)  | The reads from the database log |
| Writes (writes)  | The writes to the database log |

**Buffer Pools**

| Metric Name  |  Description |
|:------------- |:-------------|
| Hit Ratio (%)  | The percentage of hits to the buffer pool |
| Read Time (ms)  | The time to read from a buffer pool |
| Write Time (ms)  | The time to write to a buffer pool |
| Logical Data Reads (reads) | The number of logical data reads from the buffer pool |
| Logical Index Reads (reads) | The number of logical index reads from the buffer pool |
| Physical Data Reads (reads) | The number of physical data reads from the buffer pool |
| Physical Index Reads (reads) | The number of physical index reads from the buffer pool |
| Data Writes (writes) | The number of data writes to the buffer pool |
| Index Writes (writes) | The number of index writes to the buffer pool |
| Asynchronous Read Time (ms) | The time asynchronous reads take from the buffer pool |
| Asynchronous Write Time (ms) | The time asynchronous writes take to the buffer pool |
| Asynchronous Data Reads (reads) | The number of asynchronous data reads from the buffer pool |
| Asynchronous Index Reads (reads) | The number of asynchronous index reads from the buffer pool |
| Asynchronous Data Writes (writes) | The number of asynchronous data writes to the buffer pool |
| Asynchronous Index Writes (writes) | The number of asynchronous index writes to the buffer pool |

**Tablespaces**

| Metric Name  |  Description |
|:------------- |:-------------|
| Utilization (%) | The utilization percentage per tablespace |
| Total Pages (pages) | The total pages per tablespace |
| Free Pages (pages) | The number of free pages per tablespace |
| Used Pages (pages) | The number of used pages per tablespace |
| Usable Pages (pages) | The number of usable pages per tablespace |

**Queries**

| Metric Name  |  Description |
|:------------- |:-------------|
| Executions | The number of executions of a query |
| Average Execution Time (ms) | The average amount of time a query takes to execute |
| Average User CPU Time (ms) | The average user CPU time consumed by a query |
| Average System CPU Time (ms) | The average system CPU time consumed by a query |
| Rows Read (rows/minute) | The number of rows read by a particular query every minute |
| Rows Written (rows/minute) | The number of rows written by a particular query every minute |

**Summary**

| Metric Name  |  Description |
|:------------- |:-------------|
| Downtime (%) | The percentage of times during the downtime tracking window during which the system has been unavailable |
| Average Buffer Pool Hit Ratio (%) | The average hit ratio across all buffer pools on the instance |
| Total Connections (connections) | The total number of connections to the instance |
| Total Deadlocks (deadlocks/minute) | The total number of deadlocks per minutes on the instance |
| Total Active Applications | The total number of Active Applications across all db2 Databases | 
