* RabbitMQ Kuyruk Ayarları
* Bu sınıf, sistem içerisindeki farklı microservice'lerin dinleyeceği RabbitMQ kuyruk isimlerini merkezi olarak yönetmek için kullanılır. Böylece kuyruk adları sabit ve tutarlı kalmış olur.

```razor
namespace Shared.Settings
{
    public static class RabbitMQSettings
    {
        public const string StateMachineQueue = "state-machine-queue";
        public const string Stock_CheckStockQueue = "stock-check-stock-queue";
        public const string Order_OrderCreatedQueue = "order-order-created-queue";
        public const string Order_OrderFailedQueue = "order-order-failed-queue";
        public const string Order_OrderCompletedQueue = "order-order-completed-queue";  
        public const string Basket_ProductAddedToBasketQueue = "basket-add-to-basket-queue"; 
        public const string Basket_BasketFailedEventQueue = "basket-basket-failed-item-added-queue"; 
        
    }
}
```  
