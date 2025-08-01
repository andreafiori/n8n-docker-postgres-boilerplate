# 🚀 N8n + Postgres + PgAdmin Boilerplate (Docker Setup)

A ready-to-use Docker Compose configuration for running [n8n](https://n8n.io/) — a powerful open-source workflow automation tool — with a **PostgreSQL database** and **PgAdmin** interface. It's perfect for local testing, development, and automating personal or business tasks using AI workflows or custom automations.

## 🔧 Features

- 🧠 Run **n8n** locally with basic authentication
- 🐘 Use **PostgreSQL** as persistent storage
- 🛠 Access **PgAdmin** for DB management
- 🛡 Environment-based configuration via `.env`
- 📦 Easy container management via `docker-compose`

---

## 🌍 Services & Access

| Service     | URL                      | Notes                          |
|-------------|--------------------------|--------------------------------|
| **n8n**     | http://localhost:5678    | Access your workflows          |
| **PgAdmin** | http://localhost:8080    | DB GUI (use `.env` credentials)|

---


## 📁 Environment Configuration

Copy the template and configure your environment variables:

```bash
cp .env.template .env
```

Edit the .env file with your own credentials:

```
	# PostgreSQL configuration
	POSTGRES_USER=postgres
	POSTGRES_PASSWORD=postgres
	POSTGRES_DB=n8n

	# pgAdmin configuration
	PGADMIN_EMAIL=admin@example.com
	PGADMIN_PASSWORD=adminpass

	# n8n configuration
	N8N_USER=mymail@example.com
	N8N_PASSWORD=admin
	N8N_HOST=localhost
	N8N_PORT=5678
	N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS=true
	N8N_RUNNERS_ENABLED=true
```


### ▶️ GStart the containers:

	docker compose up -d --build

### Stop them:

	docker-compose down

## 🔄 Update Docker container

To fetch the latest images and rebuild:

	docker-compose pull
	docker-compose up --force-recreate --build -d
	docker image prune -f

## ⚠️ Cleanup (optional)

WARNING: This will delete your data stored in volumes!

	docker-compose down -v

## 📦 Volumes used

- postgres_data → PostgreSQL data
- pgadmin_data → PgAdmin configuration
- n8n_data → n8n workflow and credential storage

## 🤝 Contribute

Feel free to fork, improve or customize this boilerplate. Contributions are welcome — add support for other DBs, external services, or N8n enhancements!
