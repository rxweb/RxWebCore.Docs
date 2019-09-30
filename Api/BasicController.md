    ---
title: Basic Controller
author: rxcontributortwo
category: rxweb core
---

When you want basic data operations without any complexity and need to modify any of the custom business logic, basic controller is made. It includes methods which are used for simple CRUD operations.

The controller must be inherited from the class `BaseController` in which  `Model`, `View` and `RecordView` related to that entity are passed as a parameter. The controller will have a predefined route which include the controller name. For example: `[Route("api/Customer")]`

> Name of that basic controller must have a suffix "Controller". For example: `CustomerController`.

# Generate a Basic Controller

To Create a basic controller, open the `Package Manager Console` and run the following command:

> rxweb --controller --basic --main <Controller_Name> --uow <Module_Name>

Let's consider a scenario where you want a `CustomerController` in the `OrderModule`, you have to write:

> rxweb --controller --basic --main Customer --uow Order

In the above command, `basic` is the type of controller, `Customer` is the name of the controller and `Order` is the name of the module. This command will create a separate folder named as "Order" and add a basic controller named as "CustomerController" under the Api section of the project. 

# Methods

`BaseController` contain various methods used for Data interaction such as Get, Put, Post, Patch and Delete. These methods are always public methods of the Controller as the controller class methods must be publically accessible to the specific action of the of the Controller. 

There are mainly 6 methods used for the Basic Controller which needs to be there in the BaseController which are as follows: 

| Method | Return Type | Request Params | Request Body | Response|
| ----------- | ----------- | ----------- | ----------- | ----------- | 
| Get | IActionResult | - | - | complete list of that entity |
| GetById | IActionResult | Id of that entity which you want to get | - | Single entity based on the id |
| Post | IActionResult | - | New Entity object which you want to add | Ok() |
| Put | IActionResult | Id of that entity which you want to update | Complete entity object with the specific change which you want to update | NoContent() |
| Patch | IActionResult | Id of that entity which you want to update | entity object only with the specific change which you want to update in the form of `JsonPatchDocument` | NoContent() |
| Delete | IActionResult | Id of that entity which you want to delete | - | NoContent() |

# Complete Example of Basic Controller 

Here is an example of a basic controller.

```js

    [ApiController]
    [Route("api/[controller]")]
	public class CustomerController : BaseController<Customer,vCustomer,vCustomerRecord>
    {
        public CustomerController(IOrderUow uow):base(uow) {}
    }

```