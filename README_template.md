# Movies API

## Краткое описание проекта
RESTful-сервис на FastAPI для управления коллекцией фильмов.  
Поддерживает асинхронную работу с SQLite, миграции Alembic, Pydantic v2 и автогенерацию OpenAPI.

## Основные возможности приложения
- CRUD-операции с фильмами  
- Фильтрация по году и рейтингу  
- Сортировка по `title`, `year`, `rating`, `id`  
- Пагинация (limit / offset)  
- Валидация входных данных  
- Асинхронная работа с БД  
- Миграции Alembic  
- Pytest-тесты  

## Технологический стек
- Python 3.11+  
- FastAPI  
- SQLAlchemy (async)  
- Pydantic v2  
- SQLite + aiosqlite  
- Alembic  
- Uvicorn  
- pytest + httpx  

## Быстрый старт
```bash
git clone <репозиторий>
cd movies_api
pip install -r requirements.txt
alembic upgrade head
uvicorn src.main:app --reload
```

## Основные эндпоинты
- `GET /movies/` — Возвращает список всех фильмов  
- `GET /movies/{id}` — Возвращает конкретный фильм по ID
- `POST /movies/` — Добавляет новый фильм 
- `PUT /movies/{id}` — Обновляет данные уже существующего фильма
- `DELETE /movies/{id}` — Удаляет фильм с указанным ID из базы данных

## Фильтрация и сортировка
Поддерживаются параметры:
```
/movies/?year=2020&rating=7.5&sort_by=rating&order=desc
```

## Модель данных
- **id** — Integer, PK  
- **title** — String, обязательное  
- **description** — String  
- **year** — Integer  
- **rating** — Float  

## Ограничения базы данных
- Первичный ключ `id` - Обеспечивает уникальность каждой записи  
- Поле `title` обязательно - Без названия фильм нельзя добавить
- Диапазон `rating`: 0–10 - При валидации Pydantic не позволит записать рейтинг вне допустимых границ
- Индексация по `id` и `title` - Ускоряет поиск и фильтрацию по этим полям
