# Conduit Containerized Application

Containerized fullstack Conduit application based on the RealWorld specification using Angular, Django, PostgreSQL, Docker, and Docker Compose.

The project includes:

- Angular frontend served with NGINX
- Django backend running with Gunicorn
- PostgreSQL database
- Docker Compose orchestration
- Environment-based configuration
- Multi-container deployment support

---

## Table of Contents

- [Quickstart](#quickstart)
- [Usage](#usage)
- [Configuration](#configuration)
- [Services](#services)
- [Deployment](#deployment)

---

## Quickstart

Clone the repository including submodules:

```bash
git clone --recurse-submodules https://github.com/RaulCiucalau/conduit-container.git
cd conduit-container
```

Create a local environment file:

```bash
cp .env.example .env
```

Build and start all containers:

```bash
docker compose up -d --build
```

The backend entrypoint automatically:

- runs database migrations
- collects static files
- creates/updates the configured Django superuser

---

## Usage

### Frontend

```text
http://localhost:8282
```

### Backend API

```text
http://localhost:8000/api
```

### Django Admin

```text
http://localhost:8000/admin
```

---

## Configuration

Application settings are managed through a local `.env` file.

Use `.env.example` as a template and configure:

- database credentials
- application ports
- allowed hosts
- CORS origins
- frontend API URL
- Django superuser credentials

Real `.env` files are ignored by Git and should never be committed.

---

## Services

The Docker Compose setup contains three services:

### frontend

Angular production build served with NGINX.

### backend

Django REST API running with Gunicorn and WhiteNoise.

### database

PostgreSQL database with persistent Docker volume.

---

## Deployment

For VM deployment:

1. Create a `.env` file on the VM
2. Update:
   - `DJANGO_ALLOWED_HOSTS`
   - `CORS_ALLOWED_ORIGINS`
   - `FRONTEND_API_URL`
3. Rebuild the frontend container

```bash
docker compose build --no-cache frontend
docker compose up -d
```