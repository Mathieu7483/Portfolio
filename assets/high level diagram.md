graph TD
    subgraph Client [Couche Présentation (Frontend Web)]
        A[HTML/CSS/JavaScript] -- Requêtes REST (JSON) --> B(API Gateway/Router)
    end

    subgraph Server [Couche Logique Applicative (Backend Python)]
        B --> R{Routage des Requêtes}

        subgraph Gestion API & Services (dossier api/)
            R --> P[API Products/Inventory]
            R --> S[API Sales/Transactions]
            R --> U[API Users/Auth]
            R --> CD[API Clients/Doctors]
            R --> CB[Chatbot API]
        end
        
        S --> M(DashboardManager)
        
        % Dépendances Logiques
        CB --> E[NLU Processor (SpaCy)]
        P --> F(DatabaseManager)
        S --> F
        U --> F
        CD --> F
        M --> F
    end

    subgraph Persistence [Couche de Données]
        F --> H((SQLite Database))
        E --> I[[Fichiers de Connaissances Médicaments]]
    end

    style A fill:#DCEFFB, stroke:#333
    style B fill:#e0f7fa, stroke:#00BCD4
    style F fill:#FFF8E1, stroke:#FFC107
    style H fill:#E8F5E9, stroke:#4CAF50
