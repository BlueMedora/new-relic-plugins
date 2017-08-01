# New Relic Plugin for Amazon DynamoDB

The **Blue Medora New Relic Plugin for Amazon DynamoDB** allows you to monitor your Amazon DynamoDB performance data from within the New Relic platform by pulling metrics in from the system and displaying them in a set of intuitive, graph-based monitoring dashboards.
				
This guide includes instructions for installing and configuring the Blue Medora Amazon DynamoDB Plugin for New Relic. 
If you’re having a bad experience with one of our plugins, please get in touch and we’ll be happy to help you out.

----

## System Requirements

The Amazon DynamoDB plugin connects to a DynamoDB Region via account access keys. Before installing and configuring the plugin, ensure your system meets the following requirements:

**New Relic Requirements**

- A New Relic account. (Sign up for a free account [here](http://newrelic.com).)

**Amazon DynamoDB Plugin Requirements**

- Java 1.7 or higher
- **A Blue Medora License.** A trial license will ship with the plugin that is valid for 14 days. To obtain a production license or get pricing information for the plugin, please contact sales@bluemedora.com.

----

## Installing the Plugin

We recommend using the New Relic Platform Installer for installing and running your Blue Medora plugins for New Relic.

The New Relic Platform Installer (NPI) is a command line tool that helps you easily download, configure, and manage New Relic Platform Plugins.  For more information, refer to the [Installing an NPI-compatible plugin documentation](https://docs.newrelic.com/docs/plugins/plugins-new-relic/installing-plugins/installing-npi-compatible-plugin).

Once the NPI tool has been installed, run the following command:

```
  ./npi install com.bluemedora.amazon.dynamodb
``` 

**NOTE:** This command will take care of the creation of `newrelic.json` and `plugin.json` files described in the [Configuring the Plugin](#Configuring-the-Plugin) section.

###### [Download Plugin for Manual Installation](https://newrelic-bluemedora.s3.amazonaws.com/com-bluemedora-amazon-dynamodb/newrelic_amazon_dynamodb_plugin-2.1.2_20170801_144305.tar.gz)

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

The second file, `plugin.template.json`, contains data specific to each plugin (e.g., a list of hosts and port combinations for what you are monitoring). Templates for both of these files should be located in the `config` directory in your extracted plugin folder.

Make a copy of this template and rename it to `plugin.json`. Shown below is an example of the `plugin.json` file’s contents.

**NOTE** You can add multiple objects to the “agents” array to monitor multiple Amazon DynamoDB instances.

**NOTE:** Each object in the "agents" array should have a unique `instance_name`.

**Fields**

| Field Name  |  Description |
|:------------- |:-------------|
| polling_interval_seconds | The number of seconds between each data collection. |
| downtime_tracking_minutes | The number of minutes into the past that will be considered when calculating downtime |
| instance_name | Alias for the name of your Amazon DynamoDB instance that will appear in the User Interface |
| access_key_id | Amazon AWS Access Key ID can be found by following [this guide](http://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSGettingStartedGuide/AWSCredentials.html) |
| secret_access_key | Amazon AWS Secret Access Key can be found by following [this guide](http://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSGettingStartedGuide/AWSCredentials.html) |
| region | Amazon AWS region where DynamoDB instance resides. Acceptable values are `U_WEST_1`, `SA_EAST_1`, `AP_NORTHEAST_2`, `US_EAST_1`, `AP_NORTHEAST_1`, `CN_NORTH_1`, `EU_CENTRAL_1`, `AP_SOUTHEAST_1`, `AP_SOUTHEAST_2`, `US_WEST_2`, `GovCloud`, `US_WEST_1` |
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
      "access_key_id": "your_value_here",
      "secret_access_key": "your_value_here",
      "region": "US_WEST_1"      // Valid Values: "US_WEST_1", "SA_EAST_1", "AP_NORTHEAST_2", "US_EAST_1", "AP_NORTHEAST_1", "CN_NORTH_1", "EU_CENTRAL_1", "AP_SOUTHEAST_1", "AP_SOUTHEAST_2", "US_WEST_2", "GovCloud", "US_WEST_1",
      "send_to_plugin": {
        "dynamo_connection": true,
        "table": true,
        "global_secondary_index": true,
        "local_secondary_index": true,
        "key_schema": true,
      },
      "send_to_insights": {
        "dynamo_connection": true,
        "table": true,
        "global_secondary_index": true,
        "local_secondary_index": true,
        "key_schema": true,
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
For questions or issues regarding the Amazon DynamoDB Plugin for New Relic, visit http://support.bluemedora.com. 

----

## Metrics Source Documentation     

**System Overview**

| Metric Name  |  Description |
|:------------- |:-------------|
| Table Read Throttle Events (events) | The number of read throttle events across DynamoDB tables |
| Table Write Throttle Events (events) | The number of write throttle events across DynamoDB tables |
| Table Read Capacity Usage (%) | Percent usage of Provisioned Read capacity per DynamoDB table |
| Table Write Capacity Usage (%) | Percent usage of Provisioned Write capacity per DynamoDB table |
| Global Secondary Index Size (KB) | Size across global secondary indexes |
| Local Secondary Index Size (KB) | Size across local secondary indexes |

**Tables**

| Metric Name  |  Description |
|:------------- |:-------------|
| Read Throttle Events (events) | The number of read throttle events per DynamoDB tables |
| Write Throttle Events (events) | The number of write throttle events per DynamoDB tables |
| Read Capacity Usage (%) | Percent usage of Provisioned Read capacity per DynamoDB table |
| Write Capacity Usage (%) | Percent usage of Provisioned Write capacity per DynamoDB table |
| Read Capacity Remaining (Units) | The number of Read capacity units that are free per DynamoDB table |
| Write Capacity Remaining (Units) | The number of Write capacity units that are free per DynamoDB table |

**Global Secondary Index**

| Metric Name  |  Description |
|:------------- |:-------------|
| Size (KB) | Size per global secondary index |
| Item Count (items) | The number of items per global secondary index |
| Provisioned Read Capacity (units) | Provisioned Read Capacity per global secondary index |
| Provisioned Write Capacity (units) | Provisioned Write Capacity per global secondary index |

**Local Secondary Index**

| Metric Name  |  Description |
|:------------- |:-------------|
| Size (KB) | Size per local secondary index |
| Item Count (items) | The number of items per local secondary index |

**Summary**

| Metric Name  |  Description |
|:------------- |:-------------|
| Downtime (%) | The percentage of times during the downtime tracking window during which the system has been unavailable |
| Read Throttle Events | The number of recent read throttle events |
| Write Throttle Events | The number of recent write throttle events |
| Read Capacity Usage | The percentage of read capacity used |
| Write Capacity Usage | The percentage of write capacity used |

