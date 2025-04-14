* Bu sınıf, sipariş sürecini yöneten bir Saga State Machine'dir. Kullanıcının sepete ürün eklemesiyle başlayan süreçte, önce stok kontrolü yapılır. Stok yeterliyse ödeme süreci başlatılır ve ödeme tamamlandığında sipariş oluşturulur. Stok yetersizse veya ödeme başarısız olursa, süreç hata durumu ile sonlandırılır. Her adım bir durum (state) olarak takip edilir ve servisler arası iletişim RabbitMQ kuyruklarıyla sağlanır. Bu yapı, mikroservisler arasında tutarlı ve yönetilebilir bir akış sunar.

```razor
using MassTransit;
using SagaStateMachine.Service.StateInstances;
using Shared.Events.BasketEvents;
using Shared.Events.StockEvents;
using Shared.Events.OrderCreatedEvent;
using Shared.Events.OrderFailedEvent;
using Shared.Message;
using Shared.Settings;

namespace SagaStateMachine.Service.StateMachines
{
    public class OrderStateMachine : MassTransitStateMachine<OrderStateInstance>
    {
        public State ProductAdded { get; private set; }
        public State StockReserved { get; private set; }
        public State StockNotReserved { get; private set; }
        public State OrderCreated { get; private set; }
        public State OrderFailed { get; private set; }

        public Event<ProductAddedToBasketRequestEvent> ProductAddedToBasketRequestEvent { get; private set; }
        public Event<StockReservedEvent> StockReservedEvent { get; private set; }
        public Event<StockNotReservedEvent> StockNotReservedEvent { get; private set; }

        public OrderStateMachine()
        {
            InstanceState(x => x.CurrentState);

            Event(() => ProductAddedToBasketRequestEvent,
                x => x.CorrelateById(e => e.Message.CorrelationId).SelectId(e => Guid.NewGuid()));

            Event(() => StockReservedEvent,
                x => x.CorrelateById(e => e.Message.CorrelationId));

            Event(() => StockNotReservedEvent,
                x => x.CorrelateById(e => e.Message.CorrelationId));

            Initially(
                When(ProductAddedToBasketRequestEvent)
                    .Then(context =>
                    {
                        context.Instance.UserId = context.Data.UserId;
                        context.Instance.TotalPrice = context.Data.Price * context.Data.Count;
                        context.Instance.ProductId = context.Data.ProductId;
                        context.Instance.Count = context.Data.Count;
                        context.Instance.Price = context.Data.Price;
                        context.Instance.BasketId = context.Data.BasketId;
                        context.Instance.CreatedDate = DateTime.UtcNow;
                    })
                    .TransitionTo(ProductAdded)
                    .Send(new Uri($"queue:{RabbitMQSettings.Stock_CheckStockQueue}"),
                        context => new StockCheckedEvent(context.Instance.CorrelationId)
                        {
                            ProductId = context.Instance.ProductId,
                            Count = context.Instance.Count
                        })
            );

            During(ProductAdded,
                When(StockReservedEvent)
                    .TransitionTo(StockReserved)
                    .Send(new Uri($"queue:{RabbitMQSettings.Order_OrderCreatedQueue}"),
                        context => new CreateOrderCommand(context.Instance.CorrelationId)
                        {
                            UserId = context.Instance.UserId,
                            BasketId = context.Instance.BasketId,
                            TotalPrice = context.Instance.TotalPrice,
                            BasketItemMessages = new List<BasketItemMessage>
                            {
                                new BasketItemMessage
                                {
                                    ProductId = context.Instance.ProductId,
                                    Count = context.Instance.Count,
                                    Price = context.Instance.Price
                                }
                            }
                        }),


                When(StockNotReservedEvent)
                    .TransitionTo(StockNotReserved)
                    .Send(new Uri($"queue:{RabbitMQSettings.Order_OrderFailedQueue}"),
                        context => new OrderFailEvent(context.Instance.CorrelationId)
                        {
                            OrderId = context.Instance.OrderId,
                            Message = "Stok yetersiz."
                        })
            );

            SetCompletedWhenFinalized();
        }
    }
}

```
