* Stok consumer

```razor
    public class StockCheckedEventConsumer(StockDbContext stockDbContext, ISendEndpointProvider sendEndpointProvider) : IConsumer<StockCheckedEvent>
    {
        public async Task Consume(ConsumeContext<StockCheckedEvent> context)
        {
            var stockCollection = await stockDbContext.Stocks
                .AnyAsync(s => s.ProductId == context.Message.ProductId && s.Count >= context.Message.Count);
            var sendEndpoint = await sendEndpointProvider.GetSendEndpoint(new Uri($"queue:{RabbitMQSettings.StateMachineQueue}"));


            if (stockCollection)
            {
                StockReservedEvent stockReservedEvent = new(context.Message.CorrelationId)
                {
                    BasketItemMessages = new List<BasketItemMessage>
                    {
                        new BasketItemMessage
                        {
                            ProductId = context.Message.ProductId,
                            Count = context.Message.Count
                        }
                    }
                };
                await sendEndpoint.Send(stockReservedEvent);
            }
            else
            {
                StockNotReservedEvent stockNotReservedEvent = new(context.Message.CorrelationId)
                {
                    Message = $"Ürün ID: {context.Message.ProductId} için yeterli stok bulunmuyor."
                };
                await sendEndpoint.Send(stockNotReservedEvent);
            }
        }
    }
```

* Sipariş consumer
  
```razor
    public class CreateOrderCommandConsumer : IConsumer<CreateOrderCommand>
    {
        private readonly OrderDbContext _context;

        public CreateOrderCommandConsumer(OrderDbContext context)
        {
            _context = context;
        }

        public async Task Consume(ConsumeContext<CreateOrderCommand> context)
        {
            var order = new Orderss
            {
                UserId = context.Message.UserId,
                BasketId = context.Message.BasketId,
                TotalPrice = context.Message.TotalPrice,
                CretaedDate = DateTime.UtcNow,
                OrderStatus = Data.Enums.OrdeStatus.Suspend,
            };

            await _context.Orderss.AddAsync(order);
            await _context.SaveChangesAsync();

            foreach (var item in context.Message.BasketItemMessages)
            {
                await _context.OrderItems.AddAsync(new OrderItemss
                {
                    OrderId = order.ID,
                    ProductId = item.ProductId,
                    Count = item.Count,
                    TotalPrice = item.Price * item.Count
                });
            }

            await _context.SaveChangesAsync();

            await context.Publish(new OrderCompletedEvent(context.Message.CorrelationId)
            {
                OrderId = order.ID,
            });
        }
    }




    public class OrderCompletedEventConsumer(OrderDbContext orderDbContext) : IConsumer<OrderCompletedEvent>
    {
        public async Task Consume(ConsumeContext<OrderCompletedEvent> context)
        {
            Order.API.Data.Entities.Orderss order = await orderDbContext.Orderss.FindAsync(context.Message.OrderId);
            if (order != null)
            {
                order.OrderStatus = Data.Enums.OrdeStatus.Completed;
                await orderDbContext.SaveChangesAsync();
            }
        }
    }



    public class OrderFailedEventConsumer(OrderDbContext orderDbContext) : IConsumer<OrderFailEvent>
    {
        public async Task Consume(ConsumeContext<OrderFailEvent> context)
        {
            Order.API.Data.Entities.Orderss order = await orderDbContext.Orderss.FindAsync(context.Message.OrderId);
            if (order != null) 
            {
                order.OrderStatus = Data.Enums.OrdeStatus.Failed;
                await orderDbContext.SaveChangesAsync();
            }
        }
    }



```
