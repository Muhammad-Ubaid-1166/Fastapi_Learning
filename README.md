                                                                                                                                                                     │
│ # FastAPI Beyond CRUD                                                                                                                                                │
│                                                                                                                                                                      │
│ A robust and scalable FastAPI application demonstrating advanced patterns beyond basic Create, Read, Update, Delete (CRUD) operations. This project integrates       │
│ asynchronous tasks with Celery and Redis, manages database migrations with Alembic, and provides structured modules for authentication, user management, and         │
│ resource handling (Books, Reviews, Tags).                                                                                                                            │
│                                                                                                                                                                      │
│ ## Features                                                                                                                                                          │
│                                                                                                                                                                      │
│ *   **Authentication & Authorization:** Secure user registration, login, token-based authentication (JWT), and role-based access control.                            │
│ *   **Modular Project Structure:** Organized codebase with clear separation of concerns (routes, schemas, services, database models).                                │
│ *   **Database Management:** PostgreSQL integration with SQLAlchemy ORM and Alembic for schema migrations.                                                           │
│ *   **Asynchronous Task Processing:** Celery with Redis as a message broker for handling background tasks (e.g., email notifications, data processing).              │
│ *   **Email Services:** Integration for sending emails (e.g., password resets, account verification).                                                                │
│ *   **Comprehensive Error Handling:** Centralized error handling for consistent API responses.                                                                       │
│ *   **Dependency Injection:** Leverages FastAPI's dependency injection system for clean and testable code.                                                           │
│ *   **Testing:** Unit and integration tests to ensure code reliability.                                                                                              │
│                                                                                                                                                                      │
│ ## Technologies Used                                                                                                                                                 │
│                                                                                                                                                                      │
│ *   **FastAPI:** High-performance web framework for building APIs with Python.                                                                                       │
│ *   **Python:** The primary programming language.                                                                                                                    │
│ *   **SQLAlchemy:** Python SQL toolkit and Object Relational Mapper.                                                                                                 │
│ *   **Alembic:** Lightweight database migration tool for SQLAlchemy.                                                                                                 │
│ *   **PostgreSQL:** Robust relational database.                                                                                                                      │
│ *   **Celery:** Distributed task queue for asynchronous task processing.                                                                                             │
│ *   **Redis:** In-memory data structure store, used as Celery broker and for caching.                                                                                │
│ *   **Pydantic:** Data validation and settings management using Python type hints.                                                                                   │
│ *   **Uvicorn:** ASGI server for running FastAPI applications.                                                                                                       │
│                                                                                                                                                                      │
│ ## Prerequisites                                                                                                                                                     │
│                                                                                                                                                                      │
│ Before you begin, ensure you have the following installed:                                                                                                           │
│                                                                                                                                                                      │
│ *   **Docker** & **Docker Compose:** For running the database, Redis, and Celery services.                                                                           │
│ *   **Python 3.8+**                                                                                                                                                  │
│ *   **pip** (Python package installer)                                                                                                                               │
│                                                                                                                                                                      │
│ ## Getting Started                                                                                                                                                   │
│                                                                                                                                                                      │
│ Follow these steps to set up and run the project locally.                                                                                                            │
│                                                                                                                                                                      │
│ ### 1. Clone the Repository                                                                                                                                          │
│                                                                                                                                                                      │
│ ```bash                                                                                                                                                              │
│ git clone https://github.com/Muhammad-Ubaid-1166/Fastapi_Learning.git                                                                                                │
│ cd FastAPI_Learning                                                                                                                                                  │
│ ```                                                                                                                                                                  │
│                                                                                                                                                                      │
│ ### 2. Set Up Environment Variables                                                                                                                                  │
│                                                                                                                                                                      │
│ Copy the example environment file and fill in your details.                                                                                                          │
│                                                                                                                                                                      │
│ ```bash                                                                                                                                                              │
│ cp .env.example .env                                                                                                                                                 │
│ ```                                                                                                                                                                  │
│                                                                                                                                                                      │
│ Open the  file and configure your database connection string, secret keys, email settings, etc.                                                                      │
│                                                                                                                                                                      │
│ ### 3. Start Services with Docker Compose                                                                                                                            │
│                                                                                                                                                                      │
│ This will spin up PostgreSQL, Redis, and Celery services.                                                                                                            │
│                                                                                                                                                                      │
│ ```bash                                                                                                                                                              │
│ docker-compose up -d                                                                                                                                                 │
│ ```                                                                                                                                                                  │
│                                                                                                                                                                      │
│ ### 4. Install Python Dependencies                                                                                                                                   │
│                                                                                                                                                                      │
│ Create a virtual environment and install the required Python packages.                                                                                               │
│                                                                                                                                                                      │
│ ```bash                                                                                                                                                              │
│ python3 -m venv env                                                                                                                                                  │
│ source env/bin/activate                                                                                                                                              │
│ pip install -r requirements.txt                                                                                                                                      │
│ ```                                                                                                                                                                  │
│                                                                                                                                                                      │
│ ### 5. Run Database Migrations                                                                                                                                       │
│                                                                                                                                                                      │
│ Apply the database schema using Alembic.                                                                                                                             │
│                                                                                                                                                                      │
│ ```bash                                                                                                                                                              │
│ alembic upgrade head                                                                                                                                                 │
│ ```                                                                                                                                                                  │
│                                                                                                                                                                      │
│ ### 6. Run the FastAPI Application                                                                                                                                   │
│                                                                                                                                                                      │
│ ```bash                                                                                                                                                              │
│ uvicorn src.main:app --host 0.0.0.0 --port 8000 --reload          
