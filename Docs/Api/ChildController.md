---
title: Child Controller
author: rxcontributortwo
category: rxwebcore
---

When in case there is any reliancy of a parent controller while performing data operations, child controller is made. Parent and child controller are related to each other by a shared key 

The controller must be inherited from the class `BaseChildController` in which  `Model`, `View` and `RecordView` related to that child entity are passed as a parameter. The controller will have a predefined route which include the parent controller name followed by id and child controller name. For example: `[Route("api/Customer/{CustomerId}/CustomerContact")]`

> Name of that child controller must have a suffix "Controller". For example: `CustomerContactController`.

# Generate a Child Controller

To Create a child controller, open the `Package Manager Console` and run the following command:

> rxwebcore --controller --child --main <Child_Controller_Name> --parent <Parent_Controller_Name> --uow <Module_Name>

Let's consider a scenario where you want a `CustomerContactController` as a child controller and `CustomerController` as the parent Controller in the `OrderModule`, you have to write:

> rxwebcore --controller --child --main CustomerContact --parent Customer --uow Order

In the above command, `child` is the type of controller, `CustomerContact` is the name of the child controller, `Customer` is the name of the parent controller and the last parameter `Order` is the name of the module. This command will create a child controller named as "CustomerContactController" under the Api section of the project inside the same "Order" module folder. 

# Methods

`BaseChildController` is inherited by `ControllerBase` and contain various methods used for Data interaction such as Get, Put, Post, Patch and Delete. These methods are always public methods of the Controller as the child controller class methods must be publically accessible to the specific action of the of the Controller. 

There are mainly 6 methods used for the Child Controller which needs to be there in the BaseChildController which are as follows: 

<table class="table table-bordered">
<tr><th>Method</th><th>Return Type</th><th>Request Params</th><th>Request Body</th><th>Response</th></tr>
<tr><td>Get</td><td>IActionResult</td><td> - </td><td> - </td><td>complete list of that entity which binds the shared key of parent and child entity</td></tr>
<tr><td>GetById</td><td>IActionResult</td><td>Id of that entity which you want to get</td><td> - </td><td>Single entity based on the id</td></tr>
<tr><td>Post</td><td>IActionResult</td><td> - </td><td>New Entity object which you want to add</td><td>Ok()</td></tr>
<tr><td>Put</td><td>IActionResult</td><td>Id of that entity which you want to update</td><td>Complete entity object with the specific change which you want to update</td><td>NoContent()</td></tr>
<tr><td>Patch</td><td>IActionResult</td><td>Id of that entity which you want to update</td><td>entity object only with the specific change which you want to update in the form of `JsonPatchDocument`</td><td>NoContent()</td></tr>
<tr><td>Delete</td><td>IActionResult</td><td>Id of that entity which you want to delete</td><td> - </td><td>NoContent()</td></tr>
</table>

# Complete Example of Child Controller

Here is an example of child controller:

```
    
    [ApiController]
    [Route("api/Customer/{CustomerId}/[controller]")]	
	public class CustomerContactController : BaseChildController<CustomerContact,vCustomerContact,vCustomerContactRecord>
    {
        public CustomerContactController(IMasterUow uow):base(uow) {}
    }

```