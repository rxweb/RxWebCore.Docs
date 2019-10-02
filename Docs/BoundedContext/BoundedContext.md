---
title: Bounded Context
author: rxcontributortwo
category: rxweb core
---

There are some scenarios when you have to deal with too many tables, then it becomes difficult to manage those tables. For such problems `Bounded context design pattern` or `Domain-Driven Design` can be a solution.

`Bounded context design pattern` can help you in maintaining a well structured application. This represents a logical and tangible boundery which will structurize the bigger application in terms of modules and domain. It is the core part of this strategic design pattern of `Domain-Driven approach`. The core concept of this design pattern is mainly focused on the models and structuring them based on the their fundamental context. 

# Scenario

Let's consider a real time case study of `Shopping Application` where we mainly focus on models and their structuring into the domain. Now, using this design pattern we will walk through the main steps starting from deciding the models and analyzing their parent module. 

<ul>
    <li>Step 1: Deciding the primary models for the shopping application and analyze the domain</li>
    <li>Step 2: Creating BoundedContext for the primary domains</li>
    <li>Step 3: Adding reference of the respective models inside the context</li>
</ul>

> **Step 1: Deciding the primary models for the shopping application and analyze the domain**

Consider a shopping application have models like Product, Customer, Purchase, Invoice, Delivery, Category, Supplier, Catalog and Stock. Based on the model's basic fields and work, let us divide then in the moldule:
 
<ul>
    <li>OrderModule => Product, Customer, Purchase, Invoice and Delivery</li>
    <li>InventoryModule => Product, Supplier, Category, Catalog and Stock</li>
</ul>

Now, here the main modules `OrderModule` and `InventoryModule` have their separate work but are interrelated with each other by the Product model.

> **Step 2: Creating BoundedContext for the primary domains**

As we using Bounded context design pattern, we will make separate bounded context for both the modules(i.e. OrderModule and InventoryModule ). To create a context, open the `Package Manager Console` and run the following command:

> rxweb --context --main <Module_Name>

So, for creating `OrderContext` for the OrderModule, we will write

> rxweb --context --main Order

This will create an `OrderContext` in the `BoundedContext` folder in the `Domain` section.

And to create `InventoryContext`  in the `BoundedContext` folder in the `Domain` section, we will write 

> rxweb --context --main Inventory

This command will also `OrderUow` an `InventoryUow` in the `Uow` folder of the `Domain` section. Please refer Uow section for more information.

> **Step 3: Adding reference of the respective models inside the context**

Now, it's time to use model reference inside the bounded context. OrderContext will contain reference of  Product, Customer, Purchase, Invoice and Delivery model and InventoryContext will have a reference of Product, Supplier, Category, Catalog and Stock model. To add model reference in the context, you have to run the following command: 

> rxweb --context --main <Context_Name> --add-models <Table_Name>

You can also add multiple models by writing Comma separted model names. For example, if you want to add reference in OrderContext, you can write:

> rxweb --context --main Order --add-models "Product", "Customer", "Purchase", "Invoice", "Delivery"

If you want to add reference in InventoryContext, you can write:

> rxweb --context --main Inventory --add-models "Product", "Supplier", "Category", "Catalog", "Stock"

This will add reference of the respective tables in their specific context.

# Example

Here is the complete example of the OrderContext we have created:

```js

```