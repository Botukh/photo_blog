![Build Status](https://github.com/Botukh/photo_blog/actions/workflows/main.yml/badge.svg?event=push)

# Photo_blog

Photo_blog — это приложение для обмена фотографиями и общения пользователей. Проект реализован в виде REST API на Django и контейнеризирован с использованием Docker. Он включает как бэкенд с возможностями создания, редактирования и просмотра публикаций, комментариев, так и фронтенд для удобного пользовательского интерфейса. CI/CD с GitHub Actions обеспечивает автоматическое тестирование, сборку образов и деплой на удалённый сервер.

---

## Функциональность

- **Публикации:**  
  - Получение списка публикаций с поддержкой пагинации (через параметры `limit` и `offset`).  
  - Создание, обновление и удаление постов (редактировать/удалять может только автор).

- **Комментарии:**  
  - Получение комментариев к постам (без пагинации).  
  - Создание, редактирование и удаление комментариев (только автор имеет право изменять или удалять).

- **Аутентификация:**  
  - JWT-аутентификация с использованием `rest_framework_simplejwt` и Djoser.

- **Контейнеризация и CI/CD:**  
  - Проект развёрнут с помощью Docker (backend, frontend, gateway, база PostgreSQL) и orchestrated через docker-compose.  
  - GitHub Actions автоматизирует тестирование, сборку образов (kittygram_backend, kittygram_frontend, kittygram_gateway), деплой на удалённый сервер и уведомление в Telegram.

---

## Стек технологий

- **Backend:** Python, Django, Django REST Framework  
- **Аутентификация:** JWT (rest_framework_simplejwt), Djoser  
- **База данных:** PostgreSQL 13  
- **Контейнеризация:** Docker, docker-compose  
- **Gateway:** Nginx  
- **CI/CD:** GitHub Actions  
- **Frontend:** JavaScript

---

## Развёртывание проекта

### 1. Клонирование репозитория и подготовка окружения

- git clone https://github.com/Botukh/photo_blog.git
- cd photo_blog

### 2. Создание и активация виртуального окружения (локальная разработка)

- python -m venv venv
- source venv/bin/activate

### 3. Создайте файл .env в корне проекта. Пример содержимого:

**Настройки Django**
- DJANGO_SECRET_KEY=your_production_secret_key
- DEBUG=False
- ALLOWED_HOSTS=your_domain.com,localhost

**База данных PostgreSQL**
- DATABASE_NAME=kittygram_db
- DATABASE_USER=your_db_user
- DATABASE_PASSWORD=your_db_password
- DATABASE_HOST=db
- DATABASE_PORT=5432

**Другие переменные (например, настройки Telegram для уведомлений)**
- TELEGRAM_BOT_TOKEN=your_telegram_bot_token
- TELEGRAM_CHAT_ID=your_chat_id

### 4. CI/CD и деплой

**При пуше в ветку main запускается workflow GitHub Actions, который:**
- Проверяет код (PEP8, тесты) для backend и frontend.
- Собирает Docker-образы: kittygram_backend, kittygram_frontend, kittygram_gateway.
- Отправляет образы на Docker Hub (замените dockerhub_username на ваш логин).
- Обновляет контейнеры на удалённом сервере через docker-compose.
- Выполняет миграции, сбор статики.
- Отправляет уведомление в Telegram об успешном деплое.

**Автор - [Юлия Ботух](https://github.com/Botukh)**
