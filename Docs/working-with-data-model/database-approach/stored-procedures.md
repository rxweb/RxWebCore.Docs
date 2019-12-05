---
title: Stored Procedures
author: rxcontributorone
category: database-approach
---

# Stored Procedures
Stored procedures are prefered to used when large number of data is involved. It leads to high performance, reusability of code and easy maintanability. It takes input parameters for execution and based upon that it provides the output which should be as per the required resulset. It stores the programming statements for a specific task to be performed and needs to be compiled only once. 

## 1. Performing Search operation on entities having large number of records.
Suppose we have a list of employees which have records exceeds 1000 records and the user wants to search employees. A Stored procedure will be made named `spSearchEmployees` which will be used to fetch the record list to be shown on the user interface.  

## 2. Creating search lookup for performing search in a dropdown
For performing search in the dropdown, we will make `spSearchLookups` for the whole application and manage search operation based upon the entity which can be managed using switch case.     

## 3. Managing complex operations
When there are scenarios where the operation to be performed includes more than one entity and it is not been covered using the UnitOfWork method. A stored procedure is made using `DbContextManager` the transaction is being opened and the changes are commited. For more information about it refer `DbContextManager`.