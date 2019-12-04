---
title: DomainController
author: rxcontributorone
category: rxwebcore core
---

Some entities may involve complex logic while implementation of the methods in the API, When there is a lot of custom business logic required while executing the data objects a `DomainController` is made. When a domain controller is made it indicates that the complexity of the controller is high and it generates a seperate domain class where the logic is written and  it is refered in the controller class.

The controller must be inherited from the class `BaseDomainController` in which the entity name is passed as a parameter. The controller will have a predefined route which include the controller name. For example: `[Route("api/Users")]` 

Users Entity requires a custom logic to be added into it. For example it is having complex data entity implementation   

> Name of that basic controller must have a suffix "Controller". For example: `UsersController`.

# Generate a Domain Controller

To create a domain controller, open the `Package Manager Console` and run the following command.

> rxwebcore --controller --domain --main <Controller_Name> --uow <Module_Name>

Lets consider a scenario where you want to create a `UsersController` with high complexity true in the `UsersModule`, you have to write:

> rxwebcore --controller --domain --main Users --uow User

In the above command by writing --domain indicates its complexity high, Users is the controller name and User is the Module name. It will create a controller `UsersController` in `UsersModule` in Api folder of the project and `UsersDomain.cs` in the Domain folder of the project.

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
	public class UsersController : BaseDomainController<Product>
    {
        public UsersController(IProductDomain domain):base(domain) {}
    }
```

The refered `IUserDomain` interface will be created  in  `UsersDomain.cs` in the Domain folder of the project where the business logic code will use methods of `Uow`.

```js
    public class UsersDomain : IUsersDomain
    {
        public UsersDomain(IUserUow uow) {
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