graph LR
    subgraph Client [Presentation Layer (Frontend)]
        A[HTML/CSS/JS] -- API Requests --> B{Web Browser}
    end

    subgraph Server [Application Logic Layer (Backend Python)]
        C(REST API Endpoints) --> D[Services & Managers]
        D --> E[Core NLP (SpaCy)]
        D --> F[DatabaseManager]
    end

    subgraph Data [Persistence Layer]
        G((SQLite Database))
        H[[CSV/JSON Files (Drug Knowledge)]]
    end

    B -- HTTPS/JSON --> C
    F --> G
    F --> H
    
    style A fill:#DCEFFB, stroke:#333
    style C fill:#F0F8FF, stroke:#333
    style G fill:#F0FFF0, stroke:#333
