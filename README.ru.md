<div align="center">

# 🐳 Taski · Docker

**Планировщик задач Taski в контейнерах с деплоем на сервер через GitHub Actions**

![Python](https://img.shields.io/badge/Python-3.12-3776AB?logo=python&logoColor=white) ![Django](https://img.shields.io/badge/Django-5.1-092E20?logo=django&logoColor=white) ![DRF](https://img.shields.io/badge/DRF-3.15-A30000?logo=django&logoColor=white) ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-4169E1?logo=postgresql&logoColor=white) ![Docker](https://img.shields.io/badge/Docker-compose-2496ED?logo=docker&logoColor=white) ![Nginx](https://img.shields.io/badge/Nginx-gateway-009639?logo=nginx&logoColor=white) ![React](https://img.shields.io/badge/React-SPA-61DAFB?logo=react&logoColor=black) [![CI](https://github.com/ikovalll/taski-docker/actions/workflows/main.yml/badge.svg)](https://github.com/ikovalll/taski-docker/actions/workflows/main.yml) ![License](https://img.shields.io/badge/license-MIT-lightgrey)

[English](README.md) · [**Русский**](README.ru.md)

</div>

---

## 📖 О проекте

Тот же планировщик задач, что и [taski](https://github.com/ikovalll/taski), но упакованный для продакшена: бэкенд, фронтенд, PostgreSQL и Nginx-шлюз работают в отдельных контейнерах. Каждый пуш в `main` запускает тесты, собирает три Docker-образа, пушит их на Docker Hub, деплоит на сервер по SSH и присылает результат в Telegram.

---

## ✨ Возможности

- **Четыре сервиса** — бэкенд, фронтенд, PostgreSQL и Nginx-шлюз
- **Одна команда** — `docker compose up` поднимает весь стек
- **Отдельный production-compose** для сервера
- **Полный CI/CD** — тесты, сборка образов, деплой и уведомление в Telegram
- **Статика** собирается и раздаётся через шлюз

---

## 🛠 Стек технологий

| Слой | Технологии |
|---|---|
| **Бэкенд** | Python 3.12, Django 5.1, Django REST Framework |
| **Фронтенд** | React SPA |
| **База данных** | PostgreSQL 13 |
| **Инфраструктура** | Docker, Docker Compose, Nginx gateway |
| **CI/CD** | GitHub Actions, Docker Hub, SSH deploy |
| **Качество кода** | flake8, flake8-isort, Django tests |

---

## 🚀 Запуск

### Требования

- Docker и Docker Compose

### 1. Клонируйте репозиторий

```bash
git clone git@github.com:ikovalll/taski-docker.git
cd taski-docker
```

### 2. Создайте файл `.env`

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

### 3. Запустите стек

```bash
docker compose up -d
```

### 4. Выполните миграции и соберите статику

```bash
docker compose exec backend python manage.py migrate
docker compose exec backend python manage.py collectstatic --no-input
```

Приложение доступно по адресу `http://localhost:8000/`.

---

## 🧪 Тесты

```bash
docker compose exec backend python manage.py test
cd frontend && npm run test
```

---

## 📁 Структура проекта

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

При пуше в ветку `main` GitHub Actions:

1. Запускает тесты бэкенда (`flake8` + тесты Django) на PostgreSQL
2. Запускает тесты фронтенда
3. Собирает и пушит на Docker Hub три образа — backend, frontend и gateway
4. Деплоит на сервер по SSH, выполняет миграции и сборку статики
5. Отправляет уведомление в Telegram

> Шаги 4–5 выполняются только если в настройках репозитория
> задана переменная `DEPLOY_ENABLED` со значением `true`. Сервер,
> на который проект разворачивался изначально, выведен из
> эксплуатации, поэтому задача деплоя пропускается, а не падает
> на попытке подключения. Сценарий деплоя сохранён в
> `.github/workflows/main.yml` и включается обратно указанием
> доступов к рабочему серверу в секретах.

---

## 📄 Лицензия

Проект распространяется под лицензией MIT. Подробности — в файле [LICENSE](LICENSE).

---

## 👤 Автор

**Илья Коваленко**

[GitHub](https://github.com/ikovalll) · [Telegram](https://t.me/ikovalll) · [LinkedIn](https://www.linkedin.com/in/ikovalll/)
