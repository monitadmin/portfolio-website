```mermaid

graph TD
    %% ── Users / Actors ──
    subgraph USERS["👤 USERS / ACTORS"]
        U1["Clinicians"]
        U2["Nurses"]
        U3["Community Health Workers"]
        U4["Administrators"]
        U5["MoH Officials"]
    end

    %% ── Presentation Layer ──
    subgraph PRESENTATION["📱 PRESENTATION LAYER"]
        WEB["Angular Web App"]
        MOBILE["Flutter Mobile App\n(Offline-First)"]
    end

    USERS -->|"HTTPS Requests"| PRESENTATION

    %% ── API Gateway Layer ──
    subgraph GATEWAY["🔀 API GATEWAY LAYER"]
        GW["Spring Cloud Gateway"]
        GW_AUTH["Authentication\n(JWT / OAuth 2.0)"]
        GW_RL["Rate Limiting"]
        GW_LB["Load Balancing"]
        GW_ROUTE["Request Routing"]
    end

    WEB -->|"REST API Calls"| GW
    MOBILE -->|"REST API Calls"| GW
    GW --- GW_AUTH
    GW --- GW_RL
    GW --- GW_LB
    GW --- GW_ROUTE

    %% ── Business Logic / Microservices Layer ──
    subgraph MICROSERVICES["⚙️ BUSINESS LOGIC / MICROSERVICES LAYER (Java Spring Boot)"]
        MS1["Course Management\nService"]
        MS2["Assessment &\nCertification Service"]
        MS3["AI Recommendation\nEngine (Python)"]
        MS4["Simulation\nEngine"]
        MS5["Notification\nService"]
        MS6["User & Access\nManagement"]
        MS7["Analytics &\nReporting Service"]
    end

    GW -->|"Routes to Services"| MS1
    GW --> MS2
    GW --> MS3
    GW --> MS4
    GW --> MS5
    GW --> MS6
    GW --> MS7

    %% ── Integration Layer ──
    subgraph INTEGRATION["🔗 INTEGRATION LAYER"]
        MQ["Message Brokers\n(RabbitMQ / Kafka)"]
        ADAPT["Integration Adapters\n(DHIS2, OpenMRS, HR Systems)"]
    end

    MS1 <-->|"Events"| MQ
    MS2 <-->|"Events"| MQ
    MS3 <-->|"Events"| MQ
    MS5 <-->|"Events"| MQ
    MS7 <-->|"Events"| MQ
    MQ <--> ADAPT

    %% ── Data Access Layer ──
    subgraph DATA["🗄️ DATA ACCESS LAYER"]
        DB[("PostgreSQL / MySQL\n(Learner Records, Courses,\nAssessments, Certifications)")]
        CACHE[("Redis Cache\n(Sessions, Catalogues,\nRecommendations)")]
        CDN["CDN\n(Video Streaming\nHLS/DASH)"]
    end

    MS1 <--> DB
    MS2 <--> DB
    MS3 <--> CACHE
    MS6 <--> DB
    MS7 <--> DB
    MS1 <--> CDN
    MS4 <--> DB

    %% ── Infrastructure & Deployment Layer ──
    subgraph INFRA["🏗️ INFRASTRUCTURE & DEPLOYMENT LAYER"]
        DOCKER["Docker Containers"]
        K8S["Kubernetes\nOrchestration"]
        CICD["CI/CD Pipelines\n(Jenkins / GitHub Actions)"]
        MONITOR["Monitoring\n(Prometheus, Grafana,\nELK Stack)"]
    end

    DATA -.->|"Deployed on"| INFRA
    MICROSERVICES -.->|"Containerised in"| DOCKER
    DOCKER -.->|"Orchestrated by"| K8S

    %% ── External Integrations ──
    subgraph EXTERNAL["🌐 EXTERNAL INTEGRATIONS"]
        EXT1["DHIS2"]
        EXT2["OpenMRS"]
        EXT3["CPD Accreditation\nBodies"]
        EXT4["SCORM/xAPI\nContent Providers"]
        EXT5["SMS / Email\nGateways"]
    end

    ADAPT <-->|"API"| EXT1
    ADAPT <-->|"API"| EXT2
    MS2 <-->|"API"| EXT3
    MS1 <-->|"SCORM/xAPI"| EXT4
    MS5 -->|"Sends"| EXT5

    %% ── Styling ──
    classDef userStyle fill:#002060,stroke:#002060,color:#fff,font-weight:bold
    classDef presentStyle fill:#2E74B5,stroke:#1F4D78,color:#fff
    classDef gatewayStyle fill:#1F4D78,stroke:#002060,color:#fff
    classDef serviceStyle fill:#4472C4,stroke:#2E74B5,color:#fff
    classDef integrationStyle fill:#548235,stroke:#375623,color:#fff
    classDef dataStyle fill:#BF8F00,stroke:#806000,color:#fff
    classDef infraStyle fill:#7030A0,stroke:#4B0082,color:#fff
    classDef externalStyle fill:#C00000,stroke:#8B0000,color:#fff

    class U1,U2,U3,U4,U5 userStyle
    class WEB,MOBILE presentStyle
    class GW,GW_AUTH,GW_RL,GW_LB,GW_ROUTE gatewayStyle
    class MS1,MS2,MS3,MS4,MS5,MS6,MS7 serviceStyle
    class MQ,ADAPT integrationStyle
    class DB,CACHE,CDN dataStyle
    class DOCKER,K8S,CICD,MONITOR infraStyle
    class EXT1,EXT2,EXT3,EXT4,EXT5 externalStyle
