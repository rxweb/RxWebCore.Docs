---
title: Database Tables
author: rxcontributorone
category: rxwebcore  
---

# Database Tables

1)  Main Database
The main database contains all the default tables which are necessary for fulfuling the basic functionalties like authorization and authentication, application objects, localization and globalization etc.. 

## Application Modules and Objects
To effectively manage functionalities of a large enterprise application, we need to break it into seperate units/modules and assign a particular task to each of them. As we have made a human resource enterprise application we take into consideration, three main modules of the application which are Resource Management, Candidate Module and User Module.

Some objects need to be stored in the database which are often used in application and its value is limited upto some number based upon the entity. For example, the HRManagementSystem is going to work in regions where the organization has its branch, if it works in two countries(For example : India and US), their values will be stored in ApplicationObjects as below and making a seperate table for storing the values of countries is not preferable in this case.  

1. ModuleMasters

Contains information about application's master modules.

<table>
<tr><th>Column</th><th>DataType</th><th>Description</th></tr>
<tr><td>ModuleMasterId</td><td>int</td><td>PK</td></tr>
<tr><td>ModuleMasterName</td><td>varchar(100)</td><td>Name of the application module master.</td></tr> 
<tr><td>StatusId</td><td>int</td><td>FK(ApplicationObjects)</td></tr>
</table>


| ModuleMasterId | ModuleMasterName | StatusId |
| ----------- | ----------- | -------- | 
| 1 | User Management | 1 |

2. ApplicationModules

Contains information about all the modules used in the application.

<table>
<tr><th>Column</th><th>DataType</th><th>Description</th></tr>
<tr><td>ApplicationModuleId</td><td>int</td><td>PK</td></tr>
<tr><td>ModuleMasterId</td><td>int</td><td>FK(ModuleMasters).</td></tr> 
<tr><td>ParentApplicationModuleId</td><td>int</td><td>Id of parent application module in case of entering a child module</td></tr>
</table>

| ApplicationModuleId | ModuleMasterId   | ParentApplicationModuleId |
| ----------- | ----------- | -------- | 
| 1 | 1 | NULL |

3. ApplicationObjectTypes

Contains type of Application Objects like status, gender etc.

<table>
<tr><th>Column</th><th>DataType</th><th>Description</th></tr>
<tr><td>ApplicationObjectTypeId</td><td>int</td><td>PK</td></tr>
<tr><td>ApplicationObjectTypeName</td><td>varchar(100)</td><td>Name of the application Object Type.</td></tr> 
<tr><td>StatusId</td><td>int</td><td>FK(ApplicationObjects)</td></tr>
</table>

| ApplicationObjectTypeId | ApplicationObjectTypeName | StatusId |
| ----------- | ----------- | -------- | 
| 1 | Status | 1 |
| 2 | Country | 1 |

4. ApplicationObjects

Contains application objects based upon its type.

<table>
<tr><th>Column</th><th>DataType</th><th>Description</th></tr>
<tr><td>ApplicationObjectId</td><td>int</td><td>PK</td></tr>
<tr><td>ApplicationObjectTypeId</td><td>int</td><td>FK(ApplicationObjectTypes)</td></tr>
<tr><td>ApplicationObjectName</td><td>varchar(100)</td><td>Name of the application object.</td></tr> 
<tr><td>StatusId</td><td>int</td><td>FK(ApplicationObjects)</td></tr>
</table>

| ApplicationObjectId | ApplicationObjectTypeId | ApplicationObjectName | StatusId |
| ----------- | ----------- | ----------- | -------- | 
| 1 | 1 | Active | 1 |
| 2 | 2 | India  | 1 |
| 3 | 2 | U.S | 1 |

## Localization and Globalization
For an application to efficiently work in different regions, it is necessary to maintain its timezones and locales used. A multilingual application includes returning server validation messages, change the whole UI based upon the selected language and bind the dropdowns based upon it.  

5. ApplicationTimeZones

It has details of different timezones of the world. For more detail about timezones Please refer [IANA](https://www.iana.org/time-zones).

<table>
<tr><th>Column</th><th>DataType</th><th>Description</th></tr>
<tr><td>ApplicationTimeZoneId</td><td>int</td><td>PK</td></tr>
<tr><td>ApplicationTimeZoneName</td><td>nvarchar(100)</td><td>Name of the Application TimeZone</td></tr>
<tr><td>Comment</td><td>nvarchar(200)</td><td>Information related to Timezone</td></tr> 
<tr><td>StatusId</td><td>int</td><td>FK(ApplicationObjects)</td></tr>
</table>

| ApplicationTimeZoneId | ApplicationTimeZoneName | Comment | StatusId |
| ----------- | ----------- | ----------- | -------- | 
| 1 | America/Mexico_city | Central Time | 1 |

6. ApplicationLocales 

It has details of standard locales used in the world.

<table>
<tr><th>Column</th><th>DataType</th><th>Description</th></tr>
<tr><td>ApplicationLocaleId</td><td>int</td><td>PK</td></tr>
<tr><td>LocaleCode</td><td>varchar(50)</td><td>Code of the locale</td></tr>
<tr><td>LocaleName</td><td>nvarchar(300)</td><td>Name of the locale</td></tr> 
<tr><td>StatusId</td><td>int</td><td>FK(ApplicationObjects)</td></tr>
</table>

| ApplicationLocaleId | LocaleCode | LocaleName | StatusId |
| ----------- | ----------- | ----------- | -------- | 
| 241 | en-US | English(United States) | 1 |

7. LanguageContentKeys

Stores language content key based upon which the multilingual data is entered. e.g:exceptionMessage

<table>
<tr><th>Column</th><th>DataType</th><th>Description</th></tr>
<tr><td>LanguageContentKeyId</td><td>int</td><td>PK</td></tr>
<tr><td>KeyName</td><td>varchar(50)</td><td>Key/type of the language content</td></tr>
<tr><td>IsComponent</td><td>bit(300)</td><td>1 if the key is a component</td></tr> 
</table>

| LanguageContentKeyId | KeyName | IsComponent 
| ----------- | ----------- | ----------- | 
| 1 | exceptionMessage | 0 | 

8. LanguageContents

Stores language contents of different languages which are required in your application based upon the key.

<table>
<tr><th>Column</th><th>DataType</th><th>Description</th></tr>
<tr><td>LanguageContentId</td><td>int</td><td>PK</td></tr>
<tr><td>LanguageContentKeyId</td><td>int</td><td>FK(LanguageContentKeys)</td></tr>
<tr><td>ContentType</td><td>varchar(3)</td><td>Type of the content(global)</td></tr> 
<tr><td>En</td><td>varchar(max)</td><td>English value of the content</td></tr> 
<tr><td>Fr</td><td>varchar(max)</td><td>French value of the content</td></tr> 
</table>

| LanguageContentId | LanguageContentKeyId | ContentType | En | Fr |
| ----------- | ----------- | ----------- | -------- | ---- | 
| 1 | 1 | g | Invalid Credentails | NULL |  

9. ComponentLanguageContents

Stores multilingual language content component wise.

<table>
<tr><th>Column</th><th>DataType</th><th>Description</th></tr>
<tr><td>ComponentLanguageContentId</td><td>int</td><td>PK</td></tr>
<tr><td>ComponentKeyId</td><td>int</td><td>FK(LanguageContentKeys)</td></tr>
<tr><td>LanguageContentId</td><td>int</td><td>FK(LangaugeContents)</td></tr> 
<tr><td>En</td><td>varchar(max)</td><td>English value of the content</td></tr> 
<tr><td>Fr</td><td>varchar(max)</td><td>French value of the content</td></tr> 
</table>

| ComponentLanguageContentId | ComponentKeyId | LanguageContentId | En | Fr |
| ----------- | ----------- | ----------- | -------- | ---- | 
| 1 | 1 | 1 | Invalid Credentails | NULL |  


## Authorization and Authentication
Information of JWT web token, users and its roles for performing authorization and authentication. Whenever a new request is made at the time of login the jwt web token is stored and authorization will require information which will be retrieved from the database.

10. ApplicationUsersToken 

Stores information of web token which are generated when any request is made on login method.

<table>
<tr><th>Column</th><th>DataType</th><th>Description</th></tr>
<tr><td>ApplicationUsersTokenId</td><td>int</td><td>PK</td></tr>
<tr><td>UserId</td><td>int</td><td>FK(Users)</td></tr>
<tr><td>SecurityKey</td><td>varchar(200)</td><td>Generated security key while the token is created</td></tr> 
<tr><td>JwtToken</td><td>varchar(max)</td><td>Generated Jwt web token</td></tr> 
<tr><td>AudienceType</td><td>varchar(50)</td><td>Type of the audience(web user or mobile user)</td></tr> 
<tr><td>CreatedDateTime</td><td>datetimeoffset(50)</td><td>created date and time of the web token</td></tr> 
</table>

| ApplicationUsersTokenId | UserId | SecurityKey | JwtToken | AudienceType | CreatedDateTime |
| ----------- | ----------- | ----------- | ----------- | ----------- | ----------- |
| 1 | 1 | 0x2271A2EDF169C5B75291C06D9FC66A6.... | eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ.. | MobileUser | 2019-06-28 06:13:52.327 | 


11. Users

Stores information about users of the application.

<table>
<tr><th>Column</th><th>DataType</th><th>Description</th></tr>
<tr><td>UserId</td><td>int</td><td>PK</td></tr>
<tr><td>ApplicationLocaleId</td><td>int</td><td>FK(ApplicationLocales)</td></tr>
<tr><td>ApplicationTimeZoneId</td><td>int</td><td>FK(ApplicationTimeZones)</td></tr> 
<tr><td>LanguageCode</td><td>varchar(3)</td><td>Code of the language based upon user's locale</td></tr> 
<tr><td>UserName</td><td>nvarchar(50)</td><td>Name of the user</td></tr> 
<tr><td>Password</td><td>binary(132)</td><td>Password of the user</td></tr> 
<tr><td>Salt</td><td>binary(140)</td><td>Salt key used to decrypt password</td></tr> 
<tr><td>LoginBlocked</td><td>bit</td><td>1 if the login is blocked</td></tr> 
<tr><td>StatusId</td><td>int</td><td>FK(ApplicationObjects)</td></tr> 
</table>

| UserId | ApplicationLocaleId | ApplicationTimeZoneId | LanguageCode | UserName | Password | Salt | LoginBlocked | StatusId |
| ----------- | ----------- | ----------- | ----------- | ----------- | ----------- | -------- | ------------ | -----------|
| 1 | 1 | 1 | en | admin | 0x01A508148A63F34.. |  0x454353354200... | 0 | 1 |

12. Roles

Stores different roles used in the application

<table>
<tr><th>Column</th><th>DataType</th><th>Description</th></tr>
<tr><td>RoleId</td><td>int</td><td>PK</td></tr>
<tr><td>RoleName</td><td>varchar(50)</td><td>Name of the role</td></tr>
<tr><td>StatusId</td><td>int</td><td>FK(ApplicationObjects)</td></tr>
</table>

| RoleId | RoleName |
| ----------- | ----------- |
| 1 | Admin |
| 2 | Customer |

13. RolePermissions

Stores access and rights based upon the role to the application modules.

<table>
<tr><th>Column</th><th>DataType</th><th>Description</th></tr>
<tr><td>RolePermissionId</td><td>int</td><td>PK</td></tr>
<tr><td>RoleId</td><td>int</td><td>FK(Roles)</td></tr>
<tr><td>ApplicationModuleId</td><td>int</td><td>FK(ApplicationModules)</td></tr>
<tr><td>CanView</td><td>bit</td><td>Rights to view</td></tr>
<tr><td>CanAdd</td><td>bit</td><td>Rights to add</td></tr>
<tr><td>CanEdit</td><td>bit</td><td>Rights to edit</td></tr>
<tr><td>CanDelete</td><td>bit</td><td>Rights to delete</td></tr>
</table>

| RolePermissionId | RoleId | ApplicationModuleId | CanView | CanAdd | CanEdit | CanDelete |
| ----------- | ----------- | ----------- | ----------- | ----------- | ----------- | ----------- |
| 1 | 1 | 1 | True | True | True | True |
| 2 | 2 | 1 | True | False | False | False |

14. UserRoles

Stores users and their respective roles.

<table>
<tr><th>Column</th><th>DataType</th><th>Description</th></tr>
<tr><td>UserRoleId</td><td>int</td><td>PK</td></tr>
<tr><td>UserId</td><td>int</td><td>FK(Users)</td></tr>
<tr><td>RoleId</td><td>int</td><td>FK(Roles)</td></tr>
</table>


| UserRoleId | UserId | RoleId |
| ----------- | ----------- | -------- | 
| 1 | 5 | 1 |

