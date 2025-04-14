* OrderStateInstance: Saga Durum Takibi İçin Sipariş Verisi
* Bu sınıf, MassTransit ile kullanılan Saga State Machine'in bir instance'ını temsil edecektir. Her bir işlem (örneğin sipariş) için benzersiz bir "durum" tutacaktır.
* CorrelationId üzerinden takip edilir.
* SagaStateMachine de kullanacağım instance leri eklemem gerekir.

```razor

namespace SagaStateMachine.Service.StateInstances
{
    public class OrderStateInstance : SagaStateMachineInstance
    {
        public Guid CorrelationId { get; set; }
        public string CurrentState { get; set; }
        public int OrderId { get; set; }
        public int BasketId { get; set; }
        public decimal TotalPrice { get; set; }
        public int ProductId { get; set; }
        public int Count { get; set; }
        public decimal Price { get; set; }
    }
}

```
