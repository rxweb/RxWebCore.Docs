---
title: Project Structure
author: rxcontributorone
category: rxwebcore  
---

# Solution Structure
As per our clean architecture/Onion architecture, The project structure is divided into several layers of Models, domain services, Application core and API which are done based upon the thought of seperating the concerns for simpification and maintainance of code which is achieved with the help of breaking individual parts of the web application which are User interface, business logic, data access and infrastructure.

The project solution contains six projects. They are : 

1. Models
2. BoundedContext 
3. Domain
4. UnitOfWork
5. Infrastructure
6. Api

## Models
The models projects works as a `data access` layer of the application. It contains DbEntities, ViewModels, enums, constants and extensions.
DbEntities are `POCO Models` which are transformed from the database tables, ViewModels are the custom models which are used to access some properties for performing a specific task, enums are `ApplicationObjects` which are generated based upon its type mentioned in the database.
constants are used for declaring global constants of application. extensions are helper functions used for accessing data used at multiple places.        

## BoundedContext
This project contains BoundedContexts which are made based upon the defined modules. Each context can work independently based upon its 
concept. It has `MainSqlDbContext` which is used to resolve the database connection based upon the configuration of the app setting through the  GetConnection method of `BaseDbContext`. For performing multitenancy and connection resilency `BaseBoundedDbContext` is used. The Bounded context will inherit from `BaseBoundedDbContext` for resolving database configurations.

## Domain
Domain project contains Domain services which are made whenever `high complexity` APIs are made. This means that whenever a domain controller is made, it will make a domain class  for adding custom `business logic` of the domain which will be generated in the Domain project under its module's folder and its reference will be given in the controller.

## Unit Of Work
This project contains `Uow` class for its respective BoundedContext to follow repository pattern which provides methods through which the data can be manipulated. It has `BaseUow` which uses the `IRepositoryProvider` and the `IDbContext` to provide the `CoreUnitOfWork` methods to the particular domain. Each domain contains a folder having Uow classes which are used in the controllers.   

## Infrastructure
This project covers methods of necessary actions and implementation which are used application wide like determining user access and access permission, email and sms provider, authorize token etc  

It provides implementations which include:

* Proving application token using `ApplicationTokenProvider`.
* Get UserClaim of logged user with `AccessPermissionHandler`.
* Authorizing token using `TokenAuthorizer`.
* Module wise access of a user using `UserAccessConfigInfo`.

## Api
The Api project is the .Net core based web application which is the start of the project. It contains application settings, Controllers, necessery injected services like security, performance etc.

* `app.settings.json` is the json configuration of the application in which database `connection string`, connection resilency configuration, MultiTenant details, security and other details are stored.
* `Controllers` folder contains rest APIs.
* Bootstrap contains implementations of `ConfigurationOptions`, `Performance`, `Security`, `Validations` etc 

### Performance and security
Implemeted in `Performance.cs` and `Security.cs` which are configured in `ConfigureServices` method of `startup.cs`.

```js
   services.AddPerformance();
   services.AddSecurity();
```

### Singleton and scoped services
`scoped .cs` include domain services, context, Uow along with Repository provider and token Authorizer. `singleton.cs` includes TenantDbInfo and user access information. They are also configured in ConfigureServices` method of `startup.cs`.

```js
    services.AddSingletonService();
    services.AddScopedService();
```