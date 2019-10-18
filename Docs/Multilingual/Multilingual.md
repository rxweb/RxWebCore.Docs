---
title: Multilingual
author: rxcontributortwo
category: rxweb core
---

In today's global world, most of the software applications are not restricted to their local area. These large scale application can be widely used in any country. Such application must be made Multi-Lingual so that it can be used by every user in whichever language they want to. As the name describes, multi-lingual means expressing your application content in more than 1 language. 

The first step to achieve this is to follow a database structure as follows:

# Database Entries for MultiLingual Application

For developing multilingual software application using rxwebcore, let's consider a scenario where you need to display application content in 2 languages ( for example: `English` and `French` ). For creating a multi-lingual application through rxweb, we'll walk through the following steps:

## ApplicationObjectTypes

`ApplicationObjectTypes` table will contain the main object type we are using throught the application. Common application object type examples are: `Status`( like Active, InActive, Deleted etc. ), `ContentType` ( like Plain Text, Placeholder, Messages, Tooltip etc ), `Data operations` ( like Add, List, Delete etc ).

Let me share you a sample data for ApplicationObjectTypes:

| ApplicationObjectTypeId | ApplicationObjectTypeName | IsActive | 
| ----------- | ----------- | ----------- |
| 2 | ContentType | 1 |
| 3 | Status | 1 |
| 4 | DataAction | 1 |

Above `ApplicationObjectTypeId` will be passed as the foreign key reference in `ApplicationObjects` table.

## ApplicationObjects

`ApplicationObjects` table contain all the objects which we enterred in the above ApplicationObjectTypes table. 

<ul>
    <li>Active, InActive, Deleted will fall under the `Status` ApplicationObjectType.</li>
    <li>Text, Placeholder, ValidationMessages will fall under the `ContentType` ApplicationObjectType.</li>
    <li>Add, List, Delete will fall under the `DataAction` ApplicationObjectType.</li>
</ul>

Here is a sample ApplicationObjects table data:

| ApplicationObjectId | ApplicationObjectTypeId | ApplicationObjectTypeName | IsActive | 
| ----------- | ----------- | ----------- | ----------- |
| 15 | 2 | ValidationMessages | 1 |
| 16 | 2 | Text | 1 |
| 17 | 2 | Placeholder | 1 |
| 18 | 2 | ToolTip | 1 |
| 22 | 4 | List | 1 |
| 23 | 4 | Add | 1 |

## LanguageContentKeys

`LanguageContentKeys` table contains all the key names which we will use in our multi-lingual application( for which we want to change the displayed language ). Here, I am adding 2 different key names which is Required and Unique and which I will use it to show validation messages for required and unique validation for `english` as well as `french` language. 

Below is a sample example of LanguageContentKeys data.

| LanguageContentKeyId | KeyName |
| ----------- | ----------- |
| 6 | Required |
| 7 | Unique |

The above `LanguageContentKeyId` from LanguageContentKeys table will be set reference with the `LanguageContents` table. 

## LanguageContents

`LanguageContents` table will contain the English and French language content based on the LanguageContentKeyId and ContentTypeId. Here, `ContentTypeId` of `LanguageContents` table is the foreign key reference of the `ApplicationObjectId` we got from ApplicationObjects table. 

Below is the sample LanguageContents table data:

| LanguageContentId | LanguageContentKeyId | ContentTypeId | En | Fr |
| ----------- | ----------- | ----------- | ----------- | ----------- |
| 8 | 6 | 15 | This field is required | Ce champ est requis |
| 10 | 7 | 15 | This Field Should be Unique | Ce champ devrait être unique |

Here, `6 as LanguageContentKeyId` and `15 as ContentTypeId` denotes that it is a validation message for Required KeyName and `7 as LanguageContentKeyId` and `15 as ContentTypeId` denotes that it is a validation message for Unique KeyName.

## ModuleContents

`ModuleContents` table will contain the english and french language content for the respective `DataAction` based on the DataActionId and ApplicationModuleId. Here, `LanguageContentId` from LanguageContents table will be passed as a foreign key reference as well as the `DataActionId` will be same as the `ApplicationObjectId` from the ApplicationObjects table. 

Sample ModuleContents table data is shown below:

| ModuleContentId | ApplicationModuleId | LanguageContentId | DataActionId | En | Fr |
| ----------- | ----------- | ----------- | ----------- | ----------- | ----------- |
| 1 | 2 | 8 | 22 | UserName | Nom d'utilisateur |
| 2 | 3 | 10 | 23 | Enter First Name | Entrez votre prénom |

By following all these steps, you can easily update your application database to multilingual database with respect to the Application Modules and Language Contents. 
