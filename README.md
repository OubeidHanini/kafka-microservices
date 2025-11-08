Kafka Microservices – E-commerce Application

A Spring Boot microservices project using Apache Kafka for event-driven communication.

Project Structure
kafka-microservices/
├── base-domains/      # Shared entities and interfaces
├── order-service/     # Creates orders and publishes events to Kafka
├── email-service/     # Consumes events and sends confirmation emails
├── stock-service/     # Consumes events and updates inventory
└── README.md

Modules

base-domains: Shared entities and interfaces

order-service: Creates orders and publishes events to Kafka

email-service: Consumes events and sends confirmation emails

stock-service: Consumes events and updates inventory

Requirements

Java 17

Maven

Apache Kafka (running locally)

How to Run
1️⃣ Clone the project
git clone https://github.com/devflu999/kafka-microservices.git
cd kafka-microservices

2️⃣ Build the project
./mvnw clean install

3️⃣ Start Kafka (example with Docker)
docker run -p 9092:9092 apache/kafka:latest

4️⃣ Run services in separate terminals
# Terminal 1 – Order Service
./mvnw spring-boot:run -pl order-service

# Terminal 2 – Email Service
./mvnw spring-boot:run -pl email-service

# Terminal 3 – Stock Service
./mvnw spring-boot:run -pl stock-service

API Example

Create an order:

curl -X POST http://localhost:8081/api/orders \
  -H "Content-Type: application/json" \
  -d '{
    "customerId": "123",
    "items": [{"productId": "P1", "quantity": 2}]
  }'


Flow:
Order created → Event sent → Email sent → Stock updated

Author

@devflu999
Java Developer | Spring Boot | Kafka | Microservices