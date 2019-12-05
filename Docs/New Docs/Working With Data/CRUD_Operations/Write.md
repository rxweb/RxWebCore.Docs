---
title: write
author: rxcontributorone
category: newrxwebcore  
---

# Write

## Adding Single Object
`RegisterNewAsync` is used for adding entity. Here is an example of adding a single object of candidate using this method, It will change state of the object and after `commit` method is executed it will add the object to database. 

```js
    public async Task Add(Candidate candidate)
    {
      await Uow.RegisterNewAsync(candidate);
      await Uow.CommitAsync();      
    }
```

## Adding Multiple Objects
Adding Multiple Objects using `RegisterNewAsync`

```js
   public async Task AddAsyncList([FromBody]IEnumerable<Candidate> candidates)
    {
        await Uow.RegisterNewAsync(candidates);
        await Uow.CommitAsync();
    }
```

## Add Objects Using Transaction
Used for adding objects using BeginTransaction, Here the `DbContextManager` is resolved using Dependency injection in the controller.  

```js
    public CandidatesDomain(IResourceUow uow, IDbContextManager<ResourceContext> dbContextManager)
    {
      this.Uow = uow;
      DbContextManager = dbContextManager;
    }
```

The `BeginTransaction` method of DbContextManager will begin the transaction on the Uow that is resolved from the constructor(ResourceUow)
and using `RegisterNewAsync` method will change the state of the Object and the `CommitAsync` method will save the changes in the database.

## Example  
```js
    public async Task AddTransaction(Candidate candidate)
    {
      await DbContextManager.BeginTransactionAsync(this.Uow);
      await Uow.RegisterNewAsync(candidate);
      await DbContextManager.CommitAsync(this.Uow);
    }    
```