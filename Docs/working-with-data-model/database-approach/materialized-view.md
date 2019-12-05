---
title: Materialized View
author: rxcontributorone
category: database-approach 
---

# Materialized View

To perform effective quering becomes much necessary when we want to recieve our desired resultset which depends upon many factors that is the size of the data, integrity of the data. For scenarios where you want to `display a list of records` where the resultset includes more than one table and generating a query is difficult. Generating a view saves execution time in compared to complex queries. It requires less maintenance. Besides this the data in the views get high availability and resilency benefits.

> It is preferable to create a view if the number of records are limited upto 500. If it exceeds it is preferable to create a [stored procedure] for it.

In HRManagementSystem we have a list of departments to be displayed. Here there are three cases where making materialized view can be helpful which are stated below:

## 1. Displaying List of records
Suppose we want to display a list of departments, we will make a `vDepartments` view for the same. Here Departments id the table name and we add a abbreviation `v` which is here meant for a view. We do this to maintain a consistency of the naming convention used all over the application. 

```
CREATE VIEW [dbo].[vDepartments]
AS
SELECT        DepartmentId, DepartmentName
FROM            dbo.Departments
```

## 2. Displaying Data while Editing
Now we want to display records of the departments while edit call, we will make `vDepartmentRecords`. We make seperate view for displaying list of records and editing because there might be some column value differing from list and edit. For example for displaying list you dont have HeadOfDepartment column and in edit mode you want that column to be displayed. 

```
CREATE VIEW [dbo].[vDepartmentRecords]
AS
SELECT        DepartmentId, DepartmentName
FROM            dbo.Departments
GO
```

## 3. Binding data in a dropdown 
There is a grid view of employee on the user interface in you want to bind the values of departments in a dropdown, we will make `vDepartmentLookups` in this case because we only need fields which are required in the lookup.

```
CREATE VIEW [dbo].[vDepartmentLookups]
AS
SELECT        PersonId, FullName
FROM            dbo.Persons
GO
```