
* MongoDB - Program.cs 

* Gerekli usingleri ekleyeilm.

```razor
using Microsoft.Extensions.Options;
using MongoDB.Driver;
```


```razor
// MongoDB ayarlarını ekleyelim.
builder.Services.Configure<MongoDBSettings>(
    builder.Configuration.GetSection("MongoDBSettings"));

 MongoDB client'ı ekleyelim.
builder.Services.AddSingleton<IMongoClient>(sp =>
{
    var settings = sp.GetRequiredService<IOptions<MongoDBSettings>>().Value;
    return new MongoClient(settings.ConnectionString);
});
 Gerekirse Db erişimi için bu şekilde de ekleyebiliriz.
builder.Services.AddScoped(serviceProvider =>
{
    var settings = serviceProvider.GetRequiredService<IOptions<MongoDBSettings>>().Value;
    var client = serviceProvider.GetRequiredService<IMongoClient>();
    return client.GetDatabase(settings.DatabaseName);
});
```

* MongoDB - appsettings.json

```razor
{
  "MongoDBSettings": {
    "ConnectionString": "mongodb://localhost:27017",
    "DatabaseName": "SeninVeritabaniIsmin"
  }
}
```

* Kullanılacak servis içerisinden erişim işlemlerini eklemeliyiz.

```razor
public class UserService
{
    private readonly IMongoCollection<User> _usersCollection;

    public UserService(IMongoClient mongoClient, IOptions<MongoDBSettings> settings)
    {
        var database = mongoClient.GetDatabase(settings.Value.DatabaseName);
        _usersCollection = database.GetCollection<User>("Users");
    }
}
```









