# New Relic Plugin for MS SQL

The **Blue Medora New Relic Plugin for MS SQL** allows you to monitor your Microsoft SQL performance data from within the New Relic platform by pulling metrics in from the system and displaying them in a set of intuitive, graph-based monitoring dashboards.

This guide includes instructions for installing and configuring the Blue Medora New Relic Plugin for MS SQL.
If you’re having a bad experience with one of our plugins, please get in touch and we’ll be happy to help you out.

----

## System Requirements

The MS SQL plugin connects to a MS SQL database via JDBC connection. Before installing and configuring the plugin, ensure your system meets the following requirements:

**New Relic Requirements**

- A New Relic account (Sign up for a free account [here](http://newrelic.com).)

**MS SQL Plugin Requirements**

- **MS SQL versions.** The plugin is compatible with MS SQL 2008 R2, 2012, & 2014.
- Java 1.8 or higher
- **A Blue Medora License.** A trial license will ship with the plugin that is valid for 14 days. To obtain a production license or get pricing information for the plugin, please contact sales@bluemedora.com.

----
## Access Rights
To set up the minimum user permissions needed for monitoring MSSQL, the following tasks must be completed. You should use your own credentials, user, and role names.
1. Grant your Microsoft SQL Server login credentials the `VIEW ANY DEFINITION` and `VIEW SERVER STATE` permissions.

2. Next, to ensure all future-created databases are monitored, create a user that maps your MS SQL credentials and has the **db_datareader** role on the following databases:
-  each user database
- `msdb` database
- `model` database

----
## Installing the Plugin

We recommend using the New Relic Platform Installer for installing and running your Blue Medora plugins for New Relic.

The New Relic Platform Installer (NPI) is a command line tool that helps you easily download, configure, and manage New Relic Platform Plugins.  For more information, refer to the [Installing an NPI-compatible plugin documentation](https://docs.newrelic.com/docs/plugins/plugins-new-relic/installing-plugins/installing-npi-compatible-plugin).

Once the NPI tool has been installed, run the following command:

```
  ./npi install com.bluemedora.microsoft.sqlserver
```

Now complete the following steps with root permissions:
1) `service newrelic_plugin_com.bluemedora.microsoft.sqlserver stop`
1) `vi /etc/rc.d/init.d/newrelic_plugin_com.bluemedora.microsoft.sqlserver`
1) Change line that starts with `sudo -u root java` to be `sudo -u root java -Xmx1024m "-Dnewrelic.platform.config.dir=$DAEMONDIR/config" -cp "$DAEMONDIR/jtds-1.1-v20140512.jar:$DAEMONDIR/plugin.jar:." com.bluemedora.newrelic.Main >> $DAEMONDIR/daemon.log 2>&1 &`
1) Save and exit
1) `systemctl daemon-reload`
1) `service newrelic_plugin_com.bluemedora.microsoft.sqlserver start`

**Note:** This command will take care of the creation of `newrelic.json` and `plugin.json` files described in the [Configuring the Plugin](#Configuring-the-Plugin) section.

###### [Download Plugin for Manual Installation](https://newrelic-bluemedora.s3.amazonaws.com/com-bluemedora-microsoft-sqlserver/newrelic_microsoft_sqlserver_plugin-4.0.0_20180913_163734.tar.gz)

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

`proxy_protocol` - The proxy protocol (HTTP/HTTPS) used for Insights uploads

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

**NOTE:** You can add multiple objects to the “agents” array to monitor multiple Microsoft SQL Server instances.

**NOTE:** Each object in the "agents" array should have a unique "instance_name".

**Fields**

| Field Name  |  Description |
|:------------- |:-------------|
| polling_interval_seconds | The number of seconds between each data collection |
| downtime_tracking_minutes | The number of minutes into the past that will be considered when calculating downtime |
| instance_name | Alias for the name of your Microsoft SQL Server instance that will appear in the user interface |
| username | User name to log into Microsoft SQL Server |
| password | Password to log into Microsoft SQL Server |
| host | The hostname or IP address of Microsoft SQL Server |
| port | Port to connect to Microsoft SQL Server |
| instance | Microsoft SQL Server instance to monitor |
| query_count | Optional parameter, the number of queries to return for "Top X Queries" metrics |
| query_order_by | Optional parameter, the field to sort by for "Top X Queries" metrics. Valid values for this parameter are "total_elapsed_time", "total_logical_writes", "total_logical_reads", "total_physical_reads", "execution_count", "execution_time", "avg_execution_time", "unique_plans", or "last_execution" |
| use_ntlm_v2 | Optional parameter, specifies whether or not to use NTLMv2 authentication. Default is false. |
| request_ssl | Optional parameter, specifies whether or not to request SSL certification. Default is false. |
| send_to_plugin | Indicates whether or not to send data to New Relic Plugins. See [Blue Medora's New Relic Knobs and Levers Readme](https://github.com/BlueMedora/new-relic-plugins/blob/master/configuration-variants/readme.md) for more details |
| send_to_insights | Indicates whether or not to send data to New Relic Insights. See [Blue Medora's New Relic Knobs and Levers Readme](https://github.com/BlueMedora/new-relic-plugins/blob/master/configuration-variants/readme.md) for more details |

**Examples**

```
{
  "polling_interval_seconds": 300,
  "downtime_tracking_minutes": 60,
  "agents": [
    {
      "instance_name": "your_value_here",
      "username": "your_value_here",
      "password": "your_value_here",
      "host": "your_value_here",
      "instance": "your_value_here",
      "port": 1433,
      "query_count": 10,
      "send_to_plugin": {
        "query": true,
        "instance": true,
        "database": true,
        "disk": true,
        "object": true
      },
      "send_to_insights": {
        "query": true,
        "instance": true,
        "database": true,
        "availability_group": true,
        "cluster_node": true,
        "hard_replica": true,
        "object": true,
        "disk": true,
        "relationships": true,
        "notifications": "INFO"
      }
    },
    {
      "instance_name": "your_value_here",
      "username": "your_value_here",
      "password": "your_value_here",
      "host": "your_value_here",
      "instance": "your_value_here",
      "query_count": 10,
      "send_to_plugin": {
        "query": true,
        "instance": true,
        "database": true,
        "disk": true,
        "object": true
      },
      "send_to_insights": {
        "query": true,
        "instance": true,
        "database": true,
        "availability_group": true,
        "cluster_node": true,
        "hard_replica": true,
        "object": true,
        "disk": true,
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
For questions or issues regarding the MS SQL Plugin for New Relic, visit http://support.bluemedora.com.

----     

## Metrics Source Documentation

**System Overview**

| Metric Name  |  Description |
|:------------- |:-------------|
| Instance Buffer Pool Hit (%) | The percentage of buffer pools hits on the instance |
| Total Wait Time Across Instance (ms/sec) | The number of milliseconds spent ever second waiting across the instance |
| Database Top 10 Read Throughput (MB/sec) | The 10 databases with the highest read throughput |
| Database Top 10 Write Throughput (MB/sec) | The 10 databases with the highest write throughput |
| Database Top 10 Read IOPS (operations/sec) | The 10 databases with the highest read IOPS |
| Database Top 10 Write IOPS (operations/sec) | The 10 databases with the highest write IOPS |
| Query Top 10 Execution Time (sec/minute) | The 10 queries that spent the most seconds per every minute executing |
| Query Top 10 Execution Count (executions/minute) | The 10 queries with the highest number of executions per minute |

**Instance**

| Metric Name  |  Description |
|:------------- |:-------------|
| Compilations (compilations/sec) | The number of compilations per second on the instance |
| Recompilations (compilations/sec) | The number of re-compilations per second on the instance |
| Processes (processes) | The number of `Preconnect`, `Background`, `Dormant`, `Runnable`, `Suspended`, `Running`, `Blocked`, and `Sleeping` processes on the instance |
| Total Wait Time Across Instance (ms/sec) | The number of milliseconds spent ever second waiting across the instance |
| Disk Space (GB) | The amount of Disk Space on the instance |
| Runnable Tasks (tasks) | The number of runnable tasks on the instance |
| Transactions (transactions/sec) | The number of transactions per second on the instance |
| Page Splits (splits/sec) | The number of page splits per second on the instance |
| Forced Parameterizations (parameterizations/sec) | The number of forced parameterizations per second on the instance |

**Instance Buffer Pool**

| Metric Name  |  Description |
|:------------- |:-------------|
| Hit (%) | The percentage of hits on the buffer pool |
| Size (GB) | The size of the buffer pool |
| Page Life Expectancy (sec) | The life expectancy of a page in the buffer pool |
| Batch Requests (requests/sec) | The number of batch requests per second on the buffer pool |

**Databases**

| Metric Name  |  Description |
|:------------- |:-------------|
| Buffer Pool Size (GB) | The size of the buffer pool per database |
| Top 10 Read Delay (ms/sec) | The 10 databases with the highest milliseconds per second that a read is delayed per database |
| Top 10 Write Delay (ms/sec) | The 10 databases with the highest milliseconds per second that a write is delayed per database |
| Top 10 Read Throughput (MB/sec) | The 10 databases with the highest read throughput |
| Top 10 Write Throughput (MB/sec) | The 10 databases with the highest write throughput |
| Top 10 Read IOPS (operations/sec) | The 10 databases with the highest number of read operations per second |
| Top 10 Write IOPS (operations/sec) | The 10 databases with the highest number of write operations per second |

**Database Objects**

| Metric Name  |  Description |
|:------------- |:-------------|
| Top 10 Average Page Lock Wait (sec) | The 10 Database Objects with the highest Average Page Lock Wait |
| Top 10 Page Locks | The 10 Database Objects with the highest Page Locks |
| Top 10 Page Lock Waits | The 10 Database Objects with the highest Page Lock Waits |
| Top 10 Average Row Lock Waits | The 10 Database Objects with the highest Average Row Lock Waits |
| Top 10 Row Locks | The 10 Database Objects with the highest Row Locks |
| Top 10 Row Lock Waits | The 10 Database Objects with the highest Row Lock Waits |

**Queries**

| Metric Name  |  Description |
|:------------- |:-------------|
| Top 10 Execution Time (sec/minute) | The 10 queries that spent the most seconds per every minute executing |
| Top 10 Average Execution Time (ms) | The 10 queries with the highest execution time on average |
| Top 10 Execution Count (executions/minute) | The 10 queries with the highest number of executions per minute |

**Summary**

| Metric Name  |  Description |
|:------------- |:-------------|
| Downtime (%) | The percentage of times during the downtime tracking window during which the system has been unavailable |
| Buffer Pool Hit (%) | The percentage of buffer pools hits on the instance |
| Compilations (compilations/sec) | The number of compilations per second on the instance |
| Recompilations (compilations/sec) | The number of re-compilations per second on the instance |
| Average Query Execution Time (seconds) | The average query execution time across all queries |
