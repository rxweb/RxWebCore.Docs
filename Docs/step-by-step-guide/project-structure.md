---
title: Project Structure
author: rxcontributorone
category: step-by-step-guide  
---

# Solution Structure
As RxWeb follows the practices of `Clean Architecture`, Based upon this the project structure is divided into several layers of Models, domain services, Application core and API which adds the practices of seperation of concerns for simplification and maintanable code. 

The project solution contains six projects. They are : 

1. Models
2. BoundedContext 
3. UnitOfWork
4. Infrastructure
5. Domain
6. Api

## Models
It contains DbEntities, ViewModels, enums, constants and extensions.
DbEntities are `POCO Models` which are transformed from the database tables, ViewModels are the custom models which are used to access some properties for performing a specific task, enums are `ApplicationObjects` which are generated based upon its type mentioned in the database.
constants are used for declaring global constants of application. extensions are helper functions used for accessing data used at multiple places.        

## BoundedContext
This project contains BoundedContexts which are made based upon the defined modules. Each context can work independently based upon its 
concept. It has `MainSqlDbContext` which is used to resolve the database connection based upon the configuration of the app setting through the  GetConnection method of `BaseDbContext`. For performing multitenancy and connection resilency `BaseBoundedDbContext` is used. The Bounded context will inherit from `BaseBoundedDbContext` for resolving database configurations.

## Unit Of Work
This project contains `Uow` class for its respective BoundedContext to follow repository pattern which provides methods through which the data can be manipulated. It has `BaseUow` which uses the `IRepositoryProvider` and the `IDbContext` to provide the `CoreUnitOfWork` methods to the particular domain. Each domain contains a folder having Uow classes which are used in the controllers.   

## Infrastructure
This project covers methods of necessary actions and implementation which are used application wide like determining user access and access permission, email and sms provider, authorize token etc  

It contains default generated files which include:

* Proving application token using `ApplicationTokenProvider`.
* Get UserClaim of logged user with `AccessPermissionHandler`.
* Authorizing token using `TokenAuthorizer`.
* Module wise access of a user using `UserAccessConfigInfo`.

## Domain
Domain project contains Domain services which are made whenever `high complexity` APIs are made. This means that whenever a domain controller is made, it will make a domain class  for adding custom `business logic` of the domain which will be generated in the Domain project under its module's folder and its reference will be given in the controller.

## Api
The Api project is the .Net core based web application which is the start of the project. It contains application settings, Controllers, necessery injected services like security, performance etc.

* `app.settings.json` is the json configuration of the application in which database `connection string`, connection resilency configuration, MultiTenant details, security and other details are stored.
* `Controllers` folder contains rest APIs.
  It has `Core` folder having 
  1) `Authentication` Controller : Used for login(Verifying user), token generation.
  2) `Authorize` Controller : Used for get access modules(acess permissions, logout and refresh token)  

* Bootstrap contains implementations of `ConfigurationOptions`, `Performance`, `Security`, `Validations` etc 

