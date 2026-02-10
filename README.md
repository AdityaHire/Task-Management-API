# Task Management API

A RESTful API built with Django and Django REST Framework for managing tasks with CRUD operations, filtering, search, and custom actions.

## Features

- **CRUD Operations**: Create, Read, Update, and Delete tasks
- **Task Attributes**:
  - Title
  - Description
  - Completion status
  - Priority levels (Low, Medium, High)
  - Timestamps (created_at, updated_at)
- **Filtering**: Filter tasks by completion status and priority
- **Search**: Search tasks by title or description
- **Sorting**: Order tasks by creation date or priority
- **Custom Actions**:
  - Get all completed tasks
  - Get all pending tasks
  - Mark a task as complete

## Tech Stack

- **Django**: 4.2.28
- **Django REST Framework**: 3.16.1
- **Django Filter**: 25.1
- **SQLite**: Database (default)

## Project Structure

```
taskproject/
├── manage.py
├── db.sqlite3
├── requirements.txt
├── taskproject/          # Project configuration
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   ├── wsgi.py
│   └── asgi.py
└── tasks/                # Tasks app
    ├── __init__.py
    ├── models.py         # Task model
    ├── serializers.py    # Task serializer
    ├── views.py          # API views
    ├── urls.py           # API routes
    ├── admin.py
    └── migrations/
```

## Installation

### Prerequisites

- Python 3.8 or higher
- pip (Python package manager)

### Setup

1. **Clone the repository** (or navigate to the project directory)
   ```bash
   cd taskproject
   ```

2. **Create a virtual environment** (recommended)
   ```bash
   python -m venv venv
   ```

3. **Activate the virtual environment**
   - Windows:
     ```bash
     venv\Scripts\activate
     ```
   - macOS/Linux:
     ```bash
     source venv/bin/activate
     ```

4. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

5. **Run migrations**
   ```bash
   python manage.py migrate
   ```

6. **Create a superuser** (optional, for Django admin)
   ```bash
   python manage.py createsuperuser
   ```

7. **Run the development server**
   ```bash
   python manage.py runserver
   ```

The API will be available at `http://127.0.0.1:8000/`

## API Endpoints

### Base URL
```
http://127.0.0.1:8000/api/
```

### Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/tasks/` | List all tasks |
| POST | `/api/tasks/` | Create a new task |
| GET | `/api/tasks/{id}/` | Retrieve a specific task |
| PUT | `/api/tasks/{id}/` | Update a task (full) |
| PATCH | `/api/tasks/{id}/` | Update a task (partial) |
| DELETE | `/api/tasks/{id}/` | Delete a task |
| GET | `/api/tasks/completed/` | List all completed tasks |
| GET | `/api/tasks/pending/` | List all pending tasks |
| POST | `/api/tasks/{id}/mark_complete/` | Mark a task as complete |

## Usage Examples

### Create a Task
```bash
POST /api/tasks/
Content-Type: application/json

{
  "title": "Complete project documentation",
  "description": "Write comprehensive README and API documentation",
  "priority": "high",
  "completed": false
}
```

### Get All Tasks
```bash
GET /api/tasks/
```

### Get a Specific Task
```bash
GET /api/tasks/1/
```

### Update a Task
```bash
PATCH /api/tasks/1/
Content-Type: application/json

{
  "completed": true
}
```

### Delete a Task
```bash
DELETE /api/tasks/1/
```

### Filter Tasks

**By completion status:**
```bash
GET /api/tasks/?completed=true
GET /api/tasks/?completed=false
```

**By priority:**
```bash
GET /api/tasks/?priority=high
GET /api/tasks/?priority=medium
GET /api/tasks/?priority=low
```

**Combined filters:**
```bash
GET /api/tasks/?completed=false&priority=high
```

### Search Tasks
```bash
GET /api/tasks/?search=documentation
```

### Order Tasks
```bash
GET /api/tasks/?ordering=-created_at    # Newest first
GET /api/tasks/?ordering=created_at     # Oldest first
GET /api/tasks/?ordering=priority       # By priority
```

### Custom Actions

**Get all completed tasks:**
```bash
GET /api/tasks/completed/
```

**Get all pending tasks:**
```bash
GET /api/tasks/pending/
```

**Mark a task as complete:**
```bash
POST /api/tasks/1/mark_complete/
```

## Task Model

```python
{
  "id": 1,
  "title": "Task title",
  "description": "Task description",
  "completed": false,
  "priority": "medium",  # Options: "low", "medium", "high"
  "created_at": "2026-02-10T12:00:00Z",
  "updated_at": "2026-02-10T12:00:00Z"
}
```

## Testing with curl

```bash
# Create a task
curl -X POST http://127.0.0.1:8000/api/tasks/ \
  -H "Content-Type: application/json" \
  -d '{"title": "Test Task", "description": "Testing the API", "priority": "high"}'

# Get all tasks
curl http://127.0.0.1:8000/api/tasks/

# Get completed tasks
curl http://127.0.0.1:8000/api/tasks/completed/

# Update a task
curl -X PATCH http://127.0.0.1:8000/api/tasks/1/ \
  -H "Content-Type: application/json" \
  -d '{"completed": true}'

# Delete a task
curl -X DELETE http://127.0.0.1:8000/api/tasks/1/
```

## Development

### Running Tests
```bash
python manage.py test
```

### Access Django Admin
1. Create a superuser (if not already created):
   ```bash
   python manage.py createsuperuser
   ```

2. Navigate to `http://127.0.0.1:8000/admin/`

3. Log in with your superuser credentials

## Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## License

This project is open source and available under the MIT License.

## Support

For issues, questions, or contributions, please open an issue in the repository.
