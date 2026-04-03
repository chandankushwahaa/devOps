# MSSQL DBA

## BACKUP AND RESTORE
**TYPES of Backups: -**
1. **Full Backup:** a complete, page-be-page copy of an entire database including all the data. All the structures and all other objects stored within the database.

2. **Differential backups:** a backup of a database that has modified in any way since the last full backup.

3. **Transaction log A backup:** of all the committed transactions currently stored in the transaction log.

4. **Copy-only backup:** a special use backup that is independent of the regular sequence of SQL server backups.

5. **File backup:** a backup of one or more database files or filegroups.

6. **Partial backup:** contains data from only some of the filegroups in a database.

**CREATE TEST DATABASE:-**
```
use master
go
```
```
create database backupDB 
go
```
```
use backupDB
go
```
**CREATE TABLE**
```sql
create table Products (ProductID int IDENTITY (1,1) Primary Key, Productflame varchar (100), Brand varchar (100)) 
go
```
**INSERT SOME RECORDS**
```sql
INSERT INTO Products (Productflame, Brand) VALUES ('iPhone 15', 'Apple');
INSERT INTO Products (Productflame, Brand) VALUES ('Galaxy S24', 'Samsung');
INSERT INTO Products (Productflame, Brand) VALUES ('Xperia 1 V', 'Sony');
INSERT INTO Products (Productflame, Brand) VALUES ('Pixel 8', 'Google');
INSERT INTO Products (Productflame, Brand) VALUES ('ThinkPad X1 Carbon', 'Lenovo');
```
View the TABLE to verify the data
```sql
SELECT * FROM Product;
```
### 1. FULL BACKUP USING T-SQL
```sql
BACKUP DATABASE [<DB_NAME>] TO DISK N'd:\fullbackups\dbbackup.bak'
WITH NOINIT, NAME NDB NAME>-Full Database Backup", COMPRESSION STATS 10
go
-- NOINIT: not be overwitten, STATS 10: updated every 10sec
```

**STEP FOR FULL BACKUP GUI:-**
- right click on database ->Tasks->Backup
- Destination: choose location remove and add new location if required followed by file name with .bak extension.
>NOTE: Take backup in off hours because it consume high CPU.
- To see the backup go to the location where you saved it.
>NOTE: after full backup if some entries added or replace and at that time do crash then the changes will not get recovered.

### 2. TRANSACTIONAL LOG BACKUP
To take tran. log backup 1st we must have recovery model is in FULL mode and 2nd full database backup had been executed.
**TO check recovery mode in all the databases:-**
```sql
SELECT name, recovery model desc
FROM sys.databases
ORDER BY name
```
Insert data into table AFTER a full backup, but before a transactional log backup. so it will log the new entry

**Transactional BACKUP USING T-SQL:-**
```sql
BACKUP LOG [<DB_NAME>]
TO DISK N'd:\fullbackups\dbbackup.bak' WITH NOINIT,
NAMEN<DB NAME>-Transactional Log Backup', COMPRESSION
STATS-10
go
```
> NOTE: the same bkp file will have the full backup and transactional log backup.

To see the details:-
```sql
RESTORE HEADERONLY FROM DISK N'd:\fullbackup\dbbackup.bak
```
You will see 2 row one is FULL backup and other is Transaction log backup.

> NOTE: FULL backup type is 1, differential backup type is 5 and trans. log backup type is 2.

### 3. DIFFERENTIAL BACKUP
So inserting data is continuing and if this happens all day and if we take transactional log backup every 15mins than at the end we may have more then 100 transactional log backup to accommodate those change made. 50, differential backup only record the changes since the last database FULL backup and it great for the restore.

**SCRIPT**
```sql
BACKUP DATABASE [<DB_NAME>]
TO DISK N'd: \fullbackups\dbbackup.bak" WITH DIFFERENTIAL, NOINIT, NAME N'DB_NAME>-Transactional Log Backup'
COMPRESSION
STATS 10
go
```
>NOTE: Differential are cumulative in nature and they can get large in size so monitor it. IT is use in LARGE databases.

## RESTORE

Delete the database right click and delete.

right click on Databases-> restore database-> device and add backup path-> select the file and click ok-> you will see all the backups taken like Full, transactional log backup and differential backup.-->Click ok it will restore it.

**TYPES:-**

1. With Recovery

2. With No Recovery

3. Standby Mode