---
title: sms
author: rxcontributorone
category: rxwebcore
---

SMS sending is done using twilio which requires configuration like account sid and authToken given by twilio. To setup yout twilio configuration,Please refer [Twilio SMS Docs](https://www.twilio.com/docs/sms) 

SMS sending uses `SendAsync` method.

In app.settings.json you need to configure 

# SmsConfig

1) From
Type:`string`
ContactNumber of the sender

2) To
Type:`string`
ContactNumber of the reciever

3) Body
Type:`string`
Content of the sms

# TwilioSmsConfiguration

1) AccountSid
Type:`string`
AccountSid provided by twilio

2) AuthToken
Type:`string`
AuthToken provided by twilio