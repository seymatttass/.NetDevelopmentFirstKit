* Basket Entity

```razor
    public class Baskett
    {
        [Key]
        [DatabaseGenerated(DatabaseGeneratedOption.Identity)]
        public int ID { get; set; }
        public int UserId { get; set; }
        public decimal TotalPrice { get; set; }
        public List<BasketItem> BasketItems { get; set; } = new List<BasketItem>();
    }

    public class BasketItem
    {
        [Key]
        [DatabaseGenerated(DatabaseGeneratedOption.Identity)]
        public int ID { get; set; }
        public decimal Price { get; set; }
        public int Count { get; set; }
        public int BasketID { get; set; }
        public int ProductId { get; set; }
    }
```

* Order Entity

```razor
    public class Orderss    
    {
        [Key]
        [DatabaseGenerated(DatabaseGeneratedOption.Identity)]
        public int ID { get; set; }
        public int UserId { get; set; } 
        public int BasketId { get; set; } 
        public int OrderItemId { get; set; }
        public decimal TotalPrice { get; set; }
        public OrdeStatus OrderStatus { get; set; }
        public DateTime CretaedDate { get; set; }   
    }

    public class OrderItemss    
    {
        [Key]
        [DatabaseGenerated(DatabaseGeneratedOption.Identity)]
        public int ID { get; set; }
        public int OrderId { get; set; }
        public int ProductId { get; set; }
        public int ShippingId { get; set; }
        public int Count { get; set; }
        public decimal TotalPrice { get; set; }
    }
```

* Stock Entity

```razor
    public class Stock
    {
        [Key]
        [DatabaseGenerated(DatabaseGeneratedOption.Identity)]
        [Required]
        public int Id { get; set; }

        [Required]
        public int ProductId { get; set; }

        [Required]
        public int Count { get; set; } 

    }
```
