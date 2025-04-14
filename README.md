# .NetDevelopmentFirstKit

.NET tabanlı uygulama geliştirme sürecini kolaylaştırmak ve hızlandırmak için oluşturulmuş, hazır şablonlar, kod parçacıkları, veritabanı bağlantı yardımcıları ve daha fazlasını içeren bir başlangıç kitidir.

## İçindekiler

```razor
.NetDevelopmentFirstKit/
├── api/
│   ├── Controllers/
│   │   └── ... (API Controller dosyaları)
│   ├── DTOs/
│   │   └── ... (Data Transfer Object dosyaları)
│   ├── Entities/
│   │   └── ... (Entity dosyaları)
│   ├── appsettings.json
│   └── Enums/
│       └── ... (Enum dosyaları)
├── docker/
│   └── docker-compose.yml
├── dbcontext/
│   ├── mssql/
│   │   └── ... (MSSQL DbContext yapılandırma dosyaları)
│   ├── mongodb/
│   │   └── ... (MongoDB DbContext yapılandırma dosyaları)
│   ├── oracle/
│   │   └── ... (Oracle DbContext yapılandırma dosyaları)
│   ├── postgresql/
│   │   └── ... (PostgreSQL DbContext yapılandırma dosyaları)
│   └── redis/
│       └── ... (Redis DbContext yapılandırma dosyaları)
├── libraries/
│   ├── messaging/
│   │   └── ... (Mesajlaşma kütüphane dosyaları)
│   ├── caching/
│   │   └── redis/
│   │       └── ... (Redis önbellekleme kütüphane dosyaları)
│   ├── DependencyInjection/
│   │   └── Autofac/
│   │       └── ... (Autofac bağımlılık enjeksiyonu dosyaları)
│   ├── Validation/
│   │   └── FluentValidation/
│   │       └── ... (FluentValidation doğrulama dosyaları)
│   └── Mapping/
│       └── AutoMapper/
│           └── ... (AutoMapper eşleme dosyaları)
├── patterns/
│   ├── repository/
│   │   ├── IRepository.cs
│   │   └── Repository.cs
│   ├── unitofworks/
│   │   ├── IUnitOfWork.cs
│   │   └── UnitOfWork.cs
│   └── saga/
│       ├── event/
│       │   └── ... (Saga event dosyaları)
│       ├── consumers/
│       │   └── ... (Saga consumer dosyaları)
│       ├── sagainstance/
│       │   └── ... (Saga instance dosyaları)
│       ├── sagamachine/
│       │   └── ... (Saga machine dosyaları)
│       ├── sagamap/
│       │   └── ... (Saga map dosyaları)
│       ├── sagadbcontext/
│       │   └── ... (Saga DbContext yapılandırma dosyaları)
│       ├── rabbitmqsettings/
│       │   └── ... (RabbitMQ ayar dosyaları)
│       └── Program.cs (Saga program başlangıç dosyası)
└── README.md
```


Bu proje, .NET geliştiricilerinin yaygın olarak karşılaştığı sorunlara çözüm sunan ve geliştirme sürecini hızlandıran çeşitli yapıları içerir:

* **Veritabanı Yapılandırmaları:**
    * MSSQL, PostgreSQL, Oracle, Redis ve MongoDB için hazır `Program.cs` yapılandırmaları.
    * Entity Framework Core (EF Core) `DbContext` yapılandırması.
* **Mimari Desenler:**
    * Saga Pattern orkestrasyon örnekleri (instance, machine, mapper).
    * Repository ve Unit of Work desenleri için örnekler.
    * Entity ve Enum örnekleri.
* **Entegrasyonlar:**
    * Kuyruk tanımları, event ve consumer tanımları.
    * FluentValidation, AutoMapper ve Autofac kütüphanelerinin entegrasyon kodları.
* **Diğer Yardımcılar:**
    * Çeşitli kod parçacıkları ve hazır şablonlar.
    * Docker ve Docker-compose yapılandırmaları.

## Kullanım

1.  **Projeyi Klonlayın:**
    ```bash
    git clone [repo_url]
    ```
2.  **Gerekli Kütüphaneleri Yükleyin:**
    * Projede kullanılan kütüphanelerin (FluentValidation, AutoMapper, Autofac, vb.) NuGet paketlerini yükleyin.
3.  **Veritabanı Yapılandırmalarını Ayarlayın:**
    * `Program.cs` dosyalarındaki veritabanı bağlantı ayarlarını kendi veritabanı bilgilerinize göre düzenleyin.
4.  **EF Core Yapılandırması:**
    * Ef core Dbcontext yapısını kendi proje yapınıza göre düzenleyiniz.
5.  **Mimari Desenleri Uygulayın:**
    * Repository, Unit of Work ve Saga Pattern örneklerini projenizde kullanabilirsiniz.
6.  **Entegrasyonları Kullanın:**
    * Kuyruk, event ve consumer tanımlarını kendi projenize entegre edin.
    * FluentValidation, AutoMapper ve Autofac entegrasyon kodlarını projenizde kullanın.
7.  **Docker Kullanımı:**
    * Docker ve Docker-compose yapılandırmalarını kendi proje yapınıza göre düzenleyiniz.
    * Docker compose ile ayağa kaldırınız.

