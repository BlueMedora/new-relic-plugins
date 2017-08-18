# Blue Medora Cisco Nexus Plugin for New Relic

The **Blue Medora Cisco Nexus Plugin for New Relic** allows you to monitor your Cisco Nexus performance data from within the New Relic platform by pulling in metrics from the system and displaying them in a set of intuitive, graph-based monitoring dashboards.           

This guide includes instructions for installing and configuring the Blue Medora Cisco Nexus Plugin for New Relic.
If you’re having a bad experience with one of our plugins, please get in touch and we’ll be happy to help you out.

----

## System Requirements

The Cisco Nexus plugin connects to the Cisco Nexus hardware (switch) using SNMP v2, v2c, or v3.  Before installing and configuring the plugin, ensure your system meets the following requirements:

**New Relic Requirements**

- A New Relic account (Sign up for a free account [here](http://newrelic.com).)

**Cisco Nexus Plugin Requirements**

- SNMP v2, v2c, or v3 enabled **Cisco Nexus switch(es) 1k, 3k, 4k, 5k, 7k, and/or 9k**
- Java 1.7 or higher
- **A Blue Medora License.** A trial license will ship with the plugin that is valid for 14 days. To obtain a production license or get pricing information for the plugin, please contact sales@bluemedora.com.

----

## Installing the Plugin

We recommend using the New Relic Platform Installer for installing and running your Blue Medora plugins for New Relic.

The New Relic Platform Installer (NPI) is a command line tool that helps you easily download, configure, and manage New Relic Platform Plugins.  For more information, refer to the [Installing an NPI-compatible plugin documentation](https://docs.newrelic.com/docs/plugins/plugins-new-relic/installing-plugins/installing-npi-compatible-plugin).

Once the NPI tool has been installed, run the following command:

```
  ./npi install com.bluemedora.cisco.nexus
``` 

**Note:** This command will take care of the creation of `newrelic.json` and `plugin.json` files described in the [Configuring the Plugin](#Configuring-the-Plugin) section.

###### [Download Plugin for Manual Installation](https://newrelic-bluemedora.s3.amazonaws.com/com-bluemedora-cisco-nexus/newrelic_cisco_nexus_plugin-3.2.1_20170817_192706.tar.gz)

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

#### Configuring the `plugin.template.json` file: 

The second file, `plugin.template.json`, contains data specific to each plugin (e.g., a list of hosts and port combinations for what you are monitoring). Templates for both of these files should be located in the ‘config’ directory in your extracted plugin folder.

Make a copy of this template and rename it to `plugin.json`. Shown below is an example of the `plugin.json` file’s contents.

**NOTE:** You can add multiple objects to the “agents” array to monitor multiple Cisco Nexus instances. 

**NOTE:** Each object in the "agents" array should have a unique "instance_name".

**Fields**

| Field Name  |  Description |
|:------------- |:-------------|
| polling_interval_seconds | The number of seconds between each data collection. |
| downtime_tracking_minutes | The number of minutes into the past that will be considered when calculating downtime |
| instance_name | The name of your New Relic Cisco Nexus instance that will appear in the User Interface |
| version | SNMP version acceptable values `v2c` or `v3` for SNMP Version 2 or Version 3 respectively |
| management_ip | IP address of Nexus Switch |
| snmp_port | Optional field, port SNMP communicates over. Defaults to `161` |
| community_string | Only applicable if `version` is `v2c`. The SNMP community string required to connect |
| security_level | Only applicable if `version` is `v3`. Acceptable values are `auth_priv`, `auth_nopriv`, or `noauth_nopriv` |
| user | Only applicable if `version` is `v3`. SNMP user name |
| auth_password | Only applicable if `version` is `v3`. SNMP Authentication password. Only needed if `security_level` is `auth_priv` or `auth_nopriv` |
| privacy_password | Only applicable if `version` is `v3`. SNMP privacy password, Only needed if `security_level` is `auth_priv` |
| privacy_type | Only applicable if `version` is `v3`. SNMP encryption type. Acceptable values are `privAES256`, `privAES192`, `privAES128`, `privDES`, or `priv3DES` for  256 bit AES, 192 bit AES, 128 bit AES, DES, or 3-DES respectively |
| send_to_plugin | Indicates whether or not to send data to New Relic Plugins. See [Blue Medora's New Relic Knobs and Levers Readme](https://github.com/BlueMedora/new-relic-plugins/blob/master/configuration-variants/readme.md) for more details |
| send_to_insights | Indicates whether or not to send data to New Relic Insights. See [Blue Medora's New Relic Knobs and Levers Readme](https://github.com/BlueMedora/new-relic-plugins/blob/master/configuration-variants/readme.md) for more details |

**Examples**

```
{
  "polling_interval_seconds": 60,
  "downtime_tracking_minutes": 60,
  "agents": [
    {
      "instance_name": "Your SNMP Version 2 Instance",
      "version": "v2" //Valid values: v2, v2c,
      "management_ip": "your_value_here",
      "community_string": "your_value_here",
      "snmp_port": 161,
      "protocol": "https" //Valid values: http, https,
      "validate_certificate_against_truststore": "false" //Valid values: true, t, yes, y, 1, false, no, n, 0,
      "send_to_plugin": {
        "cisco_networking_switch": true,
        "cisco_networking_port": true,
        "cisco_networking_l3_interface": true
      },
      "send_to_insights": {
        "cisco_networking_hsrp_group": true,
        "cisco_networking_hsrp_group_member": true,
        "cisco_networking_fan": true,
        "cisco_networking_power_module": true,
        "cisco_networking_sensor": true,
        "cisco_networking_switch": true,
        "cisco_networking_port": true,
        "cisco_networking_l3_interface": true,
        "relationships": true,
        "notifications": "INFO" //Valid values: true, false, ERROR, WARNING, INFO, DEBUG
      }
    },
    {
      "instance_name": "Your SNMP Version 3 Instance",
      "version": "v3",
      "management_ip": "your_value_here",
      "user": "your_value_here",
      "auth_password": "your_value_here",
      "privacy_password": "your_value_here",
      "authentication_type": "authSHA" //Valid values: authSHA, authMD5 ,
      "privacy_type": "privAES256" //Valid values: privAES256, privAES192, privAES128, privDES, priv3DES ,
      "security_level": "auth_priv" //Valid values: auth_priv, auth_nopriv, noauth_priv ,
      "send_to_plugin": {
        "cisco_networking_switch": true,
        "cisco_networking_port": true,
        "cisco_networking_l3_interface": true
      },
      "send_to_insights": {
        "cisco_networking_hsrp_group": true,
        "cisco_networking_hsrp_group_member": true,
        "cisco_networking_fan": true,
        "cisco_networking_power_module": true,
        "cisco_networking_sensor": true,
        "cisco_networking_switch": true,
        "cisco_networking_port": true,
        "cisco_networking_l3_interface": true,
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
For questions or issues regarding the Blue Medora Cisco Nexus Plugin for New Relic, visit http://support.bluemedora.com. 

----     

## Metrics Source Documentation

**Switch Overview**

| Metric Name  |  Description |
|:------------- |:-------------|
| Total Throughput (MB/sec) | The total throughput in megabytes per second |
| Total Packets (Packets/sec) | The total amount of packets per second |
| Port Status Count  | The number of ports per status (Down, Up, or In Error) |

**Port**

| Metric Name  |  Description |
|:------------- |:-------------|
| Inbound Throughput (MB/sec) | The inbound throughput of a port in megabytes per second  |
| Outbound Throughput (MB/sec) | The outbound throughput of a port in megabytes per second |
| Inbound Packets (Packets/sec) | The amount of inbound packets per second of a port |
| Outbound Packets (Packets/sec) | The amount of outbound packets per second of a port |

**L3 Interface**

| Metric Name  |  Description |
|:------------- |:-------------|
| Inbound Throughput (MB/sec) | The inbound throughput of an L3 Interface in megabytes per second  |
| Outbound Throughput (MB/sec) | The outbound throughput of an L3 Interface in megabytes per second |
| Inbound Packets (Packets/sec) | The amount of inbound packets per second of an L3 Interface |
| Outbound Packets (Packets/sec) | The amount of outbound packets per second of an L3 Interface |

**Summary**

| Metric Name  |  Description |
|:------------- |:-------------|
| Inbound (bytes/sec) | The total inbound throughput in bytes per second |
| Outbound (bytes/sec) | The total outbound throughput in bytes per second |
| Ports in Error (%) | Percentage of ports in which the status is "In Error" |
| Ports Down (%) | Percentage of ports in which the status is "Down" |
| Downtime (%) | The percentage of times during the downtime tracking window during which the system has been unavailable |