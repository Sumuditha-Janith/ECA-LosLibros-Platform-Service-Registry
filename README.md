# 🧭 LosLibros - Eureka Service Registry

[![Java](https://img.shields.io/badge/Java-25-orange.svg)](https://openjdk.org/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-4.1.0-brightgreen.svg)](https://spring.io/projects/spring-boot)
[![Spring Cloud Netflix Eureka](https://img.shields.io/badge/Spring%20Cloud-Netflix%20Eureka%20Server-blue.svg)](https://spring.io/projects/spring-cloud-netflix)

The **Service Registry** is a core platform infrastructure component powered by **Spring Cloud Netflix Eureka**. It serves as the phonebook and discovery hub for all distributed services and API gateways in the LosLibros ecosystem.

---

## 🌟 Features

- **Service Registration & Discovery**: Allows microservices to dynamically register themselves with random/ephemeral ports upon startup.
- **Heartbeat & Health Monitoring**: Periodically checks instance health and evicts unavailable services.
- **Dynamic Load Balancing Support**: Supplies the API Gateway (`api-gateway`) with real-time instance metadata for client-side routing (`lb://<SERVICE_NAME>`).
- **Eureka Web Dashboard**: Provides a visual interface to monitor registered instances, UP/DOWN statuses, and system replicas.

---

## 🏗️ Technical Details

- **Service Name**: `service-registry`
- **Default Port**: `9001`
- **Configuration Source**: Fetched centrally from Config Server (`http://localhost:9000` or `http://config.platform:9000`).
- **Eureka Dashboard URL**: `http://localhost:9001`

### Registered Microservices

| Application Name | Typical Instances | Description |
| :--- | :--- | :--- |
| `API-GATEWAY` | 1+ | Spring Cloud Gateway proxy |
| `BOOK-SERVICE` | 1+ | Book catalog service instances |
| `MEMBER-SERVICE` | 1+ | Member management service instances |
| `BORROWING-SERVICE` | 1+ | Lending & borrowing transaction service instances |

---

## 🚀 Running the Service Registry

> **Important**: Ensure the **Config Server** (Port `9000`) is running prior to starting the Service Registry.

### Launch via Maven Wrapper

```bash
cd platform/service-registry
./mvnw spring-boot:run
```

### Launch via Built JAR

```bash
./mvnw clean package -DskipTests
java -jar target/Service-Registry-1.0.0.jar
```

---

## 🖥️ Accessing the Eureka Dashboard

Open a web browser and navigate to:
```
http://localhost:9001
```

The dashboard displays:
- System Status (Environment, Data Center, Current Time, Uptime)
- DS Replicas
- Instances currently registered with Eureka
- General Info (Memory, CPU usage, Renewal threshold)
