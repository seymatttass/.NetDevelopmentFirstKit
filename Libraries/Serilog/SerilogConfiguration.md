* filebat.yml : 
```razor
filebeat.inputs:
- type: log
  enabled: true
  paths:
    - /logs/*/*.log
  json.keys_under_root: true
  json.add_error_key: true
  json.message_key: message

processors:
  - add_host_metadata: ~
  - add_docker_metadata: ~

output.elasticsearch:
  hosts: ["elasticsearch:9200"]
  indices:
    - index: "microservice-logs-%{+yyyy.MM.dd}"
```


* docker-compose.elk : 
```razor
version: '3.8'

services:
  elasticsearch:
    image: docker.elastic.co/elasticsearch/elasticsearch:8.11.1
    environment:
      - "discovery.type=single-node"
      - "xpack.security.enabled=false"
      - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
    ports:
      - "9200:9200"
    volumes:
      - elasticsearch-data:/usr/share/elasticsearch/data
    networks:
      - elk-network

  kibana:
    image: docker.elastic.co/kibana/kibana:8.11.1
    ports:
      - "5601:5601"
    environment:
      - "ELASTICSEARCH_HOSTS=http://elasticsearch:9200"
    networks:
      - elk-network
    depends_on:
      - elasticsearch

  filebeat:
    image: docker.elastic.co/beats/filebeat:8.11.1
    volumes:
      - ./filebeat.yml:/usr/share/filebeat/filebeat.yml:ro
      - ./logs:/logs:ro
    networks:
      - elk-network
      - default
    depends_on:
      - elasticsearch

networks:
  elk-network:
    driver: bridge
  default:
    external: true
    name: microservice-network

volumes:
  elasticsearch-data:
```


* Program.cs yapılandırmaları tüm api'ler için : 
```razor
using Serilog;
using Serilog.Events;

var builder = WebApplication.CreateBuilder(args);


// Serilog yapılandırması
builder.Host.UseSerilog((hostingContext, loggerConfiguration) =>
    loggerConfiguration
        .MinimumLevel.Information()
        .MinimumLevel.Override("Microsoft", LogEventLevel.Warning)
        .Enrich.FromLogContext()
        .Enrich.WithProperty("ServiceName", "Basket.API")
        .WriteTo.Console()
        .WriteTo.File(
            new Serilog.Formatting.Compact.CompactJsonFormatter(),
            "logs/basket-api-.log",
            rollingInterval: RollingInterval.Day)
);
```
