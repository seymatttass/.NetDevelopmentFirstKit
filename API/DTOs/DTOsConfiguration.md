* DTOsConfiguration

```razor
{
    public class CreateBasketDTO
    {
        public int UserId { get; set; }
        public List<BasketItem> BasketItems { get; set; }

    }
}
```
```razor
{
    public class UpdateBasketDTO
    {
        [Required]
        public int Id { get; set; } 
        [Required]
        public int UserId { get; set; } 

        [Required]
        public int StockId { get; set; }  

        public List<BasketItem> BasketItems { get; set; } = new List<BasketItem>();
    }
}
```
```razor
{
    public class AddToBasketItemDTO
    {
        public int ProductId { get; set; }
        public int Count { get; set; }
        public decimal Price { get; set; }
    }
}
```

* DTO (Data Transfer Object), uygulamalar arasında veri taşımak için kullanılır. Veritabanı modelleriyle doğrudan çalışmaktan kaçınarak, yalnızca gerekli olan verilerin taşınmasını sağlar ve performansı artırır, güvenliği geliştirir.
