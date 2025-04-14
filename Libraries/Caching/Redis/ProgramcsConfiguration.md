// Redis Cache 
* Redis'i kullanmak için öncelikle StackExchange.Redis NuGet paketini projeye eklemek gerekir. Aşağıdaki komut ile yükleyebilirsiniz:
```razor
dotnet add package StackExchange.Redis

```
* Redis Bağlantısı ve Konfigürasyonu:Program.cs dosyasında, Redis ile bağlantı kurulması için gerekli ayarlar yapılır. Redis bağlantı dizesi appsettings.json dosyasından alınır ve AddStackExchangeRedisCache metodu ile Redis cache servisi eklenir.
```razor
builder.Services.AddStackExchangeRedisCache(options =>
{
    options.Configuration = configuration.GetConnectionString("RedisConnection");
    options.InstanceName = "YourAppCache:"; 
});
```
* appsettings.json Dosyasındaki Redis Konfigürasyonu: Redis bağlantı dizesi, appsettings.json dosyasına eklenir. Bu, bağlantı ayarlarının merkezi bir konumda tutulmasını sağlar.
```razor
{
  "ConnectionStrings": {
    "RedisConnection": "localhost:6379"
  }
}
```
*Redis Cache Kullanımı: Redis'in önbellek olarak kullanımı için, IDistributedCache servisini controller veya servislerinizde enjekte edebiliriz. Aşağıda, bir Redis cache kullanım örneği yer almakta:

```razor
public class BasketService : IBasketService
{
    private readonly IDistributedCache _cache;

    public BasketService(IDistributedCache cache)
    {
        _cache = cache;
    }

    public async Task<Basket> GetBasketAsync(string userId)
    {
        var cachedBasket = await _cache.GetStringAsync(userId);
        if (cachedBasket != null)
        {
            return JsonConvert.DeserializeObject<Basket>(cachedBasket);
        }

        var basket = await _basketRepository.GetBasketAsync(userId);
        await _cache.SetStringAsync(userId, JsonConvert.SerializeObject(basket));
        return basket;
    }
}

```
*Redis ile veri eklemek, almak ve silmek için IDistributedCache kullanılır. Örnek olarak, GetBasketAsync metodunda, eğer sepet daha önce önbelleğe alınmışsa Redis'ten alınır; yoksa veritabanından alınır ve ardından Redis'e eklenir.
