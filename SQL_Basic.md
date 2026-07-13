
INDEX:-
![Advanced SQL Techniques]()

# Advanced SQL Techniques

## 1. Subqueries

## 2. CTE

## 3. VIEW
It is a virtual table that shows data without storing it physically. In order to see the data, we have to execute the query behind the view.

### Database Structure
```mermaid
flowchart TD

    SQL["🗄️ SQL Server"]

    DB1["📂 Database (Sales)"]
    DB2["📂 Database (HR)"]

    SQL --> DB1
    SQL --> DB2

    SCH1["📁 Schema (Orders)"]
    SCH2["📁 Schema (Customers)"]

    DB1 --> SCH1
    DB1 --> SCH2

    TBL["📋 Table (Order_Item)"]
    VW["👁️ View (Top_Orders)"]

    SCH1 --> TBL
    SCH1 --> VW

    COL["Columns"]
    KEY["Primary Key"]

    TBL --> COL
    TBL --> KEY

    COL --> NAME["Name"]
    COL --> TYPE["Data Type"]

    VW --> VIEWCOL["Columns"]

    classDef sql fill:#FFE082,stroke:#333,stroke-width:2;
    classDef db fill:#BBDEFB,stroke:#333;
    classDef schema fill:#C8E6C9,stroke:#333;
    classDef object fill:#E1F5FE,stroke:#333;
    classDef leaf fill:#F5F5F5,stroke:#333;

    class SQL sql;
    class DB1,DB2 db;
    class SCH1,SCH2 schema;
    class TBL,VW object;
    class COL,KEY,NAME,TYPE,VIEWCOL leaf;
```

### How we get the output from Table?
The sql query trigger the queue that is attached to the view and the query is responsible to query the physical table and then the result is going to fill the structure of the view and we get back the result.

We are directly querying the view but actually we indirectly querying a physical table.

![](/images/SQL/views.png)

### Difference
| VIEW | TABLE |
|--|--|
| No Persistance | Persisted Data |
| Easy to Maintain | Hard to maintain |
| Slow Response | Fast Response |
| Read | Read/Write |
### Why to use Views?
![](./images/SQL/views2.png)

In 1st all the Analyst using the same CTE query to get the result. so it is complete redundecy and make no sense.

so, 2nd we can do the first step as view in database insist of using CTE `SUM JOIN` each time we're going to take this script and put it in the database. So, the analyst, instead of going directly to the physical tables they can goto the view.

### Difference View & CTE

| VIEWS | CTE |
|--|--|
| Reduce redundancy in multi-queries | Reduce Redundancy in single query |
| Improve reusability in multi-queries | Improve reusability in single query |
| Persisted Logic | Temporary logic |
| Need to maintain - Create/Drop| no maintenance - auto cleanup |

```sql
-- (https://github.com/DataWithBaraa/sql-ultimate-course/blob/main/datasets/sql-server/init-sqlserver-salesdb.sql)
-- To Find the running Total of Sales for each month.
-- Without View using CTE
WITH CTE_Monthly_Summary AS (
	SELECT 
	DATETRUNC(month, OrderDate) OrderMonth,
	SUM(Sales) TotalSales,
	COUNT(OrderID) TotalOrders,
	SUM(Quantity) TotalQuantities
	FROM Sales.Orders
	GROUP BY DATETRUNC(month, OrderDate)
)
SELECT OrderMonth, TotalSales, SUM(TotalSales) OVER (ORDER BY OrderMonth) AS RunningTotal
FROM CTE_Monthly_Summary;

-- Using View : if a table or view is created without specifying a schema, it defaults to the DBO.
CREATE VIEW V_Monthly_Summary AS
(
	SELECT 
	DATETRUNC(month, OrderDate) OrderMonth,
	SUM(Sales) TotalSales,
	COUNT(OrderId) TotalOrders,
	SUM(Quantity) TotalQuantities
	FROM Sales.Orders
	GROUP BY DATETRUNC(month, OrderDate)
)

-- Insist of Query the above we will query the below view.
SELECT * from V_Monthly_Summary;

SELECT OrderMonth, TotalSales, SUM(TotalSales) OVER (ORDER BY OrderMonth) AS RunningTotal
FROM V_Monthly_Summary;

-- Creating View as Sales Schema
CREATE VIEW Sales.V_Monthly_Summary AS
(
-- ...
)

-- DROP VIEW
DROP VIEW Sales.V_Monthly_Summary;

-- TO modify the existing View in SQL Server we must drop it and recreate is with the change we need.
-- In Postgres we just add `CREATE OR REPLACE VIEW ..`
-- OR using T-SQL we can replace it. see below example.
IF OBJECT_ID('V_Monthly_Summary', 'V') IS NOT NULL
	DROP VIEW V_Monthly_Summary;
GO
CREATE VIEW V_Monthly_Summary AS
(
	SELECT 
	DATETRUNC(month, OrderDate) OrderMonth,
	SUM(Sales) TotalSales,
	COUNT(OrderId) TotalOrders
	FROM Sales.Orders
	GROUP BY DATETRUNC(month, OrderDate)
)
```

## 5. STORE PROCEDURE
A **Stored Procedure** in SQL is a **precompiled collection of one or more SQL statements** that is stored in the database and can be executed whenever needed.

We have to perform , 1. `INSERT`, 2. `UPDATE`, 3.`SELECT`  query which is keep repeating to get the data everyday which is bit time confusing and we might cause human error. So, that's why we have STORE PROCEDURES in SQL. 
So, we put all those sql statements in one program called STORE PROCEDURE. And this store proc. will store in server side of the database. so, inorder to interact with sql statement we got to execute the store procedure.
When we call exec SP inside the server it will start executing all the sql statements that we have inside the stored procedure and it will return back to the user.
> We can store multiple SQL statements in specific order and we can save in inside the database and each time we need ours sql statement we can go and simply execute them.

![](./images/SQL/StoreProcedure.png)


### Syntax
```sql
CREATE PROCEDURE ProcedureName AS
BEGIN 
-- Stored Procedure Definition
END

-- Execution (Call)
EXEC ProcedureName

-- TO DROP
DROP PROCEDURE <ProcedureName>

-- TO make Change in existing Stored proc.
CREATE OR ALTER PROCEDURE ...
```
### Example
```sql
-- Find the total numbers of Customers and Average Score of US customers.
-- 1. 
SELECT COUNT(*) TotalCustomers,
AVG(Score) AvgScore
FROM Sales.Customers
WHERE Country = 'USA'

-- 2. Turning the query into a Stored Procedure
CREATE PROCEDURE GetCustomerSummary AS
BEGIN
	SELECT COUNT(*) TotalCustomers,
	AVG(Score) AvgScore
	FROM Sales.Customers
	WHERE Country = 'USA'
END -- to see under DB click on Programmability

-- To Run the above Store procedure
EXEC GetCustomerSummary 
```

### Stored Procedure with Parameters
As in the above query insist of USA we can add India. so in this we are changing the static values with a parameter. and while executing the stored proc. we can decide with country we want to execute.
```sql
CREATE PROCEDURE GetCustomerSummaryWithPara @Country NVARCHAR(50)
AS
BEGIN
	SELECT COUNT(*) TotalCustomers,
	AVG(Score) AvgScore
	FROM Sales.Customers
	WHERE Country = @Country 
END

EXEC GetCustomerSummaryWithPara @Country = 'Germany'
EXEC GetCustomerSummaryWithPara @Country = 'USA'
```

### Multi-Queries Stored Procedure

```sql
CREATE PROCEDURE GetCustomerSummaryWithMultiQuery @Country NVARCHAR(50) = 'USA'
AS
BEGIN
	SELECT COUNT(*) TotalCustomers,
	AVG(Score) AvgScore
	FROM Sales.Customers
	WHERE Country = @Country; -- add semicolon at the end of every query 

-- Total no. of Orders and Total Sales
    SELECT
    COUNT(OrderID) TotalOrders,
    SUM(Sales) TotalSales
    FROM Sales.Orders o
    JOIN Sales.Customers c
    ON c.CustomerID = o.CustomerID
    WHERE c.Country = @Country;
END

-- TO RUn the above stored proc.
EXEC GetCustomerSummaryWithMultiQuery
```

### Variable in Stored Procedure
```sql
CREATE PROCEDURE GetCustomerSummaryWithVariables @Country NVARCHAR(50) = 'USA'
AS
BEGIN

DECLARE @TotalCustomers INT, @AvgScore FLOAT;
	SELECT 
        @TotalCustomers = COUNT(*) ,
	    @AvgScore = AVG(Score) 
	FROM Sales.Customers
	WHERE Country = @Country

    PRINT 'Total Customer from '+@Country+ ': ' + CAST(@TotalCustomers AS NVARCHAR);
    PRINT 'Average Score from '+@Country+ ': ' + CAST(@AvgScore AS NVARCHAR) 
END

-- To Run the above stored proc.
EXEC GetCustomerSummaryWithVariables
EXEC GetCustomerSummaryWithVariables @Country = 'Germany'
/*OUTPUT:
Total Customer from Germany:2
Average Score from Germany:425
*/
```

## 6. Triggers
A trigger in SQL is a special type of stored program that automatically executes (fires) when a specified event occurs on a table or view. Triggers are commonly used to enforce business rules, maintain audit logs, or automatically update related data.

Suppose we have Employees Table and each time we insert the data into Employees we automatically inserting data inside logs using triggers.

**TYPES**
 - **DML Trigger** : INSERT, UPDATE, DELETE
	 - **AFTER**: Runs After Event 	
	 - **INSTEAD OF**: Runs during event
 - **DDL Triggers**: CREATE, ALTER, DROP
 - **LOGGON**

 ```sql
-- 1. CREATE LOG Table
CREATE TABLE Sales.EmployeeLogs (
	LogID INT IDENTITY(1,1) PRIMARY KEY,
	EmployeeID INT,
	LogMessage VARCHAR(255),
	LogDate DATE
)

-- 2. Create Trigger on Employees Table
CREATE TRIGGER trg_AfterInsertEmployee ON Sales.Employees
AFTER INSERT
AS
BEGIN
	INSERT INTO Sales.EmployeeLogs (EmployeeID, LogMessage, LogDate)
	SELECT
		EmployeeID,
		'New Employee Added =' + CAST(EmployeeID AS varchar),
		GETDATE()
	FROM INSERTED -- virtual copy that holds a copy of the rows that are being inserted into the target table
END

-- 3. Insert New Data Into Employees and Verify
SELECT * FROM Sales.Employees; -- check total number of rows 

INSERT INTO Sales.Employees VALUES (6, 'Chandan', 'Kushwaha', 'IT', '2001-05-22', 'M', 50000, 3);

SELECT * FROM Sales.EmployeeLogs;  -- verify the log table
 ```