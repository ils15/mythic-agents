# 🏛️ Architecture

> **Template** — fill when starting the project. Update only when the architecture changes.

---

## System Design

<!-- Diagram or description of the main flow. -->

```
Client (React)
     │
     ▼
  Traefik (reverse proxy)
     │
     ├── /api → FastAPI (backend)
     │              │
     │              ├── Services (business logic)
     │              ├── Repositories (DB access)
     │              └── Schemas (Pydantic v2)
     │
     └── / → React (frontend)
```

---

## Core Patterns

| Pattern | Description |
|---|---|
| **Repository Pattern** | All DB access via repositories — no raw queries in route handlers |
| **Async first** | All FastAPI routes are `async def` — no blocking I/O |
| **TDD** | Failing test first (RED → GREEN → REFACTOR) |
| **Migrations** | Alembic for every schema change — never alter tables manually |

---

## Layer Hierarchy

```
Router (HTTP entry point)
  └── Service (business logic, validations, rules)
        └── Repository (pure CRUD, optimized queries)
              └── Model (SQLAlchemy ORM)
```

**Rules:**
- Routers do not access the database directly
- Services do not run SQL queries
- Repositories do not execute business logic

---

## Key Architectural Decisions

<!-- List major decisions that shaped the design. For detailed decisions, see _notes/. -->

| Decision | Rationale |
|---|---|
| _Ex: JWT in httpOnly cookies_ | _Ex: XSS protection; refresh token with 7-day TTL_ |
| _Ex: PostgreSQL_ | _Ex: ACID compliance, JSONB support, geospatial extensions_ |

---

> **See also:** `_notes/` for detailed architectural decision records (ADRs) with context and alternatives.
