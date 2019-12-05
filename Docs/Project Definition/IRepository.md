---
title: IRepository 
author: rxcontributorone
category: rxwebcore
---

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
It is used when you want include data of the reference entity in the result set. 

```
    public IEnumerable<Applicant> AllInclude()
    {
        return ApplicantUow.Repository<Applicant>().AllInclude(t => t.CompanyMaster);
    }
```

## AllIncludeAsync
It is used when you want include data of the reference entity in the result set asynchronously. 

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
It is used to find the element based upon condition and include data of reference entity into the resultset.

```
    public IEnumerable<Applicant> FindByInclude()
    {
        return ApplicantUow.Repository<Applicant>().FindByInclude(t => t.LastName == "Doe", t => t.CompanyMaster);
    }
```

## FindByIncludeAsync
It is used to find the element based upon condition and include data of reference entity into the resultset asynchronously.

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
It retrieves the first element in the list based on the given condition.

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