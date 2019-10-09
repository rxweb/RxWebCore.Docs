---
title: Search Lookup Controller
author: rxcontributortwo
category: rxwebcore core
---

When you want to perform a search operation in a lookup data( for example: dropdown ), in that case `SearchLookup Controller` is made. In SearchLookup Controller, parameters are passed in `querystring` in the form of `Dictionary<string, string>` object. Lookup type need to be passed to the controller which is.

The controller must be inherited from the class `ControllerBase`. The controller will have a predefined route which include the controller name. For example: `[Route("api/CitySearch")]`

> Name of that searchLookup controller must have a suffix "Controller". For example: `CitySearchController`.

# Generate a SearchLookup Controller

To Create a searchLookup controller, open the `Package Manager Console` and run the following command:

> rxwebcore --controller --search --main <Controller_Name> --uow <Module_Name>

Let's consider a scenario where you want a `CitySearchController` in the `MasterModule`, you have to write:

> rxwebcore --controller --search --main CitySearch --uow Master

In the above command, `search` is the type of controller, `CitySearch` is the name of the controller and `Master` is the name of the module. This command will create a separate folder named as "Master" and add a searchLookup controller named as "CitySearchController" under the Api section of the project. 

# Methods

`BaseController` contain methods used for Data interaction such as Get which helps to get the data from the lookup. These methods are always public methods of the Controller as the controller class methods must be publically accessible to the specific action of the of the Controller. 

There are mainly 6 methods used for the SearchLookup Controller which needs to be there in the BaseController which are as follows: 

| Method | Return Type | Request Params | Request Body | Response|
| ----------- | ----------- | ----------- | ----------- | ----------- | 
| Get | IActionResult | - | - | complete list of that entity |
| GetById | IActionResult | Id of that entity which you want to get | - | Single entity based on the id |
| Post | IActionResult | - | New Entity object which you want to add | Ok() |
| Put | IActionResult | Id of that entity which you want to update | Complete entity object with the specific change which you want to update | NoContent() |
| Patch | IActionResult | Id of that entity which you want to update | entity object only with the specific change which you want to update in the form of `JsonPatchDocument` | NoContent() |
| Delete | IActionResult | Id of that entity which you want to delete | - | NoContent() |

# Complete Example of SearchLookup Controller 

Here is an example of a searchLookup controller.

```js

    [ApiController]
	[Route("api/[controller]")]
    public class CitySearchController : ControllerBase
    {
        private IDbContextManager<MainSqlDbContext> DbContextManager { get; set; }
        public CitySearchController(IDbContextManager<MainSqlDbContext> dbContextManager) {
            DbContextManager = dbContextManager;
        }

		[HttpGet("{lookupType}")]
        public async Task<IActionResult> Get([ModelBinder(typeof(QueryParamsBinder))]Dictionary<string, string> searchParams)
        {
            var spParameters = new object[2];
            spParameters[0] = new SqlParameter() { ParameterName = "Query", Value = JsonConvert.SerializeObject(searchParams) };
            spParameters[1] = new SqlParameter() { ParameterName = "UserId", Value = UserClaim.UserId };
            var result = await DbContextManager.SqlQueryAsync<StoreProcResult>("EXEC spLookups @Query, @UserId", spParameters);
            return Ok(result.SingleOrDefault()?.Result);
        }
    }

```