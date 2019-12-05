---
title: performance
author: rxcontributorone
category: newrxwebcore
---

ASP.NET core provides in-memory cache, distributed cache and response compression which are  used to improve durability and performance of 
the application. 

# Static Cache
Static cache is added using annotation of `[Cachable]` above the controller. In this tag, the amount of time also needs to be mentioned(in milliseconds)

```js
    [Cachable(2)]
    [ApiController]
    [Route("api/[controller]")]
	
	public class CandidatesController : BaseController<Candidate,Candidate,Candidate>
    {
        public CandidatesController(IResourceUow uow):base(uow) {}
    }
```

# Entity Tag
It is done using `[CacheETag]` annotation above the controller 
Example :

```js
    [CacheETag]
    [ApiController]
    [Route("api/[controller]")]
	
	public class CandidatesController : BaseController<Candidate,Candidate,Candidate>

    {
        public CandidatesController(IResourceUow uow):base(uow) {}

    }
```

# In-Memory Caching
In-memory caching is done using `AddMemoryCache` method which adds a non-distributed in memory implemtation of IMemoryCache to the services.
This is added in the `performance.cs` file in the bootstrap folder of the Api project. IMemoryCache represents a local in-memory cache whose values are not serialized.

```js
serviceCollection.AddMemoryCache();
```

# Distributed Cache
It is cache which are shared by multiple app servers which are maintained as an external service to the app servers that access it. It improves the performance of an .net core application when it is hosted on cloud.

```js
services.AddDistributedMemoryCache();
```

# Response Compression
Reducing size of files can reduce the payload and increase the application performance. Natively compressed assets such as images(PNG) and files having much smaller size(less than 150-1000 bytes) should not be compressed.     

```js
    serviceCollection.AddResponseCompression(options =>
    {
        options.Providers.Add<GzipCompressionProvider>();
        options.MimeTypes = ResponseCompressionDefaults.MimeTypes.Concat(new[] { "image/svg+xml" });
    });
```

and to use this response compression :

```js
    public static void UsePerformance(this IApplicationBuilder applicationBuilder)
    {
        applicationBuilder.UseResponseCompression();
    }
```
