---
title: Required
author: rxcontributortwo
category: rxwebcore
---

`Required` annotation can be used when you don't want a model property to be null. 

**Example:**

If you want to set EmailId to be required then you just have to write:

```
[Required]
public string EmailId { get; set; }
```

| Property | Description | Syntax |
| ----------- | ----------- | ----------- |
| allowWhiteSpace | You can also allow whitespace in that property, if you want to allow space in the property. | [Required(`allowWhiteSpace`: true)] |
| messageKey | You can set the messageKey based on localization with the help of `messageKey` | [Required(`messageKey`: "requiredMessageKey" )] |
| conditionalExpressionName | If you want to apply required validation based on a custom condition, pass that custom validation function's name in `conditionalExpressionName` property of Required validation. | [Required(`conditionalExpressionName`:nameof(`User.EmailConditionalExpression`))] |
| dynamicConfigExpressionName | If you want to set any validation property at runtime, then `dynamicConfigExpressionName` can be used. | [Required(`dynamicConfigExpressionName`:nameof(`EmailDynamicExpression`))] |

# conditionalExpressionName

`Required` validation annotation can be applied conditionally based on the custom validation function. You can write your condition by making a custom function in your class and pass that function's name in `nameOf` property of `conditionalExpressionName`. 

**Custom Validation Function**

```
    public partial class User {

        public bool EmailConditionalExpression(object parentEntity = null) {
            var t = this;
            return false;
        }
    }
```
**Set Required annotation**

```
    [Required( `conditionalExpressionName`: nameof( `User.EmailConditionalExpression` ))]
    public string EmailAddress { get; set; }
```

# dynamicConfigExpressionName

If you want to set any validation property at runtime, then `dynamicConfigExpressionName` can be used. 

For example, if you want to set messageKey of any model property at run time:
Here is the dynamic expression function.

```
    public partial class Hobby {

        public Dictionary<string, object> EmailDynamicExpression(object parentEntity = null) {
            return new Dictionary<string, object>()
            {
                { "CustomMessageKey","CustomRequiredKey" }
            };
        }
    }

```
**Set Required annotation dynamically**

```
    [Required( `dynamicConfigExpressionName`: nameof(`EmailDynamicExpression`))]
    public string EmailAddress { get; set; }
```
