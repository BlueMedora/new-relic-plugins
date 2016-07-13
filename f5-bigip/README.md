# New Relic Plugin for F5 BIG-IP

The **Blue Medora New Relic Plugin for F5 BIG-IP** allows you to monitor your F5 BIG-IP performance data from within the New Relic platform by pulling metrics in from the system and displaying them in a set of intuitive, graph-based monitoring dashboards.
				
This guide includes instructions for installing and configuring the Blue Medora New Relic Plugin for F5 BIG-IP.

----

## Obtaining the Plugin
You can find the New Relic Plugin for F5 BIG-IP in the following locations:

- [New Relic Storefront](//TODO Update)
- [Plugin Central](//TODO Update)					

## System Requirements

The F5 BIG-IP plugin connects to the supported F5 BIG-IP System via a management IP address. Before installing and configuring the plugin, ensure your system meets the following requirements:

**New Relic Requirements**

- A New Relic account. Sign up for a free account [here](http://newrelic.com)

**F5 BIG-IP Plugin Requirements**
- The plugin supports **F5 BIG-IP Version 11.5.0+** through REST
- **A Blue Medora License.** A trial license will ship with the plugin. This license will remain effective for the duration of the Blue Medora beta trial period.

----

## Installing the Plugin

This plugin can be installed one of the following ways:

- Using the New Relic Platform Installer
- Installing the Plugin Manually

### Using the New Relic Platform Installer

The New Relic Platform Installer (NPI) is a command line tool that helps you easily download, configure and manage New Relic Platform Plugins.  For more information, refer to the [Installing an NPI-compatible plugin documentation](https://docs.newrelic.com/docs/plugins/plugins-new-relic/installing-plugins/installing-npi-compatible-plugin).

**NOTE:** We recommend using the New Relic Platform Installer for installing and running your Blue Medora plugins for New Relic. Issues can arise by running a plugin directly in the foreground (e.g., when the machine reboots, the process will not be started again). The NPI automates much of these processes.

Once the NPI tool has been installed, run the following command:

```
  ./npi install com.bluemedora.f5.bigip
``` 

**NOTE:** This command will take care of the creation of `newrelic.json` and `plugin.json` files described in the [Configuring the Plugin](#Configuring-the-Plugin) section.

### Installing the Plugin Manually

#### Downloading and Extracting the Plugin

The latest version of the plugin can be downloaded from the locations listed in the [Obtaining the Plugin](#obtaining-the-plugin) section.  Once the plugin is on your box, extract it to your preferred directory location.

#### Configuring the Plugin

Refer to the [Configuring the Plugin](#Configuring-the-Plugin) section, for details on setting up the plugin. 

#### Running the Plugin

To run the plugin, navigate to the directory where the plugin was extracted, then execute the following command from your terminal or command line window:

```
  java -jar plugin.jar
```

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

```
{
   “license_key”: “YOUR_LICENSE_KEY_HERE”
}
```

**Insights Configuration** - Blue Medora plugins support reporting events to New Relic Insights. In order to achieve this you need to supply your `insights_api_key` and `insights_account_id`. For more information on where to find these fields, [refer to the New Relic Insights documentation]
(https://docs.newrelic.com/docs/insights/new-relic-insights/adding-querying-data/insert-custom-events-insights-api#register). Below are the fields needed to configure Insights access.

`insights_api_key` - The api key associated with your Insights account.

`insights_account_id` - The ID associated with your Insights account.

`insights_use_ssl` - Signals whether to connect to Insights via SSL. Acceptable values are `true` or `false`.


**Logging Configuration** - By default Platform plugins will have their logging turned on; however, you can modify these settings with the following configurations:

`log\_level` - The log level. Valid values: [debug, info, warn, error, fatal]. Defaults to info.

`log\_file\_name` - The log file name. Defaults to newrelic_plugin.log.

`log\_file\_path` - The log file path. Defaults to logs.

`log\_limit\_in\_kbytes` - The log file limit in kilobytes. Defaults to 25600 (25 MB). If limit is set to 0, the log file size would not be limited.

```
{
  "license_key": "YOUR_LICENSE_KEY_HERE",
  "log_level": "debug",

  "log_file_path": "log_file_path": “logs"
}
```

**Proxy Configuration** - If you are running your plugin from a machine that runs outbound traffic through a proxy, you can use the following optional configurations in your `newrelic.json` file:

`proxy\_host` - The proxy host (e.g. webcache.example.com)

`proxy\_port` - The proxy port (e.g. 8080). Defaults to 80 if a proxy_host is set

`proxy\_username` - The proxy username

`proxy\_password` - The proxy password


**Example:**

```
{
  "license_key": "YOUR_LICENSE_KEY_HERE",

  "proxy_host": "proxy.mycompany.com",

  "proxy_port": 9000
}
```

#### Configuring the plugin.template.json file: 

The second file, plugin.template.json, contains data specific to each plugin (e.g., a list of hosts and port combinations for what you are monitoring). Templates for both of these files should be located in the ‘config’ directory in your extracted plugin folder.

Make a copy of this template and rename it to plugin.json. Shown below is an example of the plugin.json file’s contents.

**NOTE** - You can add multiple objects to the “agents” array to monitor multiple F5 BIG-IP instances.

**NOTE:** Each object in the "agents" array should have a unique "instance_name".

**Fields**

| Field Name  |  Description |
|:------------- |:-------------|
| instance_name | Alias for the name of your F5 BIG-IP instance that will appear in the User Interface |
| host | IP address or hostname of F5 BIG-IP Management IP |
| port | Port used to connect to the F5 BIG-IP REST API. Default is `443` |
| username | User Name for F5 BIG-IP login. |
| password | Password for F5 BIG-IP login. |

**Example:**

```
{
  "agents": [
    {
      "instance_name": "YOUR_VALUE_HERE",
      "username": "YOUR_VALUE_HERE",
      "password": "YOUR_VALUE_HERE",
      "host": "YOUR_VALUE_HERE",
      "port": "YOUR_VALUE_HERE"
    }
  ]
}
```

## Using the Plugin
For more information about navigating New Relic’s user interface, refer to their [Using a plugin documentation](https://docs.newrelic.com/docs/plugins/plugins-new-relic/using-plugins/using-plugin) section.

## Support Resources
For questions or issues regarding the F5 BIG-IP Plugin for New Relic, visit http://support.bluemedora.com. 

## Metrics Source Documentation

**System Overview**

| Metric Name  |  Description |
|:------------- |:-------------|
| Memory (GB) |  The Used and Total memory of the F5 BIG-IP system |
| Node Received Throughput (MB/sec) |  Received throughput for Nodes |
| Node Transmitted Throughput (MB/sec) |  Transmitted throughput for Nodes  |
| Node Received Packets (Packets/sec) |  Received packets for Nodes  |
| Node Transmitted Packets (Packets/sec) |  Transmitted packets for Nodes  |
| Disk Total Space (GB)  |  Total space across disks in system  |
| Disk Used Space (GB)  |  Total used space across disks in system  |

**Disks**

| Metric Name  |  Description |
|:------------- |:-------------|
| Total Space (GB)  |  Total space across disks in system  |
| Used Space (GB)  |  Total used space across disks in system  |
| Free Space (GB)  |  Total free space across disks in system  |
| Reserved Space (GB)  |  Total reserved space across disks in system  |

**Modules**

| Metric Name  |  Description |
|:------------- |:-------------|
| Provisioned CPU (%)  |  Provisioned CPU across modules |
| Provisioned Disk Space (GB) |  Provisioned disk space across modules  |
| Provisioned Memory (GB)  |  Provisioned memory across modules |
| Provisioned Host Memory (GB) |  Provisioned host memory across modules  |

**Virtual Servers**

| Metric Name | Description |
|:------------- |:-------------|
| Requests (Requests/sec) | Requests over time |
| Connections (Connections) | Connections per virtual server |
| Received Throughput (MB/sec) | Received Throughput for virtual server |
| Transmitted Throughput (MB/sec) | Transmitted Throughput for virtual server |
| Received Packets (Packets/sec) | Received Packets for virtual server |
| Transmitted Packets (Packets/sec) | Transmitted Packets for virtual server |

**Nodes**

| Metric Name | Description |
|:------------- |:-------------|
| Requests (Requests/sec) | Requests over time |
| Connections (connections) | Connections per node |
| Received Throughput (MB/sec) | Received Throughput for node |
| Transmitted Throughput (MB/sec) | Transmitted Throughput for node |
| Received Packets (Packets/sec) | Received Packets for node |
| Transmitted Packets (Packets/sec) | Transmitted Packets for node |

**Pools**

| Metric Name | Description |
|:------------- |:-------------|
| Requests (Requests/sec) | Requests over time |
| Active Members (members) | Currently active members |
| Connections (connections) | Connections per pools |
| Received Throughput (MB/sec) | Received Throughput for pools |
| Transmitted Throughput (MB/sec) | Transmitted Throughput for pools |
| Received Packets (Packets/sec) | Received Packets for pools |
| Transmitted Packets (Packets/sec) | Transmitted Packets for pools |

**Pools Members**

| Metric Name | Description |
|:------------- |:-------------|
| Requests (Requests/sec) | Requests over time |
| Connections (connections) | Connections per pool members |
| Sessions (sessions) | Currently active session |
| Received Throughput (MB/sec) | Received Throughput for pool members |
| Transmitted Throughput (MB/sec) | Transmitted Throughput for pool members |
| Received Packets (Packets/sec) | Received Packets for pool members |
| Transmitted Packets (Packets/sec) | Transmitted Packets for pool members |