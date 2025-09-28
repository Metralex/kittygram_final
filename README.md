#  Kittygram final
[![Main Kittygram workflow](https://github.com/Metralex/kittygram_final/actions/workflows/main.yml/badge.svg)](https://github.com/Metralex/kittygram_final/actions/workflows/main.yml)

### Описание проекта

Проект Kittygram - социальная сеть на Djang/React для обмена фотографиями котов. Есть возможность входа/регистрации, создания и редактирования постов с фото котиков и добавления им достижений.

### Стек использованных технологий

- Python 3.12
- Django 4.2
- Django REST framework
- PostgreSQL
- Docker
- Nginx
- Gunicorn
- GitHub Actions

### Как локально развернуть проект

Клонировать репозиторий и перейти в него в командной строке: 
```
git clone git@github.com:Metralex/kittygram_final.git

Cоздать и активировать виртуальное окружение и обновить pip: 
```
 
```
* На Windows 
 
    ```
    python3 -m venv venv
    source venv/scripts/activate
    python3 -m pip install --upgrade pip
    ```
* На Linux или MacOS 

    ```
    python -m venv venv 
    source venv/bin/activate
    python -m pip install --upgrade pip
    ```

Установить зависимости из файла requirements.txt:
```
cd backend/
pip install -r requirements.txt
```

Выполнить миграции:
```
python3 manage.py migrate
```

Запустить проект:
```
python3 manage.py runserver
```

### CI/CD

Процесс непрерывной интеграции и развертывания (CI/CD) настроен с помощью **GitHub Actions**. Это автоматизирует проверку кода, тестирование и доставку проекта на сервер.

**Ключевые этапы Workflow:**

1.  **Проверка кода**: Автоматический запуск линтера (PEP8) для кода бэкенда.
2.  **Тестирование**: Выполнение автоматических тестов для фронтенда и бэкенда.
3.  **Сборка и публикация Docker-образов**: После успешного прохождения тестов workflow собирает Docker-образы и загружает их в Docker Hub.
4.  **Развертывание на сервере**:
    *   Устанавливается безопасное SSH-соединение с сервером.
    *   Загружаются актуальные версии Docker-образов.
    *   Приложение перезапускается с помощью `docker-compose.production.yml`.
5.  **Задачи после развертывания**:
    *   Применяются миграции базы данных (`manage.py migrate`).
    *   Собираются и переносятся статические файлы.
6.  **Уведомления**: Отправляется сообщение в Telegram об успешном завершении развертывания.

**Настройка Workflow:**

- Пример workflow находится в файле `kittygram_workflow.yml` в корне проекта.
- Для активации переместите его содержимое в `.github/workflows/main.yml`.

**Секреты для GitHub Actions:**

Для работы workflow необходимо добавить следующие переменные в `Settings → Secrets and variables → Actions` вашего репозитория:

```
DOCKER_USERNAME    # Логин в Docker Hub
DOCKER_PASSWORD    # Пароль или токен для Docker Hub
SSH_KEY            # Приватный SSH-ключ для доступа к серверу
SSH_PASSPHRASE     # Парольная фраза для SSH-ключа (если используется)
USER               # Имя пользователя на сервере
HOST               # IP-адрес или доменное имя сервера
TELEGRAM_TO        # ID вашего Telegram-аккаунта для уведомлений
TELEGRAM_TOKEN     # Токен Telegram-бота
```

**Файлы Docker Compose:**

- `docker-compose.yml`: для локальной разработки.
- `docker-compose.production.yml`: для развертывания на сервере.

Задайте учётные данные БД в .env файле, используя .env.example:

## как заполнить env
```
POSTGRES_DB=название БД
POSTGRES_USER=логин
POSTGRES_PASSWORD=пароль
DB_NAME=имя БД
DB_HOST=название хоста
DB_PORT=5432
SECRET_KEY=django_settings_secret_key
ALLOWED_HOSTS=localhost,0.0.0.0:8000,127.0.0.1,ip сервера,адрес сайта
```

## Автор:
Metralex https://github.com/Metralex
