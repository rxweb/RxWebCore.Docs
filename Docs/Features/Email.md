---
title: Email
author: rxcontributorone
category: rxwebcore
---

Common utilities include sending Email using different types like `Standard Mail`, `SendGrid` and `MailKit`. The First Step is to configure  
EmailConfiguration in app.settings.json

1) EmailType
Email Type can be either `Standard`, `SendGrid` or `MailKit`

2) Email
The Configuration that is to be done respective to the `EmailType` is to be configured in Email. 

Sending Email uses the `SendAsync` method.

# Standard Email
For sending email using standard email, you need to set EmailType as standard and set the configuration in email which are 

```js
    "EmailType":"Standard"
```

1) EmailFormatType
Type:`EmailFormatType`
Format of the email is to be set in this property.

2) From
Type:`string`
EmailId of the sender

3) To
Type:`List<string>`
EmailIds of the recievers 

4) Body
Type:`string`
The Body content of the email

5) Subject 
Type:`string`
Subject of the email

6) Attachments
Type:`Dictionary<string,Stream>`
Attachments of the email

# SendGrid
Sending email using sendgrid requires ApiKey which is provided by sendgrid. For getting configuration using sendgrid please refer 
[SendGrid Api Key](https://sendgrid.com/docs/api-reference/)
For sending email using sendgrid, you need to set EmailType as SendGrid and set the configuration in email which are 

```js
    "EmailType":"SendGrid"
```

1) ApiKey
Type:`string`
ApiKey of sendgrid.

# MailKit
For sending email using MailKit, you need to set EmailType as MailKit and set the configuration in email which are 

For more information, Please refer [MailKit](http://www.mimekit.net/docs/html/N_MailKit_Net_Smtp.htm)

```js
    "EmailType":"MailKit"
```
1) Host
Type:`string`
Stmp hostName.


2) Port
Type:`Number`
port number.

3) UserName
Type:`string`
UserName of the sender's email account.

4) Password
Type:`string`
Password of the sender's email account.

