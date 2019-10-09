---
title: Multi Tenancy
author: rxcontributortwo
category: rxweb core
---

Multitenancy means multiple organization or client can use a single software. `Multi Tenant` application means a software application which serves multiple clients from the same server. Here `tenent` word represent the client. Tenant can be a single client or an organization. Each tenant’s data is isolated and is not accessible to each other. A good example would be Github where each user or organization has their separate work area. Multi-tenancy is used while developing software that runs for different organizations.

# Multiple Database

In this approach, every tenant uses it's own database. Therefore, each client's data can be easily differentiated. Every tenant has their own set of customers. Now, whenever any user login with their credential, the most important step is to identify from which tenant the request is made.

Before the applicaton can be used by our clients, there must be a way to generate a `tenantId` that identifies the tenant for the application. Here, tenantId is generated based on the `hostUri`.
 Whenever any user will login with their credential, that tenantId will be generated and on the basis of that application will get the connection string of database of that particular tenant.

```js
    
```

While authorizing the user's action ( i.e. can view or update the record), the user's tenant must be taken care by the application. Based on that, user must be assigned their respective role and the respective role permission. 

# Identification of tenants in same database

Another approach for multi-tenancy is `Shared Database` between all the tenants, that means we keep all the tenant's data in a single database. In that case operational cost reduces as it is in the same database and do not depend on the number of clients. Maintainability becomes quite easier as in this approach isolating data is the main case study we need to think about. 

In this situation, each tenant's data is in the same tables. To isolate tenant's data we can add a discriminator column (for example: you can take `ClientId`) to respective table.

Let's consider a case study for shopping application where we have two tables in the same database which is `Clients` and `Customers`. 

Here is a sample Clients table

| ClientId | ClientName |
| ----------- | ----------- |
| 1 | IBM |
| 2 | Oracle |

Here is a sample Customers table.

| CustomerId | ClientId | CustomerName |
| ----------- | ----------- | ----------- |
| 1 | 1 | John |
| 2 | 1 | Maria |
| 3 | 2 | Tony |
| 4 | 2 | Steve |

For example: If you track `Customers` table for example, every tenant's order would be located in "dbo.Customers". Here, tenant's data is separated by a `ClientId`, that shows the main tenant of the entry. 

For using this approach, you need to set `SingleTenantColumn: "ClientId"` in the config.json and add `[TenantFilterQuery]` annotation for the Clients and Customers model. 

```js
    "SingleTenantColumn": "ClientId"
```

While login, applications will check the credentials and return ClientId. With the help of `GetTenantId` in the `BaseContext`, it will identify that customer belongs which client or tenant.

For example: If I consider Client 1

```js
    new Claim(ClaimTypes.NameIdentifier, (1).ToString()),
    new Claim(CustomClaims.SingleTenantValue,"1")
```

Here, `"1"` is the ClientId, so it will give the data of Cutomer1 or Customer2 based on the credentials.
