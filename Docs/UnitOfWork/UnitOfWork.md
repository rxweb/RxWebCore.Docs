---
title: UnitOfWork
author: rxcontributorone
category: rxwebcore
---

For applications having multiple number of domains, it is preferable to follow repository pattern for encapsulating the logic applied to data objects. Unit of work creates an abstraction layer for communication with data access layer and domain business logic, The purpose of doing this is to isolate the domain from the data access layer logic. 

Let's consider a scenario where you have a `applicant` module and you want to perform data operations of applicants. First you need to create `ApplicantContext` in package manager console which will create Uow `ApplicantUow` as below

```
  public class ApplicantUow : CoreUnitOfWork, IApplicantUow
    {
        public ApplicantUow(IApplicantContext applicantContext, IRepositoryProvider repositoryProvider)
        {
            base.SetContextRepository(applicantContext, repositoryProvider);
        }
    }

    public interface IApplicantUow : ICoreUnitOfWork
    {
    }
```

As per the below code, the domain will have a reference of the `IApplicantUow` which is the object refrence to the repository interface. The benefit of doing this is that it will execute operations without revealing the details behind it which will create single dependency of the domain and data objects which leads to easy automated unit testing or [TDD](https://en.wikipedia.org/wiki/Test-driven_development).

rxwebcore Uow works provides methods that are used for performing data operations that are :

# RegisterNewAsync
When you want to `add` applicant it is done using RegisterNewAsync method. It will change state of the object and after `commit` method is executed it will add the object to database. 

```
    public Applicant Add(Applicant applicant)
    {
        ApplicantUow.RegisterNewAsync<Applicant>(applicant);
        ApplicantUow.Commit();
        return applicant;
    }
```

# RegisterDirty
When you want to `update` applicant it is done using RegisterDirty method. It will change state of the object and after `commit` method is executed it will update the object to database. 

```
    public Applicant Update(Applicant applicant)
    {
        ApplicantUow.RegisterDirty<Applicant>(applicant);
        ApplicantUow.Commit();
        return applicant;
    }
```

# RegisterDeleted
When you want to `delete` applicant it is done using RegisterDeleted method. It will change state of the object and after `commit` method is executed it will update the object to database.

```
    public void Delete(int id)
    {
        var applicant = ApplicantUow.Repository<Applicant>().FindByKey(id);
        ApplicantUow.RegisterDeleted<Applicant>(applicant);
        ApplicantUow.Commit();
    }
```

# RegisterClean
RegisterClean method is used to clean the object instance value of the entity before `commit` method is called. If you want want the particular entity object to be added 

```     
    ApplicantUow.RegisterClean<Applicant>(applicant);       
```

# commit
commit method is used while adding, updating and deleting data to commit changes in the database after operation is executed.

```
    ApplicantUow.Commit();
```
# refresh
refresh method is used to clear all the instance value of the Uow.

```
    ApplicantUow.refresh();
```

# Repository   
Repository class provides several methods which follows linq pattern used for retrieving data based upon condition to retrieve required resultset.

## All
It is used when you want to retreive all the records of the entity.

```
	public IEnumerable<Applicant> Get() 
	{
		return ApplicantUow.Repository<Applicant>().All();
    }
```


## AllAsync
It is used when you want to retreive all the records of the entity asynchronously.

```
    public async Task<IEnumerable<Applicant>> AllAsync()
    {
        return await ApplicantUow.Repository<Applicant>().AllAsync();
    }
```

## AllInclude
It is used when you want include some reference entity in the result set. 

```
    public IEnumerable<Applicant> AllInclude()
    {
        return ApplicantUow.Repository<Applicant>().AllInclude(t => t.CompanyMaster);
    }
```

## AllIncludeAsync
It is used when you want include some reference entity in the result set asynchronously. 

```
    public async Task<IEnumerable<Applicant>> AllIncludeAsync()
    {
        return await ApplicantUow.Repository<Applicant>().AllInclude(t => t.CompanyMaster);
    }
```

## Count
It is used to get count of data in the list of entity based upon condition.

```
    public int Count()
    {
        var count = ApplicantUow.Repository<Applicant>().Count(a => a.LastName == "Christian");
        return count;
    }
```

## FindBy
It is used to find the element based upon condition.

```
    public IEnumerable<Applicant> FindBy()
    {
        return ApplicantUow.Repository<Applicant>().FindBy(t => t.LastName == "Christian"); ;
    }
```    
## FindByAsync
It is used to find the element based upon condition asynchronously.

```
    public async Task<IEnumerable<Applicant>> FindByAsync()
    {
        return await ApplicantUow.Repository<Applicant>().FindByAsync(t => t.LastName == "Doe");
    }
```


## FindByInclude
It is used to find the element based upon condition and include some reference entity into the resultset.

```
    public IEnumerable<Applicant> FindByInclude()
    {
        return ApplicantUow.Repository<Applicant>().FindByInclude(t => t.LastName == "Doe", t => t.CompanyMaster);
    }
```

## FindByIncludeAsync
It is used to find the element based upon condition and include some reference entity into the resultset asynchronously.

```
    public async Task<IEnumerable<Applicant>> FindByIncludeAsync()
    {
        return await ApplicantUow.Repository<Applicant>().FindByIncludeAsync(t => t.LastName == "Doe", t => t.CompanyMaster);
    }
```

## FindByKey
It is used to find element based upon the key.

```
    public Applicant FindByKey()
    {
        return ApplicantUow.Repository<Applicant>().FindByKey(2);
    }
```

## FindByKeyAsync
It is used to find element based upon the key asynchronously.

```
    public async Task<Applicant> FindByKeyAsync()
    {
        return await ApplicantUow.Repository<Applicant>().FindByKeyAsync(2);
    }
```

## First
It retrieves the first element in the list which fulfiles the given condition.

```
    public Applicant First()
    {
        return ApplicantUow.Repository<Applicant>().First(a => a.LastName == "Doe");
    }
```

## FirstAsync
It retrieves the first element in the list which fulfiles the given condition asynchronously.

```
    public async Task<Applicant> FirstAsync()
    {
        return await ApplicantUow.Repository<Applicant>().FirstAsync(a => a.LastName == "Doe");
    }
```

## FirstOrDefault
It retrieves the first element in the list which fulfiles the given condition if not then returns the default value as resultset .

```
    public Applicant FirstOrDefault()
    {
        return ApplicantUow.Repository<Applicant>().FirstOrDefault(a => a.LastName == "Doe");
    }
```
## FirstOrDefaultAsync
It retrieves the first element in the list which fulfiles the given condition if not then returns the default value as resultset asynchronously.

```
    public async Task<Applicant> FirstOrDefaultAsync()
    {
        return await ApplicantUow.Repository<Applicant>().FirstOrDefaultAsync(a => a.LastName == "Doe");
    }
```

## Last
It retrieves the last element in the list which fulfiles the given condition.

```
    public Applicant Last()
    {
        return ApplicantUow.Repository<Applicant>().Last(a => a.LastName == "Christian");
    }
```

## LastAsync
It retrieves the last element in the list which fulfiles the given condition asynchronously.

```
    public async Task<Applicant> LastAsync()
    {
        return await ApplicantUow.Repository<Applicant>().LastAsync(a => a.LastName == "Christian");
    }
```

## LastOrDefault
It retrieves the last element in the list which fulfiles the given condition if not then returns the default value as resultset.

```
    public Applicant LastOrDefault()
    {
        return ApplicantUow.Repository<Applicant>().LastOrDefault(a => a.LastName == "Doe");
    }
```

## LastOrDefaultAsync
It retrieves the last element in the list which fulfiles the given condition if not then returns the default value as resultset asynchronously.

```
    public async Task<Applicant> LastOrDefaultAsync()
    {
        return await ApplicantUow.Repository<Applicant>().LastOrDefaultAsync(a => a.LastName == "Doe");
    }
```

## Queryable
It is used to design a raw query to retrieve the required resultset.

```
    public IQueryable<Applicant> Queryable()
    {
        return ApplicantUow.Repository<Applicant>().Queryable().Where(a => a.LastName == "Doe");
    }
```

## Single
It retrieves the single element in the list which fulfiles the given condition.

```
    public Applicant Single()
    {
        return ApplicantUow.Repository<Applicant>().Single(a => a.FirstName == "John");
    }
```

## SingleAsync
It retrieves the single element in the list which fulfiles the given condition asynchronously.

```
    public async Task<Applicant> SingleAsync()
    {
        return await ApplicantUow.Repository<Applicant>().SingleAsync(a => a.FirstName == "John");
    }
```

## SingleOrDefault
It retrieves the single element in the list which fulfiles the given condition if not then returns the default value as resultset.

```
    public Applicant SingleOrDefault()
    {
        return ApplicantUow.Repository<Applicant>().SingleOrDefault(a => a.FirstName == "terrance");
    }
```

## SingleOrDefaultAsync
It retrieves the single element in the list which fulfiles the given condition if not then returns the default value as resultset asynchronously.

```
    public async Task<Applicant> SingleOrDefaultAsync()
    {
        return await ApplicantUow.Repository<Applicant>().SingleOrDefaultAsync(a => a.FirstName == "terrance");
    }
```