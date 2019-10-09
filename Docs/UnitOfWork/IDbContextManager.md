---
title: IDbContextManager
author: rxcontributorone
category: rxwebcore core
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

# Scenario
Let's consider a scenario where you want to save candidate's availability in which you have two tables Candidates and CandidateAvailabilities
Insertion of Candidate can be maintained by entity framework but CandidateAvailabilities can be inserted with the help of stored procedure.

Candidate Table:

| CandidateId | FirstName | EmailId | Designation | Experience |  
| ----------- | ----------- | ----------- | ----- | ------- | 
| 1 | John  | johnd@gmail.com | Software Engineering | 2 |
| 2 | Bharat | bharatp@gmail.com | Software Engineering | 2 |

CandidateAvailabilities Table:

| CandidateAvailabilityId | AvailableDate | FromTime | ToTime | CandidateId |
| ----------- | ----------- | ----------- | -------- | ------ | 
| 1 | 2019-05-01 00:00:00.000  | 10:15:00 | 10:30:00 | 1 |
| 2 | 2019-04-01 00:00:00.000 | 10:30:00 | 10:40:00 | 2 |    

First step is to begin transaction using `BeginTransaction` method in the `CandidateUow`. The `SqlQueryAsync` will execute the stored procedure using the provided params and if the result then `Commit` method is executed which will save the details if not then it will rollback the transaction using  `RollbackTransaction` method.

```js
        [HttpPost]
        public async Task<IActionResult> Post([FromBody]CandidateAvailabilities candidateAvailabilities)
        {
            DbContextManager.BeginTransaction(this.CandidateUow);
            var spParameters = new object[4];
            spParameters[0] = new SqlParameter()
            {
              ParameterName = "AvailableDate",
              Value = candidateAvailabilities.AvailableDate
            };
             spParameters[1] = new SqlParameter()
              {
              ParameterName = "FromTime",
              Value = candidateAvailabilities.FromTime
             };
             spParameters[2] = new SqlParameter()
             {
              ParameterName = "ToTime",
              Value = candidateAvailabilities.ToTime
             };
            spParameters[3] = new SqlParameter()
            {
             ParameterName = "CandidateId",
             Value = candidateAvailabilities.CandidateId
            };
            var result = await DbContextManager.SqlQueryAsync<StoreProcResult>("EXEC [dbo].spInsertcandidateAvailabilities @AvailableDate,  @FromTime, @ToTime, @CandidateId", spParameters);
            if(result)
            DbContextManager.Commit();
            else
            DbContextManager.RollbackTransaction();
            return Ok(result);
        }

```



