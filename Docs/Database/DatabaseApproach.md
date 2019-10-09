---
title: Database Approach
author: rxcontributortwo
category: rxwebcore core
---

The core part of any software application is the `database designing`. It is a process of organizing data in a proper structural way. Before working on the business logic part in the application, we must decide what data is to be stored and which elements will be interrelated to each other. With all these information, you can start creating the database and its entities with respect to that application.

# Creating Tables
Tables have data of entities in database and as every entity have multiples records, the table name should be created with name in plural for eg: [dbo].Persons and their coloumn should be in pascal case  
For example 

```js
CREATE TABLE dbo.Persons  
(  
    PurchaseOrderID int NOT NULL  
    FullName [varchar](50) NOT NULL
);  
```

# Creating Views

## View
View are virtual tables used for retrieving of records based on join queries and table coloumns. It is created based upon name of the entity and the reference table  
For eg: [dbo].vPersons 

```js
CREATE VIEW [dbo].[vPersons]
AS
SELECT        PersonId, FullName
FROM            dbo.Persons
```


## Record View
Record Views are made to retrieve data from the entity that you want to display in user interface 
For eg: [dbo].vPersonRecords

```js
CREATE VIEW [dbo].[vPersonRecords]
AS
SELECT        PersonId, FullName
FROM            dbo.Persons
GO
```

# Creating Stored Procedures
In some cases, there is a need of some operation where we want to perform complex Tansact-SQL queries inspite of queries in SQL. For such complex operations, we use `Stored Procedures`. Stored Procedures are more faster and secure as compared to the query written in application code and redure network traffic. 

Name of the Stored Procedure must start with `sp` followed by the custom name you want to give. For example: `spAuditLogs`.

> In case of search stored procedure the same must be like `spSearchPerson`
