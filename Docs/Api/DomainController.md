---
title: DomainController
author: rxcontributorone
category: rxwebcore
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

<table class="table table-bordered">
<tr><th>Method</th><th>Return Type</th><th>Request Params</th><th>Request Body</th><th>Response</th></tr>
<tr><td>GetAsync</td><td>object</td><td> - </td><td> - </td><td>complete list of that entity</td></tr>
<tr><td>GetById</td><td>Entity_Name</td><td>Id of that entity which you want to get</td><td> - </td><td>Single entity based on the id</td></tr>
<tr><td>AddValidation</td><td>string</td><td>entity object</td><td> - </td><td>Added Validation</td></tr>
<tr><td>UpdateValidation</td><td>string</td><td>entity object</td><td> - </td><td>NoContent()</td></tr>
<tr><td>AddAsync</td><td>void</td><td>entity object</td><td> - </td><td>NoContent()</td></tr>
<tr><td>UpdateAsync</td><td>void</td><td>entity object</td><td> - </td><td>NoContent()</td></tr>
<tr><td>DeleteValidation</td><td>void</td><td>entity object</td><td> - </td><td>NoContent()</td></tr>
<tr><td>DeleteAsync</td><td>void</td><td>entity object</td><td> - </td><td>NoContent()</td></tr>
</table>

# Example
```
    [ApiController]
    [Route("api/[controller]")]
    public class ProductsController : BaseDomainController<Product>
    {
        public ProductsController(IProductDomain domain):base(domain) {}
    }
```

The refered `IProductDomain` interface will be created  in  `ProductsDomain.cs` in the Domain folder of the project where the business logic code will use methods of `Uow`.

```
    public class ProductDomain : IProductDomain
    {
        public ProductDomain(IMasterUow uow) {
            this.Uow = uow;
        }

        public Task<object> GetAsync(Dictionary<string, object> parameters)
        {
            throw new NotImplementedException();
        }

        public Task<Product> GetBy(Dictionary<string, object> parameters)
        {
            throw new NotImplementedException();
        }
        

        public HashSet<string> AddValidation(Product entity)
        {
            return ValidationMessages;
        }

        public async Task AddAsync(Product entity)
        {
            await Uow.RegisterNewAsync(entity);
            await Uow.CommitAsync();
        }

        public HashSet<string> UpdateValidation(Product entity)
        {
            return ValidationMessages;
        }

        public async Task UpdateAsync(Product entity)
        {
            await Uow.RegisterDirtyAsync(entity);
            await Uow.CommitAsync();
        }

        public HashSet<string> DeleteValidation(Dictionary<string, object> parameters)
        {
            return ValidationMessages;
        }

        public Task DeleteAsync(Dictionary<string, object> parameters)
        {
            throw new NotImplementedException();
        }

        public IMasterUow Uow { get; set; }

        private HashSet<string> ValidationMessages { get; set; } = new HashSet<string>();
    }
```