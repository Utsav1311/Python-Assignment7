# Practical 7 — Student Management API (FastAPI)

A small REST API built with FastAPI and Pydantic that manages students in memory.

## Endpoints

| Method | Path                     | Description                          | Status codes        |
|--------|--------------------------|--------------------------------------|---------------------|
| GET    | `/`                      | Health check                         | 200                 |
| GET    | `/students`              | List all students                    | 200                 |
| POST   | `/students`              | Add a student                        | 201, 409, 422       |
| GET    | `/students/{student_id}` | Get one student by id                | 200, 404            |

### Validation rules
- `name`: string, at least 2 characters
- `roll_no`: string, must be unique (duplicate → `409 Conflict`)
- `marks`: number between 0 and 100 (otherwise `422`)

### Example

```bash
curl -X POST http://127.0.0.1:8000/students \
  -H "Content-Type: application/json" \
  -d '{"name": "Aarav", "roll_no": "MCA101", "marks": 85}'
```

Response (`201`):
```json
{"id": 1, "name": "Aarav", "roll_no": "MCA101", "marks": 85.0}
```

## Setup

```bash
python3 -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

## Run

```bash
uvicorn main:app --reload
```

Interactive docs: http://127.0.0.1:8000/docs

## Test

```bash
pytest -v
```

## Note
Data is stored in an in-memory list, so it resets whenever the server restarts.
