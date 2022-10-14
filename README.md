# Проект: API_YAMDB

# Автор проекта

https://github.com/bainter  

## Описание:

Проект "API для YAMDB" представляет собой интерфейс для обмена данными с сервисом YAMDB.

Он позволяет получать различные наборы данных, хранящихся в базе данных сервиса YAMDB и создавать новые данные внутри сервиса.

## Шаблон env-файла:

- DB_ENGINE=
- DB_NAME=
- POSTGRES_USER=
- POSTGRES_PASSWORD=
- DB_HOST=
- DB_PORT=

## Запуск приложения в контейнерах:

Для запуска приложения в контейнерах необходимо:

1. Клонировать репозиторий и перейти в директорию с *docker-compose.yaml*:  
`git clone git@github.com:bainter/infra_sp2.git`  
`cd infra_sp2/infra`

2. Открыть терминал wsl и запустить docker-compose с ключом `-d`:  
`docker-compose up -d`  

3. Установить зависимости из файла requirements.txt:  
`python3 -m pip install --upgrade pip`  
`pip install -r requirements.txt`

4. Выполнить миграции, создать суперюзера, собрать статику:  
`docker-compose exec web python manage.py migrate`
`docker-compose exec web python manage.py createsuperuser`
`docker-compose exec web python manage.py collectstatic --no-input`

5. Проект доступен по адресу:  
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
#### Полная документация:  
Полная документация по API доступна по адресу http://localhost/redoc после запуска сервера
