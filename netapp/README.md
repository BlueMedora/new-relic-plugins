# Blue Medora NetApp Storage Plugin for New Relic

The **Blue Medora NetApp Storage Plugin for New Relic** allows you to monitor your NetApp Storage performance data from within the New Relic platform by pulling metrics in from the system and displaying them in a set of intuitive, graph-based monitoring dashboards.						

This guide includes instructions for installing and configuring the Blue Medora NetApp Storage Plugin for New Relic.
If you’re having a bad experience with one of our plugins, please get in touch and we’ll be happy to help you out.

----

## System Requirements

The NetApp Storage plugin collects data by making REST calls to OnCommand API Services.  Before installing and configuring the plugin, ensure your system meets the following requirements:

**New Relic Requirements**

- A New Relic account (Sign up for a free account [here](http://newrelic.com).)

**NetApp Storage Plugin Requirements**

- **NetApp OnCommand ApiServices:** NetApp OnCommand API Services version 1.0 or 1.1 is required to collect data.  
- Java 1.7 or higher
- **A Blue Medora License.** A trial license will ship with the plugin that is valid for 14 days. To obtain a production license or get pricing information for the plugin, please contact sales@bluemedora.com.

----

## Installing the Plugin

We recommend using the New Relic Platform Installer for installing and running your Blue Medora plugins for New Relic.

The New Relic Platform Installer (NPI) is a command line tool that helps you easily download, configure, and manage New Relic Platform Plugins.  For more information, refer to the [Installing an NPI-compatible plugin documentation](https://docs.newrelic.com/docs/plugins/plugins-new-relic/installing-plugins/installing-npi-compatible-plugin).

Once the NPI tool has been installed, run the following command:

```
	./npi install com.bluemedora.netapp.apiservices
```

**Note:** This command will take care of the creation of `newrelic.json` and `plugin.json` files described in the [Configuring the Plugin](#Configuring-the-Plugin) section.

###### [Download Plugin for Manual Installation](https://newrelic-bluemedora.s3.amazonaws.com/com-bluemedora-netapp-apiservices/newrelic_netapp_apiservices_plugin-3.1.1_20170727_133523.tar.gz)

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

**NOTE:** You can add multiple objects to the “agents” array to monitor multiple NetApp Storage instances.

**NOTE:** Each object in the "agents" array should have a unique "instance_name".

**Fields**

| Field Name  |  Description |
|:------------- |:-------------|
| polling_interval_seconds | The number of seconds between each data collection. |
| downtime_tracking_minutes | The number of minutes into the past that will be considered when calculating downtime |
| instance_name | The name of your New Relic NetApp Storage instance that will appear in the user interface |
| username | User name to log into NetApp Storage API Services |
| password | Password to log into NetApp Storage API Services |
| server | The hostname or ip address of the server |
| protocol | Either `http` or `https` |
| port | Optional parameter, port to connect to NetApp API Services |
| send_to_plugin | Indicates whether or not to send data to New Relic Plugins. See [Blue Medora's New Relic Knobs and Levers Readme](https://github.com/BlueMedora/new-relic-plugins/blob/master/configuration-variants/readme.md) for more details |
| send_to_insights | Indicates whether or not to send data to New Relic Insights. See [Blue Medora's New Relic Knobs and Levers Readme](https://github.com/BlueMedora/new-relic-plugins/blob/master/configuration-variants/readme.md) for more details |

**Example**

```
{
  "polling_interval_seconds": 360,
	"downtime_tracking_minutes": 60,
  "agents": [
    {
      "instance_name": "Your NetApp Instance",
      "username": "your_value_here",
      "password": "your_value_here",
      "server": "your_value_here",
      "protocol": "https" //Valid values: http, https ,
			"port": "your_custom_port",
      "send_to_plugin": {
        "disk": false,
        "aggregate": true,
        "volume": true,
        "lun": true,
        "vserver": true,
        "system": true,
        "cluster": true
      },
      "send_to_insights": {
        "summary_vserver": true,
        "summary_system": true,
        "aggregate": true,
        "cluster": true,
        "disk": false,
        "lun": true,
        "qtree": true,
        "system": true,
        "volume": true,
        "vserver": true,
        "relationships": true,        
        "notifications": "INFO" //Valid values: true, false, ERROR, WARNING, INFO, DEBUG
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
For questions or issues regarding the Blue Medora NetApp Storage Plugin for New Relic, visit http://support.bluemedora.com.

----     

## Metrics Source Documentation

**System Overview**

| Metric Name  |  Description |
|:------------- |:-------------|
| SVM Used Capacity (%)  | Percentage of svm capacity used |
| Aggregate Used Capacity (%) | Percentage of aggregate capacity used |
| Volume Used Capacity (%) |  Percentage of volume capacity used  |
| LUN Used Capacity (%) |  Percentage of LUN capacity used  |
| System Latency (ms) |   The average latency for systems |
| System IOPS (ops/sec) |  The total IOPS for systems  |
| Volume Latency (ms) |  The average latency for volumes |
| Volume IOPS (ops/sec) |  The total IOPS for volumes  |
| LUN Latency (ms) |  The average latency for LUNs  |
| LUN IOPS (ops/sec) |  The total IOPS for LUNs  |

**SVMs**

| Metric Name  |  Description |
|:------------- |:-------------|
| Volume Used Capacity (%)  | Percentage of capacity used by volumes on each svm |
| Volume Used Capacity (TB) |  Terabytes of capacity used by volumes on each svm |
| Volume Total Capacity (TB) |  The total terabytes of volumes on each svm  |
| Volume Read Latency (ms) |  Average read latency for volumes on each svm |
| Volume Write Latency (ms) |  Average write latency for volumes on each svm |
| Volume Read IOPS (ops/sec) |  Total IOPS for volumes on each svm |
| Volume Write IOPS (ops/sec) |  Total write IOPS for volumes on each svm |
| Inbound Network Throughput (MB/sec) |  The inbound network throughput for svms |
| Outbound Network Throughput (MB/sec) |  The outbound network thoughput for svms  |
| Inbound Network Errors (errors/sec) |  Number of inbound network errors per second on this svm  |
| Outbound Network Errors (errors/sec) |  Number of outbound network errors per second on this svm  |

**Systems**

| Metric Name  |  Description |
|:------------- |:-------------|
| CPU Utilization (%)  | Percentage of cpu utilized by each system |
| Processors |  Number of processors on each system  |
| Data Disks |  Number of data disks on each system  |
| Read Latency (ms) |  Read latency for each system  |
| Write Latency (ms) |  Write latency for each system  |
| Read IOPS (ops/sec) |  Total read IOPS for each system  |
| Write IOPS (ops/sec) |  Total write IOPS for each system |
| Inbound Network Throughput (MB/sec) |  Inbound network throughput for each system  |
| Outbound Network Throughput (MB/sec) |  Outbound network throughput for each system  |
| Failed Fans |  Number of failed fans on each system  |
| Failed Power Supplies |  Number of failed power supplies on each system  |

**Disks**

| Metric Name  |  Description |
|:------------- |:-------------|
| Used Capacity (%)  | Percentage of capacity used for each disk |
| Used Capacity (TB) |  Terabytes of capacity used for each disk  |
| Total Capacity (TB) | The total capacity of each disk in terabytes   |
| Busy Time (%) |  Percentage of time in which the disk is busy  |
| IOPS (ops/sec) |  Total IOPS for each disk  |

**Aggregates**

| Metric Name  |  Description |
|:------------- |:-------------|
| Used Capacity (%)  |  Percentage of capacity used for each aggregate  |
| Used Capacity (TB) |  Terabytes of capacity used for each aggregate  |
| Total Capacity (TB) |  The total capacity of each aggregate in terabytes  |
| Volume Read Latency (ms) |  Average read latency for volumes on each aggregate  |
| Volume Write Latency (ms) |  Average write latency for volumes on each aggregate  |
| Volume Read IOPS (ops/sec) |  Total IOPS for volumes on each aggregate  |
| Volume Write IOPS (ops/sec) |  Total write IOPS for volumes on each aggregate  |
| Volume Deduplication Space Savings (GB) |  Space saved by deduplication on volumes on each aggregate  |
| Volume Compression Space Savings (GB) |  Space saved by compression on volumes on each aggregate  |

**Volumes**

| Metric Name  |  Description |
|:------------- |:-------------|
| Used Capacity (%)  |  Percentage of capacity used for each volume  |
| Used Capacity (TB) |  Terabytes of capacity used for each volume  |
| Total Capacity (TB) |  The total capacity of each volume in terabytes  |
| Read Latency (ms) |  Read latency for each volume  |
| Write Latency (ms) |  Write latency for each volume  |
| Read IOPS (ops/sec) |  Read IOPS for each volume  |
| Write IOPS (ops/sec) |  Write IOPS for each volume  |
| Deduplication Space Savings (GB) |  Space saved by deduplication on each volume  |
| Compression Space Savings (GB) |  Space saved by compression on each volume  |

**LUNs**

| Metric Name  |  Description |
|:------------- |:-------------|
| Used Capacity (%)  |  Percentage of capacity used for each LUN  |
| Used Capacity (TB) |  Terabytes of capacity used for each LUN  |
| Total Capacity (TB) |  The total capacity of each LUN in terabytes  |
| Read Latency (ms) |  Read latency for each LUN  |
| Write Latency (ms) |  Write latency for each LUN  |
| Read IOPS (ops/sec) |  Read IOPS for each LUN  |
| Write IOPS (ops/sec) |  Write IOPS for each LUN  |
| Read Throughput (MB/sec) |  Read throughput for each LUN  |
| Write Throughput (MB/sec) |  Write throughput for each LUN  |

**Summary**

| Metric Name  |  Description |
|:------------- |:-------------|
| SVM Used Capacity (%)  | The percentage of svm capacity used |
| System IOPS (ops/sec) |  Total IOPS for systems  |
| System Latency (ms) |  Average Latency of systems  |
