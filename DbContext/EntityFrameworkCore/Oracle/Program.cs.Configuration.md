* Oracle - Eklenmesi gereken paketler.
  
```razor
dotnet add package Oracle.EntityFrameworkCore   
```

* DbContext - Oracle

```razor
builder.Services.AddDbContext<ApplicationDbContext>(options =>
{
    options.UseOracle(
        configuration.GetConnectionString("DefaultConnection"),
});
```
