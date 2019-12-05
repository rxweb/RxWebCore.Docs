---
title: Unique
author: rxcontributortwo
category: rxwebcore
---

`Unique` validation annotation lets you enter a unique value in an array based model property. 

**Example:**

If you want to set HobbyName to be unique every time you enter a hobby, then you just have to write:

```
[Unique(typeof(IMainConnection))]
public List<string> HobbyName { get; set; }
```

<table class="table table-bordered">
<tr><th>Property</th><th>Description</th><th>Syntax</th></tr>
<tr><td>messageKey</td><td>You can set the messageKey based on localization with the help of `messageKey`</td><td>[Unique(typeof(IMainConnection),messageKey:"UniqueMessageKey")]</td></tr>
<tr><td>conditionalExpressionName</td><td>If you want to apply unique validation based on a custom condition, pass that custom validation function's name in `conditionalExpressionName` property of Unique validation.</td><td>[Unique(typeof(IMainConnection),conditionalExpressionName:nameof(Hobby.HobbyNameConditionalExpression))]</td></tr>
<tr><td>dynamicConfigExpressionName</td><td>If you want to set any validation property at runtime, then `dynamicConfigExpressionName` can be used.</td><td>[Unique(typeof(IMainConnection),conditionalExpressionName:nameof(Hobby.HobbyNameConditionalExpression))]</td></tr>
</table>

# conditionalExpressionName

`Unique` validation annotation can be applied conditionally based on the custom validation function. You can write your condition by making a custom function in your class and pass that function's name in `nameOf` property of `conditionalExpressionName`. 

**Custom Validation Function**

```
    public partial class Hobby {

        public bool HobbyNameConditionalExpression(object parentEntity = null) {
            var t = this;
            return false;
        }
    }
```
**Set Unique annotation**

```
    [Unique(`typeof`(IMainConnection), `conditionalExpressionName`: nameof( `Hobby.HobbyNameConditionalExpression` ))]
    public List<string> HobbyName { get; set; }
```

# dynamicConfigExpressionName

If you want to set any validation property at runtime, then `dynamicConfigExpressionName` can be used. 

For example, if you want to set messageKey of any model property at run time:
Here is the dynamic expression function.

```
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

```
    [Unique(typeof(IMainConnection), dynamicConfigExpressionName: nameof(HobbyNameDynamicExpression))]
    public List<string> HobbyName { get; set; }
```
