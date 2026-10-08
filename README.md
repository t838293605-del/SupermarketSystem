# Shelfwise

Shelfwise is a supermarket inventory management and stock warning system for a single store. It is a modular monolith built with Spring Boot and Vue 3, using MySQL as the system of record and Redis as an optional cache. Every stock change keeps the operator, reason, before/after quantity and an idempotency key, so the inventory history can always be audited.

## Features

- **Catalog**: products, categories and suppliers
- **Stock movements**: receiving, dispatch, corrections and stocktakes with a full audit trail; stock can never go negative and repeated requests are idempotent
- **Batches**: batch receipts, FEFO/FIFO allocation and sellable quantity that excludes expired or quarantined stock
- **Stock warnings**: out of stock, low stock, expiring, expired and slow-moving stock
- **Warning center**: assignment, confirmation, notes and recovery, with a complete action history
- **Purchasing**: replenishment requests, approval and partial receipts
- **Stock reviews**: reviewed stock counts and batch disposal
- **Reports**: dashboard, inventory health and warning analytics
- **Access control**: administrator, manager and clerk roles; session login with CSRF protection

## Tech stack

| Layer | Technology |
|---|---|
| Backend | Java 21, Spring Boot 3.5, Spring Security, Spring Data JPA, Flyway |
| Frontend | Vue 3, TypeScript, Vite 7, Element Plus, Pinia, ECharts |
| Storage | MySQL 8.4, Redis 7.4 |
| Deployment | Docker Compose, Nginx |

## Project structure

```
backend/     Spring Boot API, Flyway migrations and integration tests
frontend/    Vue 3 single-page application
docs/        requirements, API, architecture and deployment notes
scripts/     helper scripts for development, demo data and smoke tests
```

## Quick start with Docker

Requirements: Docker Desktop, or Docker Engine with the Compose plugin. Java, Maven and Node.js are not needed on the host.

```sh
cp .env.example .env            # then edit the passwords
docker compose up -d --build --wait
```

Open http://localhost:5173. With `DEMO_ENABLED=true`, the demo accounts `admin`, `manager` and `clerk` use the `DEMO_PASSWORD` from `.env`. Turn demo seeding off for a real deployment.

## Local development

Requirements: Java 21, Maven 3.9+, Node.js 22 and Docker Compose.

```sh
docker compose up -d --wait mysql redis
./scripts/backend.sh spring-boot:run
# in a second terminal
cd frontend && npm ci && npm run dev
```

The Vite dev server proxies `/api` to `localhost:8080`. `python3 scripts/seed-demo.py` adds more demo data through the API.

## Tests

```sh
./scripts/backend.sh test                                     # needs Docker for Testcontainers
cd frontend && npm ci && npm run check && npm test && npm run build
```

## Documentation

- [Requirements](docs/requirements.md)
- [API](docs/api.md)
- [Architecture](docs/architecture.md)
- [Warning and inventory rules](docs/warning-expansion.md)
- [Deployment and recovery](docs/deployment.md)

## License

[MIT](LICENSE)
