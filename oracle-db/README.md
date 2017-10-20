# New Relic Plugin for Oracle Database

The **Blue Medora New Relic Plugin for Oracle Database** allows you to monitor your Oracle Database performance data from within the New Relic platform by pulling metrics in from the system and displaying them in a set of intuitive, graph-based monitoring dashboards.
        
This guide includes instructions for installing and configuring the Blue Medora New Relic Plugin for Oracle Database.
If you’re having a bad experience with one of our plugins, please get in touch and we’ll be happy to help you out.

----  

## System Requirements

The Oracle Database plugin connects to a single Oracle Database Instance via a host or IP address. Before installing and configuring the plugin, ensure your system meets the following requirements:

**New Relic Requirements**

- A New Relic account (Sign up for a free account [here](http://newrelic.com).)

**Oracle Database Plugin Requirements**

- The plugin supports **Oracle Database Version 10.2+**
- Java 1.7 or higher
- **A Blue Medora License.** A trial license will ship with the plugin that is valid for 14 days. To obtain a production license or get pricing information for the plugin, please contact sales@bluemedora.com.

- **Access Rights.** The following list contains the minimum Oracle Database user privileges required for monitoring with the Blue Medora New Relic Plugin for Oracle Database. Ensure the Oracle Database user has these permissions granted:

```
create session
connect
select on dba_data_files
select on dba_free_space
select on dba_outstanding_alerts
select on dba_tablespaces
select on dba_temp_files
select on dba_temp_free_space (Versions 11.2 and higher)
select on dba_undo_extents
select on global_name
select on gv_$archive_dest
select on gv_$filestat
select on gv_$instance
select on gv_$parameter
select on gv_$resource_limit
select on gv_$session
select on gv_$sgainfo
select on gv_$sql
select on gv_$sysmetric
select on gv_$system_event
select on gv_$system_wait_class
select on gv_$tempstat
select on v_$archive_dest
select on v_$controlfile
select on v_$database
select on v_$datafile
select on v_$filestat
select on v_$instance
select on v_$log
select on v_$logfile
select on v_$memory_target_advice
select on v_$parameter
select on v_$recovery_area_usage
select on v_$flash_recovery_area_usage (Version 10 only)
select on v_$resource_limit
select on v_$rman_backup_job_details
select on v_$tempfile
select on v_$version
select on v$db_cache_advice
select on v$memory_target_advice
select on v$pga_target_advice
select on v$sga_target_advice
select on v$shared_pool_advice
```

----

## Installing the Plugin

We recommend using the New Relic Platform Installer for installing and running your Blue Medora plugins for New Relic.

The New Relic Platform Installer (NPI) is a command line tool that helps you easily download, configure, and manage New Relic Platform Plugins.  For more information, refer to the [Installing an NPI-compatible plugin documentation](https://docs.newrelic.com/docs/plugins/plugins-new-relic/installing-plugins/installing-npi-compatible-plugin).

Once the NPI tool has been installed, run the following command:

```
  ./npi install com.bluemedora.oracle.database
``` 

**Note:** This command will take care of the creation of `newrelic.json` and `plugin.json` files described in the [Configuring the Plugin](#Configuring-the-Plugin) section.

###### [Download Plugin for Manual Installation](https://newrelic-bluemedora.s3.amazonaws.com/com-bluemedora-oracle-database/newrelic_oracle_database_plugin-3.1.0_20171020_150705.tar.gz)

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

**NOTE:** You can add multiple objects to the “agents” array to monitor multiple Oracle Database instances.

**NOTE:** Each object in the "agents" array should have a unique "instance_name".

**Fields**

| Field Name  |  Description |
|:------------- |:-------------|
| polling_interval_seconds | The number of seconds between each data collection. |
| downtime_tracking_minutes | The number of minutes into the past that will be considered when calculating downtime |
| instance_name | Alias for the name of your Oracle Database instance that will appear in the User Interface |
| host | IP address or hostname of Oracle Database instance. |
| port | Port used to connect to the Oracle Database instance. Default is `1521` for when `ssl_enabled` is `false`, and `2484` for when `ssl_enabled` is `true`. |
| username | User Name for Oracle Database login. |
| password | Password for Oracle Database login. |
| order_queries_by | Optional paramter, specifies the metric to order query resources by. By default, the queries with the highest number of overall executions are returned. The following are valid values for this field: `elapsed_time`, `cpu_time`, `user_i/o_wait_time`, `buffer_gets`, `executions`, `parse_calls`, `sharable_memory`, `child_count`, `average_time`, `physical_read_bytes`, `physical_read_requests`, `physical_write_bytes`, `physical_write_requests`. |
| ssl_enabled | Indicates if you wish to connect while using ssl. Acceptable values are `true` and `false`. |
| show_query_text | Optional parameter, shows query text. If false, this field will default to the SQL ID. |
| show_monitoring_queries | Optional parameter, specifies whether or not to return data for queries made by the Blue Medora data collector. |
| sid | Optional parameter, SID or Service Name. |
| truststore_path | Optional parameter, only used if `ssl_enabled` is `true`. Location of truststore. |
| truststore_password | Optional parameter, only used if `ssl_enabled` is `true`. Password for the truststore. |
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
      "host": "your_value_here",
      "port": 1521,
      "order_queries_by": "executions",
      "show_query_text": true,
      "show_monitoring_queries": true,
      "sid": "your_value_here",
      "ssl_enable": false,
      "truststore_path": "your_value_here",
      "truststore_password": "your_value_here",
      "send_to_plugin": {
        "database": true,
        "instance": true,
        "table": true,
        "database_file": true,
        "query": true
      },
      "send_to_insights": {
        "database": true,
        "instance": true,
        "table": true,
        "database_file": true,
        "query": true,
        "data_guard_destination": true,
        "event_wait_group": true,
        "event": true,
        "os_user": true,
        "application": true,
        "session": true,
        "parameter": true,
        "redo_log_file": true,
        "pga_advice_entry": true,
        "memory_advice_entry": true,
        "sga_advice_entry": true,
        "shared_pool_advice_entry": true,
        "cache_advice_entry": true,
        "control_file": true,
        "tablespace": true,
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
For questions or issues regarding the Oracle Database Plugin for New Relic, visit http://support.bluemedora.com. 

----     

## Metrics Source Documentation

**System Overview**

| Metric Name  |  Description |
|:------------- |:-------------|
| Instance Waits (waits/sec) |  The number of waits per second on the instance |
| Instance Sessions (sessions) |  Inactive, Killed, No Wait, Sniped, Unblocked, Waiting, Active, Blocked, and Cached sessions on the instance |
| Instance CPU Usage (centiseconds/sec) | CPU usage of an instance |
| Tablespace Size (GB) | Size across tablespaces |
| Query Execution Time (sec/minute) | The number of seconds every minute that a query takes to execute |
| Query Wait Time (ms/minute) | The number of milliseconds every minute that a query spends waiting |
| Database File Size (GB) | File size across databases of an instance |
| Control File Size (MB) | Size of control files across an instance |

**Instance**

| Metric Name  |  Description |
|:------------- |:-------------|
| Waits (waits/sec) |  The number of waits per second on the instance |
| Time Waited (sec/minute) | The number of seconds every minute that the instance is spent waiting  |
| CPU Usage (centiseconds/sec) | CPU usage of an instance |
| Sessions (sessions) |  Inactive, Killed, No Wait, Sniped, Unblocked, Waiting, Active, Blocked, and Cached sessions on the instance |
| Cache Hit Ratio (%) | The hit precentage of instance on the cache  |
| Cache Size (GB) | The size of the instance cache  |
| Read Time (ms/minute) | The number of milliseconds every minute that the instance spends reading |
| Write Time (ms/minute) | The number of milliseconds every minute that the instance spends writing |

**Tablespaces**

| Metric Name  |  Description |
|:------------- |:-------------|
| Size (GB)  | Size across tablespaces |
| Free Space (GB)  | Free Space available across tablespaces |

**Database Files**

| Metric Name  |  Description |
|:------------- |:-------------|
| Size (GB)  | Size across database files |
| Max Size (GB)  | Max size allowed across database files |
| IO Time (ms)  | Time taken for IO operations |
| Read Time (ms/minute) | The number of milliseconds every minute across database files spent reading |
| Write Time (ms/minute) | The number of milliseconds every minute across database files spent writing |
| Reads (reads/sec) | The read rate across database files |
| Write (writes/sec) | The write rate across database files |

**Queries**

**NOTE:** Only 10 queries are displayed at a time. By default, the 10 that are displayed are the queries that have the highest number of overall executions - this can be changed by modifying the `order_queries_by` parameter in the `plugin.json` file.

| Metric Name  |  Description |
|:------------- |:-------------|
| Execution Time (sec/minute)  | The number of seconds every minute that a query takes to execute |
| Wait Time (ms/minute)  | The number of milliseconds every minute that a query spends waiting |
| CPU Time (ms/minute)  | The number of milliseconds every minute that a query spends on the cpu |
| Memory (KB/sec)  | The memory usage every second of a query |
| Executions (executions/sec)  | The number of executions per second of a query |

**Summary**

| Metric Name  |  Description |
|:------------- |:-------------|
| Downtime (%) | The percentage of times during the downtime tracking window during which the system has been unavailable |
| Waits (waits/sec)  | The total number of waits per second across all instances  |
| Average CPU Usage (centiseconds/sec)  | The average CPU usage across all instaces  |
| Active Sessions (sessions)  | The total number of active sessions across all instaces  |
| Average Query Execution Time (seconds) | The average query execution time across all queries |
