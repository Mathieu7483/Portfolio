## 2\. Entity-Relationship (ER) Model: Summary Table

This table details the six core entities (tables) in SQLite database, their main responsibilities, key attributes, and how they relate to one another via Foreign Keys.

| Entity (Table) | Purpose | Key Attributes (Columns) | Relationships (Foreign Keys) |
| :--- | :--- | :--- | :--- |
| **USER** | Represents pharmacy employees (who log in) and their access rights. | `id` (PK), `username`, `password_hash`, `is_admin`, `email` (inherited) | **1:N with SALE** (records the sale)<br>**1:N with CLIENT, DOCTOR** (manages records) |
| **PRODUCT** | Manages the inventory of drugs and products. Contains drug-specific data for the Chatbot. | `id` (PK), `name`, `stock`, `price`, `active_ingredient`, `dosage`, `is_prescription_only` | **N:M with SALE** (via `SALE_ITEM`) |
| **CLIENT** | Record of clients (optional, used for prescription tracking). | `id` (PK), `first_name`, `last_name`, `email`, `user_id` (FK) | **N:1 with USER** (record created by)<br>**N:1 with SALE** (sale associated with) |
| **DOCTOR** | Record of physicians (for prescription analysis and tracking). | `id` (PK), `first_name`, `last_name`, `email`, `phone`, `specialty`, `user_id` (FK) | **N:1 with USER** (record created by)<br>**N:1 with SALE** (prescription provided by) |
| **SALE** | Represents the overarching transaction (the 'receipt' or 'ticket'). | `id` (PK), `total_amount`, `sale_date`, `prescription_provided`, `user_id` (FK), `client_id` (FK), `doctor_id` (FK) | **N:1 with USER, CLIENT, DOCTOR**<br>**1:N with SALE\_ITEM** (contains line items) |
| **SALE\_ITEM** | **Junction Table** (M:N). Represents a single product line item within a sale. | `sale_id` (FK), `product_id` (FK), `quantity`, `price_at_sale` | **N:1 with SALE**<br>**N:1 with PRODUCT** |
