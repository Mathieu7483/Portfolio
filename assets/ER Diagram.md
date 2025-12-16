erDiagram
    % --- Core Entities ---
    USER ||--o{ SALE : records
    USER ||--o{ CLIENT : manages
    USER ||--o{ DOCTOR : manages 
    
    CLIENT ||--o{ SALE : associated_with
    DOCTOR |o--o{ SALE : prescribed_for
    
    PRODUCT ||--o{ SALE_ITEM : includes
    SALE ||--o{ SALE_ITEM : contains
    
    % --- Entity Details ---
    USER {
        string id PK
        string username
        string password_hash
        bool is_admin
    }

    CLIENT {
        string id PK
        string first_name
        string last_name
        string email
        string user_id FK "Manager"
    }

    DOCTOR {
        string id PK
        string first_name
        string last_name
        string email
        string phone
        string specialty
        string user_id FK "Manager"
    }

    PRODUCT {
        string id PK
        string name
        string active_ingredient
        int stock
        float price
        bool is_prescription_only
    }
    
    SALE {
        string id PK
        float total_amount
        datetime sale_date
        bool prescription_provided
        string user_id FK "Employee"
        string client_id FK 
        string doctor_id FK 
    }
    
    SALE_ITEM {
        string sale_id FK
        string product_id FK
        int quantity
        float price_at_sale
    }