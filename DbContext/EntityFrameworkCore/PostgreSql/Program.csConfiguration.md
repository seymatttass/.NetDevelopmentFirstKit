* DbContext - PostgreSql
* pgsql.EntityFrameworkCore.PostgreSQL paketini yükleyelim.

```razor
dotnet add package Npgsql.EntityFrameworkCore.PostgreSQL
```

* Usingleri ekleyelim.

```razor
using Microsoft.EntityFrameworkCore;
using Microsoft.Extensions.DependencyInject
```
```razor
builder.Services.AddDbContext<ApplicationDbContext>(options =>
{
    options.UseNpgsql(
        configuration.GetConnectionString("DefaultConnection"),
});
```

* PostgreSql - appsetting.json
```razor
{
  "ConnectionStrings": {
    "DefaultConnection": "Host=localhost;Port=5432;Database=SeninVeritabaniIsmin;Username=KullaniciAdin;Password=Sifren"
  }
}

```
