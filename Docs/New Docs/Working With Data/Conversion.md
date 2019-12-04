---
title: Conversion
author: rxcontributorone
category: rxwebcore  
---

# TimeZone Conversion
For applications working in different regions where people are accessing it from different locations in the world, it becomes necessary to manage timezones of every user. In this section, we will see how TimeZone coversion is done using rxwebcore but before that lets see the necessary steps done in the database for this.

**ApplicationLocales Table :**
| ApplicationLocaleId | LocaleCode | LocaleName | StatusId |
| ----------- | ----------- | ----------- | -------- | 
| 241 | en-US | English(United States) | 1 |

In user's table the `ApplicationLocaleId` is to be entered which the reference of ApplicationLocales table.

**Users Table :**
| UserId | ApplicationLocaleId | ApplicationTimeZoneId | LanguageCode | UserName | Password | Salt | LoginBlocked | StatusId |
| ----------- | ----------- | ----------- | ----------- | ----------- | ----------- | -------- | ------------ | -----------|
| 1 | **241** | 1 | en | admin | 0x01A508148A63F34.. |  0x454353354200.. | 0 | 1 |

Add the annotation of `[TimeZoneValueConversion]`

Now, we generate a web json based upon the claim of user's timezone.

```js
new Claim(CustomClaimTypes.TimeZone,user.ApplicationTimeZoneName)
```

This will retrieve the user's information as per the timezone of the user.

# Value Conversion
For fields which required to be encrypted while storing the data in the database and to be decrypted while showing the data on the Ui. For example, the EmailId field of the Candidate table has to stored in an encrypted manner in the database and has to be decrypted while rendering it in the user interface. For such cases, we need to make a ExtendedModels folder in which we will make a class for the encryption and decryption logic

## Create ExtendedModel
Create a folder named ExtendedModel and into it make a folder named main. In that create a .cs file. here we make EncryptDecrypt.cs.  

```js
  public class EncryptDecryptConverter : ValueConverter<string, string>
  {
    public static Expression<Func<string, string>> ConvertToProviderExpressions => (v) => //Encryption logic;

    public static Expression<Func<string, string>> ConvertFromProviderExpressions => (v) => // Decryption logic;

    public EncryptDecryptConverter()
      : base(ConvertToProviderExpressions, ConvertFromProviderExpressions) { }
  }
```

The above code will store the encrypted data in the database when `ConvertToProviderExpressions` is called and will retrieve the decrypted data while retrieving when `ConvertFromProviderExpressions` is called.

## Add annotation in the model class
In the Candidate.cs model class add the annotation of the created class above the property on which the value conversion should be done.

```js
[ValueConversion(typeof(StringCollectionToStringConverter))]
public string EmailId { get; set; }
```


