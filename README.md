# Shelfwise

Shelfwise is a supermarket inventory management and stock warning system for a single store. Every stock change keeps the operator, reason, before/after quantity and an idempotency key.

- Backend: Java 21, Spring Boot 3.5, Spring Security, Spring Data JPA, Flyway, MySQL 8.4, Redis 7.4
- Frontend: Vue 3, TypeScript, Vite, Element Plus, Pinia, ECharts

## Quick start with Docker

Requirements: Docker Desktop, or Docker Engine with the Compose plugin.

```sh
cp .env.example .env            # then edit the passwords
docker compose up -d --build --wait
```

Open http://localhost:5173. With `DEMO_ENABLED=true`, the demo accounts `admin`, `manager` and `clerk` use the `DEMO_PASSWORD` from `.env`.

## Local development

Requirements: Java 21, Maven 3.9+, Node.js 22 and Docker Compose.

```sh
docker compose up -d --wait mysql redis
./scripts/backend.sh spring-boot:run
# in a second terminal
cd frontend && npm ci && npm run dev
```

See [deployment](docs/deployment.md) for operations, backups and recovery.
