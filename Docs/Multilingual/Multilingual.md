---
title: Multilingual
author: rxcontributortwo
category: rxwebcore
---

In today's global world, most of the software applications are not restricted to their local area. These large scale application can be widely used in any country. Such application must be made Multi-Lingual so that it can be used by every user in whichever language they want to. As the name describes, multi-lingual means expressing your application content in more than 1 language. 

The first step to achieve this is to follow a database structure as follows:

# Database Entries for MultiLingual Application

For developing multilingual software application using rxwebcore, let's consider a scenario where you need to display application content in 2 languages ( for example: `English` and `French` ). For creating a multi-lingual application through rxweb, we'll walk through the following steps:

## ApplicationObjectTypes

`ApplicationObjectTypes` table will contain the main object type we are using throught the application. Common application object type examples are: `Status`( like Active, InActive, Deleted etc. ), `ContentType` ( like Plain Text, Placeholder, Messages, Tooltip etc ), `Data operations` ( like Add, List, Delete etc ).

Let me share you a sample data for ApplicationObjectTypes:

<table class="table table-bordered">
<tr><th>ApplicationObjectTypeId</th><th>ApplicationObjectTypeName</th><th>IsActive</th></tr>
<tr><td>2</td><td>ContentType</td><td> 1 </td></tr>
<tr><td>3</td><td>Status</td><td> 1 </td></tr>
<tr><td>4</td><td>DataAction</td><td> 1 </td></tr>
</table>

Above `ApplicationObjectTypeId` will be passed as the foreign key reference in `ApplicationObjects` table.

## ApplicationObjects

`ApplicationObjects` table contain all the objects which we enterred in the above ApplicationObjectTypes table. 

<ul>
    <li>Active, InActive, Deleted will fall under the `Status` ApplicationObjectType.</li>
    <li>Text, Placeholder, ValidationMessages will fall under the `ContentType` ApplicationObjectType.</li>
    <li>Add, List, Delete will fall under the `DataAction` ApplicationObjectType.</li>
</ul>

Here is a sample ApplicationObjects table data:

<table class="table table-bordered">
<tr><th>ApplicationObjectId</th><th>ApplicationObjectTypeId</th><th>ApplicationObjectName</th><th>IsActive</th></tr>
<tr><td>15</td><td>2</td><td>ValidationMessages</td><td> 1 </td></tr>
<tr><td>16</td><td>2</td><td>Text</td><td> 1 </td></tr>
<tr><td>17</td><td>2</td><td>Placeholder</td><td> 1 </td></tr>
<tr><td>18</td><td>2</td><td>ValidationMessages</td><td> 1 </td></tr>
<tr><td>22</td><td>3</td><td>List</td><td> 1 </td></tr>
<tr><td>23</td><td>3</td><td>Add</td><td> 1 </td></tr>
</table>

## LanguageContentKeys

`LanguageContentKeys` table contains all the key names which we will use in our multi-lingual application( for which we want to change the displayed language ). Here, I am adding 2 different key names which is Required and Unique and which I will use it to show validation messages for required and unique validation for `english` as well as `french` language. 

Below is a sample example of LanguageContentKeys data.

<table class="table table-bordered">
<tr><th>LanguageContentKeyId</th><th>KeyName</th></tr>
<tr><td>6</td><td>Required</td></tr>
<tr><td>7</td><td>Unique</td></tr>
</table>

The above `LanguageContentKeyId` from LanguageContentKeys table will be set reference with the `LanguageContents` table. 

## LanguageContents

`LanguageContents` table will contain the English and French language content based on the LanguageContentKeyId and ContentTypeId. Here, `ContentTypeId` of `LanguageContents` table is the foreign key reference of the `ApplicationObjectId` we got from ApplicationObjects table. 

Below is the sample LanguageContents table data:

<table class="table table-bordered">
<tr><th>LanguageContentId</th><th>LanguageContentKeyId</th><th>ContentTypeId</th><th>En</th><th>Fr</th></tr>
<tr><td>8</td><td>6</td><td>15</td><td>This field is required</td><td>Ce champ est requis</td></tr>
<tr><td>10</td><td>7</td><td>15</td><td>This Field Should be Unique</td><td>Ce champ devrait être unique</td></tr>
</table>

Here, `6 as LanguageContentKeyId` and `15 as ContentTypeId` denotes that it is a validation message for Required KeyName and `7 as LanguageContentKeyId` and `15 as ContentTypeId` denotes that it is a validation message for Unique KeyName.

## ModuleContents

`ModuleContents` table will contain the english and french language content for the respective `DataAction` based on the DataActionId and ApplicationModuleId. Here, `LanguageContentId` from LanguageContents table will be passed as a foreign key reference as well as the `DataActionId` will be same as the `ApplicationObjectId` from the ApplicationObjects table. 

Sample ModuleContents table data is shown below:

<table class="table table-bordered">
<tr><th>ModuleContentId</th><th>ApplicationModuleId</th><th>LanguageContentId</th><th>DataActionId</th><th>En</th><th>Fr</th></tr>
<tr><td>1</td><td>2</td><td>8</td><td>22</td><td>UserName</td><td>Nom d'utilisateur</td></tr>
<tr><td>2</td><td>3</td><td>10</td><td>23</td><td>Enter First Name</td><td>Entrez votre prénom</td></tr>
</table>

By following all these steps, you can easily update your application database to multilingual database with respect to the Application Modules and Language Contents. 
