<p align="center">
<img src="https://github.com/Mathieu7483/Portfolio/blob/main/assets/img/image%20dashboard%20documentation.png">
</p>

# 📚 Technical Documentation: Pharma Dashboard API

This document provides the architecture, technical design, and development strategies for the **Pharma Dashboard & Chatbot** project.
### 0.1 Prioritized User Stories

| Role | Requirement | Goal | Priority |
| :--- | :--- | :--- | :--- |
| **Pharmacist** | As a user, I want to process a sale and check stock levels. | To ensure product availability and record transactions. | **Must** |
| **Pharmacist** | As a user, I want to register a new doctor or client on the fly. | To complete a sale requiring a prescription without delay. | **Must** |
| **Admin** | As an administrator, I want to manage employee accounts and roles. | To secure access to sensitive pharmaceutical data. | **High** |
| **Admin** | As an administrator, I want to revert a sale and restore stock. | To correct human errors in inventory management. | **High** |
| **Staff** | As a user, I want to ask the "Caducée" AI about inventory, clients, Doctors status, and more (plannings, notifications etc...). | To get hands-free, real-time data while assisting clients. | **Medium** |


## 0. Mockups

<p align="center">
<img src="https://github.com/Mathieu7483/Portfolio/blob/main/assets/img/Croquis%20du%20dashboard.jpg">
</p>

<em>Figure 1: Initial hand-drawn wireframe highlighting the core layout (Sidebar, KPI Cards, and Data Table). This original vision served as the blueprint for the final implementation using Material Design principles.</em> </p>


<p align="center">
<img src="https://github.com/Mathieu7483/Dashboard-Pharma/blob/main/Client/assets/img/Dashboard%20Mokup%20v2.png">
</p>

<em>Figure 2: Pre-Final high-fidelity Dashboard, integrating analytical widgets, CRM management, and the "Caducée" AI assistant within a sleek Material Design interface.</em> </p>

## 1. Design System Architecture

### 1.1 High-Level Architecture (Service-Oriented)

The application implements a **Facade Pattern** to decouple the API Layer from the Business Logic, facilitating modular maintenance of the Analytics, Inventory, and Chatbot engines.

```mermaid
graph TD
    subgraph Client_Layer["Client Side (Frontend)"]
        UI["HTML (index, auth, doctors...)"]
        JS["JS (dashboard, auth, doctors...)"]
        UI --- JS
    end

    subgraph API_Layer["Server: API Layer (api/ folder)"]
        Router["app.py (Flask/FastAPI)"]
        Router --> A_AUTH["auth.py"]
        Router --> A_CLI["clients.py"]
        Router --> A_DOC["doctors.py"]
        Router --> A_INV["inventory.py"]
        Router --> A_CB["chatbot.py"]
    end

    subgraph Service_Layer["Server: Service Layer"]
        A_AUTH & A_CLI & A_DOC & A_INV & A_CB --> F["facade.py"]
    end

    subgraph Model_Layer["Server: Models Layer (models/ folder)"]
        F --> BM["basemodel.py"]
        BM --> M_USR["user.py"]
        BM --> M_CLI["client.py"]
        BM --> M_DOC["doctor.py"]
        BM --> M_PRO["product.py"]
    end

    subgraph Logic_Data_Layer["Server: Core & Database"]
        F --> CBE["ChatBot_engine.py"]
        CBE --> NLU["NLUProcessor.py"]
        F --> DBM["data_manager.py"]
        DBM --> DB[("SQLite DB")]
    end

    JS -- "REST/JSON" --> Router

```

---

## 2. Data & Component Design

### 2.1 Entity-Relationship (ER) Summary (Updated)
```mermaid
erDiagram
    USER ||--o{ PRODUCT : "creates"
    USER ||--o{ SALE : "processes"
    USER ||--o{ CLIENT : "manages"
    USER ||--o{ DOCTOR : "manages"
    CLIENT ||--o{ SALE : "associated_with"
    DOCTOR ||--o{ SALE : "prescribes"
    SALE ||--|{ SALE_ITEM : "contains"
    PRODUCT ||--o{ SALE_ITEM : "is_sold_in"

    USER {
        string id PK "UUID"
        string username UK
        string password_hash
        string first_name
        string last_name
        string email
        string address
        boolean is_admin
        datetime created_at
        datetime updated_at
    }

    PRODUCT {
        string id PK "UUID"
        string name UK
        string active_ingredient
        string dosage
        int stock
        float price
        boolean is_prescription_only
        string user_id FK
    }

    SALE {
        string id PK "UUID"
        float total_amount
        datetime sale_date
        boolean prescription_provided
        string user_id FK
        string doctor_id FK
        string client_id FK
    }

    SALE_ITEM {
        string id PK "UUID"
        string sale_id FK
        string product_id FK
        int quantity
        float price_at_sale
    }

    DOCTOR {
        string id PK "UUID"
        string first_name
        string last_name
        string email UK
        string specialty
        string phone
        string address
        string user_id FK
        datetime created_at
        datetime updated_at
    }

    CLIENT {
        string id PK "UUID"
        string first_name
        string last_name
        string email UK
        string phone
        string address
        string user_id FK
        datetime created_at
        datetime updated_at
    }
```

The schema is optimized for **Regulatory Compliance** and **Pharmacy Analytics**.

### 📊 Entity Details & Key Attributes

| Entity | Model File | Key Attributes (SQLAlchemy) | Purpose |
| :--- | :--- | :--- | :--- |
| **Product** | \`product.py\` | \`active_ingredient\`, \`dosage\`, \`stock\`, \`price\`, \`is_prescription_only\` | Pharmaceutical inventory management. |
| **Sale** | \`sale.py\` | \`total_amount\`, \`sale_date\`, \`prescription_provided\` | Main transaction record (The Receipt). |
| **SaleItem** | \`sale.py\` | \`quantity\`, \`price_at_sale\` | Junction table for Many-to-Many (Sale <-> Product). |
| **User** | \`user.py\` | \`username\`, \`password_hash\`, \`role\` | Auth & Ownership (\`user_id\` in Products/Sales). |
| **Doctor** | \`doctor.py\` | \`first_name\`, \`specialty\`, \`license_no\` | Regulatory reference for prescriptions. |
| **Client** | \`client.py\` | \`first_name\`, \`last_name\`, \`email\` | Patient tracking for medication history. |

### 🔗 Logic & Relationships

1. **Many-to-Many**: \`SaleModel\` and \`ProductModel\` are linked via \`SaleItemModel\`.
2. **Regulatory Link**: \`SaleModel\` includes \`doctor_id\` and \`prescription_provided\` to validate the sale of products where \`is_prescription_only=True\`.
3. **Ownership**: Every product is linked to a \`user_id\` (the person who added it to the inventory).
4. **Data Integrity**: \`SaleItemModel\` stores \`price_at_sale\` to preserve historical data even if the product price changes later.

---

## 3. Interaction and Flow Diagrams

### 3.1 Analytics & Chart Generation Flow
#### 3.1.1 Sequences diagram for POST Request for a client
```mermaid
sequenceDiagram
    participant UI as Frontend (JS)
    participant API as API Layer (Clients/Docs)
    participant F as FacadeService
    participant DB as SQLite (Models)

    Note over UI, API: User fills the form & clicks 'Create'
    UI->>API: POST /clients/ or /doctors/ (JSON + JWT)
    
    API->>API: Authenticate User (JWT Required)
    
    API->>F: create_entity(data)
    
    F->>F: Validate Business Rules (e.g. Unique License No)
    
    F->>DB: Instantiate Model & Save to DB
    DB-->>F: Success (Object ID generated)
    
    F-->>API: New Entity Object
    API-->>UI: 201 Created (Success Message)
```
#### 3.1.2 Sequences diagram for Create a sale (relation with client, and products)

```mermaid

sequenceDiagram
    participant UI as Frontend (JS)
    participant API as Sales API
    participant F as FacadeService
    participant DB as SQLite (Models)

    UI->>API: POST /sales/ (JWT + items_data)
    API->>API: Validate Token & Payload
    API->>F: process_sale(items_data, client_id)
    
    loop Check Stock & Prescription
        F->>DB: Query Product Stock & is_prescription_only
        DB-->>F: Product Data
        alt Insufficient Stock
            F-->>API: raise ValueError("Stock error")
            API-->>UI: 400 Bad Request
        end
    end

    F->>DB: Create Sale & SaleItems
    F->>DB: Update Product Inventory (Decrement)
    DB-->>F: Success
    F-->>API: New Sale Object
    API-->>UI: 201 Created (SaleOutput)
```

### 3.2 Chatbot Query Flow
```mermaid
sequenceDiagram
    participant U as User (Pharmacist)
    participant CB as ChatBot_engine.py
    participant NLU as NLUProcessor.py
    participant F as facade.py
    participant DB as SQLite DB

    U->>CB: "How many Amoxicillin in stock?"
    CB->>NLU: Parse intent & extract entity (Product: Amoxicillin)
    NLU-->>CB: Intent: check_stock | Entity: Amoxicillin
    
    Note over CB, F: The Chatbot calls the Facade for real-time data
    
    CB->>F: get_product_by_name("Amoxicillin")
    F->>DB: Query stock level
    DB-->>F: {name: "Amoxicillin", stock: 120}
    F-->>CB: Return Product Data
    
    CB->>CB: Generate Natural Language Response
    CB-->>U: "We currently have 120 units of Amoxicillin in stock."
```

The chatbot utilizes the `facade.py` to fetch real-time stock or price data before responding to the user.

----
### 3.3 Chatbot Sate diagram
```mermaid
stateDiagram-v2
    [*] --> Idle: User input received
    Idle --> Processing: NLU Analysis
    
    state Processing {
        [*] --> IntentIdentification
        IntentIdentification --> EntityExtraction
    }

    Processing --> DataLookup: Intent & Entity found
    Processing --> ErrorState: Unknown Intent/Missing Entity
    
    state DataLookup {
        [*] --> FacadeCall
        FacadeCall --> Success: Product/Data exists
        FacadeCall --> Failure: Product not in DB
    }

    Success --> ResponseGeneration: Formatting result
    Failure --> ResponseGeneration: "Product not found" message
    ErrorState --> ResponseGeneration: "I don't understand" message
    
    ResponseGeneration --> [*]: Send response to UI
```

---

## 4. API Endpoints (Comprehensive List)

| Entity | Route | Method | Required Role | Specific Rule |
| :--- | :--- | :--- | :--- | :--- |
| **Auth** | \`/auth/login\` | POST | Public | Returns JWT + \`is_admin\`. |
| **Users** | \`/users/\` | GET | Authenticated | List all employees. |
| **Users** | \`/users/\` | POST | **Admin** | Create employee (Default: non-admin). |
| **Users** | \`/users/<id>\` | GET/PUT | **Self or Admin** | Self-update or Admin oversight. |
| **Users** | \`/users/<id>\` | DELETE | **Admin** | Cannot delete your own account. |
| **Products** | \`/products/\` | POST | **Admin** | Regulatory compliance check. |
| **Products** | \`/products/<id>\`| PUT/DEL | **Admin** | Inventory & Price management. |
| **Doctors** | \`/doctors/\` | GET/POST | Authenticated | Employees can register new doctors. |
| **Doctors** | \`/doctors/<id>\` | PUT | **Admin/Owner** | Update healthcare provider details. |
| **Doctors** | \`/doctors/<id>\` | DELETE | **Admin** | Restricted (Data integrity for RX). |
| **Clients** | \`/clients/\` | GET/POST | Authenticated | Create/List patients for transactions. |
| **Clients** | \`/clients/<id>\` | PUT | Authenticated | Update patient contact information. |
| **Clients** | \`/clients/<id>\` | DELETE | **Admin** | Hard delete of patient records. |
| **Sales** | \`/sales/\` | POST | Authenticated | Stock check + Prescription validation. |
| **Sales** | \`/sales/<id>\` | DELETE | **Admin** | Reverts stock upon deletion. |

### 🛠️ Key Security Mechanisms Implemented
* **Token Claims:** Using \`get_jwt().get('is_admin')\` to avoid database round-trips for permission checks.
* **Payload Protection:** The \`UserInput\` model excludes \`is_admin\` to prevent self-elevation during registration.
* **Stock Integrity:** Deleting a sale (Admin only) triggers a stock restoration logic in \`facade.py\`.
EOF

---

## 5. QA & Deployment Strategies

* **Security Scanning:** **Bandit** is used to scan the `Server/` directory for vulnerabilities (SQL injection, hardcoded secrets).
* **Data Seeding:** The `utils/seeder.py` script populates the database from `initial_inventory.csv` for consistent testing.
* **Static Analysis:** `Pycodestyle` ensures PEP 8 compliance.
* **Frontend Consistency:** Unified CSS variables and shared `navbar.html` ensure a seamless UX across modules.

---

## 6. Technical Justifications

* **Facade Pattern:** Centralizes business logic. If we switch from SQLite to PostgreSQL, only the `data_manager` and `facade` are affected; the API routes remain untouched.
* **Separated Models:** Each entity resides in `models/`, allowing for robust OOP practices (e.g., the `ProductModel` handles its own dictionary conversion).
* **Audit-Ready Inventory:** The inclusion of `is_prescription_only` and `active_ingredient` fields ensures the system meets modern pharmaceutical software standards.

