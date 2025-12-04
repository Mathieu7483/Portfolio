# 💊 Dashboard Pharma - The Intelligent Pharmacy Management System

## 🚀 Project Overview (MVP)

The **Dashboard Pharma** is an intelligent, web-based Minimum Viable Product (MVP) designed to centralize and modernize the daily operations of independent pharmacies. It replaces fragmented tools (Excel, paper) with a secure, unified platform.

| Key Metric | Detail |
| :--- | :--- |
| **MVP Goal** | Centralized Stock Management (CRUD) + Secure Authentication (JWT) + AI Chatbot Core. |
| **Problem Solved** | Fragmentation of tools, resulting in time loss, stock errors, and lack of proactive critical alerts (e.g., drug interactions). |
| **Core Value** | Proactivity and Centralization. The system alerts the team instead of waiting for passive consultations. |
| **Target Audience** | Pharmacists and Pharmacy Technicians (2-8 employees). |

---

## 🛠️ Technical Stack

This project is built using a robust Python-based stack.

| Component | Technology | Role |
| :--- | :--- | :--- |
| **Backend Core** | Python 3.x, Flask | Core application framework. |
| **API** | Flask-RESTx | RESTful API definition, automatic Swagger documentation, and validation. |
| **Database** | SQLAlchemy (ORM), SQLite (MVP) | Object-Relational Mapping for structured data management. |
| **Security** | Flask-JWT-Extended, Bcrypt | Token-based authentication, Role-Based Access Control (RBAC), and password hashing. |
| **Frontend (MVP)** | HTML5, CSS3, Vanilla JavaScript | Responsive user interface. |
| **AI/NLP** | NLTK / spaCy (Planned) | Basic Natural Language Processing for the Chatbot logic. |

---

## 💻 1. MVP Features (In Scope)

The Minimum Viable Product focuses on delivering essential, secure functionality before expanding.

| Priority | Feature | Description |
| :--- | :--- | :--- |
| **CRITICAL** | **Secure API** | Full CRUD operations on inventory (`/products`). All endpoints secured by JWT with Role/Ownership access control. |
| **CRITICAL** | **Stock Management** | List, add, modify, delete medications, including low stock alert mechanisms. |
| **CRITICAL** | **Authentication** | `POST /auth/login` to obtain JWT token. Access control based on user roles (`is_admin`). |
| **HIGH** | **Intelligent Chatbot** | Core rules logic for checking drug interactions and retrieving quick info (calendar, stock). |
| **MEDIUM** | **Sales Tracking** | Basic sales recording and simple visualization statistics (Top sellers, Revenue). |
| **MEDIUM** | **Team Calendar** | Internal team scheduling and shift management. |

---

## ⚙️ 2. Project Architecture & Setup

### 2.1. Project Structure

The structure follows the Flask convention for larger applications, utilizing the **Factory Pattern** (`create_app`) and **Separation of Concerns** (SoC).

```

.
├── Server/
│   ├── api/
│   │   ├── **init**.py
│   │   ├── auth.py         \# Login, Register, Token Management
│   │   └── products.py     \# CRUD operations for inventory (SECURED)
│   ├── config.py           \# Configuration (Dev/Test/Prod)
│   ├── database/
│   │   └── initial\_inventory.csv \# Initial data for seeding
│   ├── models/             \# SQLAlchemy ORM models (User, Product, Sale)
│   ├── run.py              \# Application entry point (Starts server)
│   ├── run\_seed.py         \# Database Seeding Logic (Admin, Products)
│   ├── services/           \# Business Logic Layer
│   │   └── facade.py       \# Facade/Service layer interaction
│   └── app.py              \# Application Factory & Extension Initialization
├── venv/
└── README.md

````

### 2.2. Getting Started (Development)

1.  **Clone the repository:**
    ```bash
    git clone [YOUR_REPO_URL]
    cd Dashboard-Pharma/Server
    ```

2.  **Create a virtual environment (`venv`):**
    ```bash
    python3 -m venv venv
    source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
    ```

3.  **Install dependencies:**
    *(Assuming a `requirements.txt` is present)*
    ```bash
    pip install -r requirements.txt
    ```

4.  **Run the application:**
    The `run.py` script will automatically create the database (`database.sqlite`), seed the initial `admin` user, and import products from the CSV file before starting the server.
    ```bash
    python3 run.py
    ```

The API will be accessible at: **`http://127.0.0.1:5000/`**

---

## 🔑 3. Authentication & Testing

### Accessing Secured Routes

All critical routes (e.g., `/products/`) require a valid JWT token.

1.  **Login (Get Token):** Use the Swagger UI at `http://127.0.0.1:5000/` to send a `POST` request to **`/auth/login`** with the initial administrator credentials:
    * **Username:** `admin`
    * **Password:** `adminpass`

2.  **Test Token Validity:** Use the retrieved `access_token` to test the **`/auth/me`** endpoint.

3.  **Test Product API:** Use the `access_token` to access the secured **`/products/`** endpoints.

---

## 🗺️ 4. Project Roadmap (Post-MVP)

The following functionalities are planned for development after the MVP is stable:

| Phase | Feature | Description |
| :--- | :--- | :--- |
| **Phase 2** | Full Sales Module | Implementation of the `SaleModel` for accurate transactional tracking and stock deduction. |
| **Phase 2** | Advanced Reporting | Financial dashboards, historical sales trends, and stock forecasting. |
| **Phase 3** | Advanced Chatbot | Integration of machine learning (ML) models for better NLP, advanced clinical decision support. |
| **Phase 3** | External Integrations | Synchronization with external calendars (Google Calendar) or national drug databases. |


````
