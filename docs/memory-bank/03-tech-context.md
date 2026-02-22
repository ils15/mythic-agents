# 🛠️ Tech Context

> **Template** — fill when setting up the environment. Keep updated when the stack changes.

---

## Full Stack

| Layer | Technology | Version |
|---|---|---|
| Backend | Python + FastAPI | _Ex: 3.12 + 0.115_ |
| Frontend | React + TypeScript | _Ex: 18 + 5.x strict_ |
| ORM | SQLAlchemy + Alembic | _Ex: 2.0 + 1.x_ |
| Database | PostgreSQL | _Ex: 16_ |
| Cache | Redis | _Ex: 7_ |
| Proxy | Traefik | _Ex: 3.x_ |
| Container | Docker + Compose | _Ex: 27.x_ |

---

## Local Setup

```bash
# 1. Clone and enter the repo
git clone <repo-url> && cd <repo-name>

# 2. Copy environment variables
cp .env.example .env
# Edit .env with your local credentials

# 3. Start containers
docker compose up -d

# 4. Run migrations
docker compose exec backend alembic upgrade head

# 5. Verify
curl http://localhost:8000/health
```

---

## Required Environment Variables

| Variable | Description | Required |
|---|---|---|
| `DATABASE_URL` | PostgreSQL connection string | ✅ |
| `SECRET_KEY` | JWT secret key (min. 32 chars) | ✅ |
| `REDIS_URL` | Redis connection string | ✅ |
| `SMTP_HOST` | Mail server host | ⚠️ Optional |

---

## Common Commands

```bash
# Run tests
docker compose exec backend pytest --cov=app --cov-report=term-missing

# Create a new migration
docker compose exec backend alembic revision --autogenerate -m "describe change"

# Access database
docker compose exec postgres psql -U postgres <db-name>

# Tail logs
docker compose logs -f backend
```

---

## CI/CD Requirements

_Ex: GitHub Actions with steps: lint → test (80% coverage minimum) → build → deploy._

---

> **Note:** For agent framework prerequisites, refer to the `copilot-agents` README.
