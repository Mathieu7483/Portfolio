sequenceDiagram
    participant C as Client (dashboard.js)
    participant API as API Route (/dashboard/kpis)
    participant DM as DashboardManager
    participant DB as DatabaseManager
    participant DATA as Persistence (SQLite/Files)

    C->>API: 1. GET /dashboard/kpis (Demande d'affichage)
    activate API
    
    API->>DM: 2. Requête: get_kpis_summary()
    activate DM
    
    DM->>DB: 3. Requête: get_all_inventory_data()
    activate DB
    
    DB->>DATA: 4. Lecture des tables Product & Sale
    DATA-->>DB: 4.1 Retour: Données brutes
    deactivate DB
    
    DM->>DM: 5. Calcul des KPIs (Stock Critique, Top Ventes, Alertes Péremption)
    
    DM-->>API: 6. Retour: KPIs Finalisés (JSON)
    deactivate DM
    
    API-->>C: 7. HTTP 200 OK (Affichage Dashboard)
    deactivate API