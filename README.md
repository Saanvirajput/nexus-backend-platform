# 🍃 Nexus: Enterprise Spring Boot Microservices Platform

![Nexus Hero Banner](./assets/nexus_spring_hero_banner_1777060765269.png)

Nexus is a production-grade backend architecture built with **Spring Boot**, **Kotlin**, and **MyBatis**. It demonstrates advanced design patterns including **DDD (Domain-Driven Design)**, **CQRS**, and **Clean Architecture** to provide a scalable foundation for enterprise-level applications.

## 🌐 Live Demo

- **Live API Portal**: [https://saanvirajput.github.io/nexus-backend-platform/](https://saanvirajput.github.io/nexus-backend-platform/)

## 🏛️ Architectural Design

Nexus follows a strict layer separation to ensure maintainability and testability:

```mermaid
graph TD
    API[API Layer - Spring MVC] --> Core[Core Domain Layer]
    API --> App[Application Query Layer]
    Core --> Infra[Infrastructure Layer]
    App --> Infra
    Infra --> DB[(SQLite / PostgreSQL)]
    
    subgraph "Domain Driven Design"
    Core
    App
    end
```

## ⚡ Core Technologies

- **Framework**: Spring Boot 2.7+ (Java 11/17)
- **Persistence**: MyBatis (Data Mapper Pattern)
- **Database**: SQLite (Development) / PostgreSQL (Production)
- **API**: RESTful Endpoints + GraphQL (via Netflix DGS)
- **Security**: Spring Security + JWT Stateless Authentication
- **Patterns**: CQRS for Read/Write separation, DDD for business logic

## 🔒 Authentication Flow

```mermaid
sequenceDiagram
    participant C as Client
    participant A as Auth Filter
    participant S as Spring Security
    participant D as Database

    C->>A: POST /users/login (Credentials)
    A->>D: Find User by Email
    D-->>A: User Hash + Data
    A->>A: Verify Password
    A->>C: Return JWT Token
    
    Note over C,D: Subsequent Requests
    C->>A: GET /articles (Header: Authorization: Token <JWT>)
    A->>A: Validate JWT
    A->>S: Set Security Context
    S->>C: Return Protected Resource
```

## 🚀 Getting Started

### Prerequisites
- Java 11 or higher
- Docker (optional)

### Installation
```bash
./gradlew bootRun
```

### Build & Test
```bash
./gradlew build
./gradlew test
```

## 🐳 Docker Deployment

Build a local image and run it:
```bash
./gradlew bootBuildImage --imageName nexus-backend
docker run -p 8080:8080 nexus-backend
```

---
*Developed and Architected by Saanvi Rajput.*
