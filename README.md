# Inbound Management System (IMS) / ERP for Clinical Trials
<img width="1146" alt="image" src="https://github.com/user-attachments/assets/dd98b239-139f-4e1c-ab2e-a3771ffeeb1d">

## Project Overview
Developed a comprehensive Inbound Management System (IMS) and ERP for managing clinical trial participant recruitment projects in hospitals and pharmaceutical companies. The system includes various modules such as survey component builder, post-research-survey integration, inbound management, HR management, ad schedule management, and role-based access control.

## Architecture
```mermaid
graph TD
    A[Client] -->|HTTPS| B{Nginx Load Balancer}
    B -->|Round Robin| C[Docker Container: Angular Frontend 1]
    B -->|Round Robin| D[Docker Container: Angular Frontend 2]
    C & D --> E{API Gateway}
    E -->|JWT Auth| F[Authentication Service]
    E -->|Microservices| G[Survey Builder Service]
    E -->|Microservices| H[Inbound Management Service]
    E -->|Microservices| I[HR Management Service]
    E -->|Microservices| J[Ad Schedule Service]
    E -->|Microservices| K[Data Export Service]
    G & H & I & J & K -->|Read/Write| L[(MySQL Database)]
    G & H & I & J & K -->|Cache| M[(Redis)]
    N[Server Monitoring] -->|Auto-reboot| O[Docker Containers]
    P[Backup System] -->|Daily Backup| L
    P -->|Cloud Storage| Q[Cloud Server]
    P -->|Local Storage| R[On-premises NAS]
    S[CI/CD Pipeline] -->|Blue-Green Deployment| O

    K -->|Streaming| T[Large-scale Data Export]
    U[Encryption/Decryption Service] --> L
    V[Access Logging Service] --> L

    subgraph Custom Docker Network
    C
    D
    E
    F
    G
    H
    I
    J
    K
    L
    M
    U
    V
    end

    subgraph Security Measures
    W[JWT Authentication]
    X[Data Encryption]
    Y[Access Logging]
    Z[HTTPS]
    end

    style Custom Docker Network fill:#f9f,stroke:#333,stroke-width:2px
    style Security Measures fill:#ff9,stroke:#333,stroke-width:2px
```

## Key Features
- Survey component builder system
- Integration of posts, research, and surveys
- Inbound survey management
- Human resources management
- Advertising schedule management
- Large-scale data export (up to 100,000 rows)
- Role-based access control

## Technical Implementation
- Automated server management for environments without real-time management capabilities
- Real-time server status monitoring with automatic reboot on error detection
- Designed and implemented a small-scale ERP including a medical research consultation platform
- Developed using Express.js, Angular2+, MySQL, and Redis
- Implemented zero-downtime operations through containerization with Docker and Nginx-based round-robin load balancing
- Utilized blue-green deployment strategy with Docker containers
- Migrated from a single-process API in PM2 environment to a microservices architecture (MSA) through Docker containerization
- Established a daily database backup system with redundancy across cloud servers and on-premises NAS

## Achievements
- Automated management of company operations
- Reduced data entry and generation time from over 6 hours to 30 minutes for identical tasks
- Implemented role-based access control, enabling task allocation based on employee positions
- Enabled server operations without on-site developer presence
- Integrated survey creation and customer information collection, replacing Google Forms with a custom builder
- Improved operational efficiency through category-based ad schedule management
- Optimized large-scale data exports using streaming to prevent file generation with each creation

## Technologies Used
- Backend: Express.js, Node.js
- Frontend: Angular2+
- Database: MySQL, Redis
- DevOps: Docker, Nginx, PM2
- Cloud services and on-premises NAS for backup
- Microservices Architecture (MSA)
