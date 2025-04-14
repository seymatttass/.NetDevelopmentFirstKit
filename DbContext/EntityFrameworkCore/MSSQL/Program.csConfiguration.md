* MSSQL  - Gerekli mssql paketini indirelim. 
```razor
dotnet add package Microsoft.EntityFrameworkCore.SqlServer
```

* DbContext - MSSQL

```razor
builder.Services.AddDbContext<ApplicationDbContext>(options =>
{
    options.UseSqlServer(
        configuration.GetConnectionString("DefaultConnection"),
});

```

* MSSQL - appsettings.json yapılandırması
```razor
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=localhost;Database=SeninVeritabaniIsmin;User Id=KullaniciAdin;Password=Sifren;"
  }
}
```
