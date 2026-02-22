# 🧩 Components

> **Template** — update as project components evolve.

---

## Backend

| Module | Responsibility | Status |
|---|---|---|
| _Ex: `auth/`_ | _Ex: JWT, refresh tokens, login/logout_ | _Ex: ✅ Done_ |
| _Ex: `orders/`_ | _Ex: Order CRUD, approval workflow_ | _Ex: 🔨 In progress_ |
| _Ex: `notifications/`_ | _Ex: Email and webhooks_ | _Ex: 📋 Planned_ |

---

## Frontend

| Component / Page | Responsibility | Status |
|---|---|---|
| _Ex: `LoginForm`_ | _Ex: User authentication_ | _Ex: ✅ Done_ |
| _Ex: `OrdersTable`_ | _Ex: Order listing and filters_ | _Ex: 🔨 In progress_ |

---

## Database

| Table | Purpose | Key Indexes |
|---|---|---|
| _Ex: `users`_ | _Ex: Auth and profile data_ | _Ex: `email` (unique), `created_at`_ |
| _Ex: `orders`_ | _Ex: Orders and their status_ | _Ex: `user_id`, `status`, `created_at`_ |

---

## Infrastructure

| Service | Purpose |
|---|---|
| _Ex: `traefik`_ | _Ex: Reverse proxy, automatic SSL via Let's Encrypt_ |
| _Ex: `postgres`_ | _Ex: Primary database_ |
| _Ex: `redis`_ | _Ex: Session cache and rate limiting_ |

---

> **Note:** This file is a map. For component details, refer to the source code.
