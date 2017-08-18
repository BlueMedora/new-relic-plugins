# ![Blue Medora Logo](http://www.bluemedora.com/favicon.ico) Blue Medora Hadoop Plugin For New Relic 

The **Blue Medora Apache Hadoop Plugin for New Relic** allows you to monitor your Hadoop cluster environment within the New Relic platform by collecting metrics from the system and displaying them in an arrangement of intuitive, graphical based monitoring dashboards. 

This guide includes the proper installation and configuration needed to setup the Blue Medora Apache Hadoop Plugin for New Relic. 

----

## System Requirements 

The Apache Hadoop plugin connects to the Apache Hadoop cluster using read-only JMX managed beans formatted in JSON over HTTP.

**New Relic Requirements**

- A New Relic account. (Sign up for a free account [here](https://newrelic.com/signup/).)

**Apache Hadoop Plugin Requirements**

- Hadoop 2.7.x+ with HDFS & YARN
- Java 1.7 or higher
- **A Blue Medora License.** A trial license will ship with the plugin that is valid for 14 days. To obtain a production license or get pricing information for the plugin, please contact <sales@bluemedora.com>.

For more detailed system requirements, please refer [here](https://ambari.apache.org/1.2.3/installing-hadoop-using-ambari/content/ambari-chap1-2.html).

## Installing the Plugin 

We recommend using the New Relic Platform Installer for installing and running your Blue Medora plugins for New Relic. 
 
The New Relic Platform Installer (NPI) is a command line tool that helps you easily download, configure, and manage New Relic Platform Plugins. For more information, please refer to the [Installing an NPI-compatible plugin documentation](https://docs.newrelic.com/docs/plugins/plugins-new-relic/installing-plugins/installing-npi-compatible-plugin). 

Once the NPI tool has been installed, run the following command: 

```
	./npi install com.bluemedora.apache.hadoop
```

**Note:** This command will take care of the creation of `newrelic.json` and `plugin.json` files described in the [Configuring the Plugin](#Configuring-the-Plugin) section.

###### [Download Plugin for Manual Installation](https://newrelic-bluemedora.s3.amazonaws.com/com-bluemedora-apache-hadoop/newrelic_apache_hadoop_plugin-1.0.2_20170818_174126.tar.gz)

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

**NOTE** You can add multiple objects to the “agents” array to monitor multiple Hadoop instances.

**NOTE:** Each object in the "agents" array should have a unique `instance_name`.

**Fields**

| polling_interval_seconds | The number of seconds between each data collection. |
| downtime_tracking_minutes | The number of minutes into the past that will be considered when calculating downtime |
| instance_name | Alias for the name of your Hadoop instance that will appear in the User Interface |
| name_node_host | Comma separated list of Name Nodes |
| name_node_port | Port on which to connect to Name Nodes |
| resource_manager_host | Comma separated list of Resource Managers | 
| resource_manager_port | Port on which to connect to Resource Managers |
| timeout | Number of seconds to wait before timing out |
| max_threads | The maximum number of threads that will be used in data collection |

**Example**

```
{
  "polling_interval_seconds": 60,
  "downtime_tracking_minutes": 60,
  "agents": [
    {
      "instance_name": "your_value_here",
      "name_node_host": "name_node1, name_node2",
      "name_node_port": 50070,
      "resource_manager_host": "resourcemgr-1, resourcemgr-2",
      "resource_manager_port": 8088,
      "collection_mode": "Standard or Light",
      "timeout": 5,
      "max_threads": 30,
      "send_to_plugin": {
        "cluster": true,
        "data_node": true,
        "name_node": true,
        "node_manager": true,
        "resource_manager": true
      },
      "send_to_insights": {
        "cluster": true,
        "data_node": true,
        "name_node": true,
        "node_manager": true,
        "resource_manager": true,
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
For questions or issues regarding the Apache Hadoop Plugin for New Relic, visit http://support.bluemedora.com. 

----

## Metrics Source Documentation

**Summary**

| Metric Name  |  Description |
|:------------- |:-------------|
| Downtime (%) | The percentage of times during the downtime tracking window during which the system has been unavailable |
| Node Managers Lost | The number of Node Managers currently down |
| Data Nodes Dead | The number of Data Nodes currently dead |
| Volume Failures | The number of Volume failures |
| Containers Failures | The number of Containers failures |

**Overview**

| Metric Name  |  Description |
|:------------- |:-------------|
| Cluster Node Managers | The number of Node Managers in each state (Decommissioned, Unhealthy, Rebooted, Lost, Active) |
| Applications Failed | The number of Application failures |
| Applications Running | The number of Applications running |
| Applications Completed | The number of Application completions |
| Node Manager Memory Allocated (GB) | The amount of Allocated Memory on each Node Manager |
| Node Manager Memory Available (GB) | The amount of Available Memory on each Node Manager |


**Data Nodes**

| Metric Name  |  Description |
|:------------- |:-------------|
| Blocks Read (blocks/second) | The number of Blocks per second Read on each Data Node |
| Blocks Removed (blocks/second) | The number of Blocks per second Removed on each Data Node |
| Blocks Replicated (blocks/second) | The number of Blocks per second Replicated on each Data Node |
| Blocks Written (blocks/second) | The number of Blocks per second Written on each Data Node |
| Read Throughput (GB/second) | The amount of data Read for each Data Node |
| Write Throughput (GB/second) | The amount of data Written for each Data Node |
| Disk Space Remaining (GB) | The amount of Disk Space Remaining on each Data Node |
| Volumes Failed | The number of Volume failures |

**Name Nodes**

| Metric Name  |  Description |
|:------------- |:-------------|
| Capacity Used (GB) | The Capacity currently being used by each Name Node |
| Capacity Remaining (GB) | The Capacity currently remaining for each Name Node |
| Blocks Missing | The number of Blocks Missing on each Name Node |
| Data Nodes Dead | The number of Data Nodes currently dead |
| Volumes Failed | The number of Volume failures |

**Node Managers**

| Metric Name  |  Description |
| :------------- |:-------------|
| Containers Allocated | The amount of Containers currently Allocated |
| Containers Completed | The amount of Containers currently Completed |
| Containers Failed | The amount of Containers currently Failed |
| Containers Launched | The amount of Containers currently Launched |
| Memory Allocated (GB) | The amount of Allocated Memory on each Node Manager |
| Memory Available (GB) | The amount of Available Memory on each Node Manager |
| Virtual Cores Allocated | The amount of Virtual Cores Allocated for each Node Manager |
| Virtual Cores Allocated Ratio | The percent of Virtual Cores Allocated among Virtual Cores Total for each Node Manager |
| Virtual Cores Available | The amount of Virtual Cores Available for each Node Manager |
| Virtual Cores Total | The amount of Virtual Cores Total for each Node Manager |

**Resource Managers**

| Metric Name  |  Description |
| :------------- |:-------------|
| Applications Failed | The number of Application failures |
| Applications Complete | The number of Application completions |
| Applications Running | The number of Applications running |
| Users Active | The total number of Active Users |
| Queue Memory Allocated (GB)| The amount of Queue Memory Allocated for each Resource Manager |
| Queue Memory Available (GB)| The amount of Queue Memory Available for each Resource Manager |