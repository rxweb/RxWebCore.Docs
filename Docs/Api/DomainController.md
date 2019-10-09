---
title: DomainController
author: rxcontributorone
category: rxwebcore core
---

Some entities may involve complex logic while implementation of the methods in the API, When there is a lot of custom business logic required while executing the data objects a `DomainController` is made. When a domain controller is made it indicates that the complexity of the controller is high and it generates a seperate domain class where the logic is written and  it is refered in the controller class.

The controller must be inherited from the class `BaseDomainController` in which the entity name is passed as a parameter. The controller will have a predefined route which include the controller name. For example: `[Route("api/Products")]` 

> Name of that basic controller must have a suffix "Controller". For example: `ProductsController`.

# Generate a Domain Controller

To create a domain controller, open the `Package Manager Console` and run the following command.

> rxwebcore --controller --domain --main <Controller_Name> --uow <Module_Name>

Lets consider a scenario where you want to create a `ProductsController` with high complexity true in the `OrdersModule`, you have to write:

> rxwebcore --controller --domain --main Products --uow Orders

In the above command by writing --domain indicates its complexity high, Products is the controller name and Orders is the Module name. It will create a controller `ProductsController` in `OrdersModule` in Api folder of the project and `ProductsDomain.cs` in the Domain folder of the project.

# Methods   
| Method | Return Type | Request Params | Request Body | Response|
| ----------- | ----------- | ----------- | ----------- | ----------- | 
| GetAsync | object | - | - | complete list of that entity |
| GetById | Entity_Name | Id of that entity which you want to get | - | Single entity based on the id |
| AddValidation | string | - | entity object |-| Added Validation |
| UpdateValidation | string | entity object | - | NoContent() |
| AddAsync | void | entity object | - | NoContent() |
| UpdateAsync | void | entity object | - | NoContent() |
| DeleteValidation | void | entity object | - | NoContent() |
| DeleteAsync | void | entity object | - | NoContent() |

# Example
```js
    [ApiController]
    [Route("api/[controller]")]
	public class ProductsController : BaseDomainController<Product>
    {
        public ProductsController(IProductDomain domain):base(domain) {}
    }
```

The refered `IProductDomain` interface will be created  in  `ProductsDomain.cs` in the Domain folder of the project where the business logic code will use methods of `Uow`.

```js
  *** Example Domain File ***
```