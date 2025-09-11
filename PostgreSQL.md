# Postgress SQL



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