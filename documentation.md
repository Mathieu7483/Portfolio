<p align="center"\>

<img src="https://github.com/Mathieu7483/Portfolio/blob/main/assets/img/image%20dashboard%20documentation.png">

</p>



# 📚 Technical Documentation: Pharma Dashboard API



This document provides the architecture, technical design, and development strategies for the **Pharma Dashboard & Chatbot** project.

## 0\. Mockups 

<p align="center"\>

<img src="https://github.com/Mathieu7483/Portfolio/blob/main/assets/img/Croquis%20du%20dashboard.jpg">

</p>

## 1. Design System Architecture

### 1.1 High-Level Architecture (Service-Oriented)

The application now implements a **Facade Pattern** to decouple the API Layer from the Business Logic, facilitating modular maintenance of the Analytics and Chatbot engines.

```mermaid
graph TD
    subgraph Client_Side["Client Layer (Frontend)"]
        UI["HTML/CSS/JS"] -- JSON/REST --> Router["App Entry (app.py)"]
    end

    subgraph API_Layer["API Layer (api/ folder)"]
        Router --> BA["analytics.py"]
        Router --> BC["chatbot.py"]
        Router --> BS["sales.py"]
    end

    subgraph Service_Layer["Service Layer (services/ folder)"]
        BA & BC & BS --> F["facade.py (The Facade)"]
    end

    subgraph Logic_Layer["Core & Data Layer"]
        F --> CBE["ChatBot_engine.py"]
        F --> DBM["data_manager.py"]
        CBE --> NLU["NLUProcessor.py"]
        DBM --> SQL[("SQLite DB")]
    end

```

---

## 2. Data & Component Design

### 2.1 Entity-Relationship (ER) Summary

The schema is optimized for **Analytics** (tracking sales over time for chart generation).

| Entity | Purpose | Key Attributes | Relationships |
| --- | --- | --- | --- |
| **USER** | Auth & Roles | `id`, `password_hash`, `is_admin` | 1:N with Sales |
| **PRODUCT** | Inventory | `name`, `stock`, `price` | N:M via SALE_ITEM |
| **SALE** | Transactions | `total_amount`, `sale_date` | 1:N with SALE_ITEM |
| **SALE_ITEM** | Junction Table | `quantity`, `price_at_sale` | Links Sale & Product |

---

## 3. Interaction and Flow Diagrams

### 3.1 Analytics & Chart Generation Flow

This flow describes how data is retrieved and formatted specifically for the frontend charts (e.g., sales trends).

```mermaid
sequenceDiagram
    autonumber
    participant C as Client (dashboard.js)
    participant A as API (analytics.py)
    participant F as Facade (facade.py)
    participant DM as DataManager
    participant DB as SQLite

    C->>A: GET /api/analytics/sales-trends
    A->>F: get_sales_performance_data()
    F->>DM: get_all_sales_with_dates()
    DM->>DB: SELECT sale_date, total_amount FROM sales
    DB-->>DM: Raw Rows
    DM-->>F: List of Sale Objects
    F->>F: Process Data (Group by Day/Month for Charts)
    
    alt Data Processing Success
        F-->>A: Formatted Chart JSON (Labels & Datasets)
        A-->>C: 200 OK (Chart.js compatible data)
    else DB Connection Error
        F-->>A: Raise DatabaseError
        A-->>C: 500 Internal Server Error
    end

```

### 3.2 Chatbot Query Flow (Updated)

The chatbot now communicates through the `facade.py` to remain consistent with the rest of the app.

```mermaid
sequenceDiagram
    autonumber
    participant C as Client (chatbot.js)
    participant A as API (chatbot.py)
    participant F as Facade (facade.py)
    participant CBE as ChatBotEngine
    
    C->>A: POST /api/chatbot/query (text)
    A->>F: handle_chat_query(text)
    F->>CBE: get_response(text)
    Note right of CBE: NLU Analysis & DB Lookup via Facade
    CBE-->>F: Response String
    F-->>A: JSON Response
    A-->>C: 200 OK

```

---

## 4. API Endpoints (Internal)

| Endpoint | File | Purpose | Logic Owner |
| --- | --- | --- | --- |
| `POST /api/auth/login` | `auth.py` | User login & JWT | `facade.py` |
| `GET /api/analytics/kpis` | `analytics.py` | Top dashboard cards | `facade.py` |
| `GET /api/analytics/charts` | `analytics.py` | **Data for GraphJS/ApexCharts** | `facade.py` |
| `POST /api/chatbot/query` | `chatbot.py` | Natural Language processing | `ChatBot_engine.py` |

---

## 5. QA & Deployment Strategies

* **Security Scanning:** **Bandit** is used to scan the `Server/` directory for vulnerabilities (SQL injection, hardcoded secrets).
* **Data Seeding:** The `utils/seeder.py` script populates the database from `initial_inventory.csv` and `data_seed.json` for testing environments.
* **Static Analysis:** `Pycodestyle` ensures PEP 8 compliance across all modules.

---

## 6. Technical Justifications

* **Facade Pattern:** By using `facade.py` in the `services/` folder, we create a single entry point for all business logic. This makes the `api/` routes extremely thin and easy to test.
* **Separated Models:** Each entity (`product.py`, `sale.py`) has its own file in `models/`, allowing for specialized methods (e.g., a `Product` object knowing how to check its own stock levels).
* **Analytics Module:** Dedicated analytics routes allow for heavy data processing (aggregations, time-series formatting) to happen on the server, sending only the "ready-to-plot" JSON to the client.

---
