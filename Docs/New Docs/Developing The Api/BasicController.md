---
title: Basic Controller
author: rxcontributortwo
category: rxwebcore core
---

When you want basic data operations without any complexity and need to modify any of the custom business logic, basic controller is made. It includes methods which are used for simple CRUD operations.

The controller will be inherited from the class `BaseController` in which  `Model`, `View` and `RecordView` related to that entity are passed as a parameter. The controller will have a predefined route which include the controller name. For example: `[Route("api/Candidates")]`

The Candidate entity requires the basic data operations(Based upon the ResourceContext and ResourceUow created) to be done without addition of any custom business logic to be added. So we will generate a basic controller for the Candidate Entity of the ResourceModule.

> Name of that basic controller must have a suffix "Controller". For example: `CandidatesController`.

# Generate a Basic Controller

To Create a basic controller, open the `Package Manager Console` and run the following command:

> rxwebcore --controller --basic --main <Controller_Name> --uow <Module_Name>

Let's consider a scenario where you want a `CandidatesController` in the `ResourceModule`, you have to write:

> rxwebcore --controller --basic --main Candidates --uow Resource

In the above command, `basic` is the type of controller, `Candidates` is the name of the controller and `Candidate` is the name of the module. This command will create a separate folder named as "ResourceModule" and add a basic controller named as "CandidatesController" under the Api section of the project. 

# Methods

`BaseController` contain various methods used for Data interaction such as Get, Put, Post, Patch and Delete which will use the methods of Uow to interact with data. These methods are always public methods of the Controller as the controller class methods must be publically accessible to the specific action of the of the Controller. 

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
	public class CandidatesController : BaseController<Candidate,vCandidate,vCandidateRecord>
    {
        public CandidatesController(ICandidateUow uow):base(uow) {}
    }

```