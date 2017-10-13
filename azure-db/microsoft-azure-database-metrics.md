## Database
| Metric Name | Insights Key | Description |
| ----------- | ------------ | :---------- |
| Active Connections | number_of_active_connections | The number of active connections to the database |
| Active Transactions | active_transactions | Number of active transactions on database |
| Approximate Last Start Date | approx_last_start | The approximate time that the database was started |
| Auto Close | auto_close | Shows whether auto close is enabled |
| Auto Create Statistics | auto_create_statistics | Shows whether auto create statistics is enabled. |
| Auto Shrink | auto_shrink | Shows whether auto shrink is enabled. |
| Auto Update Statistics | auto_update_statistics | Shows whether auto update statistics is enabled. |
| Average CPU | avgerage_cpu | Average compute utilization in percentage of the limit of the service tier. |
| Average Data I/O | avgerage_data_io | Average data I/O utilization in percentage of the limit of the service tier. |
| Average Log Write | average_log_write | Average write resource utilization in percentage of the limit of the service tier. |
| Average Memory | avgerage_memory_usage | Average memory utilization in percentage of the limit of the service tier. |
| Background Processes | current_background_processes | The current number of background processes |
| Blocked Processes | blocked_processes | The current number of blocked processes |
| Buffer Ideal Page Life Expectancy | buffer_ideal_page_life_expectancy | The Buffer Ideal Page Life Expectancy of the Database. |
| Buffer Pool Size | buffer_pool_size | Total size of the buffer pool for a database |
| Connections | number_of_connections | The total number of connections to the database |
| Creation Date | creation_date | Date the database was created or last renamed |
| DTU Limit | dtu_limit | Current max database DTU setting for this database during this interval. |
| Data Space | data_space_usage | Database data space |
| Days Since Last Start | time_since_last_start | The approximate number of days since the database was started |
| Dormant Processes | dormant_processes | The current number of dormant processes |
| ID | database_id | Database identification number (unique within the Azure SQL Database server) |
| Disk IOPS | disk_iops | Total amount of disk write and read operations.* |
| In-Memory OLTP Storage | xtp_storage_percent | Storage utilization for In-Memory OLTP in percentage of the limit of the service tier (at the end of the reporting interval). |
| Index Space | index_space_usage | Database index space |
| Instance Wait Time | wait_time | Total wait time of the server* |
| Max Storage Size | maximum_storage_size | Maximum storage size for the time period, including database data, indexes, stored procedures and metadata |
| Maximum Concurrent Sessions | max_concurrent_sessions | Maximum concurrent sessions in percentage of the limit of the database’s service tier. |
| Maximum Concurrent Requests | max_concurrent_requests | Maximum concurrent workers (requests) in percentage of the limit of the database’s service tier. |
| Name | name | Name of the database (unique within the Azure SQL Database server) |
| Possible Connections | number_of_possible_connections | The maximum number of possible connections to the database |
| Preconnect Processes | current_preconnect_processes | The current number of preconnect processes |
| Read Data | read_data | Disk read data for database.* |
| Read Delay | read_delay | Total time, in milliseconds, that the users waited for reads issued on files for the database* |
| Read Only | read_only | Shows whether read only mode is enabled. |
| Read Operations | read_ops | This metric represents the amount of disk read operations over time.* |
| Recovery Model | recovery_model | Description of the recovery model selected for the database |
| Reserved Space | reserved_space | Database reserved space |
| Reserved Space Unused | unused_reserved_space | Database unused reserved space |
| Runnable Processes | runnable_processes | The current number of runnable processes |
| Runnable Tasks Count | runnable_tasks | Number of workers, with tasks assigned to them, that are waiting to be scheduled on the runnable queue |
| Running Processes | processes_running | The current number of running processes |
| Server Name | server_name | Logical server name |
| Service Tier | SKU | Service Tier of the database |
| Single User Mode | single_user_mode | Shows whether single user mode is enabled. |
| Size Used | database_size | Database size |
| Sleeping Processes | sleeping_processes | The current number of sleeping processes |
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

## Elastic Pool
| Metric Name | Insights Key | Description |
| ----------- | ------------ | :---------- |
| CPU Usage | cpu_usage | Percentage of CPU in use by the Elastic Pool. |
| DTU Consumption | dtu_consumption | Percentage of Database Transaction Units consumed by the Elastic Pool. |
| Data IO | data_io | Physical data read percentage of the Elastic Pool. |
| Database Count | database_count | Number of databases used by the Elastic Pool. |
| In-Memory OLTP Storage | xtp_storage | Percentage of in-memory Online Transaction Processing storage in use by the Elastic Pool |
| Log IO | log_io | Log write percentage of the Elastic Pool. |
| Maximum Database DTU | max_database_dtu | Maximum observed Database Transaction Unit of the Elastic Pool. |
| Minimum Database DTU | min_database_dtu | Minimum observed Database Transaction Unit of the Elastic Pool. |
| Name | name | Name of the Elastic Pool. |
| SQL Server Name | server | Name of the SQL Server which is hosting the Elastic Pool. |
| Sessions | sessions | Percentage of concurrent sessions in use. The maximum is determined by the service tier. |
| State | state | Current state of the Elastic Pool. |
| Storage | storage | Storage size, in megabytes, of the Elastic Pool. |
| Storage Limit | storage_limit | Storage limit, in bytes, of the Elastic Pool. |
| Storage Usage | storage_usage | Percentage of storage in use by the Elastic Pool. |
| Storage Used | storage_used | Storage used, in bytes, by the Elastic Pool. |
| Workers | workers | Percentage of concurrent workers (requests) which are running. The maximum is determined by the service tier. |
| eDTU Limit | edtu_limit | Elastic Database Transaction Unit limit for the Elastic Pool. |
| eDTU Used | edtu_used | Elastic Database Transaction Units used by the Elastic Pool. |

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
| Replication Lag | replication_lag_time | Time difference in seconds between the last_replication value and the timestamp of that transaction’s commit on the primary based on the primary database clock |
| Replication State | replication_state | The state of geo-replication for this database |
| Replication State Description | replication_state_description | Description of the state of geo-replication for this database |
| Role | role | The Geo-replication role for this database |
| Role Description | role_description | Description of the Geo-replication role for this database |
| Secondary Allows Connections | secondary_allow_connections | The secondary type |
| Secondary Allows Connections Description | secondary_allow_connections_description | Description of the secondary type |
| Server Name | server_name | Logical server name |
| Start Date | start_date | UTC time at a regional SQL Database datacenter when the database replication was initiated |

## Object
| Metric Name | Insights Key | Description |
| ----------- | ------------ | :---------- |
| Average Page Lock Wait Duration | average_page_lock_wait | Average number of milliseconds the Database Engine waited on a page lock |
| Average Row Lock Wait Duration | average_row_lock_wait | Average number of milliseconds the Database Engine waited on a row lock |
| Database ID | database_id | Database identification number (unique within the Azure SQL Database server) |
| Database Name | database_name | Name of the database (unique within the Azure SQL Database server) |
| Name | name | Object name |
| Page Locks Acquired | page_locks_acquired | Cumulative number of times the Database Engine waited on a page lock* |
| Page Locks Requested | page_locks_requested | Cumulative number of page locks requested* |
| Row Locks Acquired | row_locks_acquired | Cumulative number of times the Database Engine waited on a row lock* |
| Row Locks Requested | row_locks_requested | Cumulative number of row locks requested* |

## Query
| Metric Name | Insights Key | Description |
| ----------- | ------------ | :---------- |
| Average Execution Time | average_execution_time | The average execution time for the query |
| Database ID | database_id | Database identification number (unique within the Azure SQL Database server) |
| Database Name | database_name | Name of the database |
| Execution Context Name | execution_context_name | The name of the context in which the query was executed |
| Execution Context Type | execution_context_type | Type of context in which the query was executed |
| Execution Count | execution_count | Number of times that the plan has been executed since it was last compiled* |
| Execution Time | execution_time | Total amount of CPU time consumed by executions of this plan since it was compiled* |
| Last Execution | last_execution | Last time at which the plan started executing |
| Name | name | The Name of the Query. |
| SQL Handle | sql_handle | A token that refers to the batch or stored procedure that the query is part of |
| SQL Text | sql_text | The text of the query |
| Statement End Offset | statement_end_offset | Indicates, in bytes, starting with 0, the ending position of the query that the row describes within the text of its batch or persisted object. For versions before SQL Server 2014, a value of -1 indicates the end of the batch |
| Statement Start Offset | statement_start_offset | Indicates, in bytes, beginning with 0, the starting position of the query that the row describes within the text of its batch or persisted object |
| Unique Query Plans | unique_plans | The number of unique plans for this query |

## Resource Group
| Metric Name | Insights Key | Description |
| ----------- | ------------ | :---------- |
| Name | name | Name of the Resource Group. |

## Server
| Metric Name | Insights Key | Description |
| ----------- | ------------ | :---------- |
| Active Connections | number_of_active_connections | The total number of active connections across databases on the server. |
| Name | name | Logical server name |
| SQL Version | sql_version | Azure SQL Version |
| Type | type | Is the server configured in a failover cluster |

## SQL Data Warehouse
| Metric Name | Insights Key | Description |
| ----------- | ------------ | :---------- |
| CPU Usage | cpu_usage | Percentage of CPU in use by the SQL Data Warehouse. |
| Connections Blocked by Firewall | blocked_by_firewall | Number of connections to the SQL Data Warehouse which are blocked by the firewall. |
| Current Service Level Objective | service_level_objective_dw | Current service level objective of the SQL Data Warehouse. |
| DWU Consumption | dwu_consumption | Percentage of Data Warehouse Units consumed by the SQL Data Warehouse. |
| DWU Limit | dwu_limit | Data Warehouse Units limit of the SQL Data Warehouse. |
| DWU Used | dwu_used | Data Warehouse Units used by the SQL Data Warehouse. |
| Data IO | data_io | Physical data read percentage of the SQL Data Warehouse. |
| Failed Connections | failed_connections | Number of failed connections to the SQL Data Warehouse. |
| Name | name | Name of the SQL Data Warehouse |
| SQL Server Name | server | Name of the SQL Server hosting the SQL Data Warehouse. |
| Service Level Objective | service_level_objective | Service level objective of the SQL Database. |
| Status | status | Status of the SQL Database. |
| Successful Connections | successful_connections | Number of successful connections to the SQL Data Warehouse. |
| Total Database Size | database_size | The total size, in bytes, of the SQL Data Warehouse. |

## SQL Database
| Metric Name | Insights Key | Description |
| ----------- | ------------ | :---------- |
| Active Time Ratio | active_time_ratio | Ratio of time the SQL Database is active. |
| Average DTU | average_dtu | Average observed Database Transaction Units of the SQL Database. |
| CPU Usage | cpu_usage | Percentage of CPU in use by the SQL Database. |
| Connections Blocked by Firewall | blocked_by_firewall | Number of attempted connections to the SQL Database which were blocked by the firewall. |
| Current Service Level Objective | service_level_objective | Current service level objective of the SQL Database. |
| DTU Consumption | dtu_consumption | Percentage of Database Transaction Units consumed by the SQL Database. |
| DTU Limit | dtu_limit | Database Transaction Unit limit of the SQL Database. |
| DTU Used | dtu_used | Database Transaction Units used by the SQL Database. |
| Data IO | data_io | Physical data read percentage of the SQL Database. |
| Database Size Usage | database_size_usage | Percentage of storage being used by the SQL Database. |
| Deadlocks | deadlocks | Number of deadlocks in the SQL Database. |
| Failed Connections | failed_connections | Number of failed connections to the SQL Database. |
| In-Memory OLTP Storage | xtp_storage | Percentage of In-Memory Online Transaction Processing storage in use by the SQL Database |
| Log IO | log_io | Log write percentage of the SQL Database. |
| Max Database Size | max_database_size | Maximum size, in gigabytes, of the SQL Database. |
| Maximum DTU | max_dtu | Maximum observed Database Transaction Units of the SQL Database. |
| Minimum DTU | min_dtu | Minimum observed Database Transaction Units of the SQL Database. |
| Name | name | Name of the SQL Database. |
| SQL Server Name | server | Name of the SQL Server on which the SQL Database is hosted. |
| Service Tier Name | service_tier_name | Name of the current service tier of the SQL Database. |
| Sessions | sessions | Percentage of concurrent sessions in use. The maximum is determined by the service tier. |
| Status | status | Current status of the SQL Database. |
| Successful Connections | successful_connections | Number of successful connections to the SQL Database. |
| Total Database Size | database_size | Total size, in bytes, of the SQL Database. |
| Workers | workers | Percentage of concurrent workers (requests) which are running. The maximum is determined by the service tier. |

## SQL Server
| Metric Name | Insights Key | Description |
| ----------- | ------------ | :---------- |
| Average CPU Usage | cpu_usage | Average CPU usage by databases on the SQL Server. |
| Average Concurrent Sessions | sessions | Percentage of concurrent sessions in use. The maximum is determined by the service tier. |
| Average Concurrent Workers | workers | Percentage of concurrent workers (requests) which are running. The maximum is determined by the service tier. |
| Average DTUs Used | dtu_used | Average Database Transaction Units used by databases on the SQL Server. |
| Average Data IO | data_io | Average physical data read percentage of databases on the SQL Server. |
| Average Database Size | database_size | Average size in bytes of databases on the SQL Server. |
| Average In-Memory OLTP Storage | xtp_storage | Average percentage of In-Memory Online Transaction Processing storage in use by databases on the SQL Server. |
| Average Log IO | log_io | Average log write percentage of databases on the SQL Server. |
| Name | name | Name of the SQL Server. |

### * Metric Value Since Last Collection
