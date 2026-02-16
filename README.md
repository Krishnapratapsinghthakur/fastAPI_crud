<![CDATA[<div align="center">

# ✅ FastAPI Todo CRUD API

**A clean, minimal RESTful API built with FastAPI & PostgreSQL**

![Python](https://img.shields.io/badge/Python-3.12+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-0.129+-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)
![SQLAlchemy](https://img.shields.io/badge/SQLAlchemy-2.0+-D71F00?style=for-the-badge&logo=sqlalchemy&logoColor=white)

---

*A production-ready Todo API demonstrating clean architecture with FastAPI, SQLAlchemy ORM, and PostgreSQL.*

</div>

## 🚀 Features

- ⚡ **FastAPI** — High-performance async Python web framework
- 🗄️ **PostgreSQL** — Robust relational database backend
- 🔗 **SQLAlchemy ORM** — Elegant database interactions with models
- 📝 **Pydantic Schemas** — Automatic request/response validation
- 📖 **Auto-generated Docs** — Interactive Swagger UI & ReDoc out of the box
- 🏗️ **Clean Architecture** — Separated concerns: models, schemas, database, routes

---

## 📁 Project Structure

```
SIMPLE_CRUD/
├── main.py           # Application entry point & API routes
├── database.py       # Database engine & session configuration
├── models.py         # SQLAlchemy ORM models
├── schemas.py        # Pydantic request/response schemas
├── pyproject.toml    # Project metadata & dependencies
├── .gitignore        # Git ignore rules
└── README.md         # You are here!
```

---

## 🛠️ Tech Stack

| Layer          | Technology                        |
|----------------|-----------------------------------|
| **Framework**  | FastAPI                           |
| **ORM**        | SQLAlchemy 2.0+                   |
| **Database**   | PostgreSQL                        |
| **Validation** | Pydantic v2                       |
| **Server**     | Uvicorn (ASGI)                    |
| **Packaging**  | uv (modern Python package manager)|

---

## ⚙️ Getting Started

### Prerequisites

- **Python 3.12+**
- **PostgreSQL** installed and running
- **uv** package manager ([install guide](https://docs.astral.sh/uv/getting-started/installation/))

### 1. Clone the Repo

```bash
git clone https://github.com/<your-username>/fastapi-todo-crud.git
cd fastapi-todo-crud
```

### 2. Set Up the Virtual Environment

```bash
uv venv
source .venv/bin/activate  # Linux/macOS
# .venv\Scripts\activate   # Windows
```

### 3. Install Dependencies

```bash
uv sync
```

### 4. Configure the Database

Create a PostgreSQL database and update the connection string in `database.py`:

```python
SQLALCHEMY_DATABASE_URL = "postgresql://<user>:<password>@localhost/<db_name>"
```

> **💡 Tip:** Tables are created automatically when the app starts — no manual migration needed!

### 5. Run the Server

```bash
uvicorn main:app --reload
```

The API will be live at **http://127.0.0.1:8000** 🎉

---

## 📖 API Endpoints

| Method   | Endpoint            | Description           | Request Body                                          |
|----------|---------------------|-----------------------|-------------------------------------------------------|
| `POST`   | `/todos/`           | Create a new todo     | `{ "title": "...", "description": "...", "completed": false }` |
| `GET`    | `/todos/`           | List all todos        | —                                                     |
| `PUT`    | `/todos/{todo_id}`  | Update a todo by ID   | `{ "title": "...", "description": "...", "completed": true }`  |
| `DELETE` | `/todos/{todo_id}`  | Delete a todo by ID   | —                                                     |

### Example Requests

<details>
<summary>📝 <strong>Create a Todo</strong></summary>

```bash
curl -X POST http://127.0.0.1:8000/todos/ \
  -H "Content-Type: application/json" \
  -d '{"title": "Learn FastAPI", "description": "Build a CRUD API", "completed": false}'
```

**Response:**
```json
{
  "title": "Learn FastAPI",
  "description": "Build a CRUD API",
  "completed": false,
  "id": 1
}
```
</details>

<details>
<summary>📋 <strong>Get All Todos</strong></summary>

```bash
curl http://127.0.0.1:8000/todos/
```

**Response:**
```json
[
  {
    "title": "Learn FastAPI",
    "description": "Build a CRUD API",
    "completed": false,
    "id": 1
  }
]
```
</details>

<details>
<summary>✏️ <strong>Update a Todo</strong></summary>

```bash
curl -X PUT http://127.0.0.1:8000/todos/1 \
  -H "Content-Type: application/json" \
  -d '{"title": "Learn FastAPI", "description": "Build a CRUD API", "completed": true}'
```

**Response:**
```json
{
  "title": "Learn FastAPI",
  "description": "Build a CRUD API",
  "completed": true,
  "id": 1
}
```
</details>

<details>
<summary>🗑️ <strong>Delete a Todo</strong></summary>

```bash
curl -X DELETE http://127.0.0.1:8000/todos/1
```

**Response:**
```json
{
  "message": "Deleted"
}
```
</details>

---

## 📚 Interactive API Docs

FastAPI auto-generates beautiful interactive documentation:

| Doc Style    | URL                                      |
|-------------|------------------------------------------|
| **Swagger UI** | [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)       |
| **ReDoc**      | [http://127.0.0.1:8000/redoc](http://127.0.0.1:8000/redoc)     |

---

## 🏗️ Architecture Overview

```
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│   Client     │────▶│   FastAPI    │────▶│  SQLAlchemy  │────▶│  PostgreSQL  │
│  (Request)   │◀────│   Routes     │◀────│    ORM       │◀────│   Database   │
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘
                           │                     │
                     ┌─────┴─────┐         ┌─────┴─────┐
                     │  Pydantic │         │  Models   │
                     │  Schemas  │         │  (ORM)    │
                     └───────────┘         └───────────┘
```

**Flow:**
1. Client sends an HTTP request
2. FastAPI validates the request body using **Pydantic schemas**
3. Route handler uses **SQLAlchemy ORM** to interact with the database
4. Database operations are performed on **PostgreSQL**
5. Response is serialized back through Pydantic and returned to the client

---

## 🧩 Code Walkthrough

### `database.py` — Database Configuration
Sets up the SQLAlchemy engine, session factory, and declarative base for ORM models.

### `models.py` — ORM Models
Defines the `Todo` table with columns: `id`, `title`, `description`, and `completed`.

### `schemas.py` — Pydantic Schemas
- `TodoBase` — Shared fields (title, description, completed)
- `TodoCreate` — Schema for creating a todo (inherits TodoBase)
- `TodoResponse` — Schema for API responses (adds `id`, enables ORM mode)

### `main.py` — Application & Routes
- Creates the FastAPI app instance
- Auto-creates database tables on startup
- Defines the database dependency injection (`get_db`)
- Implements all 4 CRUD endpoints: `POST`, `GET`, `PUT`, `DELETE`

---

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).

---

<div align="center">

**Built with ❤️ using FastAPI**

⭐ Star this repo if you found it helpful!

</div>
]]>
