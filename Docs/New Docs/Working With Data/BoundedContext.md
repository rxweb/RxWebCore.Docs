---
title: Bounded Context
author: rxcontributorone
category: newrxwebcore  
---

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

Now lets create Resource Management, Candidate Module and User Modules. we will start with Resource Management Module and add Database models into it.

**Step 1 : Create Bounded Context**

```js
rxwebcore --context --main User
```

This will create `UserContext.cs` in the main folder of DbContext folder in the `HRManagementSystem.BoundedContext` project of the application. 

**Step 2 : Add models into it**

To add models into the context, run this command in the package manager console

```js
rxwebcore --context --main <Context_Name> --add-models <Model_Name>
```

We will add models(DbSets) into the Resource Management Context.

```js
rxwebcore --context --main User --add-models Countries
```

This will add Tables and views of the entity mentioned in the command as a DbSet and the Context will be as follows: 

***UserContext.cs:*** 
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

Now the second module, ResourceManagement

```js
rxwebcore --context --main ResourceManagement --add-models Employees,Activities
```

This will create `ResourceManagementContext.cs` at the same location of the ResourceManagement Context with added models into it.

***ResourceMangementContext.cs:*** 
```js
 public class ResourceManagementContext : BaseBoundedDbContext, IResourceManagementContext
    {
        public ResourceManagementContext(MainSqlDbContext sqlDbContext,  IOptions<DatabaseConfig> databaseConfig, IHttpContextAccessor contextAccessor,TenantDbConnectionInfo tenantDbConnection): base(sqlDbContext, databaseConfig.Value, contextAccessor,tenantDbConnection){ }

        #region DbSets
        public DbSet<vEmployeeRecord> vEmployeeRecords { get; set; }
        public DbSet<vEmployee> vEmployees { get; set; }
        public DbSet<Employee> Employees { get; set; }
        public DbSet<vActivityRecord> vActivityRecords { get; set; }
        public DbSet<vActivity> vActivities { get; set; }
        public DbSet<Activity> Activities { get; set; }
        #endregion DbSets
    }

    public interface IResourceManagementContext : IDbContext
    {
    }
```    

Now the third module Candidate Module

```js
rxwebcore --context --main Candidate --add-models Candidates,Interviews
```

This will create `CandidateContext.cs` at the same location of the ResourceManagement Context with added models into it.

***CandidateContext.cs:*** 
```js
 public class CandidateContext : BaseBoundedDbContext, IResourceManagementContext
    {
        public CandidateContext(MainSqlDbContext sqlDbContext,  IOptions<DatabaseConfig> databaseConfig, IHttpContextAccessor contextAccessor,TenantDbConnectionInfo tenantDbConnection): base(sqlDbContext, databaseConfig.Value, contextAccessor,tenantDbConnection){ }

        #region DbSets
        public DbSet<vInterviewRecord> vInterviewRecords { get; set; }
        public DbSet<vInterview> vInterviews { get; set; }
        public DbSet<Interview> Interviews { get; set; }
        public DbSet<vCandidateRecord> vCandidateRecords { get; set; }
        public DbSet<vCandidate> vCandidates { get; set; }
        public DbSet<Candidate> Candidates { get; set; }
        #endregion DbSets
    }

    public interface ICandidateContext : IDbContext
    {
    }
```    

With the creation of BoundedContext, its UnitOfWork will be generated which will be further used in the API to interact with the data. To get further information about UnitOfWork Please refer this link.