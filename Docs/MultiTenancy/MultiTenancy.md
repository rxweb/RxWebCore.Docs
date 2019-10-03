---
title: Multi Tenancy
author: rxcontributortwo
category: rxweb core
---

`Multi Tenancy` is a software architecture in which a single logical instance of a software application server runs on a single server but serves multiple clients. Each client represent a `Tenant`. The tenents can be a representation of a single client or an organization. This multitenant application are known as `Shared Resources`. Applications designed in such manner provides every tenant a dedicated instance with mechanism to provide them overall data privacy. 

> Application Data is shared logically among users but not with other users.

In a multi-tenant application, you must consider users as different tenants where users of same organization belong to a single tenant. 

# Identification of tenants in multiple database

First step that needs to be done is to identify the tenant from where the request is made based on the location. This is a very important aspect for all the tenants also as they will have their own set of users and there is no chance of mixing any user data within the tenants. So, security is one of the major aspect which needs to be taken care of. Each tenant must be allowed full access of only that data which belongs to that particular tenant

**Authentication**. 

Before the applicaton can be used by our clients(i.e. tenants), there must be a way to generate a `tenantId` that identifies the tenant for the application. Whenever any user login with their credential, that tenantId  is generated and on the basis of that application will get the connection string of database of that particular tenant.

```js
    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
        var isTenant = ServerSetting.Get<bool>("multiTenant");
        if (isTenant)
            optionsBuilder.UseSqlServer(AdminSqlDbContext.Database.GetDbConnection());
        else
            optionsBuilder.UseSqlServer(MainSqlDbContext.Database.GetDbConnection());
        base.OnConfiguring(optionsBuilder);
    }
```

Based on that connection string, with the help of `LoginContext` you can finally get the connection of that database.

```js
    public DbConnection GetConnection(string keyName)
    {
        var dbConnectionString = ServerSetting.Get<string>(string.Join(".", new string[] { "dbConnection", keyName.ToLower() }));
        if (!string.IsNullOrEmpty(dbConnectionString))
        {
            SqlDbConnection = new SqlConnection(dbConnectionString);
            return SqlDbConnection;
        }
        else
        {
            var tenantDbConnectionString = string.Format(ConnectionString, UserClaim.DbServer, string.Join(string.Empty, UserClaim.CompanyName, keyName, "Db"), string.Join(UserClaim.CompanyName, "User"), string.Join(UserClaim.CompanyName, ""));
            SqlDbConnection = new SqlConnection(tenantDbConnectionString);
            return SqlDbConnection;
        }
    }
```

**Authorization**

While authorizing the user's action ( i.e. can view or update the record), the user's tenant must be taken care by the application. Based on that, user must be assigned their respective role and the respective role permission. 

# Identification of tenants in same database

Another approach for multi-tenancy is `Shared Database` between all the tenants, that means we keep all the tenant's data in a single database. In that case operational cost reduces as it is in the same database and do not depend on the number of clients. Maintainability becomes quite easier as in this approach isolating data is the main case study we need to think about. 

In this situation, each tenant's data is in the same tables. To isolate tenant's data we can add a discriminator column (for example: you can take `ClientId`) to every table which will be tenant specific and make sure that all the queries or commands will differentiate or filter the data out of it.

Let's consider a case study for shopping application where we have two tables in the same database which is `Clients` and `Customers`. 

Here is a sample Clients table


| ClientId | ClientName |
| ----------- | ----------- |
| 1 | Abc Corp |
| 2 | Xyz Corp |

Here is a sample Customers table.

| CustomerId | ClientId | CustomerName |
| ----------- | ----------- | ----------- |
| 1 | 1 | Customer1 |
| 2 | 1 | Customer2 |
| 3 | 2 | Customer3 |
| 4 | 2 | Customer4 |

