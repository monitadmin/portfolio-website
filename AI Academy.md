graph TD
    USERS["👤 Users\nLearners · Instructors · Mentors · Admins"]
    
    subgraph FRONTEND["Presentation Layer"]
        WEB["AngularJS Web App\n+ PWA Client"]
    end

    GATEWAY["🔀 API Gateway\nSpring Cloud Gateway\n(Auth, Routing, Rate Limiting)"]

    subgraph SERVICES["Microservices Layer"]
        MS1["8 Spring Boot\nServices"]
        MS2["Python AI\nEngine"]
    end

    INTEGRATION["🔄 Integration Layer\nApache Kafka + External Adapters"]

    subgraph DATASTORE["Data Access Layer"]
        DB[("PostgreSQL\n+ pgvector")]
        CACHE[("Redis\nCache")]
        SEARCH[("Elasticsearch")]
    end

    EXTERNAL["🌐 External Systems\nGov HR · Registrars · Funding Platforms · Email/SMS"]

    INFRA["🏗️ Infrastructure\nDocker · Docker Compose/Swarm · Jenkins CI/CD"]

    USERS --> FRONTEND
    FRONTEND --> GATEWAY
    GATEWAY --> SERVICES
    SERVICES <--> INTEGRATION
    SERVICES --> DATASTORE
    INTEGRATION --> EXTERNAL
    SERVICES -.->|"Hosted on"| INFRA

    classDef blue fill:#002060,stroke:#002060,color:#fff,font-weight:bold
    classDef mid fill:#2E74B5,stroke:#1F4D78,color:#fff
    classDef green fill:#548235,stroke:#375623,color:#fff
    classDef gold fill:#BF8F00,stroke:#806000,color:#fff
    classDef red fill:#C00000,stroke:#8B0000,color:#fff
    classDef purple fill:#7030A0,stroke:#4B0082,color:#fff

    class USERS blue
    class WEB mid
    class GATEWAY green
    class MS1,MS2 mid
    class INTEGRATION green
    class DB,CACHE,SEARCH gold
    class EXTERNAL red
    class INFRA purple
