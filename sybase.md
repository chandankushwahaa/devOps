# SYBASE ASE 

LEARN

1. how to check isolation level:-
    - select @@maxpagesize
    - select @@isolation
2. 


## 1. Sybase Devices
- This device initially stores the master, model, tempdb and sybsystemdb system databases.
-  All of these databases except for master can be moved or expanded off the master device.
-  `sp_helpdevice master` : checking master device information
- `sp_helpdevice sysprocsdev` : checking device information
- `sysdevices` is the system table that records each device. It exists only in the master database.
- ```select * from sysdevices```
### DROPPING DEVICES
- ```sp_dropdevice LOGICAL_DEVICE_NAME```
- WHEN WE DROP DEVICE	
	- When we need to change, repair,or add hardware.
	- When we need to change the size of a device
- TO DO THIS, WE NEED TO DROP AND RECREATE THE DEVICE
	- We must remove all databases from a device before you can drop it.
	- `sp_dropdevice` does not delete device files from the OS. 
	- Device cannot be droped when in use.
	- Drop the database and then drop the device
		- ```drop database test```
		- ```go```
		- ```sp_helpdb test```
		- ```go``` -- This gives error because db is dropped.
		- ```sp_dropdevice datatest02```
		- ```go``` -- Device Dropped
		- ```sp_helpdevice datatest02```
		- ```go``` -- Gives error because device is dropped
		- AFTER THIS REMOVE THE FILES FROM FILE SYSTEM
		- cd /home/chandan/syb/data
		- ls -lrt
		- rm datatest02.dat
		- rm logtest02.dat  
- DISK RESIZE (Assume datatest02 is a new device)
	- `sp_helpdevice datatest02`
	- `disk resize name = 'datatest02' , size='100M'`
	- `go`
	- ```sp_helpdevice datatest02``` : check size 
### DISK DEFAULT
- When a database is created, you can specify the device on which it should be created.
- A default device is a device on which a database is created when no device has been specified.
- If there is no default device and you attempt to create a db without specifying a device, the command will fail.
### The master Device
- The master device is a default device named during installtion.
- It contains master,model,tempdb,and sybsystemdb database.
- The master db cannot be expanded off of the master device.
> `select name,vdevno from master..sysdevices` :  learn this 

## 2. DROP DATABASE
- **sp_helpdb** : it will list all the databases.
- **sp_helpdb testdb** : assume we want to delete testdb databse. It will list the db details and all device associated with it.
- **drop database testdb** : this will give error because we have to kill the processess who is use this db.
- **sp_who** : list the process which is using testdb database. copy spid and paste in below command.
- kill <PASTE_SPID> : this will kill the process.
- **drop database testdb**: now this will delete the testdb database.
- **sp_helpdb testdb**:  It throws db not found.
NEXT YOU CAN DELETE THE DEVICES ASSOCIATED WITH THAT TESTDB.
## 3. DATABASE CREATION
Before creating new database we have to create new device.
- **disk init name='datadev01', physname='/sybase/data1/datadev01.dat', size='500M'**
- **go** : this will create new data device
- **sp_helpdevice datadev01** : verify device has been created or not.
- **disk init name='logdev01', '/sybase/data1/logdev01', size='100M'**
- go
- **sp_helpdevice logdev01**
NOW WE CREATE DATABASE
- **create database testdb on datadev01="500M"**
- **log on logdev01="100M"**
- **go** : This will create new database on the above devices.
- **sp_helpdb testdb** : 

## 4. TABLE CREATION
- **sp_helpdb**
- **use testdb** : assuming testdb a database
- **go**
-
```sql
create emp{
num INT,
name CHAR(20)
}
```
- **go**
- **select * from emp**
- **go**
- **sp_help emp**
-
```sql
insert into emp values(1, "CK")
```
- **go**
-
```sql
-- view first 10 rows
SET ROWCOUNT 10
SELECT * FROM emp
SET ROWCOUNT 0
```

## 5. LOGIN ID CREATION
A system security officer creates a login account for a new user. A system administrator or database owner adds a user to database or assign a user to a group.

A locked ID means a user account is temporarily disabled and cannot log in to Sybase ASE.
- **select name from syslogins** : all users who can connect to the Sybase ASE server
- **select name from master..syslogins**
-  **sp_locklogin** : list locked login id's
- **select name, status from master..syslogins** : it will show name and status. status 0 means unlocked and other than 0 means id is locked.
- **sp_locklogin < USERNAME>, "unlock"** : this will unlock the lock id. 
- **sp_locklogin < USERNAME>, "lock"** : this will lock the unlock id.



## 6. Sybase System roles
|Role|Fuction  |
|--|--|
|sa_role  |perform system administration. |
|sso_role  |perform security administration  |
|oper_role  |perform operator function(can perform dumps and load)  |
|replication_role  |used by replication process  |
|sybase_ts_role  |used to perform undocumented maintenance tasks  |
|dtm_tm_role  |used in externally coordinated XA transactions  |
|ha_role  |controls high availability(HA) companion server actions  |
|mon_role  |provide access to monitoring tables  |
|js_admin_role  |allows for administration of the job scheduler  |
|js_client_role  |execute job scheduler task  |
|messaging_role  |administers and executes real-timemessaging  |
|web_services  |administers web services  |

**sa_role**
- installing SYBASE ASE
- creating and managing ASE login accounts.
- Granting roles and permissions to ASE users.
- managing and monitoring the use of disk space, memory and connections
- can perform dump and load for database.
- can configuring sybase ASE to achieve the best performace by using `sp_configure`, `sp_sysmon`
**sso_role**
- system security officer- All security-related tasks such as:-
- create/remove server login(sp_addlogin, sp_droplogin) 
- reset password for account (`sp_password`)
- lock/unlock Sybase ASE login
- create user defined role and grant/revoke permission.