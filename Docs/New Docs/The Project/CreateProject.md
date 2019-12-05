---
title: Create Project
author: rxcontributorone
category: newrxwebcore
---

### Create a project
In this section, we will see how a create a new .NET core based web application using `rxwebcore`.

**Step 1:**

You first need to install <a href="https://www.nuget.org/packages/RxWebCore/">`rxwebcore`</a> tool globally using command prompt. 

```js
dotnet tool install --global RxWebCore 
```

**Step 2:**

Execute Create Command 

```js
rxwebcore --add-project <Project_Name>
```

As per our scenario, we need to execute command:

```js
rxwebcore --add-project HRManagementSystem
```

**Step 3:**
provide connection strings of main and log databases 

Open the project solution in visual studio, build it and click on run. 