---
title: Validation Message
author: rxcontributorone
category: rxwebcore
---

For applications having big range of audiences, there is a possibility of having users acessing it from different regions. In such cases it is important that your application renders the whole Ui in the user specific language, other than this the validation messages should also be shown in the user sepcific language and dropdown should also bind respectively.

For showing validation messages in different languages, the first step is to add the validation messages in different languages. 

## LanguageContentKeys Table

| LanguageContentKeyId | KeyName | IsComponent 
| ----------- | ----------- | ----------- | 
| 1 | RequiredMessage | 0 | 

## LangaugeContents Table 

| LanguageContentId | LanguageContentKeyId | ContentType | En | Fr |
| ----------- | ----------- | ----------- | -------- | ---- | 
| 1 | 1 | g | This field is required | {0} is required |  

The second step is to run the command : 

```js
rxwebcore --localization
```

This will create `.json` file with en and fr json in wwwroot folder of the languagecontents.

> The users language will be stored in the Users table as a foreign key(LanguageCode)