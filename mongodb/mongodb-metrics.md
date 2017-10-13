## Cluster
| Metric Name | Insights Key | Description |
| ----------- | ------------ | :---------- |
| Server Address List | server_address_list | List of server addresses the cluster uses to connect to the MongoDB environment |

## Config Server
| Metric Name | Insights Key | Description |
| ----------- | ------------ | :---------- |
| Config Server Has Child Replica Set | has_replica_set_child | Config Server Has a Replica Set as a Child. |
| Config Server Resource | config_server_resource | Name of resource that serves as this cluster's config server |

## Database
| Metric Name | Insights Key | Description |
| ----------- | ------------ | :---------- |
| Average Object Size | avg_obj_size | Average object size of this resource |
| Client Address | client_address | Client address that was used to retrieve this resource |
| Collections Average Object Size | collections_avg_obj_size | Average size of objects in this resource's collections |
| Collections Count | collections_count | Number of objects or documents in this resource's collections |
| Collections Max | collections_max | Maximum number of documents in this resource's collections |
| Collections Max Size | collections_max_size | Maximum size of this resource's capped collections |
| Collections Size | collections_size | Size of all records in this resource's collections |
| Collections Storage Size | collections_storage_size | Storage size of all records in this resource's collections |
| Collections Total Index Size | collections_total_index_size | Total size of all in this resource's collections |
| Collections Total Indexes | collections_nindexes | Number of indexes on this resource's collections |
| Data File Version | data_file_version | Data file version for this resource | 
| Data Size | data_size | Data size of this resource |
| Extents | extents | Number of extents for this resource |
| Freelist Extents | freelist_extents | Number of extents in the freelist for this resource |
| Freelist Extents Size | freelist_extent_size | Size of the extents on the freelist for this resource |
| Indexes | indexes | Number of indexes for this resource |
| Mongo Database Name | name | Name of this resource |
| Namespace File Size | namespace_size | Namespace file size for this resource |
| Storage Size | storage_size | Storage size of this resource |
| Total Collections | collections | Number of collections for this resource |
| Total File Size | file_size | Total file size for this resource |
| Total Index Size | index_size | Total index size for this resource |
| Total Objects | objects | Number of objects for this resource |

## Mongod
| Metric Name | Insights Key | Description |
| ----------- | ------------ | :---------- |
| Active Clients | global_lock_active_clients_total | Number of active client connections to the database |
| Active Clients Performing Reads | global_lock_active_clients_readers | Number of active client connections performing read operations |
| Active Clients Performing Writes | global_lock_active_clients_writers | Number of active client connections performing write operations |
| Advisory Host FQDNs | advisory_host_fqdns | Advisory host fully qualified domain names of the machine hosting this resource |
| Arbiter Only | arbiter_only | Indicates if this resource is an arbiter |
| Asserts: Message | asserts_msg | Number of message assertions raised since the MongoDB process started* |
| Asserts: Regular | asserts_regular | Number of regular assertions raised since the MongoDB process started* |
| Asserts: Rollovers | asserts_rollovers | Number of rollovers since the MongoDB process started* |
| Asserts: User | asserts_user | Number of user assertions that have occurred since the MongoDB process started* |
| Asserts: Warning | asserts_warning | Number of warnings raised since the MongoDB process started* |
| Available Connections | connections_available | Number of unused incoming connections available to this resource |
| Available Read Tickets | ticket_avail_reads | Amount of available read tickets |
| Available Write Tickets | ticket_avail_writes | Amount of available write tickets |
| Background Flushing: Average | background_flushing_average | Average time for each flush to disk |
| Background Flushing: Flushes | background_flushing_flushes | Number of times the databases on this resource has flushed all writes to disk* |
| Background Flushing: Last | background_flushing_last | Time it took the last flush operation to complete |
| Background Flushing: Total | background_flushing_total | Time the mongod processes have spent writing data to disk |
| Build Indexes | build_indexes | Indicates if the mongod builds indexes on this resource |
| Collection Acquire Waits Exclusive Locks | collection_acquire_wait_locks_exclusive | Number of lock acquisitions with this mode waits because locks were held in a conflicting mode* |
| Collection Acquire Waits Intent Exclusive Locks | collection_acquire_wait_locks_intent_exclusive | Number of lock acquisitions with this mode waits because locks were held in a conflicting mode* |
| Collection Acquire Waits Intent Shared Locks | collection_acquire_wait_locks_intent_shared | Number of lock acquisitions with this mode waits because locks were held in a conflicting mode* |
| Collection Acquire Waits Shared Locks | collection_acquire_wait_locks_shared | Number of lock acquisitions with this mode waits because locks were held in a conflicting mode* |
| Collection Cumulative Wait Time Exclusive Locks | collection_time_acquiring_locks_exclusive | Cumulative wait time for lock acquisitions with this mode |
| Collection Cumulative Wait Time Intent Exclusive Locks | collection_time_acquiring_locks_intent_exclusive | Cumulative wait time for lock acquisitions with this mode |
| Collection Cumulative Wait Time Intent Shared Locks | collection_time_acquiring_locks_intent_shared | Cumulative wait time for lock acquisitions with this mode |
| Collection Cumulative Wait Time Shared Locks | collection_time_acquiring_locks_shared | Cumulative wait time for lock acquisitions with this mode |
| Collection Deadlocks Exclusive Locks | collection_deadlock_locks_exclusive | Number of times lock acquisitions with this mode encountered deadlocks* |
| Collection Deadlocks Intent Exclusive Locks | collection_deadlock_locks_intent_exclusive | Number of times lock acquisitions with this mode encountered deadlocks* |
| Collection Deadlocks Intent Shared Locks | collection_deadlock_locks_intent_shared | Number of times lock acquisitions with this mode encountered deadlocks* |
| Collection Deadlocks Shared Locks | collection_deadlock_locks_shared | Number of times lock acquisitions with this mode encountered deadlocks* |
| Collection Exclusive Locks | collection_acquire_locks_exclusive | Number of times the lock was acquired in this mode* |
| Collection Intent Exclusive Locks | collection_acquire_locks_intent_exclusive | Number of times the lock was acquired in this mode* |
| Collection Intent Shared Locks | collection_acquire_locks_intent_shared | Number of times the lock was acquired in this mode* |
| Collection Shared Locks | collection_acquire_locks_shared | Number of times the lock was acquired in this mode* |
| Commits | dur_commits | Transactions written to journal during latest journal group commit interval* |
| Commits In Write Lock | dur_commits_in_write_lock | Commits that occurred while a write lock was held* |
| Compression Ratio | dur_compression | Compression Ratio of the data written to journal |
| Current Cache | cache_current | Amount of bytes currently in cache |
| Current Connections | connections_current | Number of incoming connections to this resource |
| Cursor Timed Out | cursor_timed_out | Total number of cursors that have timed out* |
| Cursors Open | cursor_open | Total number of cursors this environment maintains |
| Data Journaled | dur_journaled | Data written to journal during latest journal group commit interval |
| Database Acquire Waits Exclusive Locks | database_acquire_wait_locks_exclusive | Number of lock acquisitions with this mode waits because locks were held in a conflicting mode* |
| Database Acquire Waits Intent Exclusive Locks | database_acquire_wait_locks_intent_exclusive | Number of lock acquisitions with this mode waits because locks were held in a conflicting mode* |
| Database Acquire Waits Intent Shared Locks | database_acquire_wait_locks_intent_shared | Number of lock acquisitions with this mode waits because locks were held in a conflicting mode* |
| Database Acquire Waits Shared Locks | database_acquire_wait_locks_shared | Number of lock acquisitions with this mode waits because locks were held in a conflicting mode* |
| Database Cumulative Wait Time Exclusive Locks | database_time_acquiring_locks_exclusive | Cumulative wait time for lock acquisitions with this mode |
| Database Cumulative Wait Time Intent Exclusive Locks | database_time_acquiring_locks_intent_exclusive | Cumulative wait time for lock acquisitions with this mode |
| Database Cumulative Wait Time Intent Shared Locks | database_time_acquiring_locks_intent_shared | Cumulative wait time for lock acquisitions with this mode |
| Database Cumulative Wait Time Shared Locks | database_time_acquiring_locks_shared | Cumulative wait time for lock acquisitions with this mode |
| Database Deadlocks Exclusive Locks | database_deadlock_locks_exclusive | Number of times lock acquisitions with this mode encountered deadlocks* |
| Database Deadlocks Intent Exclusive Locks | database_deadlock_locks_intent_exclusive | Number of times lock acquisitions with this mode encountered deadlocks* |
| Database Deadlocks Intent Shared Locks | database_deadlock_locks_intent_shared | Number of times lock acquisitions with this mode encountered deadlocks* |
| Database Deadlocks Shared Locks | database_deadlock_locks_shared | Number of times lock acquisitions with this mode encountered deadlocks* |
| Database Exclusive Locks | database_acquire_locks_exclusive | Number of times the lock was acquired in this mode* |
| Database Intent Exclusive Locks | database_acquire_locks_intent_exclusive | Number of times the lock was acquired in this mode* |
| Database Intent Shared Locks | database_acquire_locks_intent_shared | Number of times the lock was acquired in this mode* |
| Database Shared Locks | database_acquire_locks_shared | Number of times the lock was acquired in this mode* |
| Dirty Cache | cache_dirty | Amount of dirty data (in bytes) in cache |
| Documents Deleted | documents_deleted | Number of documents deleted* |
| Documents Inserted | documents_inserted | Number of documents inserted* |
| Documents Moved | documents_moves | Number of times documents have moved in the on-disk representation of the MongoDB data set* |
| Documents Returned | documents_returned | Number of documents returned by queries* |
| Documents Updated | documents_updated | Number of documents updated* |
| Early Commits | dur_early_commits | Requested commits before the scheduled journal group commit interval* |
| Expiration Date | security_ssl_server_certificate_expiration_date | Expiration date of the TLS/SSL certificate |
| Extended Memory Supported | mem_supported | Indicates if the machine hosting this resource supports extended memory information |
| Fastmod Operations | operations_fastmod | Number of update operations that don't cause documents to grow nor require updates to the index* |
| Global Acquire Waits Exclusive Locks | global_acquire_wait_locks_exclusive | Number of lock acquisitions with this mode waits because locks were held in a conflicting mode* |
| Global Acquire Waits Intent Exclusive Locks | global_acquire_wait_locks_intent_exclusive | Number of lock acquisitions with this mode waits because locks were held in a conflicting mode* |
| Global Acquire Waits Intent Shared Locks | global_acquire_wait_locks_intent_shared | Number of lock acquisitions with this mode waits because locks were held in a conflicting mode* |
| Global Acquire Waits Shared Locks | global_acquire_wait_locks_shared | Number of lock acquisitions with this mode waits because locks were held in a conflicting mode* |
| Global Cumulative Wait Time Exclusive Locks | global_time_acquiring_locks_exclusive | Cumulative wait time for lock acquisitions with this mode |
| Global Cumulative Wait Time Intent Exclusive Locks | global_time_acquiring_locks_intent_exclusive | Cumulative wait time for lock acquisitions with this mode |
| Global Cumulative Wait Time Intent Shared Locks | global_time_acquiring_locks_intent_shared | Cumulative wait time for lock acquisitions with this mode |
| Global Cumulative Wait Time Shared Locks | global_time_acquiring_locks_shared | Cumulative wait time for lock acquisitions with this mode |
| Global Deadlocks Exclusive Locks | global_deadlock_locks_exclusive | Number of times lock acquisitions with this mode encountered deadlocks* |
| Global Deadlocks Intent Exclusive Locks | global_deadlock_locks_intent_exclusive | Number of times lock acquisitions with this mode encountered deadlocks* |
| Global Deadlocks Intent Shared Locks | global_deadlock_locks_intent_shared | Number of times lock acquisitions with this mode encountered deadlocks* |
| Global Deadlocks Shared Locks | global_deadlock_locks_shared | Number of times lock acquisitions with this mode encountered deadlocks* |
| Global Exclusive Locks | global_acquire_locks_exclusive | Number of times the lock was acquired in this mode* |
| Global Intent Exclusive Locks | global_acquire_locks_intent_exclusive | Number of times the lock was acquired in this mode* |
| Global Intent Shared Locks | global_acquire_locks_intent_shared | Number of times the lock was acquired in this mode* |
| Global Lock Total Time | global_lock_total_time | Time since database last started and created the "globalLock" |
| Global Shared Locks | global_acquire_locks_shared | Number of times the lock was acquired in this mode* |
| Has Certificate Authority | security_ssl_server_has_certificate_authority | Indicates if the TLS/SSL certificate is associated with a certificate authority |
| Heap Used | extra_info_heap_usage_bytes | Heap used by this resources database processes |
| Hidden | hidden | Indicates if this resource is hidden by its replica set |
| Host Name | host_name | Hostname of the machine hosting this resource |
| ID | id | Name of this resource's replica set |
| IP Address | ip | IP address of the machine hosting this resource |
| Is Master | ismaster | Indicates if this resource is writable |
| Journaling Enabled | dur_enabled | Signifies if Journaling is enabled |
| MMAPv1 Journal Acquire Waits Exclusive Locks | mmapv1_journal_acquire_wait_locks_exclusive | Number of lock acquisitions with this mode waits because locks were held in a conflicting mode* |
| MMAPv1 Journal Acquire Waits Intent Exclusive Locks | mmapv1_journal_acquire_wait_locks_intent_exclusive | Number of lock acquisitions with this mode waits because locks were held in a conflicting mode* |
| MMAPv1 Journal Acquire Waits Intent Shared Locks | mmapv1_journal_acquire_wait_locks_intent_shared | Number of lock acquisitions with this mode waits because locks were held in a conflicting mode* |
| MMAPv1 Journal Acquire Waits Shared Locks | mmapv1_journal_acquire_wait_locks_shared | Number of lock acquisitions with this mode waits because locks were held in a conflicting mode* |
| MMAPv1 Journal Cumulative Wait Time Exclusive Locks | mmapv1_journal_time_acquiring_locks_exclusive | Cumulative wait time for lock acquisitions with this mode |
| MMAPv1 Journal Cumulative Wait Time Intent Exclusive Locks | mmapv1_journal_time_acquiring_locks_intent_exclusive | Cumulative wait time for lock acquisitions with this mode |
| MMAPv1 Journal Cumulative Wait Time Intent Shared Locks | mmapv1_journal_time_acquiring_locks_intent_shared | Cumulative wait time for lock acquisitions with this mode |
| MMAPv1 Journal Cumulative Wait Time Shared Locks | mmapv1_journal_time_acquiring_locks_shared | Cumulative wait time for lock acquisitions with this mode |
| MMAPv1 Journal Deadlocks Exclusive Locks | mmapv1_journal_deadlock_locks_exclusive | Number of times lock acquisitions with this mode encountered deadlocks* |
| MMAPv1 Journal Deadlocks Intent Exclusive Locks | mmapv1_journal_deadlock_locks_intent_exclusive | Number of times lock acquisitions with this mode encountered deadlocks* |
| MMAPv1 Journal Deadlocks Intent Shared Locks | mmapv1_journal_deadlock_locks_intent_shared | Number of times lock acquisitions with this mode encountered deadlocks* |
| MMAPv1 Journal Deadlocks Shared Locks | mmapv1_journal_deadlock_locks_shared | Number of times lock acquisitions with this mode encountered deadlocks* |
| MMAPv1 Journal Exclusive Locks | mmapv1_journal_acquire_locks_exclusive | Number of times the lock was acquired in this mode* |
| MMAPv1 Journal Intent Exclusive Locks | mmapv1_journal_acquire_locks_intent_exclusive | Number of times the lock was acquired in this mode* |
| MMAPv1 Journal Intent Shared Locks | mmapv1_journal_acquire_locks_intent_shared | Number of times the lock was acquired in this mode* |
| MMAPv1 Journal Shared Locks | mmapv1_journal_acquire_locks_shared | Number of times the lock was acquired in this mode* |
| Mapped Memory | mem_mapped | Amount of mapped memory by this resource's databases |
| Mapped Memory with Journal | mem_mapped_journal | Amount of mapped memory with journal by this resource's databases |
| Memory Architecture | mem_bits | Architecture of the machine hosting this resource |
| Metadata Acquire Waits Exclusive Locks | metadata_acquire_wait_locks_exclusive | Number of lock acquisitions with this mode waits because locks were held in a conflicting mode* |
| Metadata Acquire Waits Intent Exclusive Locks | metadata_acquire_wait_locks_intent_exclusive | Number of lock acquisitions with this mode waits because locks were held in a conflicting mode* |
| Metadata Acquire Waits Intent Shared Locks | metadata_acquire_wait_locks_intent_shared | Number of lock acquisitions with this mode waits because locks were held in a conflicting mode* |
| Metadata Acquire Waits Shared Locks | metadata_acquire_wait_locks_shared | Number of lock acquisitions with this mode waits because locks were held in a conflicting mode* |
| Metadata Cumulative Wait Time Exclusive Locks | metadata_time_acquiring_locks_exclusive | Cumulative wait time for lock acquisitions with this mode |
| Metadata Cumulative Wait Time Intent Exclusive Locks | metadata_time_acquiring_locks_intent_exclusive | Cumulative wait time for lock acquisitions with this mode |
| Metadata Cumulative Wait Time Intent Shared Locks | metadata_time_acquiring_locks_intent_shared | Cumulative wait time for lock acquisitions with this mode |
| Metadata Cumulative Wait Time Shared Locks | metadata_time_acquiring_locks_shared | Cumulative wait time for lock acquisitions with this mode |
| Metadata Deadlocks Exclusive Locks | metadata_deadlock_locks_exclusive | Number of times lock acquisitions with this mode encountered deadlocksNumber of times lock acquisitions with this mode encountered deadlocks* |
| Metadata Deadlocks Intent Exclusive Locks | metadata_deadlock_locks_intent_exclusive | Number of times lock acquisitions with this mode encountered deadlocksNumber of times lock acquisitions with this mode encountered deadlocks* |
| Metadata Deadlocks Intent Shared Locks | metadata_deadlock_locks_intent_shared | Number of times lock acquisitions with this mode encountered deadlocksNumber of times lock acquisitions with this mode encountered deadlocks* |
| Metadata Deadlocks Shared Locks | metadata_deadlock_locks_shared | Number of times lock acquisitions with this mode encountered deadlocksNumber of times lock acquisitions with this mode encountered deadlocks* |
| Metadata Exclusive Locks | metadata_acquire_locks_exclusive | Number of times the lock was acquired in this mode* |
| Metadata Intent Exclusive Locks | metadata_acquire_locks_intent_exclusive | Number of times the lock was acquired in this mode* |
| Metadata Intent Shared Locks | metadata_acquire_locks_intent_shared | Number of times the lock was acquired in this mode* |
| Metadata Shared Locks | metadata_acquire_locks_shared | Number of times the lock was acquired in this mode* |
| Mongod Delay Begind the Primary | delay_behind_primary | Mongod delay behind the primary not accounting for the slave delay. |
| Mongod Shares a Host | shares_host_with_other_mongod | Mongod Shares a Host with another Mongod. 1 if it shares, 0 if it does not share. |
| Mongod is Recovering | is_recovering | Mongod is recovering from a delay. |
| Network Traffic In | network_bytes_in | Bytes received by all databases of this resource* |
| Network Traffic Out | network_bytes_out | Bytes sent from all databases of this resource* |
| Number of Requests | network_num_requests | Number of requests this resource has received* |
| Operations Waiting to Read | global_lock_current_queue_readers | Number of operations currently queued and waiting for the read lock |
| Operations Waiting to Write | global_lock_current_queue_writers | Number of operations currently queued and waiting for the write lock |
| Operations: Commands | opcounters_command | Number of database commands since mongod instance last started* |
| Operations: Deletes | opcounters_delete | Number of delete operations since mongod instance last started* |
| Operations: Get More | opcounters_getmore | Number of "getmore" operations since mongod instance last started* |
| Operations: Inserts | opcounters_insert | Number of insert operations received since mongod instance last started* |
| Operations: Queries | opcounters_query | Number of queries received since mongod instance last started* |
| Operations: Updates | opcounters_update | Number of update operations received since mongod instance last started* |
| Oplog Acquire Waits Exclusive Locks | oplog_acquire_wait_locks_exclusive | Number of lock acquisitions with this mode waits because locks were held in a conflicting mode* |
| Oplog Acquire Waits Intent Exclusive Locks | oplog_acquire_wait_locks_intent_exclusive | Number of lock acquisitions with this mode waits because locks were held in a conflicting mode* |
| Oplog Acquire Waits Intent Shared Locks | oplog_acquire_wait_locks_intent_shared | Number of lock acquisitions with this mode waits because locks were held in a conflicting mode* |
| Oplog Acquire Waits Shared Locks | oplog_acquire_wait_locks_shared | Number of lock acquisitions with this mode waits because locks were held in a conflicting mode* |
| Oplog Cumulative Wait Time Exclusive Locks | oplog_time_acquiring_locks_exclusive | Cumulative wait time for lock acquisitions with this mode |
| Oplog Cumulative Wait Time Intent Exclusive Locks | oplog_time_acquiring_locks_intent_exclusive | Cumulative wait time for lock acquisitions with this mode |
| Oplog Cumulative Wait Time Intent Shared Locks | oplog_time_acquiring_locks_intent_shared | Cumulative wait time for lock acquisitions with this mode |
| Oplog Cumulative Wait Time Shared Locks | oplog_time_acquiring_locks_shared | Cumulative wait time for lock acquisitions with this mode |
| Oplog Deadlocks Exclusive Locks | oplog_deadlock_locks_exclusive | Number of times lock acquisitions with this mode encountered deadlocks* |
| Oplog Deadlocks Intent Exclusive Locks | oplog_deadlock_locks_intent_exclusive | Number of times lock acquisitions with this mode encountered deadlocks* |
| Oplog Deadlocks Intent Shared Locks | oplog_deadlock_locks_intent_shared | Number of times lock acquisitions with this mode encountered deadlocks* |
| Oplog Deadlocks Shared Locks | oplog_deadlock_locks_shared | Number of times lock acquisitions with this mode encountered deadlocks* |
| Oplog Exclusive Locks | oplog_acquire_locks_exclusive | Number of times the lock was acquired in this mode* |
| Oplog Intent Exclusive Locks | oplog_acquire_locks_intent_exclusive | Number of times the lock was acquired in this mode* |
| Oplog Intent Shared Locks | oplog_acquire_locks_intent_shared | Number of times the lock was acquired in this mode* |
| Oplog Shared Locks | oplog_acquire_locks_shared | Number of times the lock was acquired in this mode* |
| Optime | optime | Optime of the mongod |
| Out Read Tickets | ticket_out_reads | Amount of out read tickets |
| Out Write Tickets | ticket_out_writes | Amount of out write tickets |
| PID | pid | Process ID number on this resource |
| Page Faults | extra_info_page_faults | Total number of page faults* |
| Priority | priority | Signifies eligibility of this resource to become primary |
| Process | process | Current MongoDB process on this resource |
| Queries using Sort | operations_scan_and_order | Number of queries that return sorted numbers that cannot perform the sort operation using an index* |
| Queries with ID Field | operations_idhack | Number of queries that contain the "_id" field* |
| Queries with Write Conflicts | operations_write_conflicts | Number of queries that encountered write conflicts* |
| Read Cache | cache_read | Amount of bytes read into cache* |
| Read Tickets | ticket_reads | Amount of total read tickets |
| Replication Operations: Commands | opcounters_repl_command | Number of replicated database commands since mongod instance last started* |
| Replication Operations: Deletes | opcounters_repl_delete | Number of replicated delete operations since mongod instance last started* |
| Replication Operations: Get More | opcounters_repl_getmore | Number of "getmore" operations since mongod instance last started* |
| Replication Operations: Inserts | opcounters_repl_insert | Number of replicated insert operations received since mongod instance last started* |
| Replication Operations: Queries | opcounters_repl_query | Number of replicated queries received since mongod instance last started* |
| Replication Operations: Updates | opcounters_repl_update | Number of replicated update operations received since mongod instance last started* |
| Resident Memory | mem_resident | Amount of RAM used by this resource's database processes |
| Slave Delay | slave_delay | Intentional lag time behind the primary of this resource's replica set |
| State | state_str | Current state of the mongod in the replica set |
| Storage Engine Name | storage_engine_name | Name of the current storage engine |
| Storage Engine Persistent | storage_engine_persistent | Indicates if the storage engine persists data to disk |
| Storage Engine Supports Committed Reads | storage_engine_supports_committed_reads | Indicates if the storage engine supports "majority" read concern |
| Subject Name | security_ssl_server_subject_name | Subject name associated with TLS/SSL certificate |
| Tags | tags | Document that describe the replica sets settings |
| Total Connections Created | connections_created | Count of all incoming connections created to this resource* |
| Total Operations | global_lock_current_queue_total | Number of operations queued waiting for the lock |
| Uptime | uptime | Time the current MongoDB process has been active |
| Version | version | Version of the current MongoDB process |
| Virtual Memory | mem_virtual | Virtual memory being used by the mongod process |
| Votes | votes | Number of votes this resource will have in a replica set election |
| Write Backs Queued | write_backs_queued | Indicates if there are operations from a mongos instance queued for retrying |
| Write Tickets | ticket_writes | Amount of total write tickets |
| Written Cache | cache_write | Amount of bytes written from cache* |
| Written to Data Files | dur_write_to_data_files | Data written from journal during latest journal group commit interval |

## Mongos
| Metric Name | Insights Key | Description |
| ----------- | ------------ | :---------- |
| Advisory Host FQDNs | advisory_host_fqdns | Advisory host fully qualified domain names of the machine hosting this resource |
| Asserts: Message | asserts_msg | Number of message assertions raised since the MongoDB process started* |
| Asserts: Regular | asserts_regular | Number of regular assertions raised since the MongoDB process started* |
| Asserts: Rollovers | asserts_rollovers | Number of rollovers since the MongoDB process started* |
| Asserts: User | asserts_user | Number of user assertions that have occurred since the MongoDB process started* |
| Asserts: Warning | asserts_warning | Number of warnings raised since the MongoDB process started* |
| Available Connections | connections_available | Number of unused incoming connections available to this resource |
| Background Flushing: Average | background_flushing_average | Average time for each flush to disk |
| Background Flushing: Flushes | background_flushing_flushes | Number of times the databases on this resource has flushed all writes to disk* |
| Background Flushing: Last | background_flushing_last | Time it took the last flush operation to complete |
| Background Flushing: Total | background_flushing_total | Time the mongod processes have spent writing data to disk |
| Current Connections | connections_current | Number of incoming connections to this resource |
| Extended Memory Supported | mem_supported | Indicates if the machine hosting this resource supports extended memory information |
| Heap Used | extra_info_heap_usage_bytes | Heap used by this resources database processes |
| Host Name | host_name | Hostname of the machine hosting this resource |
| IP Address | ip | IP address of the machine hosting this resource |
| Mapped Memory | mem_mapped | Amount of mapped memory by this resource's databases |
| Mapped Memory with Journal | mem_mapped_journal | Amount of mapped memory with journal by this resource's databases |
| Memory Architecture | mem_bits | Architecture of the machine hosting this resource |
| Network Traffic In | network_bytes_in | Bytes received by all databases of this resource* |
| Network Traffic Out | network_bytes_out | Bytes sent from all databases of this resource* |
| Number of Requests | network_num_requests | Number of requests this resource has received* |
| Operations: Commands | opcounters_command | Number of database commands since mongod instance last started* |
| Operations: Deletes | opcounters_delete | Number of delete operations since mongod instance last started* |
| Operations: Get More | opcounters_getmore | Number of "getmore" operations since mongod instance last started* |
| Operations: Inserts | opcounters_insert | Number of insert operations received since mongod instance last started* |
| Operations: Queries | opcounters_query | Number of queries received since mongod instance last started* |
| Operations: Updates | opcounters_update | Number of update operations received since mongod instance last started* |
| PID | pid | Process ID number on this resource |
| Page Faults | extra_info_page_faults | Total number of page faults* |
| Process | process | Current MongoDB process on this resource |
| Ratio of Page Faults to Operations | page_faults_to_ops_ratio | The ratio of Page Faults to Operations. |
| Ratio of Page Faults to Operations is Greater Than Or Equal to 1 | page_faults_to_ops_ratio_greater_than_1 | The ratio of Page Faults to Operations is greater than or equal to one. |
| Resident Memory | mem_resident | Amount of RAM used by this resource's database processes |
| Total Connections Created | connections_created | Count of all incoming connections created to this resource* |
| Total connections being used. | connections_used_over_available | The percent of connections being used. |
| Uptime | uptime | Time the current MongoDB process has been active |
| Version | version | Version of the current MongoDB process |
| Virtual Memory | mem_virtual | Virtual memory being used by the mongod process |

## Replica Set
| Metric Name | Insights Key | Description |
| ----------- | ------------ | :---------- |
| Chaining Allowed | chaining_allowed | Indicated if chaining is supported on this resource |
| Election ID | election_id | Election ID of this resource |
| Election Timeout | election_timeout | Duration of this resource's election timeout |
| Heartbeat Interval | heartbeat_interval | Frequency of this resource's heartbeats |
| Heartbeat Timeout | heartbeat_timeout | Duration of this resource's heartbeat timeout |
| Last Error Default | last_error_defaults | Last error default of this resource |
| Last Error Modes | last_error_modes | Last error modes of this resource |
| Number of Data Bearing Nodes | number_of_data_nodes | Number of Data Bearing Mongods that are not Arbiters. |
| Primary Replication | primary_replication | Indicates this resource is a primary replication set |
| Protocol Version | protocol_version | Protocol version of this resource |
| Replica Set Odd Vote Count | total_votes_odd | Replica Set odd votes. 1 if odd, 0 if even. |
| Replica Set Request Votes | repl_set_votes | Total request votes in a replica set |
| Replication Arbiters | replication_arbiters | List of arbiters within this replication set |
| Replication Hosts | replication_hosts | List of hosts within this replication set |
| Replication Rollback ID | replication_rollback_id | Rollback ID of this resource |
| Replication Set ID | replica_set_id | ID for this resource |
| State | state | State of this resource |
| Version | version | Version of MongoDB this resource has |

## Shard
| Metric Name | Insights Key | Description |
| ----------- | ------------ | :---------- |
| Host | host | Host of this resource |
| Shard Has Child Replica Set | has_replica_set_child | Shard Has a Replica Set as a Child. |
| Version | version | Shard version of this resource |

### * Metric Value Since Last Collection
