---
title: Update
author: rxcontributorone
category: working-with-data-model
sub-category: data-operations 
---

# Update
Used during put request for updating object/objects of entity.

## Updating Single Object
`RegisterDirtyAsync` method is used for updating objects. Here is an example of updation of a single entity. 

```js
    public async Task UpdateAsync([FromBody]Candidate candidate)
    {
      await Uow.RegisterDirtyAsync(candidate);
      await Uow.CommitAsync();
    }
```    

## Updating Multiple Objects
Updating Multiple Objects using `RegisterDirtyAsync` 

```js
   public async Task UpdateAsyncList([FromBody]IEnumerable<Candidate> candidates)
    {     
     await Uow.RegisterNewAsync(candidate);
     await Uow.CommitAsync();
    }
```