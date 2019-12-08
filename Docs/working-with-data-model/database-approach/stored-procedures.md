---
title: Stored Procedures
author: rxcontributorone
category: working-with-data-model
sub-category: database-approach
---

Stored procedures are prefered to used when large number of data is involved. It leads to high performance, reusability of code and easy maintanability. It takes input parameters for execution and based upon that it provides the output which should be as per the required resulset. It stores the programming statements for a specific task to be performed and needs to be compiled only once. 

## 1. Performing Search operation on entities having large number of records.
Suppose we have a list of employees which have records exceeds 1000 records and the user wants to search employees with multiple search parameters, In this case the stored procedure is best optimum solution. Let create a stored procedure with the name of `spSearchEmployees` which will be used to fetch the record based upon provided search parameters.  

## 2. Creating search lookup for performing search in a dropdown
In some of the cases we have a limitation to bind the whole resultset into the dropdown, to achieve those cases we usually use autocomplete which will bind the data based upon the entered value in the textbox. To achieveing this case we will make `spUserLookups` .     

## 3. Managing complex operations
To handle large number of datasets which can't be managed through the entity framework core. In this case it is preferable to create a stored procedure and perform the Create, Update and delete operations through the stored procedure. 

> A stored procedure is made using `DbContextManager` the transaction is being opened and the changes are commited. For more information about it refer `DbContextManager`.
