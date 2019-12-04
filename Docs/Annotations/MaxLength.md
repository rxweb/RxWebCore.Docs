---
title: MaxLength
author: rxcontributortwo
category: annotation
---

You can use `MaxLength` annotation if you want to limit maximum length of any model property.

**Example:**

If you want to limit `ContactNumber` property to maximum 10 digit then you just have to set: 

```js
[MaxLength(10)]
public string ContactNumber { get; set; }
```

| Property | Description | Syntax |
| ----------- | ----------- | ----------- |
| maxLength | Enter value which you want to restrict the limit upto. | [MaxLength(10)] |
| messageKey | You can set the messageKey based on localization with the help of `messageKey` | [MaxLength(`messageKey`: "maxLengthMessageKey" )] |
| conditionalExpressionName | If you want to apply maxLength validation based on a custom condition, pass that custom validation function's name in `conditionalExpressionName` property of MaxLength validation. | [MaxLength(`conditionalExpressionName`:nameof(`User.ContactConditionalExpression`))] |
| dynamicConfigExpressionName | If you want to set any validation property at runtime, then `dynamicConfigExpressionName` can be used. | [MaxLength(`dynamicConfigExpressionName`:nameof(`HobbyNameDynamicExpression`))] |

# conditionalExpressionName

`MaxLength` validation annotation can be applied conditionally based on the custom validation function. You can write your condition by making a custom function in your class and pass that function's name in `nameOf` property of `conditionalExpressionName`. 

**Custom Validation Function**

```js
    public partial class User {

        public string Email { get; set; }

        public bool ContactConditionalExpression(object parentEntity = null) {
            var t = this;
            if (Email == "")
                return false;
            else return true;
        }
    }
```

**Set MaxLength annotation**

```js
    [MaxLength( `conditionalExpressionName`: nameof( `User.ContactConditionalExpression` ))]
    public string EmailAddress { get; set; }
```

# dynamicConfigExpressionName

If you want to set any validation property at runtime, then `dynamicConfigExpressionName` can be used. 

For example, if you want to set messageKey of any model property at run time:
Here is the dynamic expression function.

```js
    public partial class User {

        public Dictionary<string, object> AddressDynamicExpression(object parentEntity = null) {
            return new Dictionary<string, object>()
            {
                { "CustomMessageKey","CustomMaxLengthKey" }
            };
        }
    }

```
**Set MaxLength annotation dynamically**

```js
    [MaxLength( `dynamicConfigExpressionName`: nameof(`AddressDynamicExpression`))]
    public string Address { get; set; }
```
