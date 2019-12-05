---
title: ICoreUnitOfWork
author: rxcontributorone
category: rxwebcore
---

## RegisterCleanAsync
RegisterCleanAsync method is used to clean the object instance value of the entity before `commit` method is called. If you want want the particular entity object to be added.

```     
    ApplicantUow.RegisterCleanAsync<Applicant>(applicant);       
```

## RegisterDeletedAsync
When you want to `delete` applicant it is done using `RegisterDeletedAsync` method. It will change state of the object and after `commit` method is executed it will update the object to database.

```
    public void Delete(int id)
    {
        var applicant = ApplicantUow.Repository<Applicant>().FindByKey(id);
        await ApplicantUow.RegisterDeletedAsync<Applicant>(applicant);
        await ApplicantUow.Commit();
    }
```

## RegisterDirtyAsync

When you want to `update` applicant it is done using RegisterDirty method. It will change state of the object and after `commit` method is executed it will update the object to database. 

```
    public Applicant Update(Applicant applicant)
    {
        await ApplicantUow.RegisterDirtyAsync<Applicant>(applicant);
        await ApplicantUow.Commit();
        return applicant;
    }
```

## RegisterNewAsync
When you want to `add` applicant it is done using RegisterNewAsync method. It will change state of the object and after `commit` method is executed it will add the object to database. 

```
    public Applicant Add(Applicant applicant)
    {
        await ApplicantUow.RegisterNewAsync(applicant);
        await ApplicantUow.Commit();
        return applicant;
    }
```

## Commit Async
CommitAsync method is used while adding, updating and deleting data to commit changes in the database after operation is executed.

```
    ApplicantUow.CommitAsync();
```

## refresh
refresh method is used to clear all the instance value of the Uow.

```
    ApplicantUow.refresh();
```