* MasstransitConfiguration
```razor
using MassTransit;

builder.Services.AddMassTransit(configurator =>
{ 
// Burada, mesajları işlemek için 3 tane consumer (tüketici) ekliyoruz.
    configurator.AddConsumer<OrderCompletedEventConsumer>();
    configurator.AddConsumer<OrderFailedEventConsumer>();
    configurator.AddConsumer<CreateOrderCommandConsumer>();

    configurator.UsingRabbitMq((context, _configure) =>
    {
     // RabbitMQ host adresini alıyoruz ve bağlantıyı sağlıyoruz.
        _configure.Host(builder.Configuration["RabbitMQ"]);
        // Order tamamlandığında mesajları dinleyecek olan kuyruğu ayarlıyoruz.
        _configure.ReceiveEndpoint(RabbitMQSettings.Order_OrderCompletedQueue, e =>
            // OrderCompletedEventConsumer sınıfını bu kuyruğa bağladık.
            e.ConfigureConsumer<OrderCompletedEventConsumer>(context));

        _configure.ReceiveEndpoint(RabbitMQSettings.Order_OrderFailedQueue, e =>
            e.ConfigureConsumer<OrderFailedEventConsumer>(context));

        _configure.ReceiveEndpoint(RabbitMQSettings.Order_OrderCreatedQueue, e =>
            e.ConfigureConsumer<CreateOrderCommandConsumer>(context)); 
    });
});
```
* consumer eklenmesi: Mesajları dinleyip işleyen sınıflar burada belirtiliyor. Her bir consumer, belirli bir olay (event) gerçekleştiğinde çalışacak.
* RabbitMQ host ayarı: RabbitMQ'nin bağlanacağı host adresi yapılandırma dosyasından alınıyor.
* ReceiveEndpoint ayarları: Her bir ReceiveEndpoint, belirli bir kuyruğa mesajları dinleyip, hangi consumer sınıfının bu mesajları işleyeceğini belirtiyor.

```razor

configurator.UsingRabbitMq((context, _configure) =>
{
    // RabbitMQ host adresi yapılandırma dosyasından alınıp kullanılıyor.
    _configure.Host(builder.Configuration["RabbitMQ"]);

    // Sipariş tamamlandığında ilgili kuyruğu dinleyecek olan consumer'ı ayarlıyoruz.
    _configure.ReceiveEndpoint(RabbitMQSettings.Order_OrderCompletedQueue, e =>
        // OrderCompletedEventConsumer, bu kuyruğa gelen mesajları işlemek için yapılandırılıyor.
        e.ConfigureConsumer<OrderCompletedEventConsumer>(context));

    _configure.ReceiveEndpoint(RabbitMQSettings.Order_OrderFailedQueue, e =>
        e.ConfigureConsumer<OrderFailedEventConsumer>(context));

    _configure.ReceiveEndpoint(RabbitMQSettings.Order_OrderCreatedQueue, e =>
        // CreateOrderCommandConsumer, bu kuyruğa gelen mesajları işlemek için yapılandırılıyor.
        e.ConfigureConsumer<CreateOrderCommandConsumer>(context)); 
});
```
* RabbitMQ bağlantı dizesi: RabbitMQ anahtarının değeri yapılandırma dosyasından alınır ve RabbitMQ bağlantısı yapılır.
*_configure.Host: RabbitMQ sunucusunun adresi alınır ve bağlantı kurulur.
*ReceiveEndpoint: Her bir endpoint, ilgili kuyruğa gelen mesajları dinler ve uygun consumer ile ilişkilendirilir.

* Program.cs
```razor
{
  "ConnectionStrings": {
    "DefaultConnection": ".............................."
  },
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
// RabbitMQ bağlantı dizesi, yapılandırma dosyasından alınıyor.
  "RabbitMQ": "amqps:/...............",
  "AllowedHosts": "*"
}
```
