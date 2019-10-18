---
title: rxweb core commands
author: rxcontributorone
category: rxwebcore core 
---

# rxwebcore command line interface(CLI) commands:
rxwebcore commands are used for several operation in a .NET Core such as creating project, scaffolding unit of work, contexts, APIs and adding models.

## Installation
To use rxwebcore commands using package manager console, you must install `rxwebcore` globally using this command:

> dotnet install tool -g rxwebcore

This command comes with Prerequisites that .NET core 3.0 is installed

## Commands

**Project Creation**

> rxwebcore --add-project <Project_Name>

**Creating rxwebtool**  

> rxwebcore --init

**Generating Models**

> rxwebcore --models --main

**Generating Context**

> rxwebcore --context --main <Context_Name>

**add tables in context**

> rxwebcore --context --main <Context_Name> --add-models <Model_Name>

**add login context**

> rxwebcore --context --main logins

**add login Api**

> rxwebcore --add-api login

**add basic controller**

> rxwebcore --controller --basic --main <Controller_Name> --uow <Module_Name> 

**add domain controller**

> rxwebcore --controller --domain --main <Controller_Name> --uow <Module_Name>

**add lookup controller**

> rxwebcore --controller --lookup --main <Controller_Name> --uow <Module_Name>

**add child controller**

> rxwebcore --controller --child --main <Child_Controller_Name> --parent <Parent_Controller_Name> --uow <Module_Name>

**add search controller**

> rxwebcore --controller --search --main <Controller_Name> --uow <Module_Name>

**add authorization to controller**

> rxwebcore --controller --<Controller_Type> --main <Controller_Name> --uow <Module_Name> --access <ApplicationModuleId>

**To check unauthorized api**

> rxwebcore --security

**To make any module serverless**

> rxwebcore --serverless <Module_Name>