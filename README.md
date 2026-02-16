# ✅ FastAPI Todo CRUD API

A clean, minimal RESTful API for managing Todos — built with **FastAPI**, **SQLAlchemy**, and **PostgreSQL**.

![Python](https://img.shields.io/badge/Python-3.12+-3776AB?style=flat-square&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-0.129+-009688?style=flat-square&logo=fastapi&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-336791?style=flat-square&logo=postgresql&logoColor=white)
![SQLAlchemy](https://img.shields.io/badge/SQLAlchemy-2.0+-D71F00?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-yellow?style=flat-square)

---

## 🚀 Features

- **⚡ FastAPI** — High-performance async Python framework
- **🗄️ PostgreSQL** — Reliable relational database
- **🔗 SQLAlchemy ORM** — Clean database interactions
- **🛡️ Pydantic v2** — Automatic request/response validation
- **📖 Auto Docs** — Swagger UI & ReDoc built-in
- **🔒 Secure Config** — Database credentials via `.env` file
- **🏗️ Clean Architecture** — Separated models, schemas & routes

---

## 📁 Project Structure

```
├── main.py           # App entry point & CRUD routes
├── database.py       # SQLAlchemy engine & session config
├── models.py         # ORM model (Todo table)
├── schemas.py        # Pydantic validation schemas
├── .env              # Environment variables (not committed)
├── .env.example      # Template for env variables
├── pyproject.toml    # Dependencies & project config
└── README.md
```

---

## ⚙️ Getting Started

### Prerequisites

- **Python 3.12+**
- **PostgreSQL** running locally
- **uv** package manager — `curl -LsSf https://astral.sh/uv/install.sh | sh`

### Installation

```bash
# Clone the repo
git clone https://github.com/<your-username>/fastapi-todo-crud.git
cd fastapi-todo-crud

# Create virtual environment & install dependencies
uv venv
source .venv/bin/activate
uv sync
```

### Configuration

Create a `.env` file in the project root (see `.env.example`):

```env
DATABASE_URL=postgresql://user:password@localhost/your_database
```

### Run the Server

```bash
uvicorn main:app --reload
```

> 🟢 API live at → **http://127.0.0.1:8000**
>
> 📖 Swagger Docs → **http://127.0.0.1:8000/docs**
>
> 📘 ReDoc → **http://127.0.0.1:8000/redoc**

---

## 🔥 API Endpoints

| Method | Endpoint | Description |
|:------:|----------|-------------|
| `POST` | `/todos/` | Create a new todo |
| `GET` | `/todos/` | Get all todos |
| `PUT` | `/todos/{id}` | Update a todo |
| `DELETE` | `/todos/{id}` | Delete a todo |

---

## 📝 Usage Examples

### Create a Todo

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

### Get All Todos

```bash
curl http://127.0.0.1:8000/todos/
```

### Update a Todo

```bash
curl -X PUT http://127.0.0.1:8000/todos/1 \
  -H "Content-Type: application/json" \
  -d '{"title": "Learn FastAPI", "description": "Done!", "completed": true}'
```

### Delete a Todo

```bash
curl -X DELETE http://127.0.0.1:8000/todos/1
```

---

## 🧩 How It Works

```
Client Request → FastAPI Route → Pydantic Validation → SQLAlchemy ORM → PostgreSQL
```

1. **Client** sends an HTTP request (JSON body)
2. **FastAPI** routes it and **Pydantic** validates the payload
3. **SQLAlchemy** maps the data to the `todos` table
4. **PostgreSQL** stores/retrieves the data
5. Response is serialized back as JSON

---

## 🗃️ Database Model

| Column | Type | Details |
|--------|------|---------|
| `id` | Integer | Primary key, auto-increment |
| `title` | String | Indexed |
| `description` | String | Required |
| `completed` | Boolean | Default: `false` |

---

## 🛣️ Roadmap

- [ ] Pagination for `GET /todos/`
- [ ] Filtering & search queries
- [ ] Unit & integration tests
- [ ] Docker support
- [ ] Deploy to Railway / Render

---

## 🤝 Contributing

```bash
# Fork → Clone → Branch → Commit → Push → PR
git checkout -b feature/your-feature
git commit -m "Add your feature"
git push origin feature/your-feature
```

---

## 📜 License

MIT License — feel free to use this project however you like.

---

**Built with ❤️ using FastAPI** — ⭐ Star this repo if you found it helpful!
