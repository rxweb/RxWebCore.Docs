---
title: Child Controller
author: rxcontributortwo
category: rxwebcore core
---

While working with entities which are depending on a larger entity. It becomes important to manage the data using a shared key. It is managed using parent and child controller.

The data operations which are to be performed on CandidateAvailabilities entity(Based upon the ResourceContext and ResourceUow created) will be done based upon the record of a particular candidate which will be retrieved from its parent Candidate Controller. 

The controller must be inherited from the class `BaseChildController` in which  `Model`, `View` and `RecordView` related to that child entity are passed as a parameter. The controller will have a predefined route which include the parent controller name followed by id and child controller name. For example: `[Route("api/Candidate/{CandidateId}/CandidateAvailabilities")]`

> Name of that child controller must have a suffix "Controller". For example: `CandidateAvailabilitiesController`.

# Generate a Child Controller

To Create a child controller, open the `Package Manager Console` and run the following command:

> rxwebcore --controller --child --main <Child_Controller_Name> --parent <Parent_Controller_Name> --uow <Module_Name>

Let's consider a scenario where you want a `CandidateAvailabilitiesController` as a child controller and `CandidateController` as the parent Controller in the `ResourceModule`, you have to write:

> rxwebcore --controller --child --main CandidateAvailabilities --parent Candidates --uow Resource

In the above command, `child` is the type of controller, `CandidateAvailabilities` is the name of the child controller, `Candidates` is the name of the parent controller and the last parameter `Resource` is the name of the module. This command will create a child controller named as "CandidateAvailabilitiesController" under the Api section of the project inside the same "Resource" module folder. 

# Methods

`BaseChildController` is inherited by `ControllerBase` and contain various methods used for Data interaction such as Get, Put, Post, Patch and Delete. These methods are always public methods of the Controller as the child controller class methods must be publically accessible to the specific action of the of the Controller. 

There are mainly 6 methods used for the Child Controller which needs to be there in the BaseChildController which are as follows: 

| Method | Return Type | Request Params | Request Body | Response|
| ----------- | ----------- | ----------- | ----------- | ----------- | 
| Get | IActionResult | - | - | complete list of that entity which binds the shared key of parent and child entity |
| GetById | IActionResult | Id of that entity which you want to get | - | Single entity based on the id |
| Post | IActionResult | - | New Entity object which you want to add | Ok() |
| Put | IActionResult | Id of that entity which you want to update | Complete entity object with the specific change which you want to update | NoContent() |
| Patch | IActionResult | Id of that entity which you want to update | entity object only with the specific change which you want to update in the form of `JsonPatchDocument` | NoContent() |
| Delete | IActionResult | Id of that entity which you want to delete | - | NoContent() |

# Complete Example of Child Controller

Here is an example of child controller:

```js
    
    [ApiController]
    [Route("api/Customer/{CustomerId}/[controller]")]	
	public class CustomerContactController : BaseChildController<CustomerContact,vCustomerContact,vCustomerContactRecord>
    {
        public CustomerContactController(IMasterUow uow):base(uow) {}
    }

```