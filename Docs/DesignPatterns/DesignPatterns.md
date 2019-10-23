---
title: DesignPatterns
author: rxcontributorone
category: rxwebcore
---

# Domain Driven Design
It is a design pattern in which the bounded context, unit of work and Api is generated based upon the Domain. Domain Driven Design gives an aligibility to make it serverless or MicroService at any point of time.  

# BoundedContext
The purpose of integrating BoundedContext Design Pattern is to efficiently manage DbSets in seperate Contexts based upon its `Domain`. The advantage of doing this is that you can easily manage Context and access its DbSets based upon the operations you want to perform and the entity you want to interact with. 

# Unit Of Work
Unit of Work provides several methods which are used to perform data operations on the boundedContext with the use of `ICoreUnitOfWork`,`IDbContextManager` and `IRepository` methods.

# Repository Pattern
Repository pattern is preferable for applications having large number of domains for encapsulating the logic applied to data objects. It creates an abstraction layer and domain business logic which will isolate the domain from the data access layer.

# Single Responsibility Principle
Single Responsibilty Principle is related to seperation of concerns which states that object should have only one responsibility and only one reason to change.

# Interface Segregation Principle
Interface Segregation principle provides a centralized interface, When a user wants to perform some set of operations, Interface segregation principle will provide only those which are useful to the user.

# Inversion of control
The dependency inversion principle helps the application to be more testable and easy to maintain as a result. It provides higher level abstraction. 

# Cache Aside
This pattern includes loading data from the cache ensuring that consistency is maintained between the data in the cache and the data storage

# CQRS  

# Index Table
This pattern can improve query performance by allowing applications to more quickly locate the data to retrieve from a data store by creating Indexes over the fields in data stores which are frequently referenced by the queries(https://docs.microsoft.com/en-us/azure/architecture/patterns/index-table)

# Materialized View
This design pattern is used for improving application performance as it generates prepopulated views over the data in one or more data stores when the data is not providing data for required query operation(https://docs.microsoft.com/en-us/azure/architecture/patterns/materialized-view)

# Static Content Hosting
This design pattern provides a cloud based service that can deliver them directly to the client. This can reduce the need for potentially expensive compute instances(https://docs.microsoft.com/en-us/azure/architecture/patterns/static-content-hosting)