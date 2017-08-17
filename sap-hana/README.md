# New Relic Plugin for SAP HANA

The **Blue Medora New Relic Plugin for SAP HANA** allows you to monitor your SAP HANA performance data from within the New Relic platform by pulling metrics in from the system and displaying them in a set of intuitive, graph-based monitoring dashboards.
				
This guide includes instructions for installing and configuring the Blue Medora New Relic Plugin for SAP HANA.
If you’re having a bad experience with one of our plugins, please get in touch and we’ll be happy to help you out.

----

## System Requirements

The SAP HANA plugin connects to a SAP HANA system via JDBC connection. Before installing and configuring the plugin, ensure your system meets the following requirements:

**New Relic Requirements**

- A New Relic account (Sign up for a free account [here](http://newrelic.com).)

**SAP HANA Plugin Requirements**

- **SAP HANA versions.** The plugin is compatible with HANA Platform Edition 1.0, releases SPS 10, SPS 12.
- Java 1.7 or higher
- **A Blue Medora License.** A trial license will ship with the plugin that is valid for 14 days. To obtain a production license or get pricing information for the plugin, please contact sales@bluemedora.com.

----

## Installing the Plugin

We recommend using the New Relic Platform Installer for installing and running your Blue Medora plugins for New Relic.

The New Relic Platform Installer (NPI) is a command line tool that helps you easily download, configure, and manage New Relic Platform Plugins.  For more information, refer to the [Installing an NPI-compatible plugin documentation](https://docs.newrelic.com/docs/plugins/plugins-new-relic/installing-plugins/installing-npi-compatible-plugin).

Once the NPI tool has been installed, run the following command:

```
  ./npi install com.bluemedora.sap.hana
``` 

**Note:** This command will take care of the creation of `newrelic.json` and `plugin.json` files described in the [Configuring the Plugin](#Configuring-the-Plugin) section.

###### [Download Plugin for Manual Installation](https://newrelic-bluemedora.s3.amazonaws.com/com-bluemedora-sap-hana/newrelic_sap_hana_plugin-1.0.2_20170817_152754.tar.gz)


----
    
## Configuring the Plugin
From the extracted plugin folder you receive when downloading your plugin, you will find the following files: 

```
  plugin.jar
  eula.txt
  oss_attribution.txt
  [lib folder]
    sap_hana_dp_1.0.0_ga_xxxxxxxx_xxxxxx.jar
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

**NOTE:** You can add multiple objects to the “agents” array to monitor multiple SAP HANA Systems.

**NOTE:** Each object in the "agents" array should have a unique "instance_name".

**Fields**

| Field Name  |  Description |
|:------------- |:-------------|
| polling_interval_seconds | The number of seconds between each data collection |
| downtime_tracking_minutes | The number of minutes into the past that will be considered when calculating downtime |
| instance_name | Alias for the name of your SAP HANA System that will appear in the user interface |
| username | User name to log into SAP HANA System |
| password | Password to log into SAP HANA System |
| host | The hostname or IPv4 address of SAP HANA System |
| port | Port to connect to SAP HANA System |
| ssl_config | Optional parameter, valid values are `No SSL`, `No Verify` to use SSL but trust the server certificate, or `Verify` to use SSL and verify against the server certificate |
| failover_hosts | Optional parameter, Comma seperated list of SAP HANA hosts to failer over for monitoring if connection to main host fails. Ex: [10.6.5.101,10.6.5.102:30015] |
| collect_events | Optional parameter, toggle events on/off acceptable values are `true` or `false` |
| excluded_queries | Optional parameter, comma separated list of queries. If a query is in this list the plugin will not run the query while monitoring your SAP HANA System |
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
      "port": "your_value_here",
      "failover_hosts": "your_value_here",
      "collect_events": true,
      "send_to_plugin": {
        "system": true,
        "host": true,
        "disk": true,
        "service": true,
        "service_shared_memory": true,
        "volume": true
      },
      "send_to_insights": {
        "system": true,
        "host": true,
        "disk": true,
        "service": true,
        "service_shared_memory": true,
        "volume": true,
        "relationships": true,
        "notifications": "INFO"   // Valid values: true, false, "ERROR", "WARNING", "INFO", "DEBUG"
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
For questions or issues regarding the SAP HANA Plugin for New Relic, visit http://support.bluemedora.com. 

----     

## Metrics Source Documentation

**System Overview**

| Metric Name  |  Description |
|:------------- |:-------------|
| Hosts | The number of `Total`, `Inactive`, and `Running` hosts on the System |
| Connections | The number of `Running` and `Idle` connections on the System |
| Average Core Utilization | The average core utilization across the System |
| System Memory Utilization (%) | The memory utilization of the System |
| Capacity Utilization  (%) | The capacity utilization of the System |
| Capacity Totals (GB) | The total capacity of `Log`, `Trace, `Data`, `Log Backup`, and `Data Backup` on the System |
| Request Rate (requests/sec) | The request rate across the System |
| Average Response Time (ms) | The average response time across the System |

**Disks**

| Metric Name  |  Description |
|:------------- |:-------------|
| Top 10 Disk Utilization (%) | The 10 Disks with the highest total utilization  |
| Top 10 Reads (reads/sec) | The 10 Disks with the highest reads per second |
| Top 10 Writes (writes/sec) | The 10 Disks with the highest writes per second |
| Top 10 Read Size (GB) | The 10 Disks with the most data read |
| Top 10 Write Size (GB) | The 10 Disks with the most data written |
| Top 10 Total Size (GB) | The 10 Disks with the most total capacity |
| Top 10 Used Size (GB)  | The 10 Disks with the most used space |

**Hosts**

| Metric Name  |  Description |
|:------------- |:-------------|
| CPU Utilization (%) | The CPU utilization of the host  |
| Swap Space Utilization (%) | The Swap Space utilization of the host  |
| Physical Memory Utilization (%) | The Physical Memory utilization of the host  |
| Database Memory Utilization (%) | The Database Memory utilization of the host  |
| Connections | The number of connections to the host  |
| Transactions | The number of transactions of the host  |

**Services**

| Metric Name  |  Description |
|:------------- |:-------------|
| Top 10 CPU Utilization (%) | The 10 Services with the highest CPU utilization  |
| Top 10 Job Count | The 10 Services with the highest job count  |
| Top 10 Cache Inserts (inserts/sec) | The 10 Services with the highest cache insert rate  |
| Top 10 Request Rate (requests/sec) | The 10 Services with the highest request rate  |
| Top 10 Slowest Response Time (ms) | The 10 Services with the slowest response time  |

**Volumes**

| Metric Name  |  Description |
|:------------- |:-------------|
| Top 10 Reads (reads/sec) | The 10 Volumes with the highest read rate  |
| Top 10 Writes (writes/sec) | The 10 Volumes with the highest write rate  |
| Top 10 Read Size (kBps) | The 10 Volumes with the highest read data rate  |
| Top 10 Write Size (kBps) | The 10 Volumes with the highest write data rate  |

**Summary**

| Metric Name  |  Description |
|:------------- |:-------------|
| Downtime (%) | The percentage of times during the downtime tracking window during which the system has been unavailable |
| Average Core Utilization (%) | The average core utilization across the System |
| Physical Memory Utilization (%) | The physical memory utilization of the System |
| Virtual Memory Utilization (%) | The virtual memory utilization of the System |
| Average Response Time (ms) | The average response time across the System |
