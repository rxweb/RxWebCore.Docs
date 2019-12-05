---
title: IDbContextManager 
author: rxcontributorone
category: rxwebcore
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
Let's consider a scenario where you want to save candidate's a  availability in which you have two tables Candidates and CandidateAvailabilities
Insertion of Candidate can be maintained by `RegisterNewAsync` method of Uow but CandidateAvailabilities can be inserted with the help of stored procedure.

Candidate Table:

<table class="table table-bordered">
  <tr><th>CandidateId</th><th>FirstName</th><th>EmailId</th><th>Designation</th><th>Experience</th></tr>
  <tr><td>1</td><td>John</td><td>johnd@gmail.com</td><td>Software Engineering</td><td>2</td></tr>
  <tr><td>2</td><td>Bharat</td><td>bharatp@gmail.com</td><td>Software Engineering</td><td>2</td></tr>
</table>

CandidateAvailabilities Table:

<table class="table table-bordered">
  <tr><th>CandidateAvailabilityId</th><th>AvailableDate</th><th>FromTime</th><th>ToTime</th><th>CandidateId</th></tr>
  <tr><td>1</td><td>2019-05-01 00:00:00.000</td><td>10:15:00</td><td>10:30:00</td><td>1</td></tr>
  <tr><td>2</td><td>2019-04-01 00:00:00.000</td><td>10:30:00</td><td>10:40:00</td><td>2</td></tr>
</table>

First step is to begin transaction using `BeginTransaction` method in the `CandidateUow`. The `SqlQueryAsync` will execute the stored procedure using the provided params and if the result then `Commit` method is executed which will save the details if not then it will rollback the transaction using  `RollbackTransaction` method.

```
        [HttpPost]
        public async Task<IActionResult> Post([FromBody]CandidateAvailabilities candidateAvailabilities)
        {
            DbContextManager.BeginTransaction(this.CandidateUow);
            CandidateUow.RegisterNewAsync(candidate);
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
            try{
            DbContextManager.Commit();
            }
            catch(Exception e)
            {
            DbContextManager.RollbackTransaction();
            }
            return Ok(result);
        }

```