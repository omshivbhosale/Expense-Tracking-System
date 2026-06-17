# Expense Tracking System

A full-stack expense management application with a **FastAPI** backend, a **Streamlit** frontend, and a **MySQL** database. Users can add, update, and view daily expenses, and visualize spending breakdowns by category over a date range.

> This project was built as a hands-on implementation while following the **codebasics Python course**. I used it to learn how to connect a frontend, a REST API, and a database into one working application, and how to add logging and tests.

---

## Demo

<!-- TODO: Run the app, take screenshots, and add them here. You already have
some screenshots (analytics and add/update views) — drag them into the GitHub
editor to upload, then reference them like this:
![Add/Update view](app_frontend_ui.png)
![Analytics view](analytics_ui_demo1.png)
-->

*Screenshots coming soon.*

---

## Features

- **Add / update expenses** for any date (amount, category, notes)
- **View expenses** for a selected date
- **Analytics**: total spending and a percentage breakdown by category across a date range
- **REST API** built with FastAPI, with automatic interactive docs at `/docs`
- **Logging** and **unit tests** (pytest)

## Architecture

```
Streamlit frontend  ──HTTP──►  FastAPI backend  ──SQL──►  MySQL database
   (app.py)                      (server.py)              (expenses table)
```

- **Frontend** sends requests to the backend API and renders the UI.
- **Backend** exposes endpoints for fetching, adding/updating, and summarizing expenses.
- **Database** stores all expense records.

## Tech stack

- **Python**
- **FastAPI** — REST API backend
- **Streamlit** — interactive frontend
- **MySQL** — relational database (via `mysql-connector-python`)
- **Pydantic** — request/response validation
- **pytest** — unit testing
- **pandas** — data handling for analytics

## API endpoints

| Method | Endpoint | Description |
|---|---|---|
| `GET`  | `/expenses/{expense_date}` | Get all expenses for a date |
| `POST` | `/expenses/{expense_date}` | Add or update expenses for a date |
| `POST` | `/analytics/` | Get a category breakdown for a date range |

## Project structure

```
Expense-Tracking-System/
├── backend/
│   ├── server.py            # FastAPI app and API endpoints
│   ├── db_helper.py         # Database connection and queries
│   └── logging_setup.py     # Logger configuration
├── frontend/
│   ├── app.py               # Streamlit entry point (tabs)
│   ├── add_update_ui.py     # Add/update expenses tab
│   └── analytics_ui.py      # Analytics tab
├── database/
│   └── expense_db_creation.sql   # SQL script to create the database
├── tests/
│   ├── conftest.py
│   └── backend/
│       └── test_db_helper.py
├── requirements.txt
└── README.md
```

## Setup and run

### 1. Prerequisites
- Python 3.10+
- A running **MySQL** server

### 2. Clone the repository
```bash
git clone https://github.com/omshivbhosale/Expense-Tracking-System.git
cd Expense-Tracking-System
```

### 3. Create and activate a virtual environment
```bash
python -m venv .venv
source .venv/bin/activate      # On Windows: .venv\Scripts\activate
```

### 4. Install dependencies
```bash
pip install -r requirements.txt
```

### 5. Set up the database
Run the SQL script in `database/expense_db_creation.sql` against your MySQL server to create the database and `expenses` table.

> **Note:** Database credentials are set in `backend/db_helper.py`. Update the `host`, `user`, `password`, and `database` values there to match your MySQL setup.

### 6. Run the backend (from the project root)
```bash
uvicorn backend.server:app --reload
```
The API will be available at `http://localhost:8000`, with interactive docs at `http://localhost:8000/docs`.

### 7. Run the frontend (in a separate terminal)
```bash
streamlit run frontend/app.py
```
The app opens in your browser at `http://localhost:8501`.

## Running tests
```bash
pytest
```

## What I learned

- Connecting a **three-tier application**: frontend ↔ REST API ↔ database
- Designing REST endpoints with **FastAPI** and validating data with **Pydantic**
- Writing **SQL queries** for inserts, deletes, and aggregations (category summaries)
- Adding **logging** and **unit tests** to a Python project
- Building an interactive data app with **Streamlit**

## Acknowledgements

Built by following the **codebasics** Python course (codebasics.io). The project concept is from the course; this repository is my own implementation.
