* Controller Configuration

* GET – api/basket/
```razor
[HttpGet]
public async Task<ActionResult<IEnumerable<Baskett>>> GetBaskets()
{
    var baskets = await _basketService.GetAllAsync();
    return Ok(baskets); // Tüm sepetleri döndürür
}
```
* Sepet verilerini IBasketService üzerinden alır.

* GET – api/basket/{id}
```razor
[HttpGet("{id}")]
public async Task<ActionResult<Baskett>> GetBasket(int id)
{
    var basket = await _basketService.GetByIdAsync(id);

    if (basket == null)
    {
        return NotFound(); // Sepet bulunamadığında 404 döner
    }

    return Ok(basket); // Sepeti başarıyla döner
}
```

* userId ile sepeti arar ve bulamazsa 404 Not Found döner.

* POST – api/basket/items
```razor
[HttpPost("items")]
public async Task<ActionResult<BasketItem>> AddBasketItem(CreateBasketItemDTO itemDto)
{
    if (itemDto.ProductId <= 0)
    {
        return BadRequest("ProductId is required"); // ProductId geçerli değilse hata döner
    }

    var basketItem = await _basketItemService.AddAsync(itemDto); // Sepete ürün ekleniyor

    var productAddedEvent = new ProductAddedToBasketRequestEvent()
    {
        ProductId = basketItem.ProductId,
        Count = basketItem.Count,
        Price = basketItem.Price
    };

    await _publishEndpoint.Publish(productAddedEvent); // Ürün sepete eklendikten sonra event yayınlanıyor

    return CreatedAtAction("GetBasketItem", "BasketItem", new { id = basketItem.ID }, basketItem); // Yeni ürün ile yanıt
}

* sepete yeni bir ürün ekler. Ürün başarıyla eklendikten sonra, ilgili event (ProductAddedToBasketRequestEvent) yayınlanır.

```
