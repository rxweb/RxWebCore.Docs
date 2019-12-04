---
title: Generating Models
author: rxcontributorone
category: rxwebcore  
---

POCO model classes define the properties of the data that is stored in the database. These classes will be used for working with Entity Framework(ORM).   

## Generating POCO Models
For Generating models You need to run the following command : 

```js
rxweb --models --main 
```

In this command, --models is for generating models, --main is the name of the connection which is configured in `appsettings.json`.
This will generate model classes in Main folder of DbEntities folder of `HRManagementSystem.Models`
    
## Validation Models

