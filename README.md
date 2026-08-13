<div align="center">

# 🐳 Taski · Docker

**The Taski task planner containerised and deployed to a server via GitHub Actions**

![Python](https://img.shields.io/badge/Python-3.12-3776AB?logo=python&logoColor=white) ![Django](https://img.shields.io/badge/Django-5.1-092E20?logo=django&logoColor=white) ![DRF](https://img.shields.io/badge/DRF-3.15-A30000?logo=django&logoColor=white) ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-4169E1?logo=postgresql&logoColor=white) ![Docker](https://img.shields.io/badge/Docker-compose-2496ED?logo=docker&logoColor=white) ![Nginx](https://img.shields.io/badge/Nginx-gateway-009639?logo=nginx&logoColor=white) ![React](https://img.shields.io/badge/React-SPA-61DAFB?logo=react&logoColor=black) [![CI](https://github.com/ikovalll/taski-docker/actions/workflows/main.yml/badge.svg)](https://github.com/ikovalll/taski-docker/actions/workflows/main.yml) ![License](https://img.shields.io/badge/license-MIT-lightgrey)

[**English**](README.md) · [Русский](README.ru.md)

</div>

---

## 📖 About

The same task planner as [taski](https://github.com/ikovalll/taski), but packaged for production: backend, frontend, PostgreSQL and an Nginx gateway each run in their own container. Every push to `main` runs the test suites, builds three Docker images, pushes them to Docker Hub, deploys them to a server over SSH and reports the result to Telegram.

---

## ✨ Features

- **Four services** — backend, frontend, PostgreSQL and an Nginx gateway
- **One command** — `docker compose up` starts the whole stack
- **Separate production compose** file for the server
- **Full CI/CD** — tests, image builds, deployment and a Telegram notification
- **Static files** collected and served through the gateway

---

## 🛠 Tech Stack

| Layer | Technologies |
|---|---|
| **Backend** | Python 3.12, Django 5.1, Django REST Framework |
| **Frontend** | React SPA |
| **Database** | PostgreSQL 13 |
| **Infrastructure** | Docker, Docker Compose, Nginx gateway |
| **CI/CD** | GitHub Actions, Docker Hub, SSH deploy |
| **Quality** | flake8, flake8-isort, Django tests |

---

## 🚀 Getting Started

### Prerequisites

- Docker and Docker Compose

### 1. Clone the repository

```bash
git clone git@github.com:ikovalll/taski-docker.git
cd taski-docker
```

### 2. Create a `.env` file

```env
POSTGRES_USER=django_user
POSTGRES_PASSWORD=django_password
POSTGRES_DB=django_db
DB_HOST=db
DB_PORT=5432

SECRET_KEY=your-secret-key
DEBUG=False
ALLOWED_HOSTS=localhost,127.0.0.1
```

### 3. Start the stack

```bash
docker compose up -d
```

### 4. Apply migrations and collect static files

```bash
docker compose exec backend python manage.py migrate
docker compose exec backend python manage.py collectstatic --no-input
```

The app is available at `http://localhost:8000/`.

---

## 🧪 Tests

```bash
docker compose exec backend python manage.py test
cd frontend && npm run test
```

---

## 📁 Project Structure

```
taski-docker/
├── backend/               # Django application and Dockerfile
├── frontend/              # React SPA and Dockerfile
├── gateway/               # Nginx gateway and Dockerfile
├── docker-compose.yml
└── docker-compose.production.yml
```

---

## ⚙️ CI

On every push to `main` GitHub Actions:

1. Runs backend tests (`flake8` + Django tests) against PostgreSQL
2. Runs frontend tests
3. Builds and pushes three images to Docker Hub — backend, frontend and gateway
4. Deploys to the server over SSH and applies migrations and static files
5. Sends a Telegram notification

---

## 📄 License

Distributed under the MIT License. See [LICENSE](LICENSE) for details.

---

## 👤 Author

**Ilia Kovalenko**

[GitHub](https://github.com/ikovalll) · [Telegram](https://t.me/ikovalll) · [LinkedIn](https://www.linkedin.com/in/ikovalll/)
