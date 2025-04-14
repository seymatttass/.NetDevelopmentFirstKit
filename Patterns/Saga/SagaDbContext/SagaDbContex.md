* OrderStateDbContext: Saga Durum Veritabanı Bağlamı
* Bu sınıf, MassTransit ile kullanılan Saga deseninde, sipariş süreçlerinin (Order Saga) durumlarını veritabanında saklamak için özel olarak yapılandırılmış bir DbContext'tir.

```razor
namespace SagaStateMachine.Service.StateDbContext
{
    public class OrderStateDbContext : SagaDbContext
    {
        public OrderStateDbContext(DbContextOptions options) : base(options)
        {
        }

        protected override IEnumerable<ISagaClassMap> Configurations
        {
            get
            {

                yield return new OrderStateMap();
            }
        }

    }
}
```
