* AutoMapper Yapılandırması
```razor
using AutoMapper;
using Order.API.Data.Entities;
using Order.API.DTOS.OrderItemDTO.OrderItem;
using Order.API.DTOS.OrdersDTO.Orders;

namespace Order.API.Mapping
{
    public class OrderAutoMapperProfile : Profile
    {
        public OrderAutoMapperProfile()
        {
            CreateMap<CreateOrderItemDTO, OrderItemss>().ReverseMap();
            CreateMap<UpdateOrderItemDTO, OrderItemss>().ReverseMap();

            CreateMap<CreateOrdersDTO, Orderss>().ReverseMap();
            CreateMap<UpdateOrdersDTO, Orderss>().ReverseMap();
        }
    }
}
```
* CreateMap: Bu metod, kaynak ve hedef türleri arasında bir eşleme oluşturur. Örneğin, CreateMap<CreateBasketDTO, Basket>() ifadesi, CreateBasketDTO türündeki veriyi Basket türüne dönüştürür.
* ReverseMap: Bu metod, eşlemeyi iki yönlü yapar. Hem CreateBasketDTO'yu Basket'e hem de Basket'i CreateBasketDTO'ya dönüştürmek için kullanılır.
* DTO'lar ve Entity'ler: DTO'lar genellikle dışa veya içe veri taşımak için kullanılır ve genellikle controller'larda işlenir. Entity'ler ise veritabanı modelini temsil eder.
