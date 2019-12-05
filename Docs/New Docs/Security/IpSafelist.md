---
title: IpSafelist 
author: rxcontributorone
category: newrxwebcore 
---

IpSafelist means to create a list of trusted Ip addresses. It is used for validating access to limited and trusted IPs.
To have to configure allowed Ips in "AllowedIps" key of `appsettings.json` 

```js
    "AllowedIps": [
    ]
  
```  

It will validated the provided Ip list from the added service of security

```js
    services.AddSecurity(Configuration);
```

In `security.cs` file of the Bootstrap folder of the Api project, The SetIpSafeList method is called which is used to validate the list of IpAddressed which are set in the AllowedIps. 

```js
  private static void SetIpSafeList(this IApplicationBuilder applicationBuilder)
        {
            applicationBuilder.Use(async (context, next) =>
            {
                var remoteIp = context.Connection.RemoteIpAddress;
                string[] ip = SecurityConfig.AllowedIps;

                var bytes = remoteIp.GetAddressBytes();
                var badIp = true;
                foreach (var address in ip)
                {
                    var testIp = IPAddress.Parse(address);
                    if (testIp.GetAddressBytes().SequenceEqual(bytes))
                    {
                        badIp = false;
                        break;
                    }
                }

                if (badIp)
                {
                    context.Response.StatusCode = 401;
                    return;
                }
                await next();
            });
        }

```

  