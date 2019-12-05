---
title: Bounded Context
author: rxcontributorone
category: working-with-data-model  
---

# Overview 

There are some scenarios when you have to deal with too many tables, then it becomes difficult to manage those tables. For such problems `Bounded context design pattern` or `Domain-Driven Design` can be a solution.

`Bounded context design pattern` can help you in maintaining a well structured application. This represents a logical and tangible boundery which will structurize the bigger application in terms of modules and domain. It is the core part of this strategic design pattern of `Domain-Driven approach`. The core concept of this design pattern is mainly focused on the models and structuring them based on the their fundamental context. 

# Scenario
This will be helpful in those cases where we are building a large enterprise application. All features are segregated into the modules. So we take the advantage of bounded context and create the context modules wise based upon the Application needs. This gives us a comfort to add/remove the entity into the specific context without hindering to other modules(in terms of context).

In our HRManagementSystem we have three main modules. They are Resource Management, Candidate Module and User Module. Let's see how to make module wise `BoundedContext` using rxwebcore CLI commands.

In the package manager console, run this command to create a BoundedContext

```js
rxwebcore --context --main <Context_Name>
```

Parameters of creating a context 

<table class="table table-bordered table-striped">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td>--context</td><td>For generating BoundedContext</td></tr>
<tr><td>--main</td><td>key of the database connectionString mentioned in `appsettings.json`</td></tr>
<tr><td><Context_Name></td><td>Name of the context</td></tr>
</table>

# Create Bounded Context

Now lets create Resource Management, Candidate Module and User Modules. we will start with Resource Management Module and add Database models into it.

**Step 1 : Create Bounded Context**

```js
rxwebcore --context --main User
```

This will create `UserContext.cs` in the main folder of DbContext folder in the `HRManagementSystem.BoundedContext` project of the application. 

# Add Database Entities

**Step 2 : Add models into it**

To add models into the context, run this command in the package manager console

```js
rxwebcore --context --main <Context_Name> --add-models <Model_Name>
```

We will add models(DbSets) into the Resource Management Context.

```js
rxwebcore --context --main User --add-models Countries
```
> This will add tables and views of the particular entity in the context.

**UserContext.cs:** 
```js
 public class UserContext : BaseBoundedDbContext, IResourceManagementContext
    {
        public UserContext(MainSqlDbContext sqlDbContext,  IOptions<DatabaseConfig> databaseConfig, IHttpContextAccessor contextAccessor,TenantDbConnectionInfo tenantDbConnection): base(sqlDbContext, databaseConfig.Value, contextAccessor,tenantDbConnection){ }

        #region DbSets
        public DbSet<vCountryRecord> vCountryRecords { get; set; }
        public DbSet<vCountry> vCountry { get; set; }
        public DbSet<Country> Country { get; set; }
        #endregion DbSets
    }

    public interface IUserContext : IDbContext
    {
    }
``` 

With the creation of BoundedContext, its UnitOfWork will be generated which will be further used in the API to interact with the data. To get further information about UnitOfWork Please refer this link.