# SYBASE ASE 
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
- **select name from syslogins** : all users who can connect to the Sybase ASE server
- **select name from master..syslogins**
