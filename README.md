# Task Management API

A RESTful API built with Django and Django REST Framework for managing tasks with CRUD operations, filtering, and search capabilities.

## Features

- CRUD operations for tasks
- Task priority levels (Low, Medium, High)
- Filter by completion status and priority
- Search by title or description
- Custom actions: completed/pending tasks, mark complete

## Tech Stack

- Django 4.2.28
- Django REST Framework 3.16.1
- Django Filter 25.1
- SQLite

## Quick Start

1. **Clone and navigate to the project**
   ```bash
   git clone https://github.com/AdityaHire/DRF-Project.git
   cd DRF-Project
   ```

2. **Set up virtual environment**
   ```bash
   python -m venv venv
   venv\Scripts\activate  # Windows
   # source venv/bin/activate  # macOS/Linux
   ```

3. **Install dependencies and run**
   ```bash
   pip install -r requirements.txt
   python manage.py migrate
   python manage.py runserver
   ```

API available at `http://127.0.0.1:8000/api/tasks/`

## API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/tasks/` | List all tasks |
| POST | `/api/tasks/` | Create a task |
| GET | `/api/tasks/{id}/` | Get a task |
| PUT/PATCH | `/api/tasks/{id}/` | Update a task |
| DELETE | `/api/tasks/{id}/` | Delete a task |
| GET | `/api/tasks/completed/` | List completed tasks |
| GET | `/api/tasks/pending/` | List pending tasks |
| POST | `/api/tasks/{id}/mark_complete/` | Mark task complete |

## Usage Examples

**Create a task:**
```bash
curl -X POST http://127.0.0.1:8000/api/tasks/ \
  -H "Content-Type: application/json" \
  -d '{"title": "My Task", "description": "Task details", "priority": "high"}'
```

**Filter tasks:**
```bash
GET /api/tasks/?completed=false&priority=high
GET /api/tasks/?search=documentation
GET /api/tasks/?ordering=-created_at
```

