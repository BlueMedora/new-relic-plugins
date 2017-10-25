## Replication Master
| Metric Name | Description |
| ----------- | :---------- |
| Auto Positioning | Whether or not auto-positioning is in use |
| Connect Retry Durations | The number of seconds between connect retries |
| Last I/O Error Message | The error message of the most recent error that caused the I/O thread to stop |
| Last I/O Error Number | The error number of the most recent error that caused the I/O thread to stop. 0 means no error has been recorded |
| Last I/O Error Timestamp | A timestamp in YYMMDD HH:MM:SS format that shows when the most recent I/O error took place |
| Last SQL Error Message | The error message of the most recent error that caused the SQL thread to stop |
| Last SQL Error Number | The error number of the most recent error that caused the SQL thread to stop. 0 means no error has been recorded |
| Last SQL Error Timestamp | A timestamp in YYMMDD HH:MM:SS format that shows when the last SQL error occurred |
| Master Host | The master host that the slave is connected to |
| Master Port | The port used to connect to the master |
| Master Retry Count | The number of times the slave can attempt to reconnect to the master in the event of a lost connection |
| Master SSL Allowed | Whether or not an SSL connection to the master is permitted. This value will report as 'Ignored' if an SSL connection is permitted but the slave server does not have SSL support enabled |
| Master SSL Verify Server Certificate | Whether or not SSL server certificates must be validated |
| Master Server ID | The server_id value from the master |
| Master UUID | The Universally Unique Identifier from the master |
| Master User | The user name of the account used to connect to the master |
| SQL Delay | The number of seconds that the slave must lag the master |
| Slave I/O Running | Whether the I/O thread is started and has connected successfully to the master |
| Slave I/O State | A copy of the State field of the SHOW PROCESSLIST output for the slave I/O thread. This tells you what the thread is doing: trying to connect to the master, waiting for events from the master, reconnecting to the master, and so on |
| Slave SQL Running | Whether the SQL thread is started |
| Slave SQL Running State | The state of the SQL thread |

## Database
| Metric Name | Description |
| ----------- | :---------- |
| Average Delete Wait Time | The average Delete wait time |
| Average Fetch Wait Time | The average Fetch wait time |
| Average Insert Wait Time | The average Insert wait time |
| Average Read Wait Time | The average Read wait time |
| Average Read/Write Wait Time | The average R/W wait time |
| Average Update Wait Time | The average Update wait time |
| Average Write Wait Time | The average Write wait time |
| Binlog Dump Threads | The number of Binlog Dump threads |
| Change User Threads | The number of Change User threads |
| Close Statement Threads | The number of Close Statement threads |
| Connect Out Threads | The number of Connect Out threads |
| Connect Threads | The number of Connect threads |
| Connected Threads | The number of Connected threads |
| Create DB Threads | The number of Create DB threads |
| Daemon Threads | The number of Daemon threads |
| Database Data Size | The size of the database's data |
| Database Index Size | The size of the database's indexes |
| Database Name | The name of the database |
| Database Total Size | The total size of the database |
| Debug Threads | The number of Debug threads |
| Delayed Insert Threads | The number of Delayed Insert threads |
| Drop DB Threads | The number of Drop DB threads |
| Error Threads | The number of Error threads |
| Execute Threads | The number of Execute threads |
| Fetch Threads | The number of Fetch threads |
| Field List Threads | The number of Field List threads |
| I/O Misc Latency | The average latency of miscellaneous I/O |
| I/O Misc Requests | The number of I/O miscellaneous requests* |
| I/O Read Latency | The average latency of I/O reads |
| I/O Read Requests | The number of I/O read requests* |
| I/O Reads | The number of I/O reads* |
| I/O Write Latency | The average latency of I/O writes |
| I/O Write Requests | The number of I/O write requests* |
| I/O Writes | The number of I/O writes* |
| Init DB Threads | The number of Init DB threads |
| Kill Threads | The number of Kill threads |
| Long Data Threads | The number of Long Data threads |
| Maximum Delete Wait Time | The maximum Delete wait time |
| Maximum Fetch Wait Time | The maximum Fetch wait time |
| Maximum Insert Wait Time | The maximum Insert wait time |
| Maximum Read Wait Time | The maximum Read wait time |
| Maximum Read/Write Wait Time | The maximum R/W wait time |
| Maximum Update Wait Time | The maximum Update wait time |
| Maximum Write Wait Time | The maximum Write wait time |
| Minimum Delete Wait Time | The minimum Delete wait time |
| Minimum Fetch Wait Time | The minimum Fetch wait time |
| Minimum Insert Wait Time | The minimum Insert wait time |
| Minimum Read Wait Time | The minimum Read wait time |
| Minimum Read/Write Wait Time | The minimum R/W wait time |
| Minimum Update Wait Time | The minimum Update wait time |
| Minimum Write Wait Time | The minimum Write wait time |
| Misc Threads | The number of Misc threads |
| Ping Threads | The number of Ping threads |
| Prepare Threads | The number of Prepare threads |
| Processlist Threads | The number of Processlist threads |
| Query Threads | The number of Query threads |
| Quit Threads | The number of Quit threads |
| Refresh Threads | The number of Refresh threads |
| Register Slave Threads | The number of Register Slave threads |
| Reset Statement Threads | The number of Reset Statement threads |
| Rows Deleted | The number of rows deleted* |
| Rows Fetched | The number of rows fetched* |
| Rows Inserted | The number of rows inserted* |
| Rows Read | The number of rows read* |
| Rows Read/Written | The total number of rows read and written* |
| Rows Updated | The number of rows updated* |
| Rows Written | The number of rows written* |
| Set Option Threads | The number of Set Option threads |
| Shutdown Threads | The number of Shutdown threads |
| Sleep Threads | The number of Sleep threads |
| Statistics Threads | The number of Statistics threads |
| Table Dump Threads | The number of Table Dump threads |
| Total Delete Wait Time | The total Delete wait time* |
| Total Fetch Wait Time | The total Fetch wait time* |
| Total Insert Wait Time | The total Insert wait time* |
| Total Read Wait Time | The total Read wait time* |
| Total Read/Write Wait Time | The total R/W wait time* |
| Total Update Wait Time | The total Update wait time* |
| Total Write Wait Time | The total Write wait time* |
| Unused Indexes | The number of unused indexes |

## Index
| Metric Name | Description |
| ----------- | :---------- |
| Delete Latency | The total wait time of timed deletes from the index* |
| Index Name | The name of the index |
| Insert Latency | The total wait time of timed inserts into the index* |
| Is Used | Whether or not the index is used |
| Rows Deleted | The total number of rows deleted from the index* |
| Rows Inserted | The total number of rows inserted into the index* |
| Rows Selected | The total number of rows read using the index* |
| Rows Updated | The total number of rows updated in the index* |
| Select Latency | The total wait time of timed reads using the index* |
| Table Name | The table that contains the index |
| Table Schema | The schema that contains the table |
| Update Latency | The total wait time of timed updates in the index* |

## Instance
| Metric Name | Description |
| ----------- | :---------- |
| ALTER TABLE's, CREATE INDEX's, DROP INDEX's In Progress | Number of ALTER TABLE, CREATE INDEX, DROP INDEX in progress |
| Aborted Connections | The number of failed attempts to connect to the MySQL server* |
| Active Transactions | The number of active transactions |
| Active Transactions Rolled Back | The number of resurrected active transactions rolled back* |
| Adaptive Hash B-tree Searches | The number of searches using B-tree on an index search* |
| Adaptive Hash Pages Added | The number of index pages on which the Adaptive Hash Index is built* |
| Adaptive Hash Pages Removed | The number of index pages whose corresponding Adaptive Hash Index entries were removed* |
| Adaptive Hash Rows Added | The number of Adaptive Hash Index rows added* |
| Adaptive Hash Rows Deleted With No Hash Entry | The number of rows deleted that did not have corresponding Adaptive Hash Index entries* |
| Adaptive Hash Rows Removed | The number of Adaptive Hash Index rows removed* |
| Adaptive Hash Rows Updated | The number of Adaptive Hash Index rows updated* |
| Adaptive Hash Searches | The number of successful searches using Adaptive Hash Index* |
| Background Drop Table Time | The time spent to process drop table list* |
| Buffer Data Reads | The amount of data read in bytes* |
| Buffer Data Written | The amount of data written in bytes* |
| Buffer Flush Adaptive | The number of adaptive batches* |
| Buffer Flush Adaptive Pages | The pages queued as an adaptive batch* |
| Buffer Flush Adaptive Total Pages | The total pages flushed as part of adaptive flushing* |
| Buffer Flush Average Page Rate | The average number of pages at which flushing is happening |
| Buffer Flush Background | The number of background batches* |
| Buffer Flush Background Pages | The number of pages queued as a background batch* |
| Buffer Flush Background Total Pages | The total pages flushed as part of background batches* |
| Buffer Flush Batch Num Scan | The number of times buffer flush list flush is called* |
| Buffer Flush Batch Pages | The number of pages queued as a flush batch* |
| Buffer Flush Batch Rescan | The number of times rescan of flush list forced* |
| Buffer Flush Batch Scanned | The total pages scanned as part of flush batch* |
| Buffer Flush Batch Scanned Per Call | The number of pages scanned per flush batch scan |
| Buffer Flush Batch Total Pages | The total pages flushed as part of flush batch* |
| Buffer Flush Batches | The number of flush batches* |
| Buffer Flush LSN Average Rate | The average redo generation rate |
| Buffer Flush Neighbor | The number of times neighbors flushing is invoked* |
| Buffer Flush Neighbor Pages | The number of pages queued as a neighbor batch* |
| Buffer Flush Neighbor Total Pages | The total neighbors flushed as part of neighbor flush* |
| Buffer Flush Number To Flush Requested | The number of pages requested for flushing* |
| Buffer Flush Percent For Dirty | The percent of I/O capacity used to avoid max dirty page limit. |
| Buffer Flush Percent For LSN | The percent of I/O capacity used to avoid reusable redo space limit |
| Buffer Flush Sync | The number of sync batches* |
| Buffer Flush Sync Pages | The pages queued as a sync batch* |
| Buffer Flush Sync Total Pages | The total pages flushed as part of sync batches* |
| Buffer Flush Sync Waits | The number of times a wait happens due to sync flushing* |
| Buffer LRU Batch Evict Pages | The number of pages queued as a LRU evict batch* |
| Buffer LRU Batch Evict Total Pages | The total pages evicted as part of LRU evict batch* |
| Buffer LRU Batch Flush Pages | The number of pages queued as a LRU flush batch* |
| Buffer LRU Batch Flush Total Pages | The total pages flushed as part of LRU flush batch* |
| Buffer LRU Batch Number Scanned | The number of times LRU batch is called* |
| Buffer LRU Batch Pages | The number of pages queued as an LRU batch* |
| Buffer LRU Batch Scanned | The total pages scanned as part of LRU batch* |
| Buffer LRU Batch Scanned Per Call | The number of pages scanned per LRU batch call |
| Buffer LRU Batch Total Pages | The total pages flushed as part of LRU batches* |
| Buffer LRU Batches | The number of LRU batches* |
| Buffer LRU Batches Evict | The number of LRU evict batches* |
| Buffer LRU Batches Flush | The number of LRU flush batches* |
| Buffer LRU Get Free Search | The number of searches performed for a clean page* |
| Buffer LRU Search Number Scan | The number of times LRU search is performed* |
| Buffer LRU Search Scanned | The total pages scanned as part of LRU search* |
| Buffer LRU Search Scanned Per Call | The number of pages scanned per single LRU search |
| Buffer LRU Single Flush Failure Count | The number of attempts to flush a single page from LRU failed* |
| Buffer LRU Single Flush Number Scan | The number of times single page LRU flush is called* |
| Buffer LRU Single Flush Scanned | The total pages scanned as part of single page LRU flush* |
| Buffer LRU Single Flush Scanned Per Call | The number of pages scanned per single LRU flush |
| Buffer LRU Unzip Search Number Scan | The number of times LRU unzip search is performed* |
| Buffer LRU Unzip Search Scanned | The total pages scanned as part of LRU unzip search* |
| Buffer LRU Unzip Search Scanned Per Call | The number of pages scanned per single LRU unzip search |
| Buffer Page Read Extent Descriptor | The number of Extent Descriptor Pages read* |
| Buffer Page Read File Space Header | The number of File Space Header Pages read* |
| Buffer Page Read First Compressed BLOB | The number of First Compressed BLOB Pages read* |
| Buffer Page Read Index Inode | The number of Index Inode Pages read* |
| Buffer Page Read Index Insert Buffer Leaf | The number of Insert Buffer Index Leaf Pages read* |
| Buffer Page Read Index Insert Buffer Non Leaf | The number of Insert Buffer Index Non-Leaf Pages read* |
| Buffer Page Read Index Leaf | The number of Index Leaf Pages read* |
| Buffer Page Read Index Non Leaf | The number of Index Non-leaf Pages read* |
| Buffer Page Read Insert Buffer Bitmap | The number of Insert Buffer Bitmap Pages read* |
| Buffer Page Read Insert Buffer Free List | The number of Insert Buffer Free List Pages read* |
| Buffer Page Read Other | The number of other/unknown (old version of InnoDB) Pages read* |
| Buffer Page Read Subsequent Compressed BLOB | The number of Subsequent Compressed BLOB Pages read* |
| Buffer Page Read System Page | The number of System Pages read* |
| Buffer Page Read Transaction System | The number of Transaction System Pages read* |
| Buffer Page Read Uncompressed BLOB | The number of Uncompressed BLOB Pages read* |
| Buffer Page Read Undo Log | The number of Undo Log Pages read* |
| Buffer Page Written Extent Descriptor | The number of Extent Descriptor Pages written* |
| Buffer Page Written File Space Header | The number of File Space Header Pages written* |
| Buffer Page Written First Compressed BLOB | The number of First Compressed BLOB Pages written* |
| Buffer Page Written Index Inode | The number of Index Inode Pages written* |
| Buffer Page Written Index Insert Buffer Leaf | The number of Insert Buffer Index Leaf Pages written* |
| Buffer Page Written Index Insert Buffer Non Leaf | The number of Insert Buffer Index Non-Leaf Pages written* |
| Buffer Page Written Index Leaf | The number of Index Leaf Pages written* |
| Buffer Page Written Index Non Leaf | The number of Index Non-leaf Pages written* |
| Buffer Page Written Insert Buffer Bitmap | The number of Insert Buffer Bitmap Pages written* |
| Buffer Page Written Insert Buffer Free List | The number of Insert Buffer Free List Pages written* |
| Buffer Page Written Other | The number of other/unknown (old version InnoDB) Pages written* |
| Buffer Page Written Subsequent Compressed BLOB | The number of Subsequent Compressed BLOB Pages written* |
| Buffer Page Written System Page | The number of System Pages written* |
| Buffer Page Written Transaction System | The number of Transaction System Pages written* |
| Buffer Page Written Uncompressed BLOB | The number of Uncompressed BLOB Pages written* |
| Buffer Page Written Undo Log | The number of Undo Log Pages written* |
| Buffer Pages Created | The number of pages created* |
| Buffer Pages Read | The number of pages read* |
| Buffer Pages Written | The number of pages written* |
| Buffer Pool Bytes Data | The number of buffer bytes containing data |
| Buffer Pool Bytes Dirty | The number of buffer bytes currently dirty |
| Buffer Pool Pages Data | The number of buffer pages containing data |
| Buffer Pool Pages Dirty | The number of buffer pages currently dirty |
| Buffer Pool Pages Free | The buffer pages currently free |
| Buffer Pool Pages Miscellaneous | The number of buffer pages for miscellaneous use such as row locks or the adaptive hash index |
| Buffer Pool Pages Total | The total buffer pool size in pages |
| Buffer Pool Read Ahead | The number of pages read as read ahead* |
| Buffer Pool Read Ahead Evicted | The read-ahead pages evicted without being accessed* |
| Buffer Pool Read Requests | The number of logical read requests* |
| Buffer Pool Reads | The number of reads directly from disk* |
| Buffer Pool Size | The server buffer pool size (all buffer pools) in bytes |
| Buffer Pool Wait Free | The number of times waited for free buffer* |
| Buffer Pool Write Requests | The number of write requests* |
| Change Buffer Deleted Merged Operations Discarded | The number of delete merged operations discarded* |
| Change Buffer Deleted Records Merged | The number of deleted records merged by change buffering* |
| Change Buffer Insert Merged Operations Discarded | The number of insert merged operations discarded* |
| Change Buffer Inserted Records Merged | The number of inserted records merged by change buffering* |
| Change Buffer Merge Time | The time spent to process change buffer merge* |
| Change Buffer Number Merges | The number of change buffer merges* |
| Change Buffer Purge Merged Records Discarded | The number of purge merged operations discarded* |
| Change Buffer Purge Records Merged | The number of purge records merged by change buffering* |
| Change Buffer Size | The change buffer size in pages |
| Checkpoint Time | The time spent by master thread to do checkpoint* |
| Connections | The number of connection attempts (successful or not) to the MySQL server* |
| Current Rollback Size | The current rollback segment size |
| DICT LRU Processing Time | The time spent to process DICT LRU list* |
| Data Reads | The number of reads initiated* |
| Data Writes | The number of writes initiated* |
| Deadlocks | The number of deadlocks* |
| Doublewrite Operation Pages Written | The number of pages that have been written for doublewrite operations (innodb_dblwr_pages_written)* |
| Doublewrite Writes | The number of doublewrite operations that have been performed (innodb_dblwr_writes)* |
| Files Currently Open | The number of files currently open |
| Hostname | The Hostname |
| Index Page Discards | The number of index pages discarded* |
| Index Page Merge Attempts | The number of index page merge attempts* |
| Index Page Merge Successes | The number of successful index page merges* |
| Index Page Reorganization Attempts | The number of index page reorganization attempts* |
| Index Page Reorganization Successes | The number of successful index page reorganizations* |
| Index Page Splits | The number of index page splits* |
| Index Push-Down Condition Check Attempts | The number of Index Push-Down Condition check attempts* |
| Index Push-Down Conditions Match | The number of Index Push-Down Conditions with a match* |
| Index Push-Down Conditions No Match | The number of Index Push-Down Conditions with no match* |
| Index Push-Down Conditions Out Of Range | The number of Index Push-Down Conditions out of range* |
| Indexes Being Created Online | Number of indexes being created online |
| Indexes Waiting To Drop | Number of indexes waiting to be dropped after failed index creation |
| Insert And Update Commits | The number of transactions committed with inserts and updates* |
| Instance Name | The Instance Name |
| Lock Timeouts | The number of lock timeouts* |
| Log Bytes Written | The bytes of log written* |
| Log Checkpoints | The number of checkpoints* |
| Log Current LSN | The current log sequence number value |
| Log Flush Time | The time spent to flush log records* |
| Log LSN Checkpoint Age | The current log sequence number value minus log sequence number at last checkpoint* |
| Log LSN at Last Checkpoint | The log sequence number at last checkpoint |
| Log LSN of Last Flush | The log sequence number of Last flush |
| Log Number Log IO | The number of log I/Os* |
| Log Oldest LSN in Buffer Pool | The oldest modified block log sequence number in the buffer pool |
| Log Pending Checkpoint Writes | The pending checkpoints* |
| Log Pending Log Writes | The pending log writes* |
| Log Pending Writes | The number of pending log file writes* |
| Log Pending fsync Writes | The number of pending fsync writes* |
| Log Waits | The number of log waits due to small log buffer* |
| Log Write Requests | The number of log write requests* |
| Log Writes | The number of log writes* |
| Log fsync Writes | The number of fsync log writes* |
| Master Active Loops | The number of times master thread performs its tasks when server is active* |
| Master Idle Loops | The number of times master thread performs its tasks when server is idle* |
| Master Purge Time | The time spent by master thread to purge records* |
| Master Thread Sleep Time | The amount of time master thread has slept* |
| Max Connections | The Max Connections |
| Max Modified LSN Age For ASYNC Preflush | The maximum log sequence number difference; when exceeded, start asynchronous preflush |
| Max Modified LSN Age For SYNC Preflush | The maximum log sequence number difference; when exceeded, start synchronous preflush |
| Max Used Connections | The maximum number of connections that have been in use simultaneously since the server started |
| Memory Pool Size | Size of a memory pool InnoDB uses to store data dictionary and internal data structures in bytes |
| Memory Validation Time | The time spent to do memory validation* |
| Non-Locking Auto-Commit Read Only Commits | The number of non-locking auto-commit read-only transactions committed* |
| Number of Padding Decrements Due To Compression | The number of times padding is decremented due to good compressibility* |
| Number of Padding Increments Due To Compression | The number of times padding is incremented to avoid compression failures* |
| Number of Pages Compressed | The number of pages compressed* |
| Number of Pages Decompressed | The number of pages decompressed* |
| OS Waits From Exclusive Latch Request | The number of rwlock OS waits due to exclusive latch request* |
| OS Waits From Shared Latch Request | The number of rwlock OS waits due to shared latch request* |
| Page Size | The Page Size |
| Pending Reads | The number of reads pending |
| Pending Writes | The number of writes pending |
| Port | The Port |
| Purge DML Delay Time | The microseconds DML to be delayed due to purge lagging |
| Purge Delete Marked Records | The number of delete-marked rows purged* |
| Purge Invoked | The number of times purge was invoked* |
| Purge Resume Count | The number of times purge was resumed |
| Purge Stop Count | The number of times purge was stopped |
| Purge Undo Log Pages | The number of undo log pages handled by the purge* |
| Purge Update Existing Or External Records | The number of purges on updates of existing records and updates on delete marked record with externally stored field* |
| Read Only Transaction Commits | The number of read-only transactions committed* |
| Read Write Transaction Commits | The number of read-write transactions committed* |
| Record Lock Requests | The number of record locks requested* |
| Record Lock Waits | The number of record locks requested* |
| Record Locks | The current number of record locks on tables |
| Record Locks Created | The number of record locks created* |
| Record Locks Removed | The number of record locks removed from the lock queue* |
| Row Lock Current Waits | Number of row locks currently being waited for |
| Row Lock Time | Time spent in acquiring row locks* |
| Row Lock Time Average | The average time to acquire a row lock |
| Row Lock Time Max | The maximum time to acquire a row lock |
| Row Lock Waits | Number of times a row lock had to be waited for* |
| Rows Deleted | The number of rows deleted* |
| Rows Inserted | The number of rows inserted* |
| Rows Read | The number of rows read* |
| Rows Updated | The number of rows updated* |
| SSL Client Connections | The number of SSL connection attempts to an SSL-enabled master* |
| SSL Connection Renegotiates | The number of negotiates needed to establish the connection to an SSL-enabled master* |
| SSL Finished Connections | The number of successful slave connections to an SSL-enabled master* |
| Server Activity Count | The current server activity count |
| Server ID | The Identifier of the MySQL Instance |
| Server UUID | The Universally Unique Identifier of the MySQL Instance |
| TRX_RSEG_HISTORY List Length | The length of the TRX_RSEG_HISTORY list |
| Table Handles Closed | The number of table handles closed* |
| Table Handles Opened | The number of table handles opened* |
| Table Lock Waits | The number of record locks requested* |
| Table Locks | The number of tables locks* |
| Table Locks Created | The number of table locks created* |
| Table Locks Removed | The number of table locks removed from the lock queue* |
| Table Reference Count | The number of table references* |
| Tables Waiting To Drop | Number of tables in background drop table list |
| Threads Connected | The number of currently open connections |
| Total Allocated Memory | The total allocated memory |
| Transaction Rollbacks | The number of transactions rolled back* |
| Transactions Rolled Back To Savepoint | The number of transactions rolled back to savepoint* |
| Undo Slots Cached | The number of undo slots cached* |
| Undo Slots Used | The number of undo slots used* |
| Version | The Version |
| fsync() Calls Count | The number of fsync() calls* |
| rwlock Spin Loop Rounds From Exclusive Latch Request | The number of rwlock spin loop rounds due to exclusive latch request* |
| rwlock Spin Loop Rounds From Shared Latch Request | The number of rwlock spin loop rounds due to shared latch request* |
| rwlock Spin Waits From Exclusive Latch Request | The number of rwlock spin waits due to exclusive latch request* |
| rwlock Spin Waits From Shared Latch Request | The number of rwlock spin waits due to shared latch request* |

## Query
| Metric Name | Description |
| ----------- | :---------- |
| Average Errors | The total number of errors produced by occurrences of the statement |
| Average Latency | The average wait time per timed occurrence of the statement |
| Average Lock Latency | The average time waiting for locks per timed occurrence of the statement |
| Average Rows Affected | The average number of rows affected per occurrence of the statement |
| Average Rows Examined | The average number of rows read from storage engines per occurrence of the statement |
| Average Rows Sent | The average number of rows returned per occurrence of the statement |
| Average Rows Sorted | The average number of rows sorted per occurrence of the statement |
| Average Sort Merge Passes | The average number of sort merge passes per occurrence of the statement* |
| Average Temporary Tables Created In-Memory | The average number of internal in-memory temporary tables created per occurrence of the statement |
| Average Temporary Tables Created On-Disk | The average number of internal on-disk temporary tables created per occurrence of the statement |
| Average Warnings | The average number of warnings produced by occurrences of the statement |
| Database | The default database for the statement, or 'None' if there is none |
| Error Count | The total number of errors produced by occurrences of the statement* |
| Execution Count | The total number of times the statement has executed* |
| First Seen | The first time at which the statement was seen |
| Last Seen | The most recent time at which the statement was seen |
| Lock Latency | The total time waiting for locks by timed occurrences of the statement* |
| Max Latency | The maximum single wait time of timed occurrences of the statement |
| Rank | The rank of this query, according to the way queries are ordered (usually by average latency) |
| Rows Affected | The total number of rows affected by occurrences of the statement* |
| Rows Examined | The total number of rows read from storage engines by occurrences of the statement* |
| Rows Sent | The total number of rows returned by occurrences of the statement* |
| Rows Sorted | The total number of rows sorted by occurrences of the statement* |
| SQL ID | An identifier for the query, also known as the digest |
| SQL Text | The normalized statement string |
| Sort Merge Passes | The total number of sort merge passes by occurrences of the statement* |
| Temporary Tables Created In-Memory | The total number of internal in-memory temporary tables created by occurrences of the statement* |
| Temporary Tables Created On-Disk | The total number of internal on-disk temporary tables created by occurrences of the statement* |
| Total Latency | The total wait time of timed occurrences of the statement* |
| Warning Count | The total number of warnings produced by occurrences of the statement* |

## Table
| Metric Name | Description |
| ----------- | :---------- |
| Database Name | The name of the database that contains this table |
| Delete Average Wait Time | The average wait time of deletes |
| Delete Max Wait Time | The maximum wait time of deletes |
| Delete Min Wait Time | The minimum wait time of deletes |
| Delete Total Wait Time | The total wait time of deletes |
| Fetch Average Wait Time | The average wait time of fetches |
| Fetch Max Wait Time | The maximum wait time of fetches |
| Fetch Min Wait Time | The minimum wait time of fetches |
| Fetch Total Wait Time | The total wait time of fetches |
| Full Rows Scanned | The number of times the table has been fully scanned |
| I/O Misc Latency | The total wait time of miscellaneous I/O requests for the table* |
| I/O Misc Requests | The total number of miscellaneous I/O requests for the table* |
| I/O Read | The total number of bytes read from the table* |
| I/O Read Latency | The total wait time of reads from the table* |
| I/O Read Requests | The total number of read requests for the table* |
| I/O Write | The total number of bytes written to the table* |
| I/O Write Latency | The total wait time of writes to the table* |
| I/O Write Requests | The total number of write requests for the table* |
| Insert Average Wait Time | The average wait time of inserts |
| Insert Max Wait Time | The maximum wait time of inserts |
| Insert Min Wait Time | The minimum wait time of inserts |
| Insert Total Wait Time | The total wait time of inserts |
| R/W Average Wait Time | The average wait time of reads and writes |
| R/W Max Wait Time | The maximum wait time of reads and writes |
| R/W Min Wait Time | The minimum wait time of reads and writes |
| R/W Total Wait Time | The total wait time of reads and writes |
| Read Average Wait Time | The average wait time of reads |
| Read Max Wait Time | The maximum wait time of reads |
| Read Min Wait Time | The minimum wait time of reads |
| Read Total Wait Time | The total wait time of reads |
| Rows Deleted | The number of rows deleted* |
| Rows Fetched | The number of rows fetched* |
| Rows Inserted | The number of rows inserted* |
| Rows Read | The number of rows read* |
| Rows Read/Written | The total number of rows read and written* |
| Rows Updated | The number of rows updated* |
| Rows Written | The number of rows written* |
| Table Data Size | The size of the table's data |
| Table Index Size | The size of the table's indexes |
| Table Name | The name of the table |
| Table Total Size | The total size of the table |
| Update Average Wait Time | The average wait time of updates |
| Update Max Wait Time | The maximum wait time of updates |
| Update Min Wait Time | The minimum wait time of updates |
| Update Total Wait Time | The total wait time of updates |
| Write Average Wait Time | The average wait time of writes |
| Write Max Wait Time | The maximum wait time of writes |
| Write Min Wait Time | The minimum wait time of writes |
| Write Total Wait Time | The total wait time of writes |

## Tablespace
| Metric Name | Description |
| ----------- | :---------- |
| Current File Size | The actual size of the file, which is the amount of space allocated on disk |
| File Format | The tablespace file format. The data in this field is interpreted from the tablespace flags information that resides in the .ibd file |
| Maximum File Size | The apparent size of the file, which represents the maximum size of the file, uncompressed |
| Page Size | The tablespace page size. The data in this field is interpreted from the tablespace flags information that resides in the .ibd file |
| Row Format | The tablespace row format (Compact or Redundant, Dynamic, or Compressed). The data in this field is interpreted from the tablespace flags information that resides in the .ibd file |
| Space Type | The type of tablespace. Possible values include General (for InnoDB general tablespaces created using CREATE TABLESPACE) and Single (for InnoDB file-per-table tablespaces) |
| Tablespace Flag Settings | This value provides bit level information about tablespace format and storage characteristics |
| Tablespace ID | The tablespace ID |
| Tablespace Name | The database and table name |
| Zip Page Size | The tablespace zip page size. The data in this field is interpreted from the tablespace flags information that resides in the .ibd file |

## Query Plan
| Metric Name | Description |
| ----------- | :---------- |
| Plan | JSON representation of the query execution plan. |

## Replication Slave
| Metric Name | Description |
| ----------- | :---------- |
| Master Host | The host name of the slave server as specified on the slave with the --report-host option |
| Master Port | The port on the master to which the slave server is listening, as specified on the slave with the --report-port option |
| Master Server ID | The unique server ID of the master server that the slave server is replicating from |
| Slave Server ID | The server_id value from the slave |
| Slave UUID | The Universally Unique Identifier from the slave |

### * Metric Value Since Last Collection 
