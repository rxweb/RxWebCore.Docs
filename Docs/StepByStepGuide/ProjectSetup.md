---
title: Project Setup
author: rxcontributortwo
category: stepByStep
---

# Prerequisites

Before creating a new RxWebCore, you need to have:

<ul>
    <li>Visual Studio 2019 with minimum v16.3.4</li>
    <li>.Net Core 3.0 or later SDK</li>
</ul>

# Install rxweb tool

<ol>
    <li>Open Visual Studio > Create a new Project > Blank Solution.</li>
    <li>Enter Project Name ( For example: SampleProject ) and location of your project.</li>
    <li>Select `Create`.</li>
</ol>

This will create a blank solution named as `SampleProject` at your desired location. Now you need to install `rxweb` tool for that solution.

<ol>
    <li>Select `Tools` > NuGet Package Manager > Package Manager Console.</li>
    <li>Run the command : `dotnet install tool -g rxwebcore`</li>
</ol>

This will install rxweb tool in your `project solution`. Now, you can access all commands of rxweb tool.

# Project Creation

Open the `Package Manager Console` and run the following command:

> rxwebcore --add project <Project_Name>

For example if you want to create a project with the name `SampleProject`, then write:

> rxwebcore --add project SampleProject

This will create a create a project of name SampleProject with the following folder structure:

<ul>
    <li>Api
        <ul>
            <li>SampleProject.Api</li>
        </ul>
    </li>
    <li>Core
        <ul>
            <li>SampleProject.Infrastructure</li>
        </ul>
    </li>
    <li>Domain
        <ul>
            <li>SampleProject.BoundedContext</li>
            <li>SampleProject.Domain</li>
            <li>SampleProject.UnitOfWork</li>
        </ul>
    </li>
    <li>Models
        <ul>
            <li>SampleProject.Models</li>
        </ul>
    </li>
</ul>

# Configuration

After the project is created, you need to initially set connection string in `appsettings.json`. 

> If you haven't created any database, you can create a blank database for now and set its connection string here.

```js
    "ConnectionString" : {
        "<Database_Name>": "<Connection_String>"
    }
```
 
For example: If you want to set connection string of `SampleDb` for SampleProject, then you will write:

```js
    "ConnectionString" : {
        "SampleDb": "data source=yourServerAddress;initial catalog=SampleDb;persist security info=True;User Id=yourUsername;Password=yourPassword;Integrated Security=true;MultipleActiveResultSets=True;App=EntityFramework;"
    }
```

# Database Generation

For generating an effective database, you need to have proper case study of current and future implementation of functionality in large scale projects. Proper decision making is required while creating database. Based on that create a proper database with all the necessary tables, views stored procedures etc. For the detailed information, please refer `database` section.

# Model Generation

For model generation, you must have `config.json` file in `rxweb-tool` folder which consist all the folder paths and connection string path and other required configurations. For generating config.json file, you need to run the following command in Package Manager Console:

> **rxwebcore --init**

If you have properly analyzed and created all the required tables and views, you can create POCO (Plain Old CLR Object) models for all the required tables and views. 

> POCO model is a class that doesn't depend on any framework-specific base class. 

For generating their models in the application, open the `Package Manager Console` and run the following command:

> **rxwebcore --models --main**

This will generate models for all the tables and views in the `Models` folder inside the `Models` section of the project.

# Project Definition

## Api

`Api` project is a `.Net Core 3` based Web API which has a target framework of `.Net Framework 4.6.1`. It includes controllers, views and other configuration files related to your project.

## Domain

`Domain` is a `Class Library` which has a target framework of `.Net Framework 4.6.1`. It consist of your complex business logic based on your project modules.

## Bounded Context

`Bounded Context` is a `Class Library` which has a target framework of `.Net Framework 4.6.1`. It consist of some default context files as well as your custom bounded context files for the project's main modules.

## UOW

`UnitOfWork` is a `Class Library` which has a target framework of `.Net Framework 4.6.1`. It consists of some default uow as well as your custom uow files which sets the context repositories for the respective context files.

## Infrastructure

`Infrastructure` is a `Class Library` which has a target framework of `.Net Framework 4.6.1`. It includes all the default and custom filters required in your project as well as other authorization, cryptography and other security token provider files used in the project.

## Models

`Models` folder is also a class library based on same target framework of `.Net Framework 4.6.1`. It consists various subfolders like `DbEntities`, `Models` and `ViewModels`. 

<ul>
    <li>DbEntities folder contains the database table models</li>
    <li>Models folder contains the custom models which are not present in the database table models but is required as per the project.</li>
    <li>ViewModels folder contains all the `views` which you made in your database(including lookup view and record view)</li>
</ul>
