---
title: Range
author: rxcontributorone
category: data-validation
---


`Range` annotation is used when you want a property value in a specific range. 

Let's consider a scenario where there is a model class `Candidate.cs` which has properties of  CandidateId, CandidateName and Age.

## Basic Maxlength Validation

```js
    [Range(2,10)]
    public string ContactNumber { get; set; }
```

| Property | Description | Syntax |
| ----------- | ----------- | ----------- |
| maxLength | Enter value which you want to restrict the limit upto. | [(10)] |
| messageKey | You can set the messageKey based on localization with the help of `messageKey` | [MaxLength(`messageKey`: "maxLengthMessageKey" )] |
| conditionalExpressionName | If you want to apply maxLength validation based on a custom condition, pass that custom validation function's name in `conditionalExpressionName` property of MaxLength validation. | [MaxLength(`conditionalExpressionName`:nameof(`User.ContactConditionalExpression`))] |
| dynamicConfigExpressionName | If you want to set any validation property at runtime, then `dynamicConfigExpressionName` can be used. | [MaxLength(`dynamicConfigExpressionName`:nameof(`AdressDynamicExpression`))] |

## allowMaximumLength
Type : int

The minimum length based upon which the value is limited.

```js
    [MaxLength(10)]
    public string ContactNumber { get; set; }
```

## ConditionalExpression 
Type : string

`MaxLength` validation annotation can be applied conditionally based on the custom validation function. You can write your condition by making a custom function in your class and pass that function's name in `nameOf` property of `conditionalExpressionName`. 

The custom validation function is made in ExtendedModels folder of Main, In which a partial class of the model will be made.

In the ExtendedModel class
Candidate.cs :

```js
    public partial class Candidate {

        public string Email { get; set; }

        public bool ContactConditionalExpression(object parentEntity = null) {
            var t = this;
            if (Email == "")
                return false;
            else return true;
        }
    }
```

And in the DbEntities class

```js
  [MaxLength((10),conditionalExpressionName:nameof(Candidate.ContactConditionalExpression))]
  public string ContactNumber { get; set; }
```

# dynamicConfigExpressionName

If you want to set any validation property at runtime, then `dynamicConfigExpressionName` can be used. 

For example, if you want to set messageKey of any model property at run time:
Here is the dynamic expression function.

```js
    public partial class Candidate {

        public Dictionary<string, object> AdressDynamicExpression(object parentEntity = null) {
            return new Dictionary<string, object>()
            {
                { "CustomMessageKey","CustomMaxLengthKey" }
            };
        }
    }

```

In the DbEntities table :

```js
    [MaxLength( `dynamicConfigExpressionName`: nameof(`AddressDynamicExpression`))]
    public string Address { get; set; }
```

## MessageKey
Type : string

When you want to show a custom validation message based upon the entity. MessageKey property is used. Its value is stored in the database in the form of `LanguageContentKey` in LanguageContentKeys table and it's EN value is stored in LanguageContents table

**LanguageContentKeys Table**

| LanguageContentKeyId | KeyName | IsComponent 
| ----------- | ----------- | ----------- | 
| 1 | MaxLengthMessageKey | 0 | 

**LanguageContents Table**

| LanguageContentId | LanguageContentKeyId | ContentType | En | Fr |
| ----------- | ----------- | ----------- | -------- | ---- | 
| 1 | 1 | g | This candidate data exceeds the maxLength | NULL |  

In the DbEntity class : 

```js
    [MaxLength((10),messageKey:"MaxLengthMessageKey")]
     public string Address { get; set; }
```