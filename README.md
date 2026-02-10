cat > README.md << 'EOF'
# 📚 FastAPI Beyond CRUD - Full-Stack Book Review Platform

A production-ready REST API for a book review web service built with **FastAPI**, featuring advanced patterns beyond basic CRUD operations. This project demonstrates enterprise-level architecture with asynchronous task processing, role-based authentication, and scalable database design.

[![FastAPI](https://img.shields.io/badge/FastAPI-005571?style=for-the-badge&logo=fastapi)](https://fastapi.tiangolo.com/)
[![Python](https://img.shields.io/badge/python-3.10+-blue.svg?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Redis](https://img.shields.io/badge/redis-%23DD0031.svg?&style=for-the-badge&logo=redis&logoColor=white)](https://redis.io/)
[![Celery](https://img.shields.io/badge/celery-%23a9cc54.svg?style=for-the-badge&logo=celery&logoColor=ddf4a4)](https://docs.celeryproject.org/)

## ✨ Features

### Core Functionality
- 📖 **Books Management** - Create, read, update, and delete books with detailed metadata
- ⭐ **Review System** - Users can rate and review books
- 🏷️ **Tag System** - Categorize books with custom tags
- 👥 **User Management** - Complete user lifecycle with profile management

### Advanced Features
- 🔐 **JWT Authentication** - Secure token-based authentication with refresh tokens
- 🛡️ **Role-Based Access Control** - Admin and user roles with fine-grained permissions
- 📧 **Email Notifications** - Async email sending for account verification and password resets
- ⚡ **Background Tasks** - Celery integration for asynchronous task processing
- 🔄 **Database Migrations** - Alembic for version-controlled schema migrations
- 📊 **Relationship Management** - Complex SQLAlchemy relationships between entities
- ✅ **Input Validation** - Pydantic schemas for robust data validation
- 📝 **Auto-generated API Docs** - Interactive Swagger UI and ReDoc

## 🏗️ Architecture
```
fastapi-beyond-CRUD/
├── src/
│   ├── auth/              # Authentication & authorization
│   │   ├── routes.py      # Auth endpoints
│   │   ├── service.py     # Auth business logic
│   │   ├── schemas.py     # Pydantic models
│   │   └── dependencies.py # JWT & role dependencies
│   ├── books/             # Books module
│   ├── reviews/           # Reviews module
│   ├── tags/              # Tags module
│   ├── db/                # Database configuration
│   │   ├── models.py      # SQLAlchemy models
│   │   └── main.py        # DB session management
│   ├── celery_tasks.py    # Celery task definitions
│   ├── mail.py            # Email service
│   └── config.py          # App configuration
├── migrations/            # Alembic migrations
├── requirements.txt       # Python dependencies
└── alembic.ini           # Alembic configuration
```

## 🛠️ Tech Stack

| Category | Technologies |
|----------|-------------|
| **Framework** | FastAPI, Uvicorn |
| **Database** | PostgreSQL, SQLAlchemy, SQLModel |
| **Migrations** | Alembic |
| **Authentication** | JWT (PyJWT), Passlib, Bcrypt |
| **Task Queue** | Celery, Redis |
| **Email** | SMTP (configurable) |
| **Validation** | Pydantic |
| **Testing** | pytest (planned) |

## 📋 Prerequisites

- **Python** 3.10 or higher
- **PostgreSQL** 14+ (or use Docker)
- **Redis** 6+ (or use Docker)
- **pip** for package management

## 🚀 Quick Start

### 1️⃣ Clone the Repository
```bash
git clone https://github.com/YOUR_USERNAME/fastapi-beyond-CRUD.git
cd fastapi-beyond-CRUD
```

### 2️⃣ Set Up Virtual Environment
```bash
python3 -m venv env
source env/bin/activate  # On Windows: env\Scripts\activate
pip install -r requirements.txt
```

### 3️⃣ Configure Environment Variables

Create a `.env` file in the project root:
```bash
# Database
DATABASE_URL=postgresql+asyncpg://username:password@localhost:5432/bookly_db

# Redis
REDIS_URL=redis://localhost:6379/0

# JWT
JWT_SECRET=your-super-secret-jwt-key
JWT_ALGORITHM=HS256

# Email (Example with Gmail)
MAIL_USERNAME=your-email@gmail.com
MAIL_PASSWORD=your-app-password
MAIL_FROM=your-email@gmail.com
MAIL_PORT=587
MAIL_SERVER=smtp.gmail.com
MAIL_FROM_NAME="Bookly Platform"
```

### 4️⃣ Set Up Database
```bash
# Option A: Using local PostgreSQL
sudo -u postgres psql
CREATE DATABASE bookly_db;
CREATE USER your_username WITH PASSWORD 'your_password';
GRANT ALL PRIVILEGES ON DATABASE bookly_db TO your_username;
\q

# Option B: Using Docker
docker run --name bookly-postgres \
  -e POSTGRES_DB=bookly_db \
  -e POSTGRES_USER=your_username \
  -e POSTGRES_PASSWORD=your_password \
  -p 5432:5432 -d postgres:14
```

### 5️⃣ Run Database Migrations
```bash
alembic upgrade head
```

### 6️⃣ Start Redis
```bash
# Option A: Local installation
sudo systemctl start redis-server

# Option B: Using Docker
docker run --name bookly-redis -p 6379:6379 -d redis:7
```

### 7️⃣ Start the Application

**Terminal 1 - FastAPI Server:**
```bash
uvicorn src:app --reload --host 0.0.0.0 --port 8000
```

**Terminal 2 - Celery Worker:**
```bash
celery -A src.celery_tasks worker --loglevel=info
```

**Optional - Celery Flower (Task Monitor):**
```bash
celery -A src.celery_tasks flower --port=5555
```

### 8️⃣ Access the Application

- **API Documentation (Swagger):** http://localhost:8000/api/v1/docs
- **Alternative Docs (ReDoc):** http://localhost:8000/api/v1/redoc
- **Celery Flower Dashboard:** http://localhost:5555

## 📡 API Endpoints

### Authentication
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/v1/auth/signup` | Register new user |
| POST | `/api/v1/auth/login` | User login |
| GET | `/api/v1/auth/me` | Get current user |
| POST | `/api/v1/auth/refresh` | Refresh access token |
| POST | `/api/v1/auth/password-reset` | Request password reset |

### Books
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/v1/books/` | Get all books |
| POST | `/api/v1/books/` | Create new book |
| GET | `/api/v1/books/{book_uid}` | Get book details |
| PATCH | `/api/v1/books/{book_uid}` | Update book |
| DELETE | `/api/v1/books/{book_uid}` | Delete book |
| GET | `/api/v1/books/user/{user_uid}` | Get user's books |

### Reviews
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/v1/reviews/book/{book_uid}` | Add review to book |
| GET | `/api/v1/reviews/{review_uid}` | Get review details |
| DELETE | `/api/v1/reviews/{review_uid}` | Delete review |

### Tags
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/v1/tags/` | Get all tags |
| POST | `/api/v1/tags/` | Create new tag |
| POST | `/api/v1/tags/book/{book_uid}/tags` | Add tags to book |
| DELETE | `/api/v1/tags/{tag_uid}` | Delete tag |

## 🔧 Development

### Creating New Migrations
```bash
# Auto-generate migration from model changes
alembic revision --autogenerate -m "Description of changes"

# Apply migrations
alembic upgrade head

# Rollback one migration
alembic downgrade -1
```

### Running Tests (Coming Soon)
```bash
pytest tests/
```

## 🐳 Docker Deployment
```bash
# Build and run all services
docker-compose up -d

# View logs
docker-compose logs -f

# Stop services
docker-compose down
```

## 🚢 Production Deployment

This application is production-ready and can be deployed on:
- **Railway** (Recommended) - Easiest setup with PostgreSQL + Redis
- **Render** - Great free tier with database support
- **Fly.io** - Full Docker support
- **AWS/GCP/Azure** - For enterprise deployments

See the [Deployment Guide](DEPLOYMENT.md) for detailed instructions.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request
