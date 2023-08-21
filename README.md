# Проект YAMDB

## Описание проекта:

Проект **YAMDB** представляет собой платформу, которая функционирует как цифровой каталог, содержащий разнообразные художественные произведения. В этом каталоге разделены на несколько основных категорий, таких как "Книги", "Фильмы" и "Музыка".

Основной функциональностью YaMDb является возможность оценивания и обсуждения произведений. Пользователи могут оценивать произведения, выставлять им рейтинги и оставлять отзывы. Кроме того, к отзывам также можно добавлять комментарии. Проект предоставляет удобную среду для обмена мнениями и рецензиями на различные художественные работы.

Проект упакован в Docker контейнеры:
- Контейнер для Django-проекта использует образ `python:3.7-slim`.
- Контейнер для базы данных Postgres использует образ `postgres:13.0-alpine`.
- Контейнер для веб-сервера Nginx использует образ `nginx:1.21.3-alpine`.

### Документация проекта:

После запуска сервиса докуменация доступна по адресу: http://localhost/redoc

## Технологии проекта:

- Python 3.7
- Django 2.2.16
- Django rest framework 3.12.4
- Gunicorn 20.0.4
- Psycopg2 binary 2.9.3

## Запуск приложения в контейнерах:

Для запуска приложения в контейнерах необходимо:

1. Клонировать репозиторий и перейти в директорию с файлом *docker-compose.yaml*:  
```
git clone git@github.com:alekseikoznov/yamdb.git
```
```
cd yamdb/infra
```

2. Создать файл .env с переменными окружения. Пример наполнения:
```
DB_ENGINE=django.db.backends.postgresql
DB_NAME=postgres
POSTGRES_USER=postgres
POSTGRES_PASSWORD=password123
DB_HOST=db
DB_PORT=5432
```

3. Открыть терминал и запустить docker-compose с ключом `-d`:
```
docker-compose up -d
```

4. Выполнить миграции, создать суперюзера, собрать статику:
```
docker-compose exec web python manage.py migrate
```
```
docker-compose exec web python manage.py createsuperuser
```
```
docker-compose exec web python manage.py collectstatic --no-input
```

5. После успешного запуска проект станет доступен по адресу:  
http://localhost/

## Примеры запросов к API:

#### Получение списка всех произведений: GET http://localhost/api/v1/titles/

#### Пример ответа:
```
{
  [
  {
    "count": 0,
    "next": "string",
    "previous": "string",
    "results": [
      {
        "id": 0,
        "name": "string",
        "year": 0,
        "rating": 0,
        "description": "string",
        "genre": [
          {
            "name": "string",
            "slug": "string"
          }
        ],
        "category": {
          "name": "string",
          "slug": "string"
        }
      }
    ]
  }
]
}
```
#### Добавление новой категории: POST http://localhost/api/v1/categories/
```
{
  "name": "string",
  "slug": "string"
}
```
#### Пример ответа:
```
{
  "name": "string",
  "slug": "string"
}
```
