---
title: Project Setup
author: rxcontributortwo
category: step-by-step-guide
---

# Prerequisites

The prerequisites which are required before creating new project using `rxwebcore` are listed below:

<ul>
    <li>Visual Studio 2019 with minimum v16.3.4</li>
    <li>.Net Core 3.0 or later SDK</li>
</ul>

# Install rxweb tool
The first step towards creating an application is to install the [`rxwebcore`](https://www.nuget.org/packages/RxWebCore/) tool globally using below command in command prompt.

```js
 `dotnet install tool -g rxwebcore`
```

This will install `rxwebcore` tool globally which will be used for cli commands. 

# Project Creation
`rxwebcore` creates a project solution using cli command and also provides command for scaffolding things.

Let's consider a scenario where you want to create a HumanResourceApplication using the below CLI command. Before firing the below command there must be Database server having two blank databases(main and log). 

```js
rxwebcore --add-project <Project_Name>
```

For example if you want to create a project with the name `HumanResourceApplication`, then write:

```js
rxwebcore --add-project HumanResourceApplication
```

By running this command. It will ask for :

1. Would you like to create a angular project for your UI development : If you want to create write Y or N
2. Enter your main database connection string : Database connection string of main database for default application tables.
3. Enter your log database connection string : Database connection string of log database for logging(expection logging, data entity logging, requests logging)

This will create a create a project of name HumanResourceApplication with the following folder structure:

<ul>
    <li>Api
        <ul>
            <li>HumanResourceApplication.Api</li>
        </ul>
    </li>
    <li>Core
        <ul>
            <li>HumanResourceApplication.Infrastructure</li>
        </ul>
    </li>
    <li>Domain
        <ul>
            <li>HumanResourceApplication.BoundedContext</li>
            <li>HumanResourceApplication.Domain</li>
            <li>HumanResourceApplication.UnitOfWork</li>
        </ul>
    </li>
    <li>Models
        <ul>
            <li>HumanResourceApplication.Models</li>
        </ul>
    </li>
</ul>

