---
title: SearchController
author: rxcontributorone
category: rxwebcore core
---

Displaying list of the data tuples in the user interface requires a `search` operation when there is large number of records retrieved.
This involves faster search result fetching from the server which is a part defining the application efficiency, This can be achieved by
making a search controller, prior to it there must be a stored procedure which returns `json` and passes to the client side without involving of the web server.

The controller will have a predefined route which include the controller name. For example: `[Route("api/ProductsSearchController")]` 

> Name of that basic controller must have a suffix "Controller". For example: `ProductsSearchController`.

# Generate a Search Controller

To create a lookup controller, open the `Package Manager Console` and run the following command.

>  rxwebcore --controller --search --main <Controller_Name> --uow <Module_Name>

Lets consider a scenario where you want to create a `ProductsSearchController` in the `OrdersModule`, you have to write:

> rxwebcore --controller --search --main ProductsSearch --uow Order

`ProductsSearch` is the controller name and `Orders` is the module name. It will create a controller `ProductsSearchController` in search folder of api in the project

# Methods

| Method | Return Type | Request Params | Request Body | Response|
| ----------- | ----------- | ----------- | ----------- | ----------- | 
| Post |IActionResult | - | searchParams | search result |


# Example
In this example  `MainSqlDbContext` is the context of `OrdersModule` which contains the `spSearchProducts`
which is executing while fetching the search result which are retrieved by passing searchParams as dictionary object in the post method.

```js
    [ApiController]
	[Route("api/[controller]")]
    public class ProductsSearchController : ControllerBase
    {
        private IDbContextManager<MainSqlDbContext> DbContextManager { get; set; }
        public ProductsSearchController(IDbContextManager<MainSqlDbContext> dbContextManager) {
            DbContextManager = dbContextManager;
        }

        [HttpPost]
        public async Task<IActionResult> Post([FromBody]Dictionary<string,string> searchParams)
        {
            var spParameters = new object[2];
            spParameters[0] = new SqlParameter() { ParameterName = "Query", Value = searchParams["query"] };
            spParameters[1] = new SqlParameter() { ParameterName = "UserId", Value = UserClaim.UserId };
            var result = await DbContextManager.SqlQueryAsync<StoreProcResult>("EXEC [dbo].spSearchProducts @Query, @UserId", spParameters);
            return Ok(result.SingleOrDefault()?.Result);
        }
    }
 ```   