# New Relic Plugin for Apache Cassandra

The **Blue Medora Apache Cassandra Plugin for New Relic** allows you to monitor your Cassandra databases within the New Relic platform by collecting metrics from the system and displaying them in an arrangement of intuitive, graphical based monitoring dashboards. 

This guide includes the proper installation and configuration needed to setup the Blue Medora Apache Cassandra Plugin for New Relic. 

----

## System Requirements 

The Apache Cassandra plugin connects to the Apache Cassandra database using JMX.

**New Relic Requirements**

- A New Relic account. (Sign up for a free account [here](https://newrelic.com/signup/). 

**Apache Cassandra Plugin Requirements**

- **Cassandra versions.** The plugin is compatible with Cassandra versions 3.9+
- Java 1.7 or higher
- **A Blue Medora License.** A trial license will ship with the plugin that is valid for 14 days. To obtain a production license or get pricing information for the plugin, please contact <sales@bluemedora.com>.


## Installing the Plugin 

We recommend using the New Relic Platform Installer for installing and running your Blue Medora plugins for New Relic. 
 
The New Relic Platform Installer (NPI) is a command line tool that helps you easily download, configure, and manage New Relic Platform Plugins. For more information, please refer to the [Installing an NPI-compatible plugin documentation](https://docs.newrelic.com/docs/plugins/plugins-new-relic/installing-plugins/installing-npi-compatible-plugin).

Once the NPI tool has been installed, run the following command: 

```
	./npi install com.bluemedora.apache.cassandra
```

**Note:** This command will take care of the creation of `newrelic.json` and `plugin.json` files described in the [Configuring the Plugin](#Configuring-the-Plugin) section.

###### [Download Plugin for Manual Installation](https://newrelic-bluemedora.s3.amazonaws.com/com-bluemedora-apache-cassandra/newrelic_apache_cassandra_plugin-1.0.4_20170721_130118.tar.gz)

----     

## Configuring the Plugin 

From the extracted plugin folder you will receive when downloading your plugin, you will find the following files 

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

## Configuring the `newrelic.template.json` file 

The first file, `newrelic.template.json`, contains configurations used by all Platform plugins (e.g., license key, logging information, proxy settings) and can be shared across your plugins. 
Make a copy of this template and rename it to `newrelic.json`. Listed below are the configurable fields within the newrelic.json file:

**New Relic License Key** - The only requried field in the `newrelic.json` file is the License Key. This unique identifier informs New Relic about the specific account tied to the plugin. For more information on the License Key, [refer to the New Relic License key documentation](https://docs.newrelic.com/docs/accounts-partnerships/accounts/account-setup/license-key). 


**Example:**

``` 
{
	"license_key": "YOUR LICENSE KEY" 	
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

**NOTE** You can add multiple objects to the “agents” array to monitor multiple Cassandra instances.

**NOTE:** Each object in the "agents" array should have a unique `instance_name`.

**Fields**

| polling_interval_seconds | The number of seconds between each data collection. |
| downtime_tracking_minutes | The number of minutes into the past that will be considered when calculating downtime |
| instance_name | Alias for the name of your Cassandra instance that will appear in the User Interface |
| host | The hostname or IP address of any node in the Cassandra cluster |
| port | The port on which to communicate with the node |
| username | The username of a read-only database user |
| password | The password of the read-only database user |

**Example**

```
{
  "polling_interval_seconds": 60,
  "downtime_tracking_minutes": 60, 
  "agents": [
    {
      "instance_name": "your_value_here",
      "host": "your_value_here",
      "username": "your_value_here",
      "password": "your_value_here",
      "port": 7199,
      "send_to_plugin": {
        "cluster": true,
        "keyspace": true,
        "node": true,
        "nodeKeyspace": true,
        "nodeTable": true,
        "table": true
      },
      "send_to_insights": {
        "cluster": true,
        "keyspace": true,
        "node": true,
        "nodeKeyspace": true,
        "nodeTable": true,
        "table": true,
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
For questions or issues regarding the Apache Cassandra Plugin for New Relic, visit http://support.bluemedora.com. 

----

## Metrics Source Documentation

**Summary**

| Metric Name  |  Description |
|:------------- |:-------------|
| Downtime (%) | The percentage of times during the downtime tracking window during which the system has been unavailable |
| Average Read Latency (ms) | The average read latency among all Nodes |
| Average Write Latency (ms) | The average write latency among all Nodes |
| Total Used Heap Memory (bytes) | The total used heap memory among all Nodes |
| Total Used Non Heap Memory (bytes) | The total used non-heap memory among all Nodes |

**Clusters**

| Metric Name  |  Description |
|:------------- |:-------------|
| Activity Count | The number of current Activities across all Nodes |
| Average Range Slice Latency (ms) | The average range slice latency among all Nodes |
| Average Read Latency (ms) | The average read latency among all Nodes |
| Average Write Latency (ms) | The average write latency among all Nodes |
| Total Pending Compaction Executor Tasks | The amount of Compaction Executor Tasks among all Nodes |
| Total Pending Gossip Stage Tasks | The amount of Gossip Stage Tasks among all Nodes |
| Total Pending Read Stage Tasks | The amount of Read Stage Tasks among all Nodes |
| Total Pending Mutation Stage Tasks | The amount of Mutation Stage Tasks among all Nodes |
| Total Used Heap Memory (bytes) | The total used heap memory among all Nodes |
| Total Used Non Heap Memory (bytes) | The total used non-heap memory among all Nodes |
| Par New Collections (collections/second) | The rate of Par New Collections per second |
| Total Par New Collection Time (seconds) | The time of Par New Collections among all Nodes |
| Total Concurrent Mark Sweep Collections (collections/second) | The rate of Total Concurrent Mark Sweep Collections per second |
| Total Concurrent Mark Sweep Collections Time (seconds) | The time of Total Concurrent Mark Sweep Collections among all Nodes |
| Node Count | The number of Nodes in the Cluster |

**Nodes**

| Metric Name  |  Description |
|:------------- |:-------------|
| Read Latency (ms) | The read latency for each Node |
| Write Latency (ms) | The write latency for each Node |
| Range Slice (ms) | The range slice latency for each Node |
| View Write Latency (ms) | The view write latency for each Node |

**Keyspaces**

| Metric Name  |  Description |
|:------------- |:-------------|
| Average Read Latency (ms) | The average read latency for each Keyspace |
| Average Write Latency (ms) | The average write latency for each Keyspace |
| Average Range Latency (ms) | The average range slice latency for each Keyspace |
| Total Disk Space Used (MB) | The amount of Disk Space Used by each Keyspace |

**Node Keyspaces**

| Metric Name  |  Description |
|:------------- |:-------------|
| Read Latency (ms) | The read latency for each Node Keyspace |
| Write Latency (ms) | The write latency for each Node Keyspace |
| Range Latency (ms) | The range latency for each Node Keyspace |
| Total Disk Space Used (GB) | The amount of Disk Space Used by each Node Keyspace |

**Tables**

| Metric Name  |  Description |
|:------------- |:-------------|
| Average Read Latency (ms) | The average read latency for each Table |
| Average Write Latency (ms) | The average write latency for each Table |
| Average Range Latency (ms) | The average range slice latency for each Table |
| Total Disk Space Used (MB) | The amount of Disk Space Used by each Table |

**Node Tables**

| Metric Name  |  Description |
|:------------- |:-------------|
| Read Latency (ms) | The read latency for each Node Table |
| Write Latency (ms) | The write latency for each Node Table |
| Range Latency (ms) | The range latency for each Node Table |
| Total Disk Space Used (GB) | The amount of Disk Space Used by each Node Table |
