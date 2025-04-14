* Postgresql, MsSql
```razor
{
  "ConnectionStrings": {
    "DefaultConnection": "--------"
  },
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "RabbitMQ": "rabbitmq://rabbitmq",
  "AllowedHosts": "*"
}
```
* Redis
```razor
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.Hosting.Lifetime": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "ConnectionStrings": {
    "Redis": "---------"
  },
  "RabbitMQ": "-------------",
  "AllowedHosts": "*"
}
```


* MongoDb
```razor
{
  "MongoDBSettings": {
    "ConnectionString": "mongodb://localhost:27017",
    "DatabaseName": "SeninVeritabaniIsmin"
  }
}

```
