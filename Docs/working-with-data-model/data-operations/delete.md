---
title: Delete
author: rxcontributorone
category: working-with-data-model
sub-category: data-operations 
---

# Delete
Used for delete operation to be done on entity.

```js
    public async Task DeleteAsync(int id)
    {
      var candidate = Uow.Repository<Candidate>().FindByKey(id);
      await Uow.RegisterDeletedAsync(candidate);
      await Uow.CommitAsync();
    }
```    