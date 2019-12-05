---
title: Component Contents
author: rxcontributorone
category: localization-and-globalization
--- 

## LanguageContentKeys Table

<table class="table table-bordered">
<tr><th>LanguageContentKeyId</th><th>KeyName</th><th>IsComponent</th></tr>
<tr><td>1</td><td>RequiredMessage</td><td>0</td></tr>
</table>

## LangaugeContents Table 

<table class="table table-bordered">
<tr><th>LanguageContentId</th><th>LanguageContentKeyId</th><th>ContentType</th><th>En</th><th>Fr</th></tr>
<tr><td>1</td><td>1</td><td>g</td><td>This field is required</td><td>{0} is required</td></tr>
</table>


## ComponentLanguageContents

<table class="table table-bordered table-striped">
<tr><th>Column</th><th>DataType</th><th>Description</th></tr>
<tr><td>ComponentLanguageContentId</td><td>int</td><td>PK</td></tr>
<tr><td>ComponentKeyId</td><td>int</td><td>FK(LanguageContentKeys)</td></tr>
<tr><td>LanguageContentId</td><td>int</td><td>FK(LangaugeContents)</td></tr> 
<tr><td>En</td><td>varchar(max)</td><td>English value of the content</td></tr> 
<tr><td>Fr</td><td>varchar(max)</td><td>French value of the content</td></tr> 
</table>

The second step is to run the command : 

```js
rxwebcore --localization --main 
```

This will create `.json` file with en and fr json in wwwroot folder of the languagecontents.

> The users language will be stored in the Users table as a foreign key(LanguageCode)