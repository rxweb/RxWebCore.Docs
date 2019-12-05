---
title: UnitOfWork
author: rxcontributorone
category: newrxwebcore  
---

The UnitOfWork pattern is vast and we can use in multiple areas, To know more about the UnitOfWork pattern, Please refer the Martin Fowler Article, This is awesome. 

In our case, This mainly focuses on handling the database operations on data objects. As you know the framework is using the ORM of EntityFramework Core, this also follows the same practice through the DbContext class. Internally we are using the same DbContext object to performing the database opertation To handle the database operations and on top of it this manages some additional things like Entity Audit Logging which keeps a trace of every change that has been made to the entity.

Uow handles the data objects by changing its state based upon the method performed and makes a call to the database when the `commit` method is called which results to faster execution.   

As you have seen in our previouse doc of BoundedCotnext, We have created three BoundedContexts in our project. Along with it, `ResourceMangementUow.cs`, `CandidateUow.cs`, `UserUow.cs` will be created in the main folder of `HRManagementSystem.UnitOfWork`. UnitOfWork uses methods of `CoreUnitOfWork` which is the part of part of [RxWeb.Core.Data](https://www.nuget.org/packages/RxWeb.Core.Data/).

The methods of Uow which are used to change the state of the object are : 

# RegisterNewAsync
When you want to `add` User it is done using RegisterNewAsync method. It will change state of the object and after `commit` method is executed it will add the object to database. 

```js
    public User Add(User user)
    {
        UserUow.RegisterNewAsync(user);
        UserUow.Commit();
        return User;
    }
```

# RegisterDirty
When you want to `update` User it is done using RegisterDirty method. It will change state of the object and after `commit` method is executed it will update the object to database. 

```js
    public User Update(User user)
    {
        UserUow.RegisterDirty<User>(user);
        UserUow.Commit();
        return User;
    }
```

# RegisterDeleted
When you want to `delete` User it is done using RegisterDeleted method. It will change state of the object and after `commit` method is executed it will update the object to database.

```js
    public void Delete(int id)
    {
        var User = UserUow.Repository<User>().FindByKey(id);
        UserUow.RegisterDeleted<User>(user);
        UserUow.Commit();
    }
```

# RegisterClean
RegisterClean method is used to clean the object instance value of the entity before `commit` method is called. If you want want the particular entity object to be added. 

```js     
    UserUow.RegisterClean<User>(user);       
```

# CommitAsync
commit method is used while adding, updating and deleting data to commit changes in the database after operation is executed.

```js
    UserUow.CommitAsync();
```
# refresh
refresh method is used to clear all the instance value of the Uow.

```js
    UserUow.refresh();
```


Here are the Uow classes are generated, when you have created the BoundedContext of the respective module:

***ResourceMangementUow.cs :***

```js
public class ResourceManagementUow : BaseUow, IResourceManagementUow
{
    public ResourceManagementUow(IResourceManagementContext context, IRepositoryProvider repositoryProvider) : base(context, repositoryProvider) { }
}

public interface IResourceManagementUow : ICoreUnitOfWork { }
```

***CandidateUow.cs***

```js
public class CandidateUow : BaseUow, ICandidateUow
{
    public CandidateUow(ICandidateContext context, IRepositoryProvider repositoryProvider) : base(context, repositoryProvider) { }
}

public interface ICandidateUow : ICoreUnitOfWork { }
```

***UserUow.cs***

```js
public class UserUow : BaseUow, IUserUow
{
    public UserUow(IUserContext context, IRepositoryProvider repositoryProvider) : base(context, repositoryProvider) { }
}

public interface IUserUow : ICoreUnitOfWork { }
```