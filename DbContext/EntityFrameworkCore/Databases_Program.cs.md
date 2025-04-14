// DbContext - PostgreSql

```razor
builder.Services.AddDbContext<ApplicationDbContext>(options =>
{
    options.UseNpgsql(
        configuration.GetConnectionString("DefaultConnection"),
});
```

// DbContext - Oracle

```razor
builder.Services.AddDbContext<ApplicationDbContext>(options =>
{
    options.UseOracle(
        configuration.GetConnectionString("DefaultConnection"),
});
```

// DbContext - MSSQL

```razor
builder.Services.AddDbContext<ApplicationDbContext>(options =>
{
    options.UseSqlServer(
        configuration.GetConnectionString("DefaultConnection"),
});

```

// Redis Cache 

```razor
builder.Services.AddStackExchangeRedisCache(options =>
{
    options.Configuration = configuration.GetConnectionString("RedisConnection");
    options.InstanceName = "YourAppCache:";
});
```
