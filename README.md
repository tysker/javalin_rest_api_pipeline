# Java REST API with CI/CD & Traefik Deployment

## Overview

This project demonstrates how to design, build, and deploy a **production-ready Java REST API** with a fully automated **CI/CD pipeline** and container-based infrastructure, where changes are built, tested, and deployed without manual intervention.

The focus is not only on API implementation, but on the **end-to-end delivery lifecycle**: clean backend architecture, automated testing, containerization, secure routing, and zero-touch deployment.

---

## Status & CI/CD

![Build](https://img.shields.io/github/actions/workflow/status/tysker/javalin_rest_api_pipeline/deploy.yml?branch=main&style=for-the-badge)
![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Javalin](https://img.shields.io/badge/Javalin-5.x-3C9BE4?style=for-the-badge)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Traefik](https://img.shields.io/badge/Traefik-24A1C1?style=for-the-badge&logo=traefikproxy&logoColor=white)

---

## What This Project Demonstrates

- Clean, layered **Java backend architecture** (DAO → Service → Controller)
- REST API design with validation and structured error handling
- **Automated CI/CD pipeline** from Git push to production deployment
- Containerized runtime using Docker and Docker Compose
- Reverse proxy, HTTPS, and routing with **Traefik**
- Environment-based configuration suitable for real deployments

---

## Architecture Overview

```
Developer
   │
   ▼
GitHub Repository
   │
   ▼
GitHub Actions (CI/CD)
   │   - Build & Test
   │   - Build Docker Image
   │   - Push Image
   │   - Deploy via SSH
   ▼
Docker & Docker Compose
   │
   ▼
Traefik (HTTPS & Routing)
   │
   ▼
Java REST API  ──► PostgreSQL
```

---

## Repository Structure

```
src/
├── main/java/
│   ├── controllers/      # HTTP endpoints
│   ├── daos/             # Persistence layer
│   ├── services/         # Business logic
│   ├── exceptions/       # Centralized error handling
│   ├── security/         # Authentication / access control
│   ├── util/             # Shared utilities
│   └── App.java          # Application entrypoint
│
└── test/
    ├── unit/             # Unit tests
    └── integration/      # Integration tests
```

---

## CI/CD Pipeline

The pipeline is triggered automatically on pushes to the `main` branch and performs:

1. Source checkout
2. Build and test execution (`mvn package`)
3. Docker image build
4. Image push to registry
5. Remote deployment via SSH
6. Zero-downtime restart using Docker Compose

This ensures that every change is **tested, packaged, and deployed automatically**.

---

## Deployment Stack

### Backend

- Java
- Javalin
- PostgreSQL
- JUnit

### DevOps & Infrastructure

- Docker & Docker Compose
- Traefik (reverse proxy & HTTPS)
- GitHub Actions (CI/CD)
- Linux server (cloud VM)

---

## Local Development

Build and run locally:

```bash
mvn clean package
java -jar target/app.jar
```

Application runs at:

```
http://localhost:7000
```

---

## API Example

### GET /api/users

Returns a list of users.

### POST /api/users

Creates a new user.

```json
{
  "username": "john",
  "password": "secret"
}
```

---

## Error Handling

The API returns structured error responses for predictable client behavior:

```json
{
  "status": "error",
  "message": "User not found",
  "path": "/api/users/999",
  "timestamp": "2025-01-20T10:15:14Z"
}
```

---

## Why This Matters

This project reflects how backend services are built and operated in **real production environments**:

- Automated delivery instead of manual deployments
- Infrastructure-aware backend design
- Secure routing and HTTPS by default

It serves as a **practical reference** for building and shipping backend services reliably.

---

## Disclaimer

This project is a **demonstration and learning project** designed to showcase backend and DevOps practices. While simplified, the patterns and workflows mirror those used in real-world production systems.
