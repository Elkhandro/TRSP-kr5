# TRSP-KR5

## Локальный запуск

```bash
python -m venv .venv
pip install -r requirements.txt
uvicorn app.main:app --reload
```

## Тесты

```bash
pytest
```

## Docker

```bash
docker compose up --build
```

Проверка:

```bash
curl http://localhost:8000/tasks -H "X-User-Id: 10"
```

Для пустого списка задач ответ будет:

```json
[]
```

## Пример POST-запроса

Важные данные передаются через JSON-тело запроса, а не через параметры строки:

```bash
curl -X POST http://localhost:8000/tasks \
  -H "Content-Type: application/json" \
  -H "X-User-Id: 10" \
  -d '{"title":"Подготовить тесты","description":"Написать интеграционные тесты","status":"todo","priority":4}'
```

## WebSocket

Маршрут:

```text
/ws/rooms/{room_id}?username=alice
```

Если `username` отсутствует или состоит из пробелов, соединение закрывается с кодом `1008`.

Сообщение клиента:

```json
{
  "type": "message",
  "text": "Всем привет"
}
```

Если текст длиннее 300 символов, отправитель получает:

```json
{
  "type": "error",
  "detail": "Message is too long"
}
```
