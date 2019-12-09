---
title: rxweb core commands
author: rxcontributorone
category: rxwebcore 
---

# rxwebcore command line interface(CLI) commands:
rxwebcore commands are used for several operation in a .NET Core such as creating project, scaffolding unit of work, contexts, APIs and adding models.

## Installation :
To use rxwebcore commands using package manager console, you must install `rxwebcore` globally using this command:

> dotnet install tool -g rxwebcore

## Commands : 

### Project Creation

To create a new project using rxwebcore CLI. Run this command 

> rxwebcore --add-project <Project_Name>

For more information on creating a project. Please refer []

### Generating Models

> rxwebcore --models --<ConnectionString_Name> 

This command will generate POCO model classes having database objects as properties. In this command --models denote generation of models, --<ConnectionStringName> is the name of the connection which is configured in `appsettings.json` as mentioned below. 

```js
"Database": {
      "ConnectionString": {
      "Main": Your main Db connection string,
	   "Log": Your log Db connection string,
    },
}
```

### Generating Context

> rxwebcore --context --main <Context_Name>

This command generates a bounded context where --context denotes making of a context, --main is the key of the connectionstring which is configured in the `appsetting.json` in connectionstring of the database configuration and mention the Context name based upon the module.

Eg : rxwebcore --context --main Client

### Adding Single Model
   
> rxwebcore --context --main <Context_Name> --add-models <Model_Name> 

This command adds a single DbSet of the model name which is specified as model name(Including tables and views)  which is same as the name of Table.

Eg : rxwebcore --context --main Client  --add-models Candidates

### Adding Multiple Tables In Context

> rxwebcore --context --main <Context_Name> --add-models <Model_Name1>, <Model_Name2>

This command adds a Multiple DbSets of the model name which is specified as model name which is same as the name of Table.

Eg : rxwebcore --context --main Client --add-models Candidates, Clients, Employees

### Generating Controllers
These are the types of controller which are generated based upon the entity type and the operations to be performed.

### Basic Controller

> rxwebcore --controller --basic --main <Controller_Name> --uow <Module_Name> 
This command creates a basic controller which is used while performing simple data CRUD operations

Eg : rxwebcore --controller --basic --main Candidates --uow Master
 
### Domain Controller

> rxwebcore --controller --domain --main <Controller_Name> --uow <Module_Name>
This command creates a domain controller which is used while performing complex data operations which requires some business logic 

Eg : rxwebcore --controller --domain --main UserRoles --uow Master 

### Lookup Controller

> rxwebcore --controller --lookup --main <Controller_Name> --uow <Module_Name>
This command creates a controller for binding data in dropdown   

Eg : rxwebcore --controller --lookup --main MasterLookUps --uow MasterLookUp 

### Add lookups in lookup controller 
Adding lookups in the controller:

> rxwebcore --controller --lookup --main <Country_Name> --uow <Module_Name> --add-lookups <Lookup>

As per this controller : 

> rxwebcore --controller --lookup --main CountryLookups --uow CountryLookup --add-lookups vCountryLookups
### Child Controller

1) Basic Controller :

> rxwebcore --controller --basic --main <Controller_Name> --uow <Module_Name> --parent Users
This command creates a ###basic### child controller 

Eg : rxwebcore --controller --basic --main UserRoles --uow Master --parent Users

2) Domain Controller :

> rxwebcore --controller --domain --main <Controller_Name> --uow <Module_Name> --parent Users
This command creates a ###domain### child controller 

Eg : rxwebcore --controller --domain --main UserRoles --uow Master --parent Users

### Search Controller 

> rxwebcore --controller --search --main <Controller_Name> --spname <Name_of_storedprocedure>
This command creates a search controller with the following stored procedure. 

Eg : rxwebcore --controller --search --main Persons --spname spPersons

### Add authorization to controller

> rxwebcore --controller --<Controller_Type> --main <Controller_Name> --uow <Module_Name> --access <ApplicationModuleId>

This will add `[access]` annotation above the controller with the rights in respect to the application module.

> rxwebcore --controller --basic --main Candidates --uow Master --access 1

### Adding localization

> rxwebcore --localization --main 

This will add json files of the data of languages that are there in the database tables. For more information refer 

### Devops

> rxwebcore --dev-ops

Information coming soon