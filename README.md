# Reactive Identity & Access Management (IAM) Service

A high-performance, non-blocking microservice dedicated to user registration, authentication, and secure token issuance.

## Overview
This service handles the security layer of the ecosystem. Built with **Spring WebFlux** and **R2DBC**, it provides a fully reactive, end-to-end non-blocking pipeline for managing user identities and secure access via JWT.

## Key Technical Features
*   **Fully Reactive Stack**: Built with **Spring WebFlux** to handle high concurrency with a minimal thread count.
*   **Reactive Data Access**: Implements **R2DBC (Reactive Relational Database Connectivity)** for non-blocking communication with **PostgreSQL**, ensuring the application doesn't block on I/O operations.
*   **Modern Java**: Leverages **Java 21** features for improved performance and maintainability.
*   **Secure Token Management**:
    *   Issues **JWT (JSON Web Tokens)** for stateless authentication across the microservice cluster.
    *   Configurable token expiration, issuers, and secure signing keys.
*   **Scalable Architecture**: Designed to be the source of truth for user authentication for both the WebSocket Gateway and the Game Server.

## Tech Stack
*   **Language:** Java 21
*   **Framework:** Spring Boot 3+ (WebFlux)
*   **Persistence:** PostgreSQL with R2DBC
*   **Security:** JWT
*   **Containerization:** Docker

---

## Configuration

The service is configured via `application.yml` or environment variables.

### Local Development Settings
The following parameters are required for local execution:

| Parameter | Default / Example Value |
| :--- | :--- |
| `server.port` | 8083 |
| `spring.r2dbc.url` | `r2dbc:postgresql://[host]:[port]/[db]?currentSchema=[schema]` |
| `jwt_key` | Secure HMAC-SHA signing key |
| `issuer` | `npc_crawler` |
| `jwt_token_exp_date` | Token validity period in milliseconds |

### Logging & Debugging
Detailed R2DBC and SQL logs are enabled for the `io.r2dbc` and `org.springframework.r2dbc` packages to monitor reactive stream behavior and database performance.

---

## Getting Started

### Building with Docker
The service includes an optimized `Dockerfile` for containerized deployment:

```bash
# Build the image
docker build -t iam-service .

# Run the container
docker run -p 8083:8083 -e JWT_KEY=your_very_long_secret_key_here iam-service
```