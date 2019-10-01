---
title: IDbContextManager
author: rxcontributorone
category: rxweb core
---

Uow interacts with data objects to execute various operations with entity framework core, but when stored procedures are used for execution of data operations It is managed with the help of `IDbContextManager`. 

It provides methods which are used for managing transactions in Uow, rollback transaction, commit transaction and executing sql query in stored procedure. 

## Begin Transaction
It is used to begin a transaction in Uow before executing the operations in the stored procedure.

## Commit
It is used to commit changes in the database after execution of the operation when the entity state is modified based upon entity framework core methods and stored procedure both.

## RollbackTransaction
It is used to rollback the transaction before commiting the changes to the database.

## SqlQueryAsync
It is used for executing of sql queries to fetch a result from stored procedure.


