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
