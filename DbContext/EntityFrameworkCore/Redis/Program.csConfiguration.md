* Eklemek gereken paketler.
 ```razor 
  
dotnet add package StackExchange.Redis                                 //Redis’e bağlanmak ve temel işlemler için.   
dotnet add package Microsoft.Extensions.Caching.StackExchangeRedis    //Redis’i .NET Core cache sistemiyle entegre kullanmak
dotnet add package Microsoft.AspNetCore.Session                      //ASP.NET Core içinde Redis Session yönetimi
```

* Redis Cache 

```razor
builder.Services.AddStackExchangeRedisCache(options =>
{
    options.Configuration = configuration.GetConnectionString("RedisConnection");
    options.InstanceName = "YourAppCache:";
});
```
