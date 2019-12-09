---
title: Generating Data Models
author: rxcontributorone
category: working-with-data-model  
---

# Generate POCO Model

`POCO` means `Plain Old CLR Object`. POCO Entity is a class that doesn't depend on any framework-specific base class. These models act as a data carriers and has validation and any other business logic you want to implement. 

> POCO model must be publically accessible.

Database entities which can be generated as POCO models are:

<ul>
    <li>Tables</li>
    <li>Views</li>
    <li>Record View</li>
    <li>Lookup View</li>
</ul>

 you can create POCO models for all the required tables and views. For creating their POCO models in the application, open the `Package Manager Console` and run the following command:

```js
rxwebcore --models --main
```

This will generate POCO models for all the tables and views in the `DbEntities` folder inside the `Models` section of the project.

## Example

Here is an example of the generated model:

```
    public partial class Document
    {
        [NotMapped]
        public string FileName { get; set; }
        [NotMapped]
        public string FileExtention { get; set; }
        [NotMapped]
        public string FileData { get; set; }
        [NotMapped]
        public string FileType { get; set; }
    }
```