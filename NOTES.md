# 🚀 Deployment Pipeline (Traefik + Docker + GitHub Actions)

This branch contains the **full deployment pipeline** for the Javalin REST API.
It includes everything needed to run the application in production using Docker, Traefik, and GitHub Actions.

---

## 📌 What This Branch Includes

* **Dockerfile** (production-ready)
* **docker-compose.yml** (local)
* **docker-compose.prod.yml** (production)
* **Traefik reverse proxy**

  * Automatic HTTPS with Let's Encrypt
  * Routers, services, middleware
* **Environment variables** (`.env` templates)
* **GitHub Actions CI/CD**

  * Build + Test
  * Docker image push
  * Deploy to remote server

This branch is **only the pipeline setup** — the API code lives in the main branch.

---

## 🧰 Tech Used

* Docker
* Docker Compose
* Traefik v3
* GitHub Actions
* DigitalOcean (remote target)

---

## 📂 Folder Overview

```
deployment/
├── docker/
│   ├── Dockerfile
│   ├── docker-compose.yml
│   └── docker-compose.prod.yml
│
├── traefik/
│   ├── traefik.yml
│   ├── traefik_dynamic.yml
│   └── acme.json
│
└── github/
    └── workflows/
        └── deploy.yml
```

---

## 🚀 How Deployment Works

1. You push to **main**
2. GitHub Actions:

   * builds the project
   * runs tests
   * builds Docker image
   * pushes image to Docker Hub
3. Server pulls image via SSH
4. `docker compose up -d` restarts the containers
5. Traefik automatically handles HTTPS + routing

---

## ⚙️ Environment Variables

Create a `.env` file inside `deployment/docker/`:

```
DOMAIN=mydomain.com
EMAIL=admin@mydomain.com

POSTGRES_URL=jdbc:postgresql://db:5432/app
POSTGRES_USER=user
POSTGRES_PASSWORD=password

APP_PORT=7000
```

---

## ▶️ Local Development

```bash
docker compose up --build
```

API available at:

```
http://localhost:7000
```

Traefik dashboard (if enabled):

```
http://localhost:8080
```

---

## 📦 Production Deployment

On the server:

```bash
docker compose -f docker-compose.prod.yml pull
docker compose -f docker-compose.prod.yml up -d
```



