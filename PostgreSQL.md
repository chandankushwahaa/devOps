# 1. PostgreSQL
- PostgreSQL is an open-source ORDBMS.

## Key Features
1. **ACID Compliance**: Four properties of ACID(automicity, consistency, isolation and durability) to make sure that database transactions are handled reliably.
2. **Concurrency Control**: Postgres offers multi-version concurrency control(MVCC), which enables concurrent access to the same data by serveral transactions without conflicts.
3. **Community-driven development**: Postgres is an open-source project with a large, active community, which contribute to the development and maintenance of the database.
4. **Extensibility**: The database supports a wide range of data types and can be easily extended with custom functions, operators and aggreates.
5. **Replication and high availability**: Postgres supports both synchronous and asynchronous replication and provides serverl tools forarchieving high availability.
6. **SQL compliance**: Postgres is compliant with the SQL standard which ensures it is easy to use for developers and analysts familiar with SQL.
## PostgreSQL Limits
|Items|Upper Limit | Description  |
|--|--| -- |
| Database Size | Unlimited | |
| Number of Databases | 4,294,950,911 | |
| Relations(Tables) per database | 1,431,650,303 | |
| Relation Size | 32TB | Default BLCKSZ of 8192 bytes |
| Rows per table | Limites by the number of tuples that can fit onto 4,294,967,295 pages  | |
| Columns per table | 1600 | |
| Field size | 1GB | |
| Identifier length | 63 bytes | |
| Indexes per table | Unlimited | Contraned by maximum relations per database |
| Columns per index | 32 | |
| Partition keys | 32 | |

# 2. Architecture 
- It is an ORDBMS based on client and server architecture.
- It consits of postgres server process, backgroung processes, backend process, memory structures and data files which constitutes an instance.
- It uses "Process per-user" client/server model.
- Program run by clients connect to the server instance and request read and write operations.
- Default port of PostgreSQL is **5432**.
## Process and Memory Architecture
![](/images/1postgresArchitecture.jpg)

## Postmaster Process / Master Postgres Process
- The postgres process is the first process started when you start postgreSQL.
- postgres server process is the parent of all processes related to database cluster management.
- Postgres process acts as supervisor process, whose job is to monitor, start, restart some processes if they die.
- It acts a listener and receive new connection request from the client.
- Authentication and Authorization of all incoming request is taken care by postgres process.
- It is responsible for performing recovery, initialize shared memory, and run background processes.
- It's also responsible for spawing backend process when there is a connection request from the client process.
- To Check processes and there process ID: 	
	- Windows: *goto taskmanager --> click details --> search for postgres.exe*
	- Linux: *ps -ef | grep postgres**

## Background Processes
|Process| Description|
| -- | -- |
|Check Pointer|Ensure that all the dirty buffers created up to a certain point are sent to disk so that the WAL up to that point can be recycled.|
|Autovacuum launcher|It is the responsibility of the autovacuum daemon to carry vacuum operations on bloated tables.|
|Archiver|When in archive log mode, copy the WAL file to the specified directory|
|Logger|Write the error message to the log file.|
|Writer|Periodically writes the special dirty buffer to a file.|
|Wal Writer|Write the WAL to the WAL file.|

## Memmory Components
|Shared Buffer|Wal Buffer|
|--|--|
|Determines how much memory is dedicated to postgreSQL to use for caching data.|Determmine the memory used to WAL data that has not yet been written to disk.|
|Primary objective is to minimize DISK IO.|This WAL data is the metadata information about changes to the acutal data and is sufficient to reconstruct actual data during database recovery opertaions|
|Frequently used blocks must be in the buffer for as long as possible|Wal buffer are flushed from the buffer area to wal segments by wal writer.|
|It is controlled by parameter named shared_buffer located in `postgresql.conf` file.|It is controlled by the `wal_buffers` parameter.|
|Default values is 128MB|Default values is 16MB|

## Local Memory(Backend Process)
|Process|Description|
|--|--|
|Work_Mem|Space used for sorting, bitmap operations, hash joins and merge joins. The default setting is 4 MB|
|Temp_buffers|These are session-local buffers used only for access to temporary tables. The default setting is 8MB|
|Maintenance_work_mem|Space used for vacuum and CREATE INDEX. The default setting is 64MB|

## Physical Files
|||
|--|--|
|Data Files|file which is used to store data|
|Wal files|Write ahead log file, where all transactions are recorded before the data is written to the data files.|
|Log files|All server messages incluing stderr, csvlog and syslog are logged in log files|
|Archive Logs(Optional)|Wal files which are copied to the archive location|


#  3. Storage Internals
### Pages
- It is the fixed length block of data.
- Every table and index is stored as an array of pages of fixed size. 
- All the data in the database resides in pages.
- By default, the page in 8KB in size.
- We can configure different page size during compiling the server. 
- Pages are smallest unit of data storage.
![]()
**Page Layout Description**

|Items| Description |
|--|--|
| PageHeader Data | 24 Bytes Long, contains general information about the page, including free space pointers |
|ItemIdData|Array of pairs pointing to the actual items, 4 Bytes per item.|
|Free Space|The unallocated space, new item pointers are allocated from the start of this area, new items from the end|
|Tuple|The actual item themselves|
|Special Space|Index access method specific data. Different methods store different data. Empty is ordinary tables|

## Rows 
- To accommodate rows into the pages we need to see size of row, datatypes & size of fields and amount of data.
### Segment
-  Made of multiple pages. 1GB in size.
- When a table or index exceeds 1GB it is divided into gigabyte sized segments.
- The segment size can be adjusted using the configuration option with segsize when building  postgreSQL.
### Toast
- TOAST(The oversized-Attribute Storage Technique) mechanism to handle very large rows that don't fir into a standard page.
- Handle large rows, automatic handling.
- Toasting breaks up the data into smaller parts across multiple pages.

# 4. Database Cluster
- Database cluster is a collection of databases that is managed by a single instance on a sever.
- Initdb creates a new PostgreSQL database cluster.
- Creating a database cluster consists of creating the directions in which the data is store. We call this ths *data directory*.
- Popluar Location of Data Directory:-
	- Linux : /var/lib/pgsql/data

**Initdb utility**
- initdb must be run as the user that will own the server process.
- initdb is not needed for windows environment
- there are two way to initialize database.
	- `initdb -D /usr/local/pgsql/data`
	- `pg_ctl -D /usr/local/pgsql/data initdb`
	- -D : data directory location
	- -W : we can use this option to force the super user to provide password before initialize db.
### Start/Stop Cluster
- Start Cluster Syntax:
	- Windows : pg_ctl –D  “C:\Program Files\PostgreSQL\version\data” start
	- Windows : Services.msc > Start Postgresql-version
	- Linux : pg_ctl –D  /var/lib/pgsql/data  start
	- Linux Central Tool : systemctl start postgresql-<version>
- Stop Cluster Syntax:-
	- Windows : pg_ctl -D “C:\Program Files\PostgreSQL\<version>\data” stop
	- Windows : Services.msc > Stop Postgresql-version.
	- Linux : pg_ctl –D  /var/lib/pgsql/data  stop
	- Linux Central Tool : systemctl stop postgresql-<version>
**NOTE:** `pg_ctl stop -m shutdown mode`
### Reload\Restart Cluster
- Syntax for Reload of Cluster:
	- Windows/Linux: pg_ctl reload
	- Linux Central Tool : systemctl reload postgresql-<version>

- Syntax for Restart of Cluster:
	- Windows/Linux: pg_ctl restart
	- Linux Central Tool : systemctl restart postgresql-<version>

- Psql Command line: 
	- `SQL : SELECT pg_reload_conf();` (Irrespective of Env)
	
### `pg_ctl` Commands
- Find status of postgresql cluster.
	- `pg_ctl status`

- How to register Postgresql as system service in Windows.
	- `pg_ctl  register [-D datadir] [-N servicename]  [-S a[uto]`

- How to unregister Postgresql as system service in Windows.
	- `pg_ctl  unregister [-N servicename]`

	





## 1. Working With Databases
- **\list** - show list of databases.
- **\! cls** - clear screen
- **psql -U postgress** - connect to postgress via cmd.
- **SELECT datname FROM pg_database;** - query to list databases.
- **\l** - command to list of databases
- **CREATE DATABASE test;** - create new database with name `test`.
- **\c <DB_NAME>** - to change database.
- **psql -U <your_username> -d <your_database>** -  Connect to the Database. username is default **postgres**.

## 2. Working With Table NOOB
- CREATING
	```sql
	CREATE TABLE person(
		id INT,
		name VARCHAR(100),
		city VARCHAR(100)
	);
	```
	- **\d <TABLE_NAME> or \dt** - will the column in which format data to be stored.
- INSERTING
	```sql
	INSERT INTO person (id, name, city)
	VALUES (101, 'Ram', 'Delhi');
	```
- READING 
```sql
SELECT * FROM person;
```
- UPDATING
```sql
UPDATE person SET city='Mumbai' WHERE id=102;
```
- DELETING
```sql
DELETE FROM person WHERE id=104;
```
## 3. DATATYPE

###  a. Numeric Types

| Data Type     | Description                                | Range/Size                      |
|---------------|--------------------------------------------|----------------------------------|
| `smallint`    | Small-range integer                        | -32,768 to +32,767 (2 bytes)     |
| `integer`     | Typical choice for integer                 | -2,147,483,648 to +2,147,483,647 (4 bytes) |
| `bigint`      | Large-range integer                        | -9,223,372,036,854,775,808 to +9,223,372,036,854,775,807 (8 bytes) |
| `decimal(p,s)`| Exact numeric with precision & scale       | User-defined                     |
| `numeric(p,s)`| Same as `decimal`                          | User-defined                     |
| `real`        | Single precision floating-point number     | 6 decimal digits precision (4 bytes) |
| `double precision` | Double precision floating-point number | 15 decimal digits precision (8 bytes) |
| `serial`      | Auto-incrementing integer (4 bytes)        | 1 to 2,147,483,647               |
| `bigserial`   | Auto-incrementing big integer (8 bytes)    | 1 to 9,223,372,036,854,775,807   |

---

### b. Character Types

| Data Type        | Description                                     |
|------------------|-------------------------------------------------|
| `char(n)`        | Fixed-length character string                   |
| `varchar(n)`     | Variable-length character string with limit     |
| `text`           | Variable-length character string, no limit      |

---

### c. Date/Time Types

| Data Type           | Description                                  |
|---------------------|----------------------------------------------|
| `date`              | Calendar date (YYYY-MM-DD)                   |
| `time`              | Time of day (no time zone)                   |
| `time with time zone` (`timetz`) | Time of day with time zone         |
| `timestamp`         | Date and time (no time zone)                 |
| `timestamp with time zone` (`timestamptz`) | Date and time with time zone  |
| `interval`          | Time span (duration)                         |

---

### d. Boolean Type

| Data Type | Description                     |
|-----------|---------------------------------|
| `boolean` | Stores `TRUE`, `FALSE`, or `NULL` |
---

### e. Enumerated Types (Enum)
Custom data types with predefined values.
```sql
CREATE TYPE mood AS ENUM ('sad', 'ok', 'happy');
```


## 4. PRO LEVEL of CREATING TABLE

- CREATE - this inside test database

```sql
	CREATE TABLE customers(
	acc_no SERIAL PRIMARY KEY,
	name VARCHAR(100) NOT NULL,
	acc_type VARCHAR(50) NOT NULL DEFAULT 'Savings'
);
```
- INSERT 
```sql
-- 1.
INSERT INTO customers (name) VALUES ('Chandan Kushwaha');
-- 2. 
INSERT INTO customers (name, acc_type) VALUES ('Kaliya', 'Current');

```