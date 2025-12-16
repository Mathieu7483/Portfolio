sequenceDiagram
    participant C as Client (Chatbot Window)
    participant API as API Route (/chatbot/query)
    participant CH as ChatBot_engine
    participant NLP as NLUProcessor (SpaCy)
    participant DB as DatabaseManager

    C->>API: 1. POST /chatbot/query (user_query)
    activate API
    
    API->>CH: 2. process_query(user_query)
    activate CH
    
    CH->>NLP: 3. extract_entities(user_query)
    activate NLP
    
    alt Entité (Médicament) Trouvée
        NLP-->>CH: 3.1 Retour: Entité et Intention
        deactivate NLP
        
        CH->>DB: 4. get_drug_info(entity_name)
        activate DB
        
        DB-->>CH: 4.1 Retour: Données du Médicament
        deactivate DB
        
        CH->>CH: 5. Génération de la Réponse Formattée
    else Entité Non Trouvée
        NLP-->>CH: 3.2 Retour: Intention Générique
        deactivate NLP
        
        CH->>CH: 5. Génération de Réponse par Défaut
    end

    CH-->>API: 6. Retour: Réponse Chatbot (JSON)
    deactivate CH
    
    API-->>C: 7. HTTP 200 OK (Réponse)
    deactivate API
    
    C->>C: 8. Affichage de la Réponse