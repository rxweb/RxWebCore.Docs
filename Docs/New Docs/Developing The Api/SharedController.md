---
title: Shared Controller
author: rxcontributortwo
category: rxwebcore 
---

To manage data which are to be used in multiple data entity operations, A shared controller is made. For example, If you want to perform delete operation of multiple objects at one call.

# Generate a Shared Controller

To Create a shared controller, open the `Package Manager Console` and run the following command:

> rxwebcore --controller --shared --main <Controller_Name> --uow <Module_Name>

Let's consider a scenario where you want a `DeleteSharedController` in the `UsersModule`, you have to write:

> rxwebcore --controller --shared --main DeleteSharedController --uow Users

