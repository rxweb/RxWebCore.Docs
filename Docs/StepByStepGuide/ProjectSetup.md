---
title: Project Setup
author: rxcontributortwo
category: rxwebcore
---

# Prerequisites

The prerequisites which are required before creating new project using `rxwebcore` are listed below:

<ul>
    <li>Visual Studio 2019 with minimum v16.3.4</li>
    <li>.Net Core 3.0 or later SDK</li>
</ul>

# Install rxweb tool
The first step towards creating an application is to install the `rxwebcore` tool globally using below command in command prompt.

```js
 `dotnet install tool -g rxwebcore`
```

This will install `rxwebcore` tool globally which will be used for cli commands. 

# Project Creation
`rxwebcore` creates a project solution using cli command 

Let's consider a scenario where you want to create a HumanResourceApplication. For creating an application. If you want to create angular application 

```js
rxwebcore --add-project <Project_Name>
```

For example if you want to create a project with the name `HumanResourceApplication`, then write:

```js
rxwebcore --add-project HumanResourceApplication
```

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

