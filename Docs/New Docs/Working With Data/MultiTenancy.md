---
title: MultiTenancy
author: rxcontributorone
category: newrxwebcore  
---

MultiTenancy is used for the purpose of developing software that runs for different group of users. It is important to select the strategy of implementing multitenancy based upon the number of users of strength of the organization.     

As per our application of HRManagementSystem working for multiple manpower companies in which there is a candidate form which should be accessed by different organizations. Let's see how it will be implemented based upon the organization.

# Single Database
This approach means keeping all the tenant's data in a single database, This is maintained by keeping a shared database between all the tenants. This is applicable to organizations and companies having less number of employees where less number of candidates are to be managed.

## Benefits

1. Cost effective
2. Easy Maintainance

There are two tables in the database Client and Candidate. 

Here is the Clients table

<table class="table table-bordered">
<tr><th>ClientId</th><th>ClientName</th></tr>
<tr><td>1</td><td>IBM</td></tr>
<tr><td>2</td><td>Oracle</td></tr>
</table>

Here is the Customers table.

<table class="table table-bordered">
<tr><th>CustomerId</th><th>ClientId</th><th>CustomerName</th></tr>
<tr><td>1</td><td>1</td><td>John</td></tr>
<tr><td>2</td><td>1</td><td>Maria</td></tr>
<tr><td>3</td><td>2</td><td>Tony</td></tr>
<tr><td>4</td><td>2</td><td>Steve</td></tr>
</table>

Coming to the project, the `ClientId` is to be configured in the `appsettings.json` where `TenantColumnName` is the key Name and `ClientId` is the value.

After that you need to run the CLI command to add models which will add the `[TenantFilterQuery]` annotation above the ClientId property. Further we need to generate a JWT web joken based upon the TenantId in the `GetTokenAsync` method of ApplicationTokenProvider.cs which is located in the security folder of `HRManagementSystem.Infrastructure`.

```js
new Claim(CustomClaimTypes.TenantId,1.ToString())
```

Once the token is generated based upon the provided TenantId and the candidates operations will be done based upon the candidate.

# Multiple Database
Multitenancy with multiple databases means keeping seperate database each tenant wise, A seperate database is made for each organization for storing its data. It is useful for organizations having large number of employees.   

## Step 1 : 
Create a database named `HRManagementAdminDb` and create a table named `MultiTenants`

<table class="table table-bordered">
<tr><th>MultiTenantId</th><th>HostUri</th><th>ConnectionName</th><th>ConnectionString</th></tr>
<tr><td>1</td><td>localhost:44395</td><td>Main</td><td>Your connection string</td></tr>
</table>

## Step 2 : 
Run cli command   

```js
rxwebcore --add-feature --multitenant

```

## Step 3 : 
Add the connectionString of admin in `appsettings.json` and remove main ConnectionString from it.

The data operations will be further done according to the connection established based upon the AdminDb configuration. 
