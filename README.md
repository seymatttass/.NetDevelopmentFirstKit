# .NetDevelopmentFirstKit

.NET tabanlı uygulama geliştirme sürecini kolaylaştırmak ve hızlandırmak için oluşturulmuş, hazır şablonlar, kod parçacıkları, veritabanı bağlantı yardımcıları ve daha fazlasını içeren bir başlangıç kitidir.

## İçindekiler

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


## İletişim

Sorularınız veya geri bildirimleriniz için lütfen [e-posta adresiniz] ile iletişime geçin.
