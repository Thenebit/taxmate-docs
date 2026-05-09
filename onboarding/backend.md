# Backend Setup — TaxSmart GH

## Prerequisites

- Git
- Docker & Docker Compose

That's it. No Python, no Postgres, no Redis to install locally.

## First Time Setup

```bash
# 1. Clone the repo
git clone https://github.com/thexistech/taxsmart-backend.git
cd taxsmart-backend

# 2. Create your env file
cp .env.example .env

# 3. Build and start everything
docker compose up --build
```

## What's Running

| Service | URL / Port | Purpose |
|---------|-----------|---------|
| API | http://localhost:8000 | FastAPI backend |
| API Docs | http://localhost:8000/docs | Swagger UI |
| PostgreSQL | localhost:5432 | Database |
| Redis | localhost:6379 | Queues & cache |
| Celery Worker | — | Background jobs (GRA filing, reminders) |
| Celery Beat | — | Scheduled tasks |
| Mailhog | http://localhost:8025 | Dev email catcher |

## Common Commands

```bash
# Start the stack
docker compose up

# Start in background
docker compose up -d

# Stop everything
docker compose down

# Rebuild after changing requirements
docker compose up --build

# View logs
docker compose logs api --tail 50
docker compose logs worker --tail 50

# Run tests
docker compose exec api python -m pytest tests -v --rootdir /code

# Run a specific test file
docker compose exec api python -m pytest tests/test_auth/ -v --rootdir /code

# Open a Python shell inside the API container
docker compose exec api python

# Run database migrations
docker compose exec api alembic upgrade head

# Create a new migration
docker compose exec api alembic revision --autogenerate -m "describe the change"

# Reset the database (destroys all data)
docker compose down -v
docker compose up --build
```

## Project Structure
{I WILL DO THIS LATER}

## Module Pattern

Every feature module follows the same structure:
app/transactions/
├── router.py    # Endpoints (HTTP layer)
├── schemas.py   # Request/response models (Pydantic)
├── models.py    # Database tables (SQLModel)
└── service.py   # Business logic (router calls this)

**Rule:** routers call services, services call the database. Routers never touch the DB directly.

## Environment Variables

See `.env.example` for all required variables. Key ones:
POSTGRES_USER=         # DB username
POSTGRES_PASSWORD=     # DB password
POSTGRES_DB=           # DB name
DB_HOST=               # db (Docker service name)
DB_PORT=               # 5432
REDIS_URL=             # redis://redis:6379/0
SECRET_KEY=            # JWT signing key

## Troubleshooting

**API won't start:**
```bash
docker compose logs api --tail 30
```

**DB connection refused:**
The database might not be ready yet. The healthcheck handles this, but if it persists:
```bash
docker compose down
docker compose up --build
```

**Tests failing with import errors:**
Make sure you're running from inside the container, not your local machine.

**Need a clean slate:**
```bash
docker compose down -v
docker compose up --build
```
The `-v` flag removes the database volume, so all data is wiped.
