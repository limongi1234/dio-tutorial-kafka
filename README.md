# Tutorial Kafka — DIO x ExpertosTech 🔄

> 🔱 **Fork** de um tutorial da [DIO](https://www.dio.me) em parceria com a ExpertosTech, originalmente criado por **Rodrigo Tavares**. Repositório mantido aqui para **estudo e referência** — o código pertence ao autor original.

Tutorial de **arquitetura orientada a eventos** com **Apache Kafka** e **Spring Boot**, demonstrando a comunicação assíncrona entre dois microsserviços através de um broker de mensagens.

## 🧩 Arquitetura

O projeto é dividido em dois módulos que se comunicam via Kafka:

| Módulo | Papel |
|--------|-------|
| **tutorial-rest-kafka** | API REST que recebe pedidos (`POST /api/salva-pedido`) e **publica** o evento no Kafka (*producer*) |
| **tutorial-microsservico-kafka** | Microsserviço que **consome** os eventos do Kafka e processa/salva o pedido (*consumer*) |

O fluxo: a API REST recebe um pedido → publica no tópico Kafka → o microsserviço consome e processa, de forma desacoplada.

> O diagrama da arquitetura está em `Arquitetura-Eventos.drawio`.

## 🛠️ Tecnologias

![Java](https://img.shields.io/badge/Java-ED8B00?style=flat&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=flat&logo=springboot&logoColor=white)
![Apache Kafka](https://img.shields.io/badge/Apache_Kafka-231F20?style=flat&logo=apachekafka&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white)

- **Java + Spring Boot** (Spring Web, **Spring Kafka**)
- **Apache Kafka** + **Zookeeper** (via Docker Compose — imagens Bitnami)

## 🚀 Como executar

```bash
git clone https://github.com/limongi1234/dio-tutorial-kafka.git
cd dio-tutorial-kafka

# 1. suba o Kafka e o Zookeeper
docker-compose up -d

# 2. em terminais separados, rode cada módulo
cd tutorial-rest-kafka && ./mvnw spring-boot:run
cd tutorial-microsservico-kafka && ./mvnw spring-boot:run
```

Envie um pedido para a API REST:

```bash
curl -X POST http://localhost:8080/api/salva-pedido \
  -H "Content-Type: application/json" \
  -d '{"id": 1, "produto": "exemplo", "valor": 100}'
```

> 📚 Material de estudo sobre mensageria e microsserviços com Kafka (DIO / ExpertosTech).
