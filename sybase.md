# SYBASE ASE 

LEARN
1. how to check isolation level:-
    - select @@maxpagesize
    - select @@isolation
2. Executing Queries
```sql
<FILENAME.bat> <SERVERNAME> <DATABASENAME> sysadmin <PASSWORD>
isql -Usysadmin -P***** -D<DB_NAME> -S<SERVERNAME> -i<INPUTFILENAME.sql> -o<OUTPUTFILENAME.txt>
```

### Sybase Basics:-

We have general IDs:-
1. sybdba : to perform basic activities.
2. sybase: to perform all major activities like software installation, licence renewal, etc. is done using sybase.
3. `/sybase/ase16sp04pl07/ASE-16_0` : we have all sybase related information.
4. `SYSAM-2.0` : inside this we have all details of sybase licences.

Important Files: `SYBASE.sh`, `SYBASE.csh`, `SYBASE.env`
`ls -la` : list all hidden files, `SYBASE.sh` responsible for executing all the sybase related command.

`pwd`
`/home/sybdba/etc`: inside this we can see which database we have to  configured.
`cat FullDB_env.cfg`: in this we can see database name that is configured for backup


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

## 2. DATABASE CREATION
Before creating new database we have to create new device.

```sql
-- allocating db space  HOSTNAME: like USALUSTG001
disk init
name='tst_db_data1',
physname='/sybase/<HOSTNAME>/data1/tst_db_data1.dat',
size='300M'
go
```
```sql
-- allocating log
disk init
name='tst_db_log1',
physname='/sybase/<HOSTNAME>/tlog1/tst_db_log1.dat',
size='200M'
go
```

```sql
-- This will create new database
create database tst_db on tst_db_data1 = '300M' log on tst_db_log1 = '200M'
go
```

### Adding Space in Existing Database
```sql
sp_helpdevice DB_NAME
go -- follow the devie name sequence if last device is data002 the create new device with data003
```
```sql
disk  init
name='tst_db_data1',
physname='/sybase/<HOSTNAME>/data1/tst_db_data1.dat',
size='10G'
go
```
>NOTE: sometime after running the above if we get error like: " The maximum number 150 of configured devices has been reached. Please reconfigured 'number of devices' to larger  value."
```sql
sp_configure 'number of devices', 300
go -- this will changed the value from 150 to 300. means we can add upto 300 device in the current database.
```
```sql
-- TO verify the device that we have initlize 
select name from sysdevices where name like 'tst_db_data%' 
```
```sql
alter database tst_db on tst_db_data1 = "10G"
go -- this will take some time dependin upon the size 
```
### ADDING LOGS
```sql
-- allocating db space HOSTNAME: like USALUSTG001
disk  init
name='tst_db_data1',
physname='/sybase/<HOSTNAME>/tlogs1/tst_db_log1.dat',
size='10G'
go
alter database tst_db on tst_db_data1 = "10G"
go
```
## 4. TABLE CREATION
```sql
sp_helpdb -- list all dbs
sp_helpdb tst_db 
```

```sql
sp_help -- to check all the tables
-- creating user table
create table table1(a int, b int)
```
```sql
use tst_db
go
create emp{ -- create user table
num INT,
name CHAR(20)
}
go
select * from emp
go
sp_help emp  -- to view table details

```
```sql
insert into emp values(1, "CK")
go
-- view first 10 rows
SET ROWCOUNT 10
SELECT * FROM emp
SET ROWCOUNT 0
```
### Adding Space in Current User Database


## 3. DROP DATABASE
- **sp_helpdb** : it will list all the databases.
- **sp_helpdb tst_db** : assume we want to delete testdb databse. It will list the db details and all device associated with it.
- **drop database tst_db** : this will give error because we have to kill the processess who is use this db.
- **sp_who** : list the process which is using testdb database. copy spid and paste in below command.
- **kill <PASTE_SPID>** : this will kill the process.
- **drop database testdb**: now this will delete the testdb database. But device inside db is not dropped so we have to drop the devices
- **sp_dropdevice tst_db_data1** : we have to drop all the device associated with the database.
- **sp_helpdevice tst_db** : to  check all the devices
- **sp_helpdb tstdb**:  It throws db not found.

We have to delete some files which is created when we created new device this will delete from sysprocesses and sysusers db's.
- `rm /sybase/<HOSTNAME>/data1/tst_db_data1.dat`
- `rm /sybase/<HOSTNAME>/tlogs1/tst_db_log1.dat`

## 5. LOGIN ID CREATION
A system security officer creates a login account for a new user. A system administrator or database owner adds a user to database or assign a user to a group.

**Creating New Login With Same SUID in Primary, Reporting and DR Server:-**
1. Before adding SUID we have to check the last SUID on the server then add +1. ex. if SUID is 331 then for new account creation we have to put 332.

```sql
select max(suid) from master..syslogins -- run in primary server
```

2. Run the below in master db first in primary then reporting and at last DR server.
```sql
create login chandann with password Chandan@12345 suid 332 fullname "Chandan Kushwaha" password expiration 90 min password length 8 max failed attempts 10
```
3. Now add user in Primary
```sql
use <DB_NAME>
sp_adduser chandann, chandann, <GROUP_NAME>
```
4. Verify in Reporting and DR server
```sql
use <DB_NAME>
sp_helpuser chandann -- without any error
```
5. Now Lock the user in Primary Server
```sql
sp_locklogin chandann, "lock"
sp_displaylogin chandann -- to verify login is locked
```


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








