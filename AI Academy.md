flowchart TD


    %% 1. Users Layer
    subgraph Users [👨‍🎓 1. Users]
        direction LR
        U1([Learners])
        U2([Instructors])
        U3([Mentors])
        U4([Admins])
    end
    class Users,U1,U2,U3,U4 userLayer

    %% 2. Presentation Layer
    subgraph Presentation [📱 2. Presentation Layer]
        P1[AngularJS + PWA Client]
    end
    class Presentation,P1 presentationLayer

    %% Infrastructure Envelope wrapping Backend Systems
    subgraph Infrastructure [⚙️ Infrastructure: Docker, Docker Compose/Swarm, Jenkins CI/CD]
        
        %% 3. API Gateway Layer
        subgraph APIGateway [🚪 3. API Gateway Layer]
            G1[Spring Cloud Gateway<br/>Auth, Routing, Rate Limiting]
        end

        %% 4. Microservices Layer
        subgraph Microservices [🧩 4. Microservices Layer]
            direction LR
            M1[8 Spring Boot Services]
            M2[Python AI Engine]
        end

        %% 5. Integration Layer
        subgraph Integration [🔄 5. Integration Layer]
            direction LR
            I1[Apache Kafka Event Bus]
            I2[External Adapters]
        end

        %% 6. Data Access Layer
        subgraph DataAccess [💾 6. Data Access Layer]
            direction LR
            D1[(PostgreSQL + pgvector)]
            D2[(Redis Cache)]
            D3[(Elasticsearch)]
        end
    end
    class Infrastructure infraLayer
    class APIGateway,G1 gatewayLayer
    class Microservices,M1,M2 microservicesLayer
    class Integration,I1,I2 integrationLayer
    class DataAccess,D1,D2,D3 dataLayer

    %% External Systems
    subgraph ExternalSystems [🌐 External Systems]
        direction LR
        E1[Gov HR]
        E2[University Registrars]
        E3[Funding Platforms]
        E4[Email/SMS]
    end
    class ExternalSystems,E1,E2,E3,E4 externalLayer

    %% --- Connections & Data Flow ---
    
    U1 & U2 & U3 & U4 -->|HTTPS Interact| P1
    P1 -->|API Requests| G1
    G1 -->|Routed & Authenticated| M1 & M2
    
    M1 <-->|Produce/Consume Events| I1
    M2 <-->|AI Task Queueing| I1
    I1 <-->|Transform & Route| I2
    
    M1 -->|CRUD & Queries| D1
    M1 -->|Cache Get/Set| D2
    M1 -->|Full-Text Search| D3
    M2 -->|Vector Search / Embeddings| D1
    
    I2 -->|API Calls / Webhooks| E1 & E2 & E3 & E4
