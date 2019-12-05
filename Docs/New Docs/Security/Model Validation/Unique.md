---
title: Unique
author: rxcontributorone
category: newrxwebcore  
---

`Unique` validation annotation lets you enter unique value in an array based model property. 

let's consider a scenario where there is a model class `Person.cs` which has properties of PersonId, PersonName.

## Basic Unique Validation  

```js
    [Unique(connection: typeof(IMainDatabaseFacade), uniqueQueryMethod:nameof(Person.UniqueQueryMethod))]
```

The Unique validation function will be made in the main folder of the ExtendedModels folder. 

```js
        private List<UniqueQuery> UniqueQueryMethod()
        {
            var uniqueQueries = new List<UniqueQuery> {
            new UniqueQuery{
            ColumnName = "IsActive",
            QueryOperator= RxWeb.Core.Annotations.Enums.SqlQueryOperator.NotEqual,
            Value = false
            }
            };
            return uniqueQueries;
        }
```

| Property | Description | Syntax |
| ----------- | ----------- | ----------- |
| messageKey | You can set the messageKey based on localization with the help of `messageKey` | [Unique(typeof(IMainDatabaseFacade),`messageKey`:"UniqueMessageKey")] |
| conditionalExpressionName | If you want to apply unique validation based on a custom condition, pass that custom validation function's name in `conditionalExpressionName` property of Unique validation. | [Unique(`typeof`(IMainConnection),`conditionalExpressionName`:nameof(`Person.PersonNameConditionalExpression`))] |
| dynamicConfigExpressionName | If you want to set any validation property at runtime, then `dynamicConfigExpressionName` can be used. | [Unique(`typeof`(IMainConnection),`dynamicConfigExpressionName`:nameof(`PersonNameDynamicExpression`))] |

## ConditionalExpressionName
Type : string

When you want the validation to be fired based upon some custom validation function. It is passed in the `ConditionalExpressionName` property.
The custom validation function is made in ExtendedModels folder of Main, In which a partial class of the model will be made.

In the ExtendedModel class
Person.cs :

```js
    public partial class Person {

        public bool PersonConditionalExpression(object parentEntity = null) {
            var t = this;
            return false;
        }
    }
```

And in the DbEntities class
Person.cs

```js
  [Unique(conditionalExpressionName:nameof(Person.PersonConditionalExpression))]
  public string PersonName { get; set; }
```

## DynamicConfigExpressionName
Type : string

When you want to set validation property of validation at runtime(on the fly) validation, `DynamicConfigExpressionName` is set in which the custom function of dynamicExpressionName is passed.

In the ExtendedModel class

```js
    public partial class Person {

        public Dictionary<string, object> PersonNameDynamicExpression(object parentEntity = null) {
            return new Dictionary<string, object>()
            {
                { "CustomMessageKey","CustomUniqueKey" }
            };
        }
    }

```

In the DbEntities class

```js
    [Unique(dynamicConfigExpressionName: nameof(PersonNameDynamicExpression))]
    public string PersonName { get; set; }
```

## MessageKey
Type : string

When you want to show a custom validation message based upon the entity. MessageKey property is used. Its value is stored in the database in the form of `LanguageContentKey` in LanguageContentKeys table and it's EN value is stored in LanguageContents table

**LanguageContentKeys Table**

| LanguageContentKeyId | KeyName | IsComponent 
| ----------- | ----------- | ----------- | 
| 1 | UniqueMessageKey | 0 | 

**LanguageContents Table**

| LanguageContentId | LanguageContentKeyId | ContentType | En | Fr |
| ----------- | ----------- | ----------- | -------- | ---- | 
| 1 | 1 | g | This candidate data should be unique | NULL |  

In the DbEntity class : 

```js
    [Unique(messageKey:"UniqueMessageKey")]
     public string PersonName { get; set; }
```