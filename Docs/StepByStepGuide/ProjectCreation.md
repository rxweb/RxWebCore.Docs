---
title: Project Creation
author: rxcontributortwo
category: rxwebcore
---

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
