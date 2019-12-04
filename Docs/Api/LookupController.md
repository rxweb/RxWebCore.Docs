---
title: LookupController
author: rxcontributorone
category: api
---

Large modules have entities which need to be bind as a dropdown, In such cases a lookup controller is made for the module which accesses Uow to manipulate data based upon the entity and display the data of module entities in a dropdown.  

The controller must be inherited from the class `BaseLookupController`. The controller will have a predefined route which include the controller name. For example: `[Route("api/OrderLookupsController")]` 

# Generate a Lookup Controller

To create a lookup controller, open the `Package Manager Console` and run the following command.

> rxwebcore --controller --lookup --main <Controller_Name> --uow <Module_Name>

Lets consider a scenario where you want to create a `OrderLookupsController` in the `OrdersModule`, you have to write:

> rxwebcore --controller --lookup --main OrderLookup --uow Order

`OrderLookups` is the controller name and `Orders` is the module name. It will create a controller `OrderLookupsController` in lookup folder of api in the project

# Methods

<table class="table table-bordered">
<tr><th>Method</th><th>Return Type</th><th>Request Params</th><th>Request Body</th><th>Response</th></tr>
<tr><td>AllAsync</td><td>list</td><td> - </td><td> - </td><td>complete list of that entity</td></tr>
<tr><td>OrderBy</td><td>list</td><td>predicate</td><td> - </td><td>list</td></tr>
<tr><td>Where</td><td>list</td><td>predicate</td><td> - </td><td>list</td></tr>
</table>

| Method | Return Type | Request Params | Request Body | Response|
| ----------- | ----------- | ----------- | ----------- | ----------- | 
| AllAsync | complete list of that entity | - | - | complete list of that entity |
| OrderBy | list | predicate | - | list |
| Where | list | predicate | - | list |

# Example

```js
    [ApiController]
    [Route("api/[controller]")]
	
	public class OrderLookUpsController : BaseLookupController
    {
        public OrderLookUpsController(IOrderLookUpUow uow):base(uow) {}

        #region Lookups
        		[HttpGet("Countries")]
		public IQueryable<vCountry> GetCountries()
		{
			return Uow.Repository<vCountry>().Queryable();
		}
            #endregion Lookups

    }

```