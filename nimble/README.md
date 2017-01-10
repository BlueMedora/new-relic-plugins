# Blue Medora Nimble Storage Plugin for New Relic

The **Blue Medora Nimble Storage Plugin for New Relic** allows you to monitor your Nimble Storage performance data from within the New Relic platform by pulling in metrics from the system and displaying them in a set of intuitive, graph-based monitoring dashboards.           

This guide includes instructions for installing and configuring the Blue Medora Nimble Storage Plugin for New Relic.
If you’re having a bad experience with one of our plugins, please get in touch and we’ll be happy to help you out.

----

## System Requirements

The Nimble Storage plugin connects to the Nimble hardware using REST and optionally SNMP v2 for additional group metrics.  Before installing and configuring the plugin, ensure your system meets the following requirements:

**New Relic Requirements**

- A New Relic account (Sign up for a free account [here](http://newrelic.com).)

**Nimble Storage Plugin Requirements**

- The plugin supports **Nimble 2.3+** through REST
- **SNMP v2** can be used for additional group metrics 
- Java 1.7 or higher
- **A Blue Medora License.** A trial license will ship with the plugin that is valid for 14 days. To obtain a production license or get pricing information for the plugin, please contact sales@bluemedora.com.

----

## Installing the Plugin

We recommend using the New Relic Platform Installer for installing and running your Blue Medora plugins for New Relic.

The New Relic Platform Installer (NPI) is a command line tool that helps you easily download, configure, and manage New Relic Platform Plugins.  For more information, refer to the [Installing an NPI-compatible plugin documentation](https://docs.newrelic.com/docs/plugins/plugins-new-relic/installing-plugins/installing-npi-compatible-plugin).

Once the NPI tool has been installed, run the following command:

```
  ./npi install com.bluemedora.nimble.storage
``` 

**Note:** This command will take care of the creation of `newrelic.json` and `plugin.json` files described in the [Configuring the Plugin](#Configuring-the-Plugin) section.

###### [Download Plugin for Manual Installation](https://newrelic-bluemedora.s3.amazonaws.com/com-bluemedora-nimble/newrelic_nimble_storage_plugin-3.0.0_20161201_193541.tar.gz) 

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

**NOTE:** You can add multiple objects to the “agents” array to monitor multiple Nimble Storage instances. 

**NOTE:** Each object in the "agents" array should have a unique "instance_name".

**Fields**

| Field Name  |  Description |
|:------------- |:-------------|
| polling_interval_seconds | The number of seconds between each data collection. |
| instance_name | The name of your New Relic Nimble Storage instance that will appear in the user interface. |
| username | Username to make REST calls to your Nimble Storage device. |
| password | Password to make REST calls to your Nimble Storage device. |
| hostname | IP address or fully qualified host name of your Nimble Storage device. |
| rest_port | Optional: if not specified, default port '5392' will be used. |
| community_string | Optional: community string required to connect to SNMP (not including disables SNMP metrics). |
| snmp_port | Optional: if not specified and 'community_string' is specified, default port '161' will be used. |
| send_to_plugin | Indicates whether or not to send data to New Relic Plugins. See [Blue Medora's New Relic Knobs and Levers Readme](https://github.com/BlueMedora/new-relic-plugins/blob/master/configuration-variants/readme.md) for more details |
| send_to_insights | Indicates whether or not to send data to New Relic Insights. See [Blue Medora's New Relic Knobs and Levers Readme](https://github.com/BlueMedora/new-relic-plugins/blob/master/configuration-variants/readme.md) for more details |

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
For questions or issues regarding the Blue Medora Nimble Storage Plugin for New Relic, visit http://support.bluemedora.com. 

----     

## Metrics Source Documentation

**Group Overview**

| Metric Name  |  Description |
|:------------- |:-------------|
| Capacity (TB) |  The free, usable, used, and unused reserve capacity of the Nimble group |
| Disk Usage (GB)  | The disk used in the Nimble group by volumes and snapshots |
| Latency (ms)  | The read and write latency of the Nimble group |
| Cache Hit (%)  | The percentage of non-sequential read cache hits to non-sequential reads for the Nimble group  |
| Throughput (MB/sec)  | The read and write throughput for the Nimble group |
| IOPS (ops/sec)  | The read and write IOPs for the Nimble group |

**Pools**

| Metric Name  |  Description |
|:------------- |:-------------|
| Capacity (TB) |  The total, free, and used capacity of each Nimble pool |
| Associated Objects  | The number of child objects on each Nimble pool |
| Cache Capacity (TB)  | The pinable, pinned, and total cache capacity of each Nimble pool |

**Folders**

| Metric Name  |  Description |
|:------------- |:-------------|
| Capacity (TB) | The free, used, and unused reserve capacity of each Nimble folder |
| Compression Ratios  | The snapshot, volume, and folder compression ratio for each Nimble folder |
| Volume Usage (GB)  | The space used by volumes for each Nimble folder |
| Snapshot Usage (GB) | The space used by snapshots for each Nimble folder|
| Snapshots | The number of snapshots on each Nimble folder |

**Volumes**

| Metric Name  |  Description |
|:------------- |:-------------|
| Capacity (TB) | The total, free, and usable capacity of each Nimble volume |
| Compression Ratio | The compression ratio of folders and volume for each Nimble volume |
| Pinned Cache Capacity (GB)  | The pinned cache capacity of each Nimble volume |
| Snapshot Capacity (GB) | The snapshot capacity of each Nimble volume |
| Connections | The number of connections on each Nimble volume |
| Snapshots | The number of snapshots on each Nimble volume |

**Arrays**

| Metric Name  |  Description |
|:------------- |:-------------|
| Capacity (TB) | The free, usable, and used capacity of each Nimble array |
| Compression Ratio  | The compression ratio of volumes and snapshots on each Nimble array |
| Usage (TB)  | The space used by volumes and snapshots for each Nimble array |
| Space Saved (TB) | The space saved by volumes and snapshots for each Nimble array |

**Summary**

| Metric Name  |  Description |
|:------------- |:-------------|
| Cache Hit (%) | The cache hit percent of the Nimble group |
| Read Latency (ms)  | The average read latency of the Nimble group |
| Write Latency (ms)  | The average write latency Nimble group |
| Read Throghput (bytes/sec) | The read throughput of the Nimble group |
| Write Throghput (bytes/sec) | The write throughput of the Nimble group |
