---
title: Authorization
author: rxcontributorone
category: rxwebcore core
---

`Authorization` is a method of adjudging which user is able to do what. It uses `authentication` for identifying the user, It is done using role based authorization mechanism through which the access modules of the user is determined based upon role where rules are maintained in the database.

# Role Based Authorization.
Role based authorization is a mechanism through which we determine that which user can have which acess for what module. For example, the admin user has the right to add elements, read elements, edit elements and delete elements and a non admin user has some specific rights based upon the user permissions which is managed in `RolePermissions` table where Role is defined from `Roles`.

Roles Table:

| RoleId | RoleName |
| ----------- | ----------- |
| 1 | Admin |
| 2 | Customer |

RolePermissions Table:

| RolePermissionId | RoleId | ApplicationModuleId | CanView | CanAdd | CanEdit | CanDelete |
| ----------- | ----------- | ----------- | ----------- | ----------- | ----------- | ----------- |
| 1 | 1 | 1 | True | True | True | True |
| 2 | 2 | 1 | True | False | False | False |


Based upon the RoleId and ApplicationModuleId it will retrieve the information about which user has how much access of which module based upon the role defined in Roles Table. 
The application module in `RolePermissions` table is a FK reference from `ApplicationModules` table

ApplicationModules Table:

| ApplicationModuleId | ModuleMasterId | ParentApplicationModuleId |
| ----------- | ----------- | ----------- |
| 1 | 1 | 1 |

The Module is defined in `ModuleMasters` Table

ModuleMasters Table: 

| ModuleMasterId | ModuleMasterName | StatusId |
| ----------- | ----------- | ----------- |
| 1 | Registration | 1 |


## Access
It is done using `Access` in which id of the application module is passed. Through which it will execute authorization based upon which the user rights are determined.

```js
    [ApiController]
    [Route("api/[controller]")]
	[Access(1)]
	public class CustomerController : BaseController<Customer,vCustomer,vCustomerRecord>
    {
        public CustomerController(IOrderUow uow):base(uow) {}
    }
```        

To add authorization in the controller using access, the following command is used:

> -- rxwebcore --controller --basic --main Customer --uow --Order --access 1

In this command `Customer` is the controller name, `Order` is the module and 1 is the application module Id retrieved from the database. 

The user can check whether which controller are having authorization and which are by-pass.

> --rxwebcore security

## AllowAnonymous

When you want to by-pass the controller without any authorization when you want any user to access the specific action. For example: If you have a scenario where you want to by-pass the post action of registeration.

As per the below scenario it will allow any user to access this `Post` method and allow new user to register.  

```js
    [ApiController]
    [Route("api/[controller]")]
	[AllowAnonymous]
	public class UserController : BaseController<User,vUser,vUserRecord>
    {
        public UserController(IRegisterUow uow):base(uow) {}
    }
```