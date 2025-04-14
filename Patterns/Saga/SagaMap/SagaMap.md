* OrderStateMap: Order Saga Verisinin EF Core ile Eşleştirilmesi
* Bu sınıf, OrderStateInstance nesnesinin Entity Framework Core ile veritabanında nasıl haritalanacağını (mapping) tanımlar.

```razor
namespace SagaStateMachine.Service.StateMap
{
    public class OrderStateMap : SagaClassMap<OrderStateInstance>
    {
        protected override void Configure(EntityTypeBuilder<OrderStateInstance> entity, ModelBuilder model)
        {
            entity.Property(x => x.OrderId)
                .IsRequired();
            entity.Property(x => x.TotalPrice)
                .HasDefaultValue(0);
        }
    }
}

```
