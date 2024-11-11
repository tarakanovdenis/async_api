# Async API Service

Проект представляет собой асинхронное API для чтения записей используемых данных (кинофильмы, жанры, актеры, режиссеры и сценаристы). Проект реализован посредством взаимодействия следующих компонентов: PostgreSQL, Elasticsearch, ETL для выгрузки данных с PostgreSQL и загрузки в Elasticsearch, Redis, FastAPI, Nginx. Также написаны тесты (pytest) для сервиса Async API.

Для **запуска проекта** необходимо выполнить следующее:
- **применить схему и создать таблицы** в контейнере базы данных PostgreSQL:
    - `docker compose exec -it postgres_db psql -U $(echo $POSTGRES_USER) -d $(echo $POSTGRES_DB) -f movies_database.dll`
- **перенести данные** из SQLite в PostgreSQL и проверить корректность переноса данных (реализован скрипт и написаны соответствующие тесты для переноса данных) в **сервисе ETL**:
    - `docker compose exec -it etl_from_postgres_to_es python sqlite_to_postgres/load_data.py`
- использовать ETL сервис `etl_from_postgres_to_es` для постоянной выгрузки данных из PostgreSQL в Elastisearch

Для **запуска тестов** Async API необходимо запустить docker-compose.py в директории `./async_api/src/tests/functional/`

Проект запускается через docker-compose и состоит из следующих контейнеров:
- async_api_backend
- postgres_db
- redis
- elasticsearch
- etl_from_postgres_to_es
- nginx
- pgadmin (optional)
