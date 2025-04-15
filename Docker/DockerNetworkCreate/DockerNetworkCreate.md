* Docker da network oluşturmak ve apilerimizi bu networke eklemek için cmd ekranında aşağıdaki işlemleri gerçekleştirmeliyiz.

```razor


docker network create your-microservices-network           // Mikroservisler için özel bir Docker ağı oluşturur

docker-compose up -d                                    // Ana docker-compose dosyasındaki servisleri başlatır ve arkaplanda (detached mode) çalıştırır

docker-compose -f docker-compose.elk.yml up -d       // ELK stack (Elasticsearch, Logstash, Kibana) için ayrı bir docker-compose dosyasıyla servisleri başlatır

docker network inspect microservice-network         // "microservice-network" adlı ağın detaylarını gösterir (bağlı containerlar, IP aralığı vb.)

docker network connect microservice-network SagaStateMachine.Service    // SagaStateMachine.Service adlı servisi "microservice-network" ağına bağlar  

docker network connect microservice-network Basket.API              // Basket.API adlı servisi "microservice-network" ağına bağlar

docker network connect microservice-network Stock.API        // Stock.API adlı servisi "microservice-network" ağına bağlar


```
