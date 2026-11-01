# 🚀 N8n + Postgres + PgAdmin Boilerplate (Docker Setup)

A ready-to-use Docker Compose configuration for running [n8n](https://n8n.io/) — a powerful open-source workflow automation tool — with a **PostgreSQL database** and **PgAdmin** interface. Perfect for local testing, development, and automating personal or business tasks using AI workflows or custom automations.

## 📦 Pinned versions

| Service  | Image                    | Notes                                  |
|----------|--------------------------|----------------------------------------|
| n8n      | `n8nio/n8n:2.46.3`       | latest stable 2.x (use `1.123.91` for the 1.x line) |
| Postgres | `postgres:17.11`         | PG 17 LTS line                         |
| pgAdmin  | `dpage/pgadmin4:9.19`    |                                        |

## 🔧 Features

- 🧠 Run **n8n** locally with basic authentication
- 🐘 **PostgreSQL** as persistent storage, with healthcheck-gated startup
- 🛠 **PgAdmin** for DB management (server mode disabled for local use)
- 🛡 Environment-based configuration via `.env`
- 🩺 Container **healthchecks** — n8n/pgAdmin only start once Postgres accepts connections
- ⚙️ Tuned Postgres defaults (`max_connections`, `shared_buffers`, WAL compression) and n8n connection pool settings
- 📦 Easy container management via `docker compose`

## 🚀 Getting started

### 1. Create the environment file

```bash
cp .env.template .env
```

Edit `.env` with your own credentials (user, passwords, host/protocol, timezone).

### 2. Start the stack

```bash
docker compose up -d
```

### 3. Stop / update / cleanup

```bash
docker compose down                 # stop (data kept)
docker compose pull && docker compose up -d --force-recreate   # update images
docker image prune -f              # remove dangling images
docker compose down -v             # ⚠️ DELETE all data in volumes!
```

## 🌍 Services & Access

| Service   | URL                   | Notes                          |
|-----------|-----------------------|--------------------------------|
| **n8n**   | `http://localhost:5678` | basic auth (see `.env`)    |
| **PgAdmin** | `http://localhost:8080` | DB GUI (see `.env`)       |

## 🔌 Connection details

- n8n connects to Postgres over the internal `n8n_net` bridge network (`DB_POSTGRESDB_HOST=postgres`).
- Pool size / timeouts / SSL are set via `DB_POSTGRESDB_POOL_SIZE`, `DB_POSTGRESDB_CONNECTION_TIMEOUT`, `DB_POSTGRESDB_SSL_ENABLED` in `.env`.
- `N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS` **must stay `false` on Windows/Docker Desktop** — it only works on native Linux.

## 📦 Volumes

- `postgres_data` → PostgreSQL data
- `n8n_data`      → n8n workflows & credentials
- `pgadmin_data`  → PgAdmin configuration

## 🤝 Contribute

Feel free to fork, improve or customize this boilerplate. Contributions are welcome — add support for other DBs, external services, or n8n enhancements!
