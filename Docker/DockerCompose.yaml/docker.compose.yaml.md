* Başlangıç olarak, Docker Compose yapılandırması eklemek için API projenize Docker desteği eklemeniz gerekiyor. Bunun için:
 - API projenizi açın. -->  Proje Sağ Tık yapın. -->  "Docker Support" seçeneğini tıklayın. Bu seçenek, projenize Dockerfile ve docker-compose.yml dosyalarını ekleyecektir.

   
```razor
version: '3.8'
services:
  basketapi:
    container_name: basketapi.dev
    build:
      context: .
      dockerfile: Basket.API/Dockerfile
    ports:
      - "32786:8080"
    networks:
      - microservice-network
  usersapi:
    container_name: usersapi.dev
    build:
      context: .
      dockerfile: Users.API/Dockerfile
    ports:
      - "32788:8080"
    networks:
      - microservice-network
  orderapi:
    container_name: orderapi.dev
    build:
      context: .
      dockerfile: Order.API/Dockerfile
    ports:
      - "32794:8080"
    networks:
      - microservice-network
  sagastatemachineservice:
    container_name: sagastatemachineservice.dev
    build:
      context: .
      dockerfile: SagaStateMachine.Service/Dockerfile
    networks:
      - microservice-network
  redis:
    container_name: redis
    image: redis:latest
    ports:
      - "6379:6379"
    networks:
      - microservice-network
networks:
  microservice-network:
    driver: bridge

```
