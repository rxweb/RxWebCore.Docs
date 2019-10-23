---
title: Unique
author: rxcontributortwo
category: annotation
---

`Unique` validation annotation lets you enter a unique value in an array based model property. 

**Example:**

If you want to set HobbyName to be unique every time you enter a hobby, then you just have to write:

```js
[Unique(typeof(IMainConnection))]
public List<string> HobbyName { get; set; }
```

| Property | Description | Syntax |
| ----------- | ----------- | ----------- |
| messageKey | You can set the messageKey based on localization with the help of `messageKey` | [Unique(t`ypeof`(IMainConnection),`messageKey`:"UniqueMessageKey")] |
| conditionalExpressionName | If you want to apply unique validation based on a custom condition, pass that custom validation function's name in `conditionalExpressionName` property of Unique validation. | [Unique(`typeof`(IMainConnection),`conditionalExpressionName`:nameof(`Hobby.HobbyNameConditionalExpression`))] |
| dynamicConfigExpressionName | If you want to set any validation property at runtime, then `dynamicConfigExpressionName` can be used. | [Unique(`typeof`(IMainConnection),`dynamicConfigExpressionName`:nameof(`HobbyNameDynamicExpression`))] |


# conditionalExpressionName

`Unique` validation annotation can be applied conditionally based on the custom validation function. You can write your condition by making a custom function in your class and pass that function's name in `nameOf` property of `conditionalExpressionName`. 

**Custom Validation Function**

```js
    public partial class Hobby {

        public bool HobbyNameConditionalExpression(object parentEntity = null) {
            var t = this;
            return false;
        }
    }
```
**Set Unique annotation**

```js
    [Unique(`typeof`(IMainConnection), `conditionalExpressionName`: nameof( `Hobby.HobbyNameConditionalExpression` ))]
    public List<string> HobbyName { get; set; }
```

# dynamicConfigExpressionName

If you want to set any validation property at runtime, then `dynamicConfigExpressionName` can be used. 

For example, if you want to set messageKey of any model property at run time:
Here is the dynamic expression function.

```js
public partial class Hobby {

        public Dictionary<string, object> HobbyNameDynamicExpression(object parentEntity = null) {
            return new Dictionary<string, object>()
            {
                { "CustomMessageKey","CustomUniqueKey" }
            };
        }
    }

```
**Set Unique annotation dynamically**

```js
    [Unique(`typeof`(IMainConnection), `dynamicConfigExpressionName`: nameof(`HobbyNameDynamicExpression`))]
    public List<string> HobbyName { get; set; }
```
