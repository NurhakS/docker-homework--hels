graph TB
    subgraph "Your Computer"
        PC[Desktop/Tablet] -- "kubectl apply" --> Master
    end

    subgraph "Internet"
        User((User)) -- "HTTP Request (Port 80)" --> SVC
    end

    subgraph "Kubernetes Cluster"
        SVC[Service: Load Balancer] -- "Route Traffic" --> Pod1
        SVC -- "Route Traffic" --> Pod2

        subgraph "Node 1 (Host Machine)"
            Pod1[Pod: Game Server]
            Pod1 --> C1[Container: Unity/Go]
        end

        subgraph "Node 2 (Host Machine)"
            Pod2[Pod: Blog Web]
            Pod2 --> C2[Container: Ghost/Node]
            Pod2 --- V1[(Volume: SQLite/Files)]
        end

        subgraph "Node 3 (Host Machine)"
            Pod3[Pod: Database]
            Pod3 --> C3[Container: PostgreSQL]
            Pod3 --- V2[(Volume: DB Storage)]
        end
    end

    %% Citing Exercise Requirements
    %% Includes: Pod, Cluster, Container, Service, Volume
