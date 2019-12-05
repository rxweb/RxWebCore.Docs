---
title: Authentication
author: rxcontributorone
category: rxwebcore
---

Authentication is the process of ascertaining who a user is. Authentication may create one or more identities for the current user based upon which user is `Authorized`. When it comes to authenticating lightweighted single page applications it should be token based. rxwebcore uses JWT web token for doing the same.    

# JWT Token 

It is a json web token which is used to verify authenticity which can be encrypted in case of sensitive information. Once the user is logged in, each HTTP request will include the token based upon which the user is able to access modules, services, routes based upon the role. The `JwtBearerHandler` will handle all the requests.The advantage of using JWT web token is that it can be used by different domains.

The token is used in the Authorization header using a schema which communicates with the server for sending response to the client.
Futher the token is sent to the browser for making requests. The token is stored in variable which is generated through `WriteToken` method of `TokenProvider` in which you can pass security Claims based upon which the web json token will be generated. In the above code    `ClaimTypes.NameIdentifier` is passed in the writeToken method which means it will consider 1 as userId and in customClaims singleTenantValue is 1 which is configured in config json of rxweb when the init command is run **rxwebcore --init** as 

```
    "SingleTenantColumn": "ClientId"
```
and along with set you must set `validity` of the token which in the above example is set of 2 days.


```
            var token = TokenProvider.WriteToken(
                new[]
                        {
                                new Claim(ClaimTypes.NameIdentifier, (1).ToString()),
                                new Claim(CustomClaims.SingleTenantValue,"1")
                        },
                "Web",
                "User",
                DateTime.Now.AddDays(2)
                );
```

