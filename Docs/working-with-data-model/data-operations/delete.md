---
title: Delete
author: rxcontributorone
category: working-with-data-model
subcategory: data-operations 
---

Used for delete operation to be done on entity.

```js
    public async Task DeleteAsync(int id)
    {
      var candidate = Uow.Repository<Candidate>().FindByKey(id);
      await Uow.RegisterDeletedAsync(candidate);
      await Uow.CommitAsync();
    }
```    