# system-architecture!
graph TB
    %% Step 1: Client Applications
    subgraph ClientApps["Client Applications"]
        direction TB
        subgraph Web["Web Platform"]
            WTP["Trading Platform"]
            WAP["Analytics Platform"]
            WAD["Admin Dashboard"]
        end
        subgraph Mobile["Mobile Apps"]
            MTA["Trading App"]
            MAA["Analytics App"]
        end
    end

    %% Step 2: Security & Gateway Layer
    subgraph SecurityGateway["Security & Gateway"]
        direction LR
        WAF["Web Application Firewall"]
        APIG["API Gateway"]
        AUTH["Authentication & Authorization"]
        MFA["Multi-Factor Auth"]
        KMS["Key Management"]
        LB["Load Balancer"]
    end

    %% Step 3: Core Trading Services
    subgraph TradingCore["Core Trading Services"]
        direction TB
        OMS["Order Management System"]
        RVE["Risk Engine"]
        OPP["Options Pricing & Strategies"]
    end

    %% Step 4: Market Data Systems
    subgraph MarketData["Market Data Systems"]
        direction LR
        MDF["Market Data Feed"]
        HDS["Historical Data Store"]
        TAS["Technical Analysis & Aggregation"]
    end

    %% Step 5: Analytics & Reporting
    subgraph Analytics["Analytics & Reporting"]
        direction TB
        PNA["P&L & Portfolio Analytics"]
        TPA["Trading Performance"]
        RPT["Reporting Services"]
    end

    %% Step 6: Data Layer
    subgraph DataLayer["Data Management"]
        direction LR
        TSDB[(Time Series DB)]
        OLTP[(OLTP Database)]
        CACHE[(Redis & Memcached Cache)]
        OBJ[(Object Storage)]
        DWH[(Data Warehouse)]
    end

    %% Step 7: External Integration
    subgraph External["External Systems"]
        direction TB
        EXC["Exchanges & Brokers"]
        NTF["Notification & Email Services"]
    end

    %% Step 8: Monitoring & Operations
    subgraph DevOps["Monitoring & Operations"]
        direction LR
        MON["System Monitoring & Alerts"]
        DRP["Disaster Recovery"]
    end

    %% Core Connections
    ClientApps --> SecurityGateway
    SecurityGateway --> TradingCore
    TradingCore --> MarketData
    TradingCore --> DataLayer
    MarketData --> DataLayer
    TradingCore --> Analytics
    Analytics --> DataLayer
    TradingCore --> External
    DevOps --> |Monitors| TradingCore
    DevOps --> |Monitors| MarketData
    DevOps --> |Monitors| Analytics

    %% Styling
    classDef primary fill:#1f77b4,stroke:#0d3b66,color:white,stroke-width:2px;
    classDef secondary fill:#ff7f0e,stroke:#d62728,color:white,stroke-width:2px;
    classDef database fill:#2ca02c,stroke:#1d7a2e,color:white,stroke-width:2px;
    classDef external fill:#9467bd,stroke:#6a51a3,color:white,stroke-width:2px;
    classDef monitoring fill:#e377c2,stroke:#d62728,color:white,stroke-width:2px;

    class Web,Mobile primary
    class SecurityGateway secondary
    class TradingCore,MarketData,Analytics primary
    class DataLayer database
    class External external
    class DevOps monitoring
