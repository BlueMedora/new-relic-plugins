## Application
| Metric Name | Description | 
| ----------- | :---------- | 
| Device Group | Device group running Application Service | 
| Full Path | BIG-IP defined unique full path | 
| Kind | BIG-IP defined type | 
| Name | User defined name | 
| Pool to Use | Server side pool load balancing requests | 
| Self Link | BIG-IP unique link and full path | 
| Template | Template applied to Application including security and monitoring rules | 
| Template Modified | Indicator of modifications made to out of the box template | 
| Traffic Group | Current traffic group service is applied to | 
 
## System
| Metric Name | Description | 
| ----------- | :---------- | 
| Average CPU IO Wait Utilization | Average percentage of time the CPU is waiting on IO | 
| Average CPU Idle Utilization | Average percentage of time the CPU is idle | 
| Average CPU Interrupt Request Utilization | Average percentage of time the CPU is handling interrupt requests | 
| Average CPU Nice Level Utilization | Average percentage of time the CPU is handling nice level processes | 
| Average CPU Soft Interrupt Request Utilization | Average percentage of time the CPU is handling soft interrupt requests | 
| Average CPU Stolen Utilization | Average percentage of time the CPU is handling reclaimed cycles by the hypervisor | 
| Average CPU System Utilization | Average percentage of time the CPU is used by the kernel | 
| Average CPU User Utilization | Average percentage of time the CPU is used by user processes | 
| CPU Idle Ticks | Amount of CPU ticks that the CPU was idle* | 
| CPU Usage Ticks: System | Amount of CPU ticks used by the kernel processes* | 
| CPU Usage Ticks: User | Amount of CPU ticks used by user processes* | 
| Chassis Serial Number | Chassis Serial Number for the current device | 
| Device Name | Name of the current device | 
| Host and Port | Host and Port combination we are using to connect to this BIG-IP System | 
| Memory Total | Total amount of Memory available on the current device | 
| Memory Used | Current Memory being used on the current device | 
| Platform | Platform of the current device | 
| Product | Product Name for the current device | 
 
## Device
| Metric Name | Description | 
| ----------- | :---------- | 
| Chassis ID | Chassis ID | 
| Edition | Edition type | 
| Failover State | Failover state | 
| Full Path | BIG-IP System full path of the device | 
| Host Name | Hostname used for dns | 
| Kind | Kind of Device | 
| Management IP | IP to access the Management Console | 
| Marketing Name | Marketing name defined for the device | 
| Name | Name of the Device | 
| Platform | Unique ID for the Type of Platform | 
| Product | Product Name of the device | 
| Self Device | Identifier of the Self Device | 
| Self Link | Internal Link defining the Device object in BIG-IP | 
| Sync State | Synchronization state of the BIG-IP Device to the cluster | 
| Version | Version of the BIG-IP System device | 
 
## Device Group
| Metric Name | Description | 
| ----------- | :---------- | 
| Auto Sync | Auto Sync Setting | 
| Description | User defined Description | 
| Full Path | BIG-IP System full path | 
| Kind | Kind of Group | 
| Name | User defined Name | 
| Network Failover | Network Failover Type | 
| Self Link | Internal Link defining the Device Group object in BIG-IP | 
| Sync State | Current Sync State | 
| Type | Type of Group | 
 
## Disk
| Metric Name | Description | 
| ----------- | :---------- | 
| Free Space | Free space for the active disk | 
| Full Path | BIG-IP System path for the disk | 
| Kind | Type of Disk | 
| Mode | Current Usage mode of the disk | 
| Name | Name of the Disk | 
| Self Link | Internal Link defining the Disk object in BIG-IP | 
| Size | Size of the Disk | 
| Space In-Use | Used space for the active disk | 
| Space Reserved | Reserved space for the active disk | 
 
## Module
| Metric Name | Description | 
| ----------- | :---------- | 
| CPU Provisioned | The amount of CPU provisioned for the module | 
| Disk Provisioned | The amount of disk space provisioned for the module | 
| Full Path | The Full path of the Module on the BIG-IP System | 
| Host Memory Provisioned | The amount of Host memory provisioned for the module | 
| Kind | The Type of Module | 
| Memory Provisioned | The amount of Memory provisioned for the module | 
| Name | The Name of the Module | 
| Provisioning Level | The provisioning Level of the Module on the BIG-IP System | 
| Self Link | Internal Link defining the Module object in BIG-IP | 
 
## Node
| Metric Name | Description | 
| ----------- | :---------- | 
| Availability State | Current BIG-IP availability state to the Node | 
| Bits In | The amount of data received from the BIG-IP Node* | 
| Bits Out | The amount of data sent to the BIG-IP Node* | 
| Current Connections | Current number of network connections from BIG-IP | 
| Current Sessions | Current number of sessions | 
| Enabled State | Current BIG-IP enabled state | 
| Full Path | BIG-IP full path identification | 
| IP Address | BIG-IP network address to send to the node | 
| Kind | Type of Node in BIG-IP | 
| Maximum Connections | Current highest number of network connections reported from BIG-IP | 
| Monitor Rule | BIG-IP Health Monitor rule | 
| Monitor Status | Current Health Monitor rule status | 
| Name | User defined name | 
| Packets In | The number of packets received from the BIG-IP Node* | 
| Packets Out | The number of packets sent to the BIG-IP Node* | 
| Requests | Current number of requests over the last collection from BIG-IP* | 
| Self Link | BIG-IP System internal link and full path for the Node | 
| Session Status | Current status of the session | 
| State | Current BIG-IP State | 
| Status Reason | BIG-IP reason for the current status | 
 
## Pool
| Metric Name | Description | 
| ----------- | :---------- | 
| Active Member Count | Number of active pool members | 
| Availability State | Current availability state | 
| Bits In | The amount of data received from the BIG-IP Pool* | 
| Bits Out | The amount of data sent to the BIG-IP Pool* | 
| Current Connections | Current number of connections | 
| Description | User defined Description | 
| Enabled State | Current enabled state, can be user defined | 
| Full Path | BIG-IP System full path | 
| Kind | Kind of Pool | 
| Load Balancing Mode | Current Load Balancing Mode | 
| Maximum Connections | Current max number of connections seen at one point | 
| Monitor Rule | Current Health Monitoring Rule applied | 
| Name | User defined name | 
| Packets In | The number of packets received from the BIG-IP Pool* | 
| Packets Out | The number of packets sent to the BIG-IP Pool* | 
| Requests | The total number of requests to the Pool* | 
| Self Link | Internal Link defining the Pool object in BIG-IP | 
| Status Reason | Textual Property explaining the overall health reason | 
 
## Pool Member
| Metric Name | Description | 
| ----------- | :---------- | 
| Availability State | Current availability from the BIG-IP System | 
| Bit In | The amount of data received from the BIG-IP Pool Member* | 
| Bit Out | The amount of data sent to the BIG-IP Pool Member* | 
| Current Connections | Current Connections | 
| Current Sessions | Current session count | 
| Enabled State | Enabled state of the Pool Member with regards to the parent pool | 
| Full Path | BIG-IP System full path to the Pool Member | 
| Kind | Pool Member Kind | 
| Maximum Connections | Maximum Connections | 
| Monitor Rule | Health Monitoring rule applied to the pool member | 
| Monitor Status | Montior Status | 
| Name | Pool Member Name | 
| Node Name | Name of the node the Pool Member is using | 
| Packets In | The number of packets received from the BIG-IP Pool Member* | 
| Packets Out | The number of packets sent to the BIG-IP Pool Member* | 
| Pool Name | Name of the Pool the Pool Member belongs | 
| Port | Port the Pool Member listens on | 
| Requests | Current number of requests over the last collection interval* | 
| Self Link | Internal Link defining the Pool Member object in BIG-IP | 
| Session Status | Current session health status | 
| State | Current state | 
| Status Reason | Explanation of the current status | 
 
## SSL Certificate
| Metric Name | Description | 
| ----------- | :---------- | 
| Created By | User who created the Certificate | 
| Days Until Expiration | Days until Certificate will expire | 
| Expiration Date | Expiration date of the Certificate | 
| Issuer | Certificate Issuer | 
| Key Type | Certificate Key Type | 
| Kind | Type of Certificate | 
| Name | Certificate Name | 
| Self Link | Internal Link defining the SSL Certificate object in BIG-IP | 
 
## Virtual Server
| Metric Name | Description | 
| ----------- | :---------- | 
| Application Service | Current Application Service assigned | 
| Availability State | BIG-IP defined availability | 
| Bits In | The amount of data received from the BIG-IP Virtual Server* | 
| Bits Out | The amount of data sent to the BIG-IP Virtual Server* | 
| Current Connections | Current number of connections from BIG-IP | 
| Destination | Destination address picked up by BIG-IP | 
| Enabled State | Current enabled state (disabled, enabled) | 
| Full Path | BIG-IP defined full path | 
| Kind | BIG-IP Type of Virtual Server | 
| Maximum Connections | Highest number of connections from BIG-IP | 
| Name | User defined name | 
| Packets In | The number of packets received from the BIG-IP Virtual Server* | 
| Packets Out | The number of packets sent to the BIG-IP Virtual Server* | 
| Pool | Pool the Virtual Server uses for load balancing | 
| Requests | Number of requests in the last collection interval to BIG-IP* | 
| Self Link | unique link identifier and full path to the Virtual Server | 
| Status Reason | Explanation of the current status | 
 
### * Metric Value Since Last Collection 
