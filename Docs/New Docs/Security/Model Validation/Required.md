---
title: Required
author: rxcontributorone
category: newrxwebcore  
---

`Required` annotation will be used when you don't want the model property to be null. There are many properties of the validation which can be used based upon the scenario 

Let's consider a scenario where there is a model class `Candidate.cs` which has properties of  CandidateId, CandidateName.

## Basic Required Validation

```js
[Required]
public string CandidateName { get; set; }
```

Using required annotation before the property, this is not allow null value to be entered in CandidateName. There are several additional properties of the annotations which can be used to validate the property which are listed below:

| Property | Description | Syntax |
| ----------- | ----------- | ----------- |
| allowWhiteSpace | You can also allow whitespace in that property, if you want to allow space in the property. | [Required(allowWhiteSpace: true)] |
| messageKey | You can set the messageKey based on localization with the help of `messageKey` | [Required(messageKey: "requiredMessageKey" )] |
| conditionalExpressionName | If you want to apply required validation based on a custom condition, pass that custom validation function's name in `conditionalExpressionName` property of Required validation. | [Required(conditionalExpressionName:nameof(User.EmailConditionalExpression))] |
| dynamicConfigExpressionName | If you want to set any validation property at runtime, then `dynamicConfigExpressionName` can be used. | [Required(dynamicConfigExpressionName:nameof(EmailDynamicExpression))] |

## allowWhiteSpace
Type : boolean

allowWhiteSpace property is set to true when you want to allow space in the CandidateName value. It should be set true before the annotation. By default it is set false.  

```js
[Required(allowWhiteSpace:true)]
public string CandidateName { get; set; }
```

## ConditionalExpressionName
Type : string
    
When you want the validation to be fired based upon some custom validation function. It is passed in the `ConditionalExpressionName` property.
The custom validation function is made in ExtendedModels folder of Main, In which a partial class of the model will be made.

In the ExtendedModel class
Candidate.cs :

```js
    public partial class User {

        public bool CandidateNameConditionalExpression(object parentEntity = null) {
            var t = this;
            return false;
        }
    }
```

And in the DbEntities class

```js
  [Required(conditionalExpressionName:nameof(User.EmailConditionalExpression))]
  public string CandidateName { get; set; }
```

## DynamicConfigExpressionName
Type : string

When you want to set validation property of validation at runtime(on the fly) validation, `DynamicConfigExpressionName` is set in which the custom function of dynamicExpressionName is passed.

In the ExtendedModel class

```js
    public partial class User {

        public Dictionary<string, object> CandidateNameDynamicExpression(object parentEntity = null) {
            return new Dictionary<string, object>()
            {
                { "CustomMessageKey","CustomRequiredKey" }
            };
        }
    }

```

In the DbEntities class

```js
    [Required(dynamicConfigExpressionName: nameof(CandidateNameDynamicExpression))]
    public string CandidateName { get; set; }
```

## MessageKey
Type : string

When you want to show a custom validation message based upon the entity. MessageKey property is used. Its value is stored in the database in the form of `LanguageContentKey` in LanguageContentKeys table and it's EN value is stored in LanguageContents table

**LanguageContentKeys Table**

| LanguageContentKeyId | KeyName | IsComponent 
| ----------- | ----------- | ----------- | 
| 1 | RequiredMessageKey | 0 | 

**LanguageContents Table**

| LanguageContentId | LanguageContentKeyId | ContentType | En | Fr |
| ----------- | ----------- | ----------- | -------- | ---- | 
| 1 | 1 | g | This candidate data is required | NULL |  

In the DbEntity class : 

```js
    [Required(messageKey:"RequiredMessageKey")]
     public string CandidateName { get; set; }
```