// DbContext - Oracle

```razor
builder.Services.AddDbContext<ApplicationDbContext>(options =>
{
    options.UseOracle(
        configuration.GetConnectionString("DefaultConnection"),
});
```
