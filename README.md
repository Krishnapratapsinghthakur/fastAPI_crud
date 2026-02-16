<![CDATA[<!-- Header Banner -->
<div align="center">
  
  <img src="https://fastapi.tiangolo.com/img/logo-margin/logo-teal.png" alt="FastAPI" width="300"/>

  <br/>
  <br/>

  # 🗂️ Todo CRUD API
  
  ### A **blazing-fast** RESTful API for managing Todos — powered by FastAPI & PostgreSQL

  <br/>

  [![Python](https://img.shields.io/badge/python-3.12+-blue?style=flat-square&logo=python&logoColor=white)](https://www.python.org/)
  [![FastAPI](https://img.shields.io/badge/FastAPI-0.129+-00C7B7?style=flat-square&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
  [![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15+-336791?style=flat-square&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
  [![SQLAlchemy](https://img.shields.io/badge/SQLAlchemy-2.0+-red?style=flat-square)](https://www.sqlalchemy.org/)
  [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)
  [![uv](https://img.shields.io/badge/uv-package%20manager-blueviolet?style=flat-square)](https://docs.astral.sh/uv/)

  <br/>

  **[Explore the Docs »](http://127.0.0.1:8000/docs)** · **[Report Bug](../../issues)** · **[Request Feature](../../issues)**

  <br/>
  
  ---

</div>

<br/>

## � About

> **Simple. Clean. Production-ready.**

This project is a fully functional **CRUD (Create, Read, Update, Delete) API** for managing a Todo list. It's built as a learning reference and starter template showcasing:

- 🏛️ Clean separation of concerns *(models → schemas → routes)*
- � Dependency injection for database sessions
- 🛡️ Automatic request validation with Pydantic v2
- � Auto-generated interactive API documentation

<br/>

## 🗺️ Architecture

```
                    ┌─────────────────────────────────────────────────┐
                    │                  CLIENT                         │
                    │           (curl / Postman / Frontend)           │
                    └────────────────────┬────────────────────────────┘
                                         │  HTTP Request
                                         ▼
┌────────────────────────────────────────────────────────────────────────────┐
│                           FastAPI Application                              │
│                                                                            │
│   ┌─────────────┐    ┌──────────────┐    ┌─────────────┐    ┌───────────┐ │
│   │  main.py    │───▶│  schemas.py  │    │  models.py  │    │database.py│ │
│   │  (Routes)   │    │  (Validate)  │    │  (ORM Map)  │    │ (Engine)  │ │
│   └──────┬──────┘    └──────────────┘    └──────┬──────┘    └─────┬─────┘ │
│          │                                       │                 │       │
│          └───────────────────────────────────────┴─────────────────┘       │
│                                         │                                  │
└─────────────────────────────────────────┼──────────────────────────────────┘
                                          │  SQLAlchemy ORM
                                          ▼
                              ┌──────────────────────┐
                              │    PostgreSQL DB      │
                              │    ┌──────────────┐   │
                              │    │  todos table  │   │
                              │    └──────────────┘   │
                              └──────────────────────┘
```

<br/>

## 📁 Project Structure

```bash
.
├── 🚀 main.py          # App instance, dependency injection & all CRUD routes
├── 🗄️ database.py       # SQLAlchemy engine, session factory & Base
├── 📦 models.py         # Todo ORM model (maps to 'todos' table)
├── 🛡️ schemas.py        # Pydantic schemas for validation & serialization
├── 📋 pyproject.toml    # Project config & dependency list (managed by uv)
├── 🔒 uv.lock           # Locked dependency versions
└── 📖 README.md
```

<br/>

## ⚡ Quick Start

### Prerequisites

| Tool | Version | Install |
|------|---------|---------|
| Python | `3.12+` | [python.org](https://www.python.org/downloads/) |
| PostgreSQL | `15+` | [postgresql.org](https://www.postgresql.org/download/) |
| uv | latest | `curl -LsSf https://astral.sh/uv/install.sh \| sh` |

### Setup in 60 seconds ⏱️

```bash
# 1️⃣  Clone
git clone https://github.com/<your-username>/fastapi-todo-crud.git && cd fastapi-todo-crud

# 2️⃣  Create virtual environment & install deps
uv venv && source .venv/bin/activate && uv sync

# 3️⃣  Configure your database URL in database.py
#     SQLALCHEMY_DATABASE_URL = "postgresql://user:password@localhost/your_db"

# 4️⃣  Launch! 🚀
uvicorn main:app --reload
```

> 🟢 **Server running at** → `http://127.0.0.1:8000`
> 
> 📖 **Swagger Docs** → `http://127.0.0.1:8000/docs`
> 
> 📘 **ReDoc** → `http://127.0.0.1:8000/redoc`

<br/>

## � API Reference

### Endpoints

| Method | Endpoint | Description | Status |
|:------:|----------|-------------|:------:|
| 🟢 `POST` | `/todos/` | Create a new todo | `201` |
| 🔵 `GET` | `/todos/` | Fetch all todos | `200` |
| 🟡 `PUT` | `/todos/{id}` | Update a todo | `200` |
| 🔴 `DELETE` | `/todos/{id}` | Delete a todo | `200` |

### Usage Examples

<details>
<summary><b>� POST</b> — Create a Todo</summary>

<br/>

```bash
curl -X POST http://127.0.0.1:8000/todos/ \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Learn FastAPI",
    "description": "Build a production-ready CRUD API",
    "completed": false
  }'
```

```json
// ✅ Response 201
{
  "title": "Learn FastAPI",
  "description": "Build a production-ready CRUD API",
  "completed": false,
  "id": 1
}
```

</details>

<details>
<summary><b>� GET</b> — Fetch All Todos</summary>

<br/>

```bash
curl http://127.0.0.1:8000/todos/
```

```json
// ✅ Response 200
[
  {
    "title": "Learn FastAPI",
    "description": "Build a production-ready CRUD API",
    "completed": false,
    "id": 1
  }
]
```

</details>

<details>
<summary><b>🟡 PUT</b> — Update a Todo</summary>

<br/>

```bash
curl -X PUT http://127.0.0.1:8000/todos/1 \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Learn FastAPI",
    "description": "CRUD API ✅ Done!",
    "completed": true
  }'
```

```json
// ✅ Response 200
{
  "title": "Learn FastAPI",
  "description": "CRUD API ✅ Done!",
  "completed": true,
  "id": 1
}
```

</details>

<details>
<summary><b>� DELETE</b> — Delete a Todo</summary>

<br/>

```bash
curl -X DELETE http://127.0.0.1:8000/todos/1
```

```json
// ✅ Response 200
{
  "message": "Deleted"
}
```

</details>

<br/>

## 🧠 How It Works

```mermaid
flowchart LR
    A[📱 Client Request] --> B{FastAPI Router}
    B -->|Validate| C[🛡️ Pydantic Schema]
    C --> D[📦 SQLAlchemy Model]
    D --> E[(🗄️ PostgreSQL)]
    E --> D
    D --> F[🛡️ Response Schema]
    F --> G[📱 JSON Response]
    
    style A fill:#f9f,stroke:#333,stroke-width:2px
    style E fill:#336791,stroke:#333,stroke-width:2px,color:#fff
    style G fill:#0f0,stroke:#333,stroke-width:2px
```

| Step | What Happens |
|------|-------------|
| **1. Request** | Client sends HTTP request with JSON body |
| **2. Validation** | Pydantic schema validates & parses the payload |
| **3. ORM** | SQLAlchemy model maps the data to the database |
| **4. Database** | PostgreSQL persists / retrieves the data |
| **5. Response** | Data is serialized back via Pydantic & returned as JSON |

<br/>

## 🧩 Key Files Explained

<details>
<summary><code>📄 database.py</code> — Database Configuration</summary>

<br/>

- Creates the **SQLAlchemy engine** connected to PostgreSQL
- Configures `SessionLocal` — a session factory for database transactions
- Exports `Base` — the declarative base all ORM models inherit from

</details>

<details>
<summary><code>📄 models.py</code> — ORM Model</summary>

<br/>

Defines the `Todo` model mapped to the `todos` table:

| Column | Type | Details |
|--------|------|---------|
| `id` | `Integer` | Primary key, auto-increment |
| `title` | `String` | Indexed for fast lookups |
| `description` | `String` | Required field |
| `completed` | `Boolean` | Defaults to `False` |

</details>

<details>
<summary><code>📄 schemas.py</code> — Pydantic Schemas</summary>

<br/>

| Schema | Purpose |
|--------|---------|
| `TodoBase` | Shared fields: title, description, completed |
| `TodoCreate` | Input schema for POST/PUT (inherits TodoBase) |
| `TodoResponse` | Output schema — adds `id` + enables `from_attributes` |

</details>

<details>
<summary><code>📄 main.py</code> — Routes & Application</summary>

<br/>

- Initializes the **FastAPI app**
- Auto-creates tables via `Base.metadata.create_all()`
- Provides `get_db()` dependency for database session management
- Defines all **4 CRUD routes** with proper HTTP methods & status codes

</details>

<br/>

## 🛣️ Roadmap

- [ ] Add pagination to `GET /todos/`
- [ ] Add filtering & search (`?completed=true`, `?q=search`)
- [ ] Environment variable support for database URL
- [ ] Add unit & integration tests
- [ ] Dockerize the application
- [ ] Deploy to Railway / Render

<br/>

## 🤝 Contributing

Contributions are welcome! Feel free to open an issue or submit a PR.

```bash
# Fork → Clone → Branch → Commit → Push → PR
git checkout -b feature/amazing-feature
git commit -m "Add amazing feature"
git push origin feature/amazing-feature
```

<br/>

## 📜 License

Distributed under the **MIT License**. See `LICENSE` for more information.

<br/>

---

<div align="center">
  
  **Built with 🐍 Python & ⚡ FastAPI**

  <br/>

  If this helped you, give it a ⭐!
  
  <br/>

  <a href="https://fastapi.tiangolo.com/"><img src="https://img.shields.io/badge/Docs-FastAPI-009688?style=for-the-badge&logo=fastapi" /></a>
  <a href="https://www.sqlalchemy.org/"><img src="https://img.shields.io/badge/Docs-SQLAlchemy-D71F00?style=for-the-badge" /></a>
  <a href="https://www.postgresql.org/"><img src="https://img.shields.io/badge/Docs-PostgreSQL-336791?style=for-the-badge&logo=postgresql&logoColor=white" /></a>

</div>
]]>
