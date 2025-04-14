* Sepet eventleri.

```razor
    public class ProductAddedToBasketRequestEvent : CorrelatedBy<Guid>
    {
        public Guid CorrelationId { get; set; }
        public int ProductId { get; set; }
        public int Count { get; set; }
        public decimal Price { get; set; }
        public int UserId { get; set; }

        public int BasketId { get; set; }

        public List<BasketItemMessage> BasketItemMessages { get; set; }
    }

    public class BasketFailedEvent
    {

        public int BasketId { get; set; }
        public string Message { get; set; }

    }

    public class BasketCompletedEvent : CorrelatedBy<Guid>
    {
        public BasketCompletedEvent(Guid correlationId)
        {
            CorrelationId = correlationId;
        }

        public Guid CorrelationId { get; set; }
        public int BasketId { get; set; }
        public int ProductId { get; set; }
        public int UserId { get; set; }
        public int Count { get; set; }
        public decimal TotalPrice { get; set; }



    }
```

* Stok eventleri.
  
```razor
    public class StockCheckedEvent : CorrelatedBy<Guid>
    {
        public Guid CorrelationId { get; }
        public StockCheckedEvent(Guid correlationId)
        {
            CorrelationId = correlationId;
        }
        public int ProductId { get; set; }
        public int Count { get; set; }
    }

    public class StockNotReservedEvent : CorrelatedBy<Guid>
    {
        public Guid CorrelationId { get; }
        public StockNotReservedEvent(Guid correlationId)
        {
            CorrelationId = correlationId;
        }
        public string Message { get; set; }
    }

    public class StockReservedEvent : CorrelatedBy<Guid>
    {
        public Guid CorrelationId { get; }
        public StockReservedEvent(Guid correlationId)
        {
            CorrelationId = correlationId;
        }
        public List<BasketItemMessage> BasketItemMessages { get; set; }


    }
```




* Sipariş eventleri.


```razor
    public class CreateOrderCommand : CorrelatedBy<Guid>
    {
        public CreateOrderCommand(Guid correlationId)
        {
            CorrelationId = correlationId;
        }

        public Guid CorrelationId { get; set; }
        public int UserId { get; set; }
        public int BasketId { get; set; }
        public decimal TotalPrice { get; set; }
        public List<BasketItemMessage> BasketItemMessages { get; set; }
    }

    public class OrderCompletedEvent : CorrelatedBy<Guid>
    {
        public OrderCompletedEvent(Guid correlationId)
        {
            CorrelationId = correlationId;
        }

        public Guid CorrelationId { get; set; }
        public int OrderId { get; set; }
        public int AddressId { get; set; }

    }

    public class OrderFailEvent : CorrelatedBy<Guid>
    {
        public OrderFailEvent(Guid correlationId)
        {
            CorrelationId = correlationId;
        }
        public int OrderId { get; set; }
        public string Message { get; set; }
        public Guid CorrelationId { get; }
    }


```


















