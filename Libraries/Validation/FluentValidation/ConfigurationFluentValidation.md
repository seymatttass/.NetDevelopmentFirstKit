* FluentValidation Configuration

```razor
using FluentValidation;
using Order.API.DTOS.OrderItemDTO.OrderItem;

namespace Order.API.DTOS.OrderItemDTO.Validators
{
// CreateOrderItemDTO nesnesi için doğrulama kurallarını tanımlıyoruz
    public class CreateOrderItemValidator : AbstractValidator<CreateOrderItemDTO>
    {
        public CreateOrderItemValidator()
        {
            RuleFor(x => x.ProductId)
                .GreaterThan(0).WithMessage("ProductId must be greater than zero.");

            RuleFor(x => x.ShippingId)
                .GreaterThan(0).WithMessage("ShippingId must be greater than zero.");

            RuleFor(x => x.Count)
                .GreaterThan(0).WithMessage("Count must be at least 1.");

            RuleFor(x => x.TotalPrice)
                .GreaterThan(0).WithMessage("TotalPrice must be a positive value.");
        }
    }
}
```
//Faydaları 
* Hata mesajlarını özelleştirmek oldukça kolaydır.
* Tekrarlayan Kodları Azaltır
* Tekrarlayan Kodları Azaltır
