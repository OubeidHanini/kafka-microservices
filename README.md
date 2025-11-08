🚀 Kafka Microservices – E-commerce Application

A modern Spring Boot microservices project leveraging Apache Kafka for event-driven communication in an e-commerce context.

📋 Table of Contents

Overview
Project Structure
Architecture
Prerequisites
Getting Started
API Usage
Event Flow
Author


🎯 Overview
This project demonstrates a microservices architecture using Spring Boot and Apache Kafka to build a scalable, event-driven e-commerce application. Each service communicates asynchronously through Kafka topics, ensuring loose coupling and high scalability.

📁 Project Structure
kafka-microservices/
├── base-domains/      # 📦 Shared entities and interfaces
├── order-service/     # 🛒 Creates orders and publishes events to Kafka
├── email-service/     # 📧 Consumes events and sends confirmation emails
├── stock-service/     # 📊 Consumes events and updates inventory
└── README.md
Modules Description
ModulePortDescriptionbase-domains-Shared DTOs, entities, and common interfaces used across all servicesorder-service8081Handles order creation and publishes order events to Kafkaemail-service8082Listens to order events and sends email confirmationsstock-service8083Listens to order events and updates product inventory

🏗️ Architecture
Layered Architecture
🎨 PRESENTATION LAYER
Responsible for:

✅ Performing authentication
✅ Converting JSON data to objects (and vice versa)
✅ Handling HTTP requests
✅ Transferring authentication to the business layer

💼 BUSINESS LAYER
Responsible for:

✅ Performing validation
✅ Performing authorization
✅ Handling business logic and rules

💾 PERSISTENCE LAYER
Responsible for:

✅ Containing storage logic
✅ Fetching objects and translating them into database rows (and vice versa)

🗄️ DATABASE LAYER
Responsible for:

✅ Performing database operations (CRUD)

Software Architecture Diagram
Afficher l'image

📦 Prerequisites
Before running the application, ensure you have the following installed:

☕ Java 17 or higher
📦 Maven 3.x
🐳 Docker (for running Kafka)
🗃️ Database (PostgreSQL/MySQL) - Configure connection in application.properties or application.yml


🚀 Getting Started
1️⃣ Clone the Repository
bashgit clone https://github.com/devflu999/kafka-microservices.git
cd kafka-microservices
2️⃣ Build the Project
bash./mvnw clean install
3️⃣ Start Apache Kafka
Using Docker:
bashdocker run -p 9092:9092 apache/kafka:latest
4️⃣ Configure Database
Update the database connection settings in each service's application.properties or application.yml:
propertiesspring.datasource.url=jdbc:postgresql://localhost:5432/yourdb
spring.datasource.username=yourusername
spring.datasource.password=yourpassword
5️⃣ Run the Services
Open three separate terminals and run each service:
bash# Terminal 1 – Order Service (Port 8081)
./mvnw spring-boot:run -pl order-service

# Terminal 2 – Email Service (Port 8082)
./mvnw spring-boot:run -pl email-service

# Terminal 3 – Stock Service (Port 8083)
./mvnw spring-boot:run -pl stock-service

🔌 API Usage
Create an Order
Endpoint: POST http://localhost:8081/api/orders
Request:
bashcurl -X POST http://localhost:8081/api/orders \
  -H "Content-Type: application/json" \
  -d '{
    "customerId": "123",
    "items": [
      {
        "productId": "P1",
        "quantity": 2
      }
    ]
  }'
Response:
json{
  "orderId": "ORD-123456",
  "status": "CREATED",
  "message": "Order created successfully"
}

🔄 Event Flow
1. Client sends order request
         ↓
2. Order Service creates order
         ↓
3. Order Event published to Kafka
         ↓
    ┌────┴────┐
    ↓         ↓
4. Email     Stock
   Service   Service
    ↓         ↓
5. Send     Update
   Email    Inventory
Detailed Flow:

📝 Order Created – Client submits an order via REST API
📤 Event Published – Order service publishes event to Kafka topic
📧 Email Sent – Email service consumes event and sends confirmation
📊 Stock Updated – Stock service consumes event and updates inventory


🛠️ Technologies Used

Spring Boot – Microservices framework
Apache Kafka – Event streaming platform
Maven – Dependency management
Docker – Containerization
PostgreSQL/MySQL – Database (configurable)


👨‍💻 Author
@devflu999
