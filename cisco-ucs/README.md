# Blue Medora Cisco UCS Plugin for New Relic

The **Blue Medora Cisco UCS Plugin for New Relic** allows you to monitor your Cisco UCS performance data from within the New Relic platform by pulling metrics in from the system and displaying them in a set of intuitive, graph-based monitoring dashboards.           

This guide includes instructions for installing and configuring the Blue Medora Cisco UCS Plugin for New Relic.
If you’re having a bad experience with one of our plugins, please get in touch and we’ll be happy to help you out.

----

## System Requirements

The Cisco UCS plugin collects data by making REST calls to the Cisco UCS Manager.  Before installing and configuring the plugin, ensure your system meets the following requirements:

**New Relic Requirements**

- A New Relic account (Sign up for a free account [here](http://newrelic.com).)

**Cisco UCS Plugin Requirements**

- The plugin supports **Cisco UCS Manager 2.2+**
- Java 1.7 or higher
- **A Blue Medora License.** A trial license will ship with the plugin that is valid for 14 days. To obtain a production license or get pricing information for the plugin, please contact sales@bluemedora.com.

----

## Installing the Plugin

We recommend using the New Relic Platform Installer for installing and running your Blue Medora plugins for New Relic.

The New Relic Platform Installer (NPI) is a command line tool that helps you easily download, configure, and manage New Relic Platform Plugins.  For more information, refer to the [Installing an NPI-compatible plugin documentation](https://docs.newrelic.com/docs/plugins/plugins-new-relic/installing-plugins/installing-npi-compatible-plugin).

Once the NPI tool has been installed, run the following command:

```
  ./npi install com.bluemedora.cisco.ucs
```

**NOTE:** This command will take care of the creation of `newrelic.json` and `plugin.json` files described in the [Configuring the Plugin](#Configuring-the-Plugin) section.

###### [Download Plugin for Manual Installation](https://newrelic-bluemedora.s3.amazonaws.com/com-bluemedora-cisco-ucs/newrelic_cisco_ucs_plugin-3.1.1_20170727_132448.tar.gz)

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

#### Configuring the plugin.template.json file:

The second file, `plugin.template.json`, contains data specific to each plugin (e.g., a list of hosts and port combinations for what you are monitoring). Templates for both of these files should be located in the ‘config’ directory in your extracted plugin folder.

Make a copy of this template and rename it to `plugin.json`. Shown below is an example of the `plugin.json` file’s contents.

**NOTE:** You can add multiple objects to the “agents” array to monitor multiple Cisco UCS instances.

**NOTE:** Each object in the "agents" array should have a unique "instance_name".

**Fields**

| Field Name  |  Description |
|:------------- |:-------------|
| polling_interval_seconds | The number of seconds between each data collection. |
| downtime_tracking_minutes | The number of minutes into the past that will be considered when calculating downtime |
| instance_name | The name of your New Relic Cisco UCS instance that will appear in the User Interface |
| username | User name to log into UCS Manager |
| password | Password to log into UCS Manager |
| host | The hostname or ip address of UCS Manager |
| protocol | Either `http` or `https` |
| port | Optional parameter, port to connect to UCS Manager |
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
      "protocol": "https" //Valid values: http, https,
      "ucs_manager_disabled": false,
      "send_to_plugin": {
        "ucs_manager": true,
        "blade": true,
        "fabric_interconnect": true,
        "ethernet_port": true,
        "chassis": true,
        "fan": true,
        "fiber_channel_port": true,
        "io_module": true,
        "port_channel": true,
        "psu": true,
        "rack": true,
        "vhba": true,
        "vnic": true
      },
      "send_to_insights": {
        "ucs_manager": true,
        "blade": true,
        "fabric_interconnect": true,
        "ethernet_port": true,
        "chassis": true,
        "fan": true,
        "fiber_channel_port": true,
        "io_module": true,
        "port_channel": true,
        "psu": true,
        "rack": true,
        "vhba": true,
        "vnic": true,
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
For questions or issues regarding the Blue Medora Cisco UCS Plugin for New Relic, visit http://support.bluemedora.com.

----     

## Metrics Source Documentation

**System Overview**

| Metric Name  |  Description |
|:------------- |:-------------|
| Fabric Interconnect Load (%) | The average load percentage of the fabric interconnect |
| Chassis Power (watts) | The power in watts of the chassis |
| Blade Total Memory (GB) | The total memory per blade |
| Blade Available Memory (GB) | The memory available on a blade |
| Blade Memory Speed (MHz) | The speed of memory on a blade |
| IO Module Temperature (C) | The temperature of the IO module in celsius |
| IO Module Inbound Throughput (bits/sec)| The inbound throughput of the IO module |
| IO Module Outbound Throughput (bits/sec)| The outbound throughput of the IO module |
| Fabric Interconnect Inbound Throughput (bits/sec)| The inbound throughput of the fabric interconnect |
| Fabric Interconnect Outbound Throughput (bits/sec)| The outbound throughput of the fabric interconnect |

**Fabric Interconnects**

| Metric Name  |  Description |
|:------------- |:-------------|
| Load (%) | The load percentage of the fabric interconnect   |
| Effective Memory (GB) | The amount of effective memory   |
| Cached Memory (GB) | The cached memory  |
| Top 10 Ethernet Port Inbound Throughput (bits/sec) | The 10 ethernet ports with the highest inbound throughput  |
| Top 10 Ethernet Port Outbound Throughput (bits/sec)  | The 10 ethernet ports with the highest outbound throughput  |
| Top 10 Ethernet Port Inbound Packets (packets/sec) | The 10 ethernet ports with the highest inbound packets  |
| Top 10 Ethernet Port Outbound Packets (packets/sec) | The 10 ethernet ports with the highest outbound packets  |
| Top 10 Fiber Channel Inbound Throughput (bits/sec)  | The 10 fiber channels with the highest inbound throughput  |
| Top 10 Fiber Channel Outbound Throughput (bits/sec)  | The 10 fiber channels with the highest outbound throughput |
| Top 10 Fiber Channel Inbound Packets (packets/sec)  | The 10 fiber channels with the highest inbound packets |
| Top 10 Fiber Channel Outbound Packets (packets/sec)  | The 10 fiber channels with the highest outbound packets  |

**Chassis**

| Metric Name  |  Description |
|:------------- |:-------------|
| Top 10 Fan Speed (RPM)     | The 10 fans with the highest speed |
| Input Power (watts) | The input power of a chassis   |
| Output Power (watts) | The output power of a chassis   |
| PSU Output Power (watts) | The power supply units power output  |
| PSU Voltage (volts)  | The power supply units voltage |
| PSU Output Current (amps)  | The power supply units output current  |
| PSU Ambient Temperature (C) | The power supply units ambient temperature |

**Port Channels**

| Metric Name  |  Description |
|:------------- |:-------------|
| Top 10 Bandwidth (bits/sec) | The 10 port channels with the highest bandwidth |
| Top 10 Admin Speed (bits/sec) | The 10 port channels with the highest admin speed |
| Top 10 Operating Speed (bits/sec) | The 10 port channels with the highest operating speed |
| Top 10 Inbound Throughput (bits/sec) | The 10 port channels with the highest inbound throughput |
| Top 10 Outbound Throughput (bits/sec) | The 10 port channels with the highest outbound throughput |
| Top 10 Inbound Packets (packets/sec) | The 10 port channels with the highest inbound packets |
| Top 10 Outbound Packets (packets/sec) | The 10 port channels with the highest outbound packets |

**IO Modules**

| Metric Name  |  Description |
|:------------- |:-------------|
| Ambient Temperature (C)     | The ambient temperature of the IO module |
| Internal Temperature (C) | The internal temperature of the IO module  |
| Top 10 Ethernet Port Inbound Throughput (bits/sec) | The 10 ethernet ports with the highest inbound throughput |
| Top 10 Ethernet Port Outbound Throughput (bits/sec) | The 10 ethernet ports with the highest outbound throughput  |
| Top 10 Ethernet Port Inbound Packets (packets/sec)  | The 10 ethernet ports with the highest inbound packets  |
| Top 10 Ethernet Port Outbound Packets (packets/sec)  | The 10 ethernet ports with the highest outbound packets |

**Blades**

| Metric Name  |  Description |
|:------------- |:-------------|
| Available Memory (GB)  | The available memory of a blade |
| Total Memory (GB) | The total memory of a blade |

**Rack Units**

| Metric Name  |  Description |
|:------------- |:-------------|
| Temperature (C)     | The temperature in celsius of a rack unit  |
| Available Memory (GB) | The available memory of a rack unit  |
| Total Memory (GB) | The total memory of a rack unit  |
| Top 10 vHBA Inbound Throughput (bits/sec) | The 10 vHBAs with the highest inbound throughput |
| Top 10 vHBA Outbound Throughput (bits/sec) | The 10 vHBAs with the highest outbound throughput  |
| Top 10 vHBA Inbound Packets (packets/sec)  | The 10 vHBAs with the highest inbound packets  |
| Top 10 vHBA Outbound Packets (packets/sec)  | The 10 vHBAs with the highest outbound packets |
| Top 10 vHBA Inbound Dropped Packets (packets/sec)  | The 10 vHBAs with the highest inbound dropped packets  |
| Top 10 vHBA Outbound Dropped Packets (packets/sec)  | The 10 vHBAs with the highest outbound dropped packets |
| Top 10 vHBA Inbound Errors (errors/sec)  | The 10 vHBAs with the highest inbound errors  |
| Top 10 vHBA Outbound Errors (errors/sec)  | The 10 vHBAs with the highest outbound errors |

**Summary**

| Metric Name  |  Description |
|:------------- |:-------------|
| Average Load (%) | The average load percentage across fabric interconnects |
| Average IO Module Temperature | The average temperature of the IO modules |
| Average Chassis Power | The average power of the chassis |
| Average Inbound per Fabric Interconnect (bits/sec) | The average Fabric Interconnect inbound throughput |
| Average Outbound per Fabric Interconnect (bits/sec) | The average Fabric Interconnect outbound throughput |
