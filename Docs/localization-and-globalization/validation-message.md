---
title: Validation Message
author: rxcontributorone
category: localization-and-globalization
---

For applications having big range of audiences, there is a possibility of having users acessing it from different regions. In such cases it is important that your application renders the whole Ui in the user specific language, other than this the validation messages should also be shown in the user sepcific language and dropdown should also bind respectively.

For showing validation messages in different languages, the first step is to add the validation messages in different languages. 

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

The second step is to run the command : 

```js
rxwebcore --localization
```

This will create `.json` file with en and fr json in wwwroot folder of the languagecontents.

> The users language will be stored in the Users table as a foreign key(LanguageCode)