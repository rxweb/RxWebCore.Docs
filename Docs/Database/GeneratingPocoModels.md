---
title: Generating POCO Models
author: rxcontributortwo
category: rxweb core
---

The core part of any software application is the `database designing`. It is a process of organizing data in a proper structural way. Before working on the business logic part in the application, we must decide what data is to be stored and which elements will be interrelated to each other. With all these information, you can start creating the database and its entities with respect to that application.

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

**Tables**

In a database, `table` is a set of data elements ( or values ) represented in the form of vertical columns and horizontal rows where column represent the model fields or the type of information and total rows represents the total number of data.

> As per the standard naming convention, table Names must be in the plural form.

**Views**

`View` is a type of searchable object and is a type of `virtual table` which can be used to fetch the record from one or more tables using joins. 

> As per the standard naming convention, names of views must be in the format like `v<Table_Name>` like `vCountries`.

For example:

Let's consider a scenario where in the Users table, there is a field named `Status` which will consist an id like `0` for `Inactive` or `1` for `Active`. But that status text (i.e. Active or Inactive) is stored in a different table. In final representation of UI, it should be displayed as Active or Inactive inspite of 1 or 0, then in that case we can create a view to fetch the original value.

**Record View**

There are some scenarios when you want to fetch a single record from the table whenever a user clicks the edit button or view button. For such cases, `RecordView` is created.

> As per the standard naming convention, names of RecordView must be in the format like `v<Table_Name>Record` like `vCountriesRecord`.

**Lookup View**

There are some scenarios when you want to display dropdown based on a table and you want only the id and text which is to be displayed. For such cases, `LookupView` is created. 

> As per the standard naming convention, names of LookupView must be in the format like `v<Table_Name>` like `vCountry`.

If you have properly analyzed and created all the required database entities for a particular module, you can create POCO models for all the required tables and views. For creating their POCO models in the application, open the `Package Manager Console` and run the following command:

> **rxweb --models --main**

This will generate POCO models for all the tables and views in the `DbEntities` folder inside the `Models` section of the project.

# Example

Here is an example of the generated model:

```js
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
