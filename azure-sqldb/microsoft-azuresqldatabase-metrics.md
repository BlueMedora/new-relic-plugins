## Database
| Metric Name | Insights Key | Description | 
| ----------- | ------------ | :---------- | 
| Active Connections | number_of_active_connections | The number of active connections to the database | 
| Active Transactions | active_transactions | Number of active transactions on database | 
| Approximate Last Start Date | approx_last_start | The approximate time that the database was started | 
| Auto Close | auto_close | Shows whether auto close is enabled | 
| Auto Create Statistics | auto_create_stat | Shows whether auto create statistics is enabled. | 
| Auto Shrink | auto_shrink | Shows whether auto shrink is enabled. | 
| Auto Update Statistics | auto_update_stat | Shows whether auto update statistics is enabled. | 
| Average CPU | avg_cpu_percent | Average compute utilization in percentage of the limit of the service tier. | 
| Average Data I/O | avg_data_io_percent | Average data I/O utilization in percentage of the limit of the service tier. | 
| Average Log Write | avg_log_write_percent | Average write resource utilization in percentage of the limit of the service tier. | 
| Average Memory | avg_memory_usage_percent | Average memory utilization in percentage of the limit of the service tier. | 
| Background Processes | background | The current number of background processes | 
| Blocked Processes | blocked | The current number of blocked processes | 
| Buffer Ideal Page Life Expectancy | buffer_ideal_page_life_expectancy | The Buffer Ideal Page Life Expectancy of the Database. | 
| Buffer Pool Size | buffer_pool_size | Total size of the buffer pool for a database | 
| Connections | number_of_connections | The total number of connections to the database | 
| Creation Date | creation_date | Date the database was created or last renamed | 
| DTU Limit | dtu_limit | Current max database DTU setting for this database during this interval. | 
| Data Space | data_space_usage | Database data space | 
| Days Since Last Start | time_since_last_start | The approximate number of days since the database was started | 
| Dormant Processes | dormant | The current number of dormant processes | 
| ID | database_id | Database identification number (unique within the Azure SQL Database server) | 
| IOPS | iops | Total amount of disk write and read operations.* | 
| In-Memory OLTP Storage | xtp_storage_percent | Storage utilization for In-Memory OLTP in percentage of the limit of the service tier (at the end of the reporting interval). | 
| Index Space | index_space_usage | Database index space | 
| Instance Wait Time | wait_time | Total wait time of the server* | 
| Max Storage Size | storage_in_megabytes | Maximum storage size for the time period, including database data, indexes, stored procedures and metadata | 
| Maximum Concurrent Sessions | max_session_percent | Maximum concurrent sessions in percentage of the limit of the database’s service tier. | 
| Maximum Concurrent Workers | max_worker_percent | Maximum concurrent workers (requests) in percentage of the limit of the database’s service tier. | 
| Name | name | Name of the database (unique within the Azure SQL Database server) | 
| Possible Connections | number_of_possible_connections | The maximum number of possible connections to the database | 
| Preconnect Processes | preconnect | The current number of preconnect processes | 
| Read Data | read_data | Disk read data for database.* | 
| Read Delay | read_delay | Total time, in milliseconds, that the users waited for reads issued on files for the database* | 
| Read Only | read_only | Shows whether read only mode is enabled. | 
| Read Operations | read_ops | This metric represents the amount of disk read operations over time.* | 
| Recovery Model | recovery_model | Description of the recovery model selected for the database | 
| Reserved Space | reserved_space | Database reserved space | 
| Reserved Space Unused | reserved_space_not_used | Database unused reserved space | 
| Runnable Processes | runnable | The current number of runnable processes | 
| Runnable Tasks Count | runnable_tasks_count | Number of workers, with tasks assigned to them, that are waiting to be scheduled on the runnable queue | 
| Running Processes | running | The current number of running processes | 
| Server Name | servername | Logical server name | 
| Service Tier | SKU | Service Tier of the database | 
| Single User Mode | single_user_mode | Shows whether single user mode is enabled. | 
| Size Used | size | Database size | 
| Sleeping Processes | sleeping | The current number of sleeping processes | 
| Status | status | Description of the database state | 
| Suspended Processes | suspended | The current number of suspended processes | 
| Threads | thread_count | The number of workers that are associated with this database. This includes workers that are not assigned any task | 
| Time Since Creation | time_since_creation | Days since database was created. | 
| Total Data | total_data | Total disk read and write data for database.* | 
| User Lookups | user_lookups | Total number of bookmark lookups by user queries* | 
| User Scans | user_scans | Total number of scans by user queries. This represents scans that did not use 'seek' predicate.* | 
| User Seeks | user_seeks | Total number of seeks by user queries* | 
| User Updates | user_updates | Total number of updates by user queries. This includes Insert, Delete and Updates representing number of operations done not the actual rows affected. For example, if you delete 1000 rows in one statement, this count will increment by 1* | 
| Write Data | write_data | Disk write data for database.* | 
| Write Delay | write_delay | Total time, in milliseconds, that users waited for writes to be completed on files for the database* | 
| Write Operations | write_ops | This metrice represents the amount of disk write operations over time.* | 
 
## Geo-Replication Database
| Metric Name | Insights Key | Description | 
| ----------- | ------------ | :---------- | 
| Database Name | database_name | Name of the database (unique within the Azure SQL Database server) | 
| Last Replication | last_replication | The timestamp of the last transaction’s acknowledgement by the secondary based on the primary database clock | 
| Link ID | link_id | Unique ID of the geo-replication link | 
| Modify Date | modify_date | UTC time at regional SQL Database datacenter when the database geo-replication has completed. The new database is synchronized with the primary database as of this time. | 
| Name | name | Name of the database and the logical server | 
| Partner Database ID | database_id | Partner database identification number (unique within the Azure SQL Database server) | 
| Partner Server Name | partner_servername | Name of the logical server containing the linked database | 
| Replication Lag | replication_lag | Time difference in seconds between the last_replication value and the timestamp of that transaction’s commit on the primary based on the primary database clock | 
| Replication State | replication_state | The state of geo-replication for this database | 
| Replication State Description | replication_state_desc | Description of the state of geo-replication for this database | 
| Role | role | The Geo-replication role for this database | 
| Role Description | role_desc | Description of the Geo-replication role for this database | 
| Secondary Allows Connections | secondary_allow_connections | The secondary type | 
| Secondary Allows Connections Description | secondary_allow_connections_desc | Description of the secondary type | 
| Server Name | servername | Logical server name | 
| Start Date | start_date | UTC time at a regional SQL Database datacenter when the database replication was initiated | 
 
## Object
| Metric Name | Insights Key | Description | 
| ----------- | ------------ | :---------- | 
| Average Page Lock Wait Duration | avg_page_lock_wait | Average number of milliseconds the Database Engine waited on a page lock | 
| Average Row Lock Wait Duration | avg_row_lock_wait | Average number of milliseconds the Database Engine waited on a row lock | 
| Database ID | database_id | Database identification number (unique within the Azure SQL Database server) | 
| Database Name | database_name | Name of the database (unique within the Azure SQL Database server) | 
| Name | name | Object name | 
| Page Locks Acquired | page_lock_wait_count | Cumulative number of times the Database Engine waited on a page lock* | 
| Page Locks Requested | page_lock_count | Cumulative number of page locks requested* | 
| Row Locks Acquired | row_lock_wait_count | Cumulative number of times the Database Engine waited on a row lock* | 
| Row Locks Requested | row_lock_count | Cumulative number of row locks requested* | 
 
## Query
| Metric Name | Insights Key | Description | 
| ----------- | ------------ | :---------- | 
| Average Execution Time | avg_execution_time | The average execution time for the query | 
| Database ID | database_id | Database identification number (unique within the Azure SQL Database server) | 
| Database Name | database_name | Name of the database | 
| Execution Context Name | context_name | The name of the context in which the query was executed | 
| Execution Context Type | context_type | Type of context in which the query was executed | 
| Execution Count | execution_count | Number of times that the plan has been executed since it was last compiled* | 
| Execution Time | execution_time | Total amount of CPU time consumed by executions of this plan since it was compiled* | 
| Last Execution | last_execution | Last time at which the plan started executing | 
| Name | name | The Name of the Query. | 
| SQL Handle | sql_handle | A token that refers to the batch or stored procedure that the query is part of | 
| SQL Text | sql_text | The text of the query | 
| Statement End Offset | statement_end_offset | Indicates, in bytes, starting with 0, the ending position of the query that the row describes within the text of its batch or persisted object. For versions before SQL Server 2014, a value of -1 indicates the end of the batch | 
| Statement Start Offset | statement_start_offset | Indicates, in bytes, beginning with 0, the starting position of the query that the row describes within the text of its batch or persisted object | 
| Unique Query Plans | unique_plans | The number of unique plans for this query | 
 
## Server
| Metric Name | Insights Key | Description | 
| ----------- | ------------ | :---------- | 
| Active Connections | number_of_active_connections | The total number of active connections across databases on the server. | 
| Name | name | Logical server name | 
| SQL Version | sql_version | Azure SQL Version | 
| Type | type | Is the server configured in a failover cluster | 
 
### * Metric Value Since Last Collection 

    