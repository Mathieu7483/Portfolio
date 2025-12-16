classDiagram
    direction BT

    class BaseModel {
        +string id
        +datetime created_at
        +datetime updated_at
        +save()
        +delete()
    }

    class PersonModel {
        +string first_name
        +string last_name
        +string address
    }
    
    class UserModel {
        +string username
        +string password_hash
        +bool is_admin
        +set_password(password)
        +check_password(password)
    }

    class ClientModel {
        +string email
        +string user_id (FK)
    }

    class DoctorModel {
        +string email
        +string specialty
        +string phone
        +string user_id (FK)
    }

    class ProductModel {
        +string name
        +string active_ingredient
        +string dosage
        +int stock
        +float price
        +bool is_prescription_only
        +string user_id (FK)
        +SaleItemModel[] sales_entries
    }
    
    class SaleItemModel {
        +int quantity
        +float price_at_sale
        +string sale_id (FK)
        +string product_id (FK)
    }
    
    class SaleModel {
        +float total_amount
        +datetime sale_date
        +bool prescription_provided
        +string doctor_id (FK)
        +string user_id (FK)
        +string client_id (FK)
        +SaleItemModel[] items
    }
    
    class DatabaseManager {
        +save()
        +get_product_info(name)
        +update_stock(id, qty)
    }
    
    class DashboardManager {
        -DatabaseManager db_manager
        +map get_kpis_summary()
    }
    
    BaseModel <|-- PersonModel
    PersonModel <|-- UserModel
    PersonModel <|-- ClientModel
    PersonModel <|-- DoctorModel
    BaseModel <|-- ProductModel
    BaseModel <|-- SaleModel
    
    SaleModel "1" *-- "*" SaleItemModel : includes
    ProductModel "1" *-- "*" SaleItemModel : part of
    
    DatabaseManager <-- DashboardManager : uses
    DatabaseManager <-- ChatBot_engine : queries