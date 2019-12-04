---
title: LookupController
author: rxcontributorone
category: rxwebcore core
---

Large modules have entities which need to be bind as a dropdown, In such cases a lookup controller is made for the module which accesses Uow to manipulate data based upon the entity and display the data of module entities in a dropdown.  

The controller must be inherited from the class `BaseLookupController`. The controller will have a predefined route which include the controller name. For example: `[Route("api/CountryLookupsController")]` 

# Generate a Lookup Controller

To create a lookup controller, open the `Package Manager Console` and run the following command.

> rxwebcore --controller --lookup --main <Controller_Name> --uow <Module_Name>

Lets consider a scenario where you want to create a `CountryLookupsController` in the `UsersModule`, you have to write:

> rxwebcore --controller --lookup --main CountryLookups --uow User

`CountryLookups` is the controller name and `User` is the module name. It will create a controller `CountryLookupsController` in lookup folder of api in the project

# Methods

| Method | Return Type | Request Params | Request Body | Response|
| ----------- | ----------- | ----------- | ----------- | ----------- | 
| AllAsync | complete list of that entity | - | - | complete list of that entity |
| OrderBy | list | predicate | - | list |
| Where | list | predicate |-| list |

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