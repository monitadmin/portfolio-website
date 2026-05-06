```mermaid

graph TD
    USERS["👤 Users\nClinicians · Nurses · CHWs · Admins"]
    
    subgraph FRONTEND["Presentation Layer"]
        WEB["Angular Web App"]
        MOBILE["Flutter Mobile App"]
    end

    GATEWAY["🔀 API Gateway\nSpring Cloud Gateway"]

    subgraph SERVICES["Microservices Layer (Java Spring Boot)"]
        MS1["Course\nManagement"]
        MS2["Assessment &\nCertification"]
        MS3["AI Engine\n(Python)"]
        MS4["Simulation\nEngine"]
        MS5["Notifications"]
        MS6["User\nManagement"]
        MS7["Analytics"]
    end

    BROKER["📨 Message Broker\nRabbitMQ / Kafka"]

    subgraph DATASTORE["Data Layer"]
        DB[("PostgreSQL\n/ MySQL")]
        CACHE[("Redis\nCache")]
        CDN["CDN\n(Video)"]
    end

    EXTERNAL["🌐 External Systems\nDHIS2 · OpenMRS · CPD Bodies\nSCORM/xAPI · SMS/Email"]

    INFRA["🏗️ Infrastructure\nDocker · Kubernetes · CI/CD"]

    USERS --> FRONTEND
    FRONTEND --> GATEWAY
    GATEWAY --> SERVICES
    SERVICES <--> BROKER
    SERVICES <--> DATASTORE
    BROKER <--> EXTERNAL
    SERVICES -.->|"Deployed on"| INFRA

    classDef blue fill:#002060,stroke:#002060,color:#fff,font-weight:bold
    classDef mid fill:#2E74B5,stroke:#1F4D78,color:#fff
    classDef green fill:#548235,stroke:#375623,color:#fff
    classDef gold fill:#BF8F00,stroke:#806000,color:#fff
    classDef red fill:#C00000,stroke:#8B0000,color:#fff
    classDef purple fill:#7030A0,stroke:#4B0082,color:#fff

    class USERS blue
    class WEB,MOBILE mid
    class GATEWAY green
    class MS1,MS2,MS3,MS4,MS5,MS6,MS7 mid
    class BROKER green
    class DB,CACHE,CDN gold
    class EXTERNAL red
    class INFRA purple
Much cleaner — 7 layers, one node each (except the microservices detail which is the core of the architecture), with simple directional flows between them. Paste into mermaid.live to render and export. Want me to insert the rendered image back into the document?


