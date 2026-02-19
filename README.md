# Travel Platform

Travel Platform is a microservices-based application designed to manage travel-related services, including booking, points of interest (POI), user management, itineraries, authentication, and notifications. This platform provides a scalable, modular, and fully observable architecture suitable for production deployment with monitoring, caching, and logging.

## Architecture Overview

The platform is composed of multiple independent microservices, each responsible for a specific domain:

| Service                         | Responsibility                                                                 |
| ------------------------------- | ------------------------------------------------------------------------------ |
| **travel-auth-service**         | Handles user authentication and authorization.                                 |
| **travel-users-service**        | Manages user profiles, preferences, and account information.                   |
| **travel-poi-service**          | Manages Points of Interest (POI) data including storage, search, and indexing. |
| **travel-booking-service**      | Manages bookings for POIs including creation, update, and retrieval.           |
| **travel-itinerary-service**    | Manages travel itineraries and trip planning.                                  |
| **travel-notification-service** | Sends notifications to users (email, SMS, push).                               |


All services are fully independent and communicate over REST APIs. They share common infrastructure components for caching, monitoring, and observability.

## Technologies Used
### Core Frameworks:

- Java 21 – Modern JVM language with strong typing and performance.

- Spring Boot 4.0 – Rapid microservice development with auto-configuration.

- Spring Data JPA – Simplified database interaction.

- Spring Cache + Redis – Distributed caching for improved performance.

- Spring Validation – Input validation for DTOs.

### Databases:

- PostgreSQL – Relational database for transactional data.

- Redis – In-memory caching and session storage.

### Observability & Monitoring:

- Prometheus – Metrics collection.

- Grafana – Visualization and dashboards for metrics.

- Spring Boot Actuator – Health checks, metrics, and application insights.

- Logstash Logback Encoder – Structured JSON logging for monitoring systems.

### Build & DevOps:

- Gradle 9 – Build automation and dependency management.

- Docker & Docker Compose – Containerized services and infrastructure.

- Testcontainers – Integration testing with ephemeral Docker containers.

- Flyway – Database migration and versioning.

### Mapping & Utilities:

- MapStruct – DTO ↔ Entity mapping.

- Lombok – Boilerplate code reduction (getters/setters/builders).

### Testing:

- JUnit 5 – Unit and integration testing.

- Mockito – Mocking for isolated tests.

- Spring Boot Test – Integration tests with Spring context.

## Multi-Module Project Structure
```
travel-platform/
├── travel-auth-service/
├── travel-users-service/
├── travel-poi-service/
├── travel-booking-service/
├── travel-itinerary-service/
├── travel-notification-service/
├── travel-common/        # Optional: shared DTOs, exceptions, utilities
├── build.gradle          # Root build file
├── settings.gradle       # Module inclusion
└── docker-compose.yml    # Centralized deployment with Redis, Prometheus, Grafana
```

Each microservice has its own build.gradle, application.yml, and Docker configuration for complete independence.

## Getting Started
### Prerequisites:

- Java 21 JDK

- Docker & Docker Compose

- Gradle (optional; can use Gradle wrapper)

- Running Locally

### Clone the repository:
```
git clone https://github.com/yourusername/travel-platform.git
cd travel-platform
```

### Build the platform:
```
./gradlew clean build
```

### Start all services and infrastructure via Docker Compose:
```
docker-compose up --build
```

### This will start:

- All microservices (auth, users, poi, booking, itinerary, notification)

- Redis

- Prometheus

- Grafana

### Access services:

- POI Service: http://localhost:8082

- Booking Service: http://localhost:8083

- Prometheus: http://localhost:9090

- Grafana: http://localhost:3000 (default login: `admin/admin`)

## API Endpoints

- POI Service: /api/v1/pois

- Booking Service: /api/v1/bookings

- Auth Service: /api/v1/auth

- User Service: /api/v1/users

- Itinerary Service: /api/v1/itineraries

- Notification Service: /api/v1/notifications

Each service exposes REST endpoints and health checks via Spring Boot Actuator (/actuator/health).

## Best Practices Implemented

- Microservices are independent and deployable.

- Each service has its own database (PostgreSQL).

- Redis caching for performance.

- Prometheus metrics and Grafana dashboards for observability.

- Structured logging for monitoring.

- Centralized Gradle multi-module build for dependency management.

- Integration tests with Testcontainers.

## Monitoring & Logging

- Metrics are exposed at `/actuator/prometheus`.

- Prometheus scrapes metrics from each service.

- Grafana dashboards visualize metrics such as:

- Requests per second

- DB connection pool

- Cache hit/miss rates

- Service health status

- Logging format (JSON) allows aggregation via ELK stack if desired.

## Next Steps / Future Enhancements

- Implement API Gateway (e.g., Spring Cloud Gateway) for unified access.

- Add distributed tracing (e.g., OpenTelemetry, Zipkin).

- Add authentication & authorization (JWT, OAuth2).

- CI/CD pipelines for automated build, test, and deployment.

- Load balancing and service discovery for high availability.

## License

This project is licensed under MIT License. See LICENSE for details.

This README provides developers and operators a full understanding of your platform, technology stack, and how to build/run it.
