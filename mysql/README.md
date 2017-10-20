# New Relic Plugin for MySQL

The **Blue Medora New Relic Plugin for MySQL** allows you to monitor your MySQL performance data from within the New Relic platform by pulling metrics in from the system and displaying them in a set of intuitive, graph-based monitoring dashboards.
				
This guide includes instructions for installing and configuring the Blue Medora New Relic Plugin for MySQL.
If you’re having a bad experience with one of our plugins, please get in touch and we’ll be happy to help you out.

----

## System Requirements

The MySQL plugin connects to a MySQL or MariaDB instance via JDBC connection. Before installing and configuring the plugin, ensure your system meets the following requirements:

**New Relic Requirements**

- A New Relic account (Sign up for a free account [here](http://newrelic.com).)

**MySQL Plugin Requirements**

- **MySQL and Maria DB versions.** The plugin is compatible with MySQL versions 5.6+ and MariaDB versions 10.0 and 10.1.
- For MySQL versions prior to 5.7.7 the `sys` schema must be installed before installing the plugin in order to collect query information 
- Java 1.7 or higher
- **A Blue Medora License.** A trial license will ship with the plugin that is valid for 14 days. To obtain a production license or get pricing information for the plugin, please contact sales@bluemedora.com.

----
## Access Rights
In order to access and return certain metrics from your database, specific privileges must be granted to the designated MySQL user:

- **Table and database I/O Metrics:**
In order to access these metrics, enable the `EXECUTE` privilege. This applies to MySQL 5.7 only.

- **Slave Replication Metrics:**
In order to access these metrics, enable the `REPLICATION CLIENT` privilege.

- **Instance Metrics:**
In order to access these metrics, enable the `PROCESS` privilege. This grants access to the following metrics:
```
- Instance Adaptive Hash
- Index
- Buffer
- Buffer Page I/O
- Change Buffer
- Compression
- DDL
- DML
- File System
- ICP
- Index
- Lock
- Metadata
- OS
- Purge
- Recovery
- Server
- Transaction
- Tablespace
```
- **Query Metrics:**
In order to access these metrics, ensure the `sys` schema is install. If it is not installed, run the following commands:

These steps are based on the [mysql-sys](<https://github.com/mysql/mysql-sys>) repository.

Shell commands to install `sys` schema found here: <https://docs.selectstar.io/docs/mysql>

-------
## Installing the Plugin

We recommend using the New Relic Platform Installer for installing and running your Blue Medora plugins for New Relic.

The New Relic Platform Installer (NPI) is a command line tool that helps you easily download, configure, and manage New Relic Platform Plugins.  For more information, refer to the [Installing an NPI-compatible plugin documentation](https://docs.newrelic.com/docs/plugins/plugins-new-relic/installing-plugins/installing-npi-compatible-plugin).

Once the NPI tool has been installed, run the following command:

```
  ./npi install com.bluemedora.mysql
``` 

**Note:** This command will take care of the creation of `newrelic.json` and `plugin.json` files described in the [Configuring the Plugin](#Configuring-the-Plugin) section.

###### [Download Plugin for Manual Installation](https://newrelic-bluemedora.s3.amazonaws.com/com-bluemedora-mysql/newrelic_mysql_plugin-3.1.0_20171020_143738.tar.gz)

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

**NOTE:** You can add multiple objects to the “agents” array to monitor multiple MySQL instances.

**NOTE:** Each object in the "agents" array should have a unique "instance_name".

**Fields**

| Field Name  |  Description |
|:------------- |:-------------|
| polling_interval_seconds | The number of seconds between each data collection. |
| downtime_tracking_minutes | The number of minutes into the past that will be considered when calculating downtime |
| instance_name | Alias for the name of your MySQL instance that will appear in the User Interface |
| username | User name to log into MySQL |
| password | Password to log into MySQL |
| host | The hostname or ip address of MySQL |
| port | Optional parameter, Port to connect to MySQL. If not supplied 3306 will be used. |
| monitor_queries | Optional Parameter, indicates whether or not to monitor queries, valid values are `true` or `false`. If `false` the `Queries` will not be populated. If not supplied 'true' will be used. |
| monitor_tables| Optional Parameter, indicates whether or not to monitor tables, valid values are `true` or `false`. If `false` the `Queries` will not be populated. If not supplied 'true' will be used. |
| ssl_enable | Optional Parameter, indicates whether ssl certification should be used to connect, valid values are `true` or `false`. If not supplied 'false' will be used. |
| query_count | Optional parameter, the number of queries to return for "Top X Queries" metrics. If not supplied 10 will be used. |
| query_history_interval | Optional Parameter, indicates the number of hours query history will be collected for. If not supplied 24 will be used. |
| order_queries_by | Optional Parameter, indicates how queries will be ordered, valid valus are `lock_latency_avg`, `total_latency`, `avg_latency`, `rows_sent_avg`, `tmp_tables_avg`, `sort_merge_passes_avg`, `rows_examined_avg`, `rows_sorted_avg`, `rows_affected_avg`, `exec_count`, `max_latency`, `err_count_avg`, `tmp_disk_tables_avg`, `warn_count_avg`. If not supplied `avg_latency` will be used.|
| ssl_cert_path | Optional parameter, ff `ssl_enable` is `true` this should be the path to your MySQL cert. |
| database | Optional parameter, comma separated list of databases to monitor |
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
      "username": "your_value_here",
      "password": "your_value_here",
      "port": 3306,
      "host": "your_value_here",
      "database": "your_value_here",
      "ssl_enable": false,
      "ssl_cert_path": "your_value_here",
      "monitor_tables": false,
      "monitor_queries": false,
      "query_count": 10,
      "query_history_interval": 24,
      "order_queries_by": "avg_latency",
      "send_to_plugin": {
        "mysql_instance": true,
        "mysql_tablespace": true,
        "mysql_table": true,
        "mysql_database": true,
        "mysql_index": true,
        "mysql_query": true
      },
      "send_to_insights": {
        "mysql_instance": true,
        "mysql_tablespace": true,
        "mysql_table": true,
        "mysql_database": true,
        "mysql_index": true,
        "mysql_query": true,
        "relationships": true,
        "notifications": "INFO"
      }
    }
  ]
}
```

## Using the Plugin
For more information about navigating New Relic’s user interface, refer to their [Using a plugin documentation](https://docs.newrelic.com/docs/plugins/plugins-new-relic/using-plugins/using-plugin) section.


**NOTE:** MySQL queries are given an ID calculated from a MD5 hash of the query text. To match a query ID to the text the following query can be run.

```
SELECT 
CAST(sql_text AS CHAR(10000) CHARACTER SET utf8) AS sql_text, 
MD5(CAST(sql_text AS CHAR(10000) CHARACTER SET utf8)) AS sql_id 
from mysql.slow_log
```

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

**Query Data Not Populating.** The plugin will attempt to monitor queries by default. If query data is not populating, you must enable slow queries to be written to the `mysql.slow_log` table. 
The size of this table must be limited or monitoring queries may severely affect system performance.

----     

## Support Resources
For questions or issues regarding the MySQL Plugin for New Relic, visit http://support.bluemedora.com. 

----     

## Metrics Source Documentation

**System Overview**

| Metric Name  |  Description |
|:------------- |:-------------|
| Instance Size (GB) | The size of the MySQL instance |
| Instance Connections (connections/minute) | The number of connections per minute to the MySQL instance |
| Database IO Read (MB/sec) | The IO read rate per database |
| Database IO Write (MB/sec) | The IO write rate per database |
| Database Size (MB) | Size per database |

**Instance**

| Metric Name  |  Description |
|:------------- |:-------------|
| Size (GB) | The size of the MySQL instance |
| Connections (connections/minute) | The number of connections per minute to the MySQL instance |
| Data Reads (reads/sec) | The number of reads across the MySQL instance |
| Data Writes (writes/sec) | The number of writes across the MySQL instance |
| Deadlocks (deadlocks/minutes) | The number of deadlocks per minutes across the MySQL instance |
| OS Waits (waits/minutes) | The number of operating system related waits per minutes across the MySQL instance |
| Spin Waits (waits/minutes) | The number of spin waits per minutes across the MySQL instance |
| Waits (waits/minutes) | The number of miscellaneous waits per minutes across the MySQL instance |

**Tablespaces**

| Metric Name  |  Description |
|:------------- |:-------------|
| Size (GB) | The size per tablespace |
| Max File Size (GB) | The maximum size of a file per tablespace |

**Databases**

| Metric Name  |  Description |
|:------------- |:-------------|
| Size (MB) | The size per databases |
| Data Size (MB) | The size of data stored in a database |
| Index Size (MB) | The size of indexes in a database |
| Wait Time (sec/minute) | The number of seconds for each minute that is spent waiting for a database |
| IO Read (MB/sec) | The read rate per database |
| IO Write (MB/sec) | The write rate per database |
| IO Read Latency (ms) | The read latency per database |
| IO Write Latency (ms) | The write latency per database |

**Tables**

| Metric Name  |  Description |
|:------------- |:-------------|
| Top 10 Size (MB) | The 10 tables with the largest size |
| Top 10 Wait Time (ms) | The 10 tables with the longest wait time |
| Top 10 Read (KB/sec) | The 10 tables with the highest read rate |
| Top 10 Write (KB/sec) | The 10 tables with the highest write rate |
| Top 10 Read Latency (ms) | The 10 tables with the highest read latency |
| Top 10 Write Latency (ms) | The 10 tables with the highest write latency |

**Indexes**

| Metric Name  |  Description |
|:------------- |:-------------|
| Row Operations (rows/minutes) | The number of rows operated on per minutes by an index |
| Latency (ms) | The latency of per index |

**Queries**

**NOTE:** Only 10 queries are displayed at a time. The 10 that are displayed are the queries that have the highest number of overall calls.

| Metric Name  |  Description |
|:------------- |:-------------|
| Execution Time (ms) | The execution time of a query |
| Average Latency (ms) | The average latency of a query |
| Executions (executions/second) | The number of executions per second for a query |

**Summary**

| Metric Name  |  Description |
|:------------- |:-------------|
| Downtime (%) | The percentage of times during the downtime tracking window during which the system has been unavailable |
| Connections (connections/minute) | The number of connections per minute to the MySQL instance |
| Deadlocks (deadlocks/minute) | The number of deadlocks per minute to the MySQL instance |
| Average I/O Read Latency (ms) | The average read latency across all databases |
| Average Query Latency (ms) | The average query latency across all queries |
