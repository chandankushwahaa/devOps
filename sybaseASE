# Sybase

1. [Overview](#1-overview)
2. [Database Design](#2-database-design-and-management)



## **1. Overview**
- **Sybase**: A software company founded in 1984, known for its relational database management system (RDBMS), Sybase Adaptive Server Enterprise (ASE), and other data management tools. Acquired by SAP in 2010, Sybase now primarily refers to its database and middleware products under SAP's umbrella.
-   **Sybase ASE**: A traditional RDBMS optimized for high-performance transactional workloads, competing with Oracle Database and Microsoft SQL Server. It uses a client-server architecture and supports SQL.
- **Sybase ASE** is a client-server RDBMS designed for scalability, high performance, and reliability. It supports structured query language (SQL) for data manipulation and management, with additional features like stored procedures, triggers, and advanced transaction control. It competes with databases like Oracle, Microsoft SQL Server, and IBM DB2.
-   **Sybase ASE** is known for low-latency transaction processing, often used in financial systems (e.g., trading platforms).

### Key Features:

-   **High Availability**: Supports clustering and failover mechanisms.
-   **Performance**: Optimized for online transaction processing (OLTP) and decision support systems (DSS).
-   **Security**: Robust encryption, authentication, and access control.
-   **Scalability**: Handles large datasets and high-concurrency environments.
-   **Cross-Platform**: Runs on Windows, Linux, and Unix-based systems.
-    Supports T-SQL (Transact-SQL), similar to Microsoft SQL Server.

### Key Features:
- Banking and financial systems.

- Telecommunications.

- Large enterprise applications with high transaction volumes.


### **2. Sybase Architecture**

Sybase ASE follows a client-server architecture, where the database server processes requests from multiple clients over a network. Here’s a detailed look at its architecture:

#### **Components**

1.  **Database Server (Data Server)**:
    -   The core of Sybase ASE, responsible for managing databases, executing queries, and handling transactions.
    -   Uses a multi-threaded architecture to handle concurrent user requests efficiently.
    -   Key processes include:
        -   **Data Engine**: Manages data storage, retrieval, and query execution.
        -   **Transaction Manager**: Ensures ACID (Atomicity, Consistency, Isolation, Durability) properties for transactions.
        -   **Memory Manager**: Allocates memory for caching data, query plans, and buffers.
        -   **I/O Manager**: Handles disk operations for data storage and retrieval.
2.  **Clients**:
    -   Applications or tools (e.g., SQL clients, ODBC/JDBC drivers) that connect to the server to send queries and receive results.
    -   Common client tools include **isql** (command-line interface), SAP ASE Cockpit, and third-party tools like SQL Developer.
3.  **Storage**:
    -   Data is stored in **databases**, which are logical containers for tables, indexes, and other objects.
    -   Each database is divided into **devices** (physical disk files) for data and logs.
    -   **Pages** (typically 2KB, 4KB, 8KB, or 16KB) are the smallest unit of storage, organized into extents (8 pages).
4.  **Network Layer**:
    -   Uses protocols like TCP/IP for client-server communication.
    -   Supports Open Client/Server APIs for connectivity (e.g., CT-Lib, DB-Lib).

### 3. Syntax

1. **Creating a Database**:
```sql
CREATE DATABASE mydatabase
ON mydevice = 100 -- 100MB for data
LOG ON logdevice = 50 -- 50MB for transaction log
```
2. **Creating a Table**:
```sql
CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    hire_date DATE,
    salary DECIMAL(10,2)
)
```
3. **Inserting Data**:    
```sql    
 SELECT first_name, last_name, salary FROM employees WHERE salary >  50000  ORDER  BY salary DESC
```    
4.  **Updating Data**:
    
```sql
UPDATE employees SET salary = salary *  1.1  WHERE hire_date <  '2024-01-01'`
   ```
5  **Deleting Data**:
```sql
DELETE  FROM employees WHERE emp_id =  1
```    
6   **Creating a Stored Procedure**:
```sql 
CREATE  PROCEDURE sp_get_employee (@emp_id INT) AS  BEGIN  SELECT  *  FROM employees WHERE emp_id =  @emp_id END`
  ```
7   **Transaction Control**:
 ```sql
 BEGIN TRANSACTION UPDATE employees SET salary =  80000  WHERE emp_id =  1  IF @@ERROR  =  0  COMMIT TRANSACTION ELSE  ROLLBACK TRANSACTION`
  ```

### 4.  **Learning and Using Sybase**

#### **Best Practices**

-   **Indexing**: Create indexes on frequently queried columns, but avoid over-indexing to prevent performance degradation.
-   **Transaction Management**: Use transactions for critical operations to ensure data integrity.
-   **Backup**: Regularly use `DUMP DATABASE` and `DUMP TRANSACTION` for backups.
-   **Performance Tuning**: Monitor query plans using `SET SHOWPLAN ON` and optimize slow queries.

#### **Common Tools**

-   **isql**: Command-line tool for executing SQL queries.
-   **SAP ASE Cockpit**: Web-based interface for monitoring and managing ASE servers.
-   **DBArtisan**: Third-party GUI for database administration.
-   **ODBC/JDBC Drivers**: For connecting applications to Sybase.

### 5. Default system databases in Sybase
- **master** : stores system configuration information. Its primary role is to manage and control the operation of the Sybase ASE server and all other databases within it.
- **model** : serves as a template for creating new user databases.
- **tempdb** : Used for temporary storage of data.
- **sybsystemdb** : Manages distributed transaction information.
- **sybsystemprocs** : Contains system stored procedures used for administrative tasks.

### 6.  Sybase Transaction Management
Sybase (SAP ASE) handles **transaction management** using standard **ACID** (Atomicity, Consistency, Isolation, Durability) principles, ensuring data integrity in multi-user environments. Here's how it works in detail:

###  1. **Transaction Control**
In Sybase ASE, transactions can be either:
-   **Implicit Transactions** (auto-managed by the server)
    
-   **Explicit Transactions** (manually controlled using `BEGIN TRAN`, `COMMIT`, `ROLLBACK`)
- ####  Explicit Transaction Example:
```sql
BEGIN TRANSACTION
    UPDATE accounts SET balance = balance - 500 WHERE id = 1
    UPDATE accounts SET balance = balance + 500 WHERE id = 2
COMMIT
```

### 2. **Transaction Isolation Levels**
Sybase supports multiple **isolation levels** (as per SQL standards), which control how data is read or locked during transactions:
|Level	| Description  |
|--|--|
| READ UNCOMMITTED | allows dirty reads |
| READ COMMITTED | prevents dirty reads |
| REPEATABLE READ | prevents non-repeatable reads |
| SERIALIZABLE | prevents phantom rows |

```sql
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE
```
### 3. **Locking Mechanism**
Sybase uses **page-level** and **row-level locking** for concurrency control. It automatically locks the necessary resources during a transaction, based on isolation level and access type.

-   Shared Locks: For reads.
-   Exclusive Locks: For writes/updates.
-   Intent Locks: Indicate future locks needed at lower levels.
- 
### 4. **Durability and Recovery**

Sybase uses a **transaction log (syslogs)** to ensure durability. All transaction steps are recorded here.

-   On **COMMIT**: Log is flushed to disk.
-   On **ROLLBACK**: Changes are undone using the log.
-   On **crash recovery**: Sybase replays or rolls back transactions from the log.

### 5. **Savepoints**
Sybase supports `SAVE TRAN` for partial rollbacks within a transaction:
```sql
BEGIN TRANSACTION
    UPDATE table1 ...
    SAVE TRAN mySave
    UPDATE table2 ...
    ROLLBACK TRANSACTION mySave
COMMIT

```


## 2. Database Design and Management

### 🔹 1. Creating and Managing Users in Sybase

In Sybase ASE, users are managed at two levels: **server-level logins** (for accessing the server) and **database-level users** (for accessing specific databases).
#### 1.  Creating Users
1. **Create a Server Login**:
-   Use the `sp_addlogin` stored procedure to create a login.
```sql
sp_addlogin 'username', 'password', 'default_database', 'default_language', 'fullname'
```
-   username: Login name.
-   password: Password for the login.
-   default_database: Database the user connects to by default (e.g., master).
-   default_language: Optional language setting.
-   fullname: Optional full name for the user.

2. **Create a Database User**:
    -   After creating a login, add the user to a specific database using `sp_adduser`.
    -   Example:
 ```sql
USE my_database sp_adduser 'username', 'user_alias', 'group_name'
```  
  - user_alias: Optional alias for the user within the database.
  -   group_name: Optional group for role-based access (if applicable).
        
3.   **Grant Permissions**:
-   Assign permissions using `GRANT` (e.g., SELECT, INSERT, EXECUTE) or roles.  
-   Example:
  ```sql
 GRANT  SELECT  ON my_table TO username 
 GRANT sa_role TO username -- Assigns system administrator role
 ```
 
#### 4.  **Managing Users**
-   **Modify Login**:
    -   Use `sp_modifylogin` to update login properties (e.g., password, default database).
    -   Example:
       ```sql
       sp_modifylogin 'username', 'passwd', 'new_password'
       ```
        
-   **Drop Login/User**:
    -   Remove a login with `sp_droplogin` (must drop user from all databases first).
    -   Remove a database user with `sp_dropuser`.
    -   Example:
        ```sql
        sp_dropuser 'username'  -- From a specific database  
        sp_droplogin 'username'  -- From the server
        ```
        
-   **Monitor Users**:
    -   View logins: `SELECT * FROM master..syslogins`
    -   View database users: `SELECT * FROM sysusers` (in the specific database).
-   **Roles**:
    -   Sybase supports predefined roles (e.g., sa_role, sso_role) and custom roles.
    -   Create a role: CREATE ROLE my_role
    -   Assign a role: GRANT ROLE my_role TO username

### 🔹 2. Types of indexes in Sybase, and how do they impact performance?

1. **Clustered Index** :
	- Physically sorts and stores the table’s data in the order of the index key.
	-   Only one clustered index per table (as it dictates physical data order).
	-   Best for: Range queries, joins, and queries with `ORDER BY` on the indexed column.
	```sql
	CREATE CLUSTERED INDEX idx_emp_id ON employees(emp_id)
	```
2. **Non-Clustered Index** :
	-  Stores a separate structure with pointers to the actual data, leaving the table’s physical order unchanged.
	-   Multiple non-clustered indexes are allowed per table.
	-   Best for: Point queries, selective WHERE clauses, and covering queries.
	```sql
	CREATE NONCLUSTERED INDEX idx_emp_name ON employees(last_name)
	```
3. **Unique Index** :
	-   Ensures no duplicate values in the indexed column(s).
	-   Can be clustered or non-clustered.
```sql
CREATE  UNIQUE NONCLUSTERED INDEX idx_unique_email ON employees(email)
```
4. **Composite Index** :
	-   Indexes multiple columns together, useful for queries involving multiple columns in WHERE, JOIN, or ORDER BY.
```sql
CREATE NONCLUSTERED INDEX idx_comp ON employees(dept_id, hire_date)
```
5. **Function-Based Index** :
	-   Indexes the result of a function or expression, useful for queries with computed values.
```sql
CREATE NONCLUSTERED INDEX idx_upper_name ON employees(UPPER(last_name))
```
#### Impact on Performance

-   **Benefits**:
    -   **Faster Reads**: Indexes speed up SELECT queries, especially for WHERE, JOIN, and ORDER BY.
    -   **Clustered Indexes**: Optimize range queries and sequential access due to physical data ordering.
    -   **Non-Clustered Indexes**: Improve point queries and searches on non-ordered columns.
    -   **Covering Indexes**: Include all columns needed by a query, reducing disk I/O.
-   **Drawbacks**:
    -   **Slower Writes**: Indexes increase overhead for INSERT, UPDATE, and DELETE operations, as the index must be updated.
    -   **Storage Overhead**: Indexes consume additional disk space.
    -   **Maintenance**: Indexes require periodic rebuilding (REORG) to maintain performance, especially after heavy data modifications.
    -   **Query Optimizer Dependency**: Poorly designed indexes or outdated statistics can lead to suboptimal query plans.

### 🔹 3. **Locking in Sybase and Its Types**
Locking in Sybase ASE ensures data consistency during concurrent transactions by restricting access to data being modified. It prevents issues like dirty reads, lost updates, and non-repeatable reads, aligning with transaction isolation levels.

#### Types of Locks :-
Sybase ASE uses several lock types, primarily at the **page**, **row**, or **table** level:

1.  **Shared Lock (S)**:
	- For read operations. Others can read, but not write.
    -   Acquired during SELECT operations to allow multiple transactions to read the same data.
    -   Prevents concurrent writes but allows concurrent reads.
    -   Example: A SELECT query locks a page/row to ensure stable data during reading.
2.  **Exclusive Lock (X)**:
	- For write operations. Blocks others.
    -   Acquired during INSERT, UPDATE, or DELETE operations.
    -   Prevents other transactions from reading or modifying the locked data until the transaction completes.
    -   Example: An UPDATE query locks the affected rows exclusively.
3.  **Update Lock (U)**:
	- Used during potential writes to avoid deadlocks.
    -   A hybrid lock used during the initial phase of an UPDATE operation.
    -   Allows concurrent reads but prevents other updates, converting to an exclusive lock when the data is modified.
    -   Reduces deadlocks in complex transactions.
4.  **Intent Lock**:
    -   Indicates a transaction’s intent to lock a resource at a lower granularity (e.g., table-level intent lock for row-level locking).
    -   Ensures hierarchical locking consistency (e.g., table → page → row).
#### Locking Granularity

-   **Row-Level Locking**: Locks individual rows, minimizing contention for concurrent transactions.
-   **Page-Level Locking**: Locks an entire data page (default in older versions or specific configurations).
-   **Table-Level Locking**: Locks the entire table, used for operations like CREATE INDEX or when explicitly requested.
-   Configured via sp_configure or table-level options (LOCK TABLE).

#### Impact on Performance

-   **Concurrency**: Row-level locking improves concurrency but increases overhead. Page-level locking is less granular but faster for bulk operations.
-   **Deadlocks**: Occur when transactions wait for each other’s locks. Sybase detects and resolves deadlocks by rolling back one transaction.
-   **Isolation Levels**: Higher isolation levels (e.g., Level 3) use more restrictive locking, reducing concurrency but ensuring data consistency.

>Use `sp_who` to view active transactions and `sp_lock` to inspect locks.
```sql
SELECT  *  FROM master..syslocks
```

### 🔹  4. **Performing Backups and Restores**
#### Database Backups
Sybase ASE uses the `DUMP` command to back up databases and transaction logs. Backups are critical for recovery and should include both the database and its transaction log.

1. **Full Database Backup**:
-   Backs up the entire database, including data and log.
	```sql
	DUMP DATABASE my_database TO '/path/to/backup/my_database.dmp'
	```
2. **Transaction Log Backup**:
-   Backs up the transaction log for point-in-time recovery.
-   Requires the database to have a separate log segment and trunc log on chkpt disabled.
```sql
DUMP TRANSACTION my_database TO '/path/to/backup/my_database_log.dmp'
```
4. **Cumulative Backup** (Sybase ASE 15.7+):
-   Backs up all changes since the last full backup.
```sql
DUMP DATABASE my_database TO '/path/to/backup/my_database_cumulative.dmp' WITH CUMULATIVE
```
**Best Practices**:
-   Schedule regular full and transaction log backups.
-   Store backups on separate storage for safety.
-   Use sp_helpdb to verify database backup eligibility.
- 
#### Database Restores
The `LOAD` command restores databases or transaction logs from backup files.
1. **Restore a Database**:
```sql
LOAD DATABASE my_database FROM '/path/to/backup/my_database.dmp'
```
2. **Restore Transaction Logs**:
-   Apply transaction log backups in sequence to recover up to a specific point.
```sql
LOAD TRANSACTION my_database FROM '/path/to/backup/my_database_log.dmp'
```
- Use `WITH UNTIL_TIME` for point-in-time recovery:
```sql
LOAD TRANSACTION my_database FROM '/path/to/backup/my_database_log.dmp' WITH UNTIL_TIME = '2025-06-10 10:00:00'
```
3. **Bring Database Online**:
After loading, bring the database online:
```sql
ONLINE DATABASE my_database
```
**Best Practices**:
-   Test backups regularly to ensure restorability.
-   Verify backup files with `sp_dbcc_verifybackup`.
-   Document the restore sequence for disaster recovery.
- 
### 🔹 5. **Transaction Log Purpose and Management**
#### Purpose of the Transaction Log
The transaction log in Sybase ASE is a system table (stored in the database’s log segment) that records all data modifications `(INSERT, UPDATE, DELETE)` to ensure durability and support recovery.

#### Managing the Transaction Log
1. **Monitor Log Space**:
-   Check log usage with `sp_spaceused` or `dbcc checktable(syslogs).`
```sql
SELECT name, log_size = size/512.0 FROM sysdatabases WHERE name = 'my_database'
```
2. **Truncate the Log**:
-   Remove inactive log records to free space (only if transaction log backups are not needed).
```sql
DUMP TRANSACTION my_database WITH TRUNCATE_ONLY
```
 -   Use `WITH NO_LOG` for emergency truncation if the log is full and backups aren’t required.
3. **Back Up the Log**:
-   Regularly back up the transaction log to enable point-in-time recovery and free log space.
```sql
DUMP TRANSACTION my_database TO '/path/to/backup/my_database_log.dmp'
```
4. **Expand Log Space**:
If the log fills up, extend the log segment:
```sql
ALTER DATABASE my_database LOG ON device_name = size_in_MB
```
5. **Configure Log Truncation**:
- Enable/disable automatic log truncation on checkpoint:
```sql
sp_dboption 'my_database', 'trunc log on chkpt', true  -- Truncates log automatically
```
-    Disable for databases requiring transaction log backups.
6. **Handle Log Full Issues**:
-   If the log fills, transactions may suspend. Use `sp_who` to identify blocking transactions and resolve them.
-   Emergency fix: Temporarily increase log size or truncate with `NO_LOG`.
7. **Best Practices**:
-   Separate data and log segments on different devices for performance.
-   Schedule regular transaction log backups for critical databases.
-   Monitor log growth with tools like `sp_monitor` or `sp_logdevice`.

-   **Security**: Ensure only authorized users (e.g., sa_role) manage critical operations like backups or user creation.
-   **Performance Tuning**: Regularly update statistics (UPDATE STATISTICS) and rebuild indexes (REORG) to maintain performance.
-   **Monitoring**: Use system stored procedures (sp_who, sp_lock, sp_helpdb) for real-time monitoring.