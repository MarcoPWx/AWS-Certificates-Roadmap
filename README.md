# Fullstack Project - PayLane 

Personal exploration project for full-stack development with LLM's and modern cloud architecture.

Overview
--------

This document outlines the architecture, resilience, disaster recovery, contingency plans, scalability, and failover strategies for the kiosk system. Additionally, it covers the offline mode considerations, GitHub Pages documentation setup, and the technical due diligence processes.

Table of Contents
-----------------

1.  [Tech Stack Overview](#tech-stack-overview)
2.  [System Architecture](#system-architecture)
3.  [Resilience and Scalability](#resilience-and-scalability)
4.  [Disaster Recovery and Contingency Planning](#disaster-recovery-and-contingency-planning)
5.  [Failover Strategies](#failover-strategies)
6.  [Security Considerations](#security-considerations)
7.  [Offline Mode](#offline-mode)
8.  [GitHub Pages Documentation](#github-pages-documentation)
9.  [Technical Due Diligence Setup](#technical-due-diligence-setup)
10. [Testing and Monitoring](#testing-and-monitoring)

* * * * *

### Tech Stack Overview

#### Backend:

-   **Node.js/NestJS**: API and microservices framework, facilitating loose coupling and service reuse.
-   **PostgreSQL**: High-performance database with sharding and replication features.
-   **Supabase**: Supabase's PostgreSQL instance for scalable database hosting, coupled with its built-in authentication and real-time capabilities.
-   **Redis**: In-memory data store for caching and queue management.
-   **Supabase Functions**: Edge-based, serverless functions for fast, distributed request processing.

#### Frontend:

-   **React.js (Next.js)**: Frontend with Server-Side Rendering (SSR) for fast load times, combined with static rendering for pre-generated pages.
-   **React Query**: Handles caching and synchronization of remote data with local state.

#### Other Components:

-   **GraphQL & REST APIs**: Flexible and comprehensive APIs for client requests.
-   **WebSockets**: Real-time communication between kiosks and the backend for live updates.
-   **Docker & Kubernetes**: Container orchestration for managing microservices deployment.

### System Architecture

The kiosk system is built using **microservices architecture** and designed to support a distributed network of kiosks across various locations. It includes several key components to ensure it can scale and remain resilient:

-   **Microservices**: Modular services for check-ins, payments, notifications, etc., all communicating via APIs.
-   **API Gateway**: Centralized access point for all requests, providing load balancing and rate limiting.
-   **Database Sharding and Replication**: PostgreSQL databases are sharded and replicated across multiple instances for better performance and fault tolerance.
-   **Redis Caching**: Caches frequently requested data and ensures a quick response during peak times.
-   **WebSockets**: Maintain real-time updates for kiosk status, helping to synchronize states across devices.

### Resilience and Scalability

**Key Features:**

-   **Horizontal Scaling**: Microservices can scale horizontally with Kubernetes, automatically adding or removing instances based on demand.
-   **Stateless Microservices**: Ensuring all services are stateless allows for easy scaling and migration.
-   **Circuit Breakers and Retries**: Protect services from overload by implementing circuit breakers, with retry mechanisms following exponential backoff patterns.

**Scalability Considerations:**

-   **Auto-scaling**: Automatically scales services based on resource usage, allowing the system to handle varying loads without manual intervention.
-   **Load Balancing**: Distributes incoming traffic across service instances to ensure high availability and performance.

### Disaster Recovery and Contingency Planning

**Key Components of the DR Plan:**

-   **Automated Database Backups**: Scheduled PostgreSQL backups, stored in geographically distinct locations to ensure data recovery in case of regional failure.
-   **Multi-Zone Replication**: Database replicas across different availability zones allow for quick failover in case of node failure.
-   **Disaster Recovery Drills**: Regular simulation drills to ensure all recovery processes are functional and able to handle real-world scenarios.

**Contingency Plans:**

-   **Cloud-Agnostic Architecture**: Ability to migrate between cloud providers if necessary.
-   **Hot/Cold Standby**: Critical components have hot standby instances for immediate failover, while less critical components use cold standby for cost efficiency.

### Failover Strategies

**Strategies to Minimize Downtime:**

-   **Automatic Failover for Databases**: If the primary database instance fails, a replica is automatically promoted to take over.
-   **Redundant Services**: Microservices are deployed in redundant clusters, ensuring that any failure is automatically mitigated by spinning up new instances.
-   **Failover Drills**: Regular failover testing ensures that the system responds correctly under failure scenarios.

### Security Considerations

-   **JWT Authentication**: JSON Web Tokens (JWT) are used to authenticate API requests, ensuring that only authorized users can access resources.
-   **Data Encryption**: All data is encrypted in transit (via HTTPS) and at rest.
-   **Role-Based Access Control (RBAC)**: Ensures that sensitive endpoints are accessible only by authorized users based on roles.
-   **DDoS Mitigation**: Rate limiting and firewall rules help prevent DDoS attacks.

### Offline Mode

The kiosk system is designed to support **offline mode**, ensuring continuity of service even if the network connection is disrupted.

**Offline Mode Features:**

-   **Local Data Storage**: Data is temporarily stored on the kiosk device itself when the connection is unavailable.
-   **Queued Requests**: When the system goes offline, user actions are queued locally and synced with the central server once the connection is restored.
-   **Conflict Resolution**: In the event of conflicting data (e.g., user check-ins), conflict resolution strategies are employed to ensure data consistency once the system is back online.

### GitHub Pages Documentation

The documentation for the entire kiosk system is hosted on GitHub Pages, ensuring that all architectural decisions, system designs, and diagrams are easily accessible for developers and stakeholders.

**Structure:**

-   **Architecture Overview**: Explains the high-level design of the system.
-   **Dependency Injection & Microservices**: Details on service decoupling and reusability.
-   **Algorithms and Scaling**: Information on key algorithms (e.g., retry/backoff, rate-limiting, caching).
-   **Security and Compliance**: Documentation on JWT handling, encryption, and security policies.
-   **Disaster Recovery and Offline Mode**: Comprehensive guides on how the system handles outages and operates offline.

The documentation is continuously updated as new features and considerations are implemented.

### Technical Due Diligence Setup

As part of the technical due diligence for the kiosk system, a comprehensive checklist is followed to ensure that the system is **scalable**, **resilient**, and meets **compliance standards**. The due diligence setup covers:

1.  **System Architecture Review**: Detailed documentation and presentations for stakeholders, focusing on architecture scalability and redundancy.
2.  **Resilience & Failover Testing**: Automated and manual tests to simulate service failures and observe recovery mechanisms.
3.  **Offline Mode Validation**: Testing to ensure that the system functions as expected without an internet connection, including proper synchronization once the connection is restored.
4.  **Security Audits**: Review of the security setup, including JWT handling, encryption, and data protection strategies.

### Testing and Monitoring

To ensure reliability, extensive testing and monitoring are employed:

-   **Unit and Integration Testing**: Ensures that individual services and their interactions function as expected.
-   **End-to-End (E2E) Testing**: Full-system testing simulates real-world user behavior, from check-in to payments.
-   **Performance Monitoring**: Tools like Prometheus and Grafana are used to track system performance, while alerts are set for anomalies such as high latency or service failures.
-   **Continuous Integration and Deployment (CI/CD)**: Automated pipelines ensure that code is tested and deployed to production with minimal human intervention.


### Tech Stack Overview

#### 1\. **Backend**

-   **Node.js (NestJS Framework)**: A progressive Node.js framework for building efficient and scalable server-side applications. It leverages TypeScript and is highly suitable for developing microservices architectures.
-   **PostgreSQL**: A powerful, open-source relational database that supports advanced features such as sharding, replication, and partitioning, crucial for scaling and handling high throughput.
-   **Supabase**: Provides a managed PostgreSQL instance with real-time subscriptions and built-in authentication. It integrates easily with the backend and supports serverless functions for distributed logic execution.
-   **Redis**: An in-memory data structure store used for caching frequently accessed data, session storage, and implementing distributed locking mechanisms.
-   **Supabase Edge Functions**: Serverless functions deployed close to users for low-latency interactions and to handle quick, stateless API tasks at the edge.

#### 2\. **Frontend**

-   **React.js (Next.js Framework)**: A hybrid framework for building static and server-side rendered (SSR) React applications. Used for fast client-server interactions, server-side logic, and SEO-friendly web applications.
-   **TypeScript**: Ensures type safety across the application codebase, minimizing runtime errors and improving overall development productivity.
-   **React Query**: For data fetching, caching, synchronization, and server-state management, allowing the frontend to handle asynchronous data updates seamlessly.
-   **GraphQL**: Used alongside REST APIs to enable flexible and precise data queries for the frontend, allowing clients to request only the data they need.

#### 3\. **Database and Data Storage**

-   **PostgreSQL (Supabase)**: The core relational database used for storing transactional data, managing user sessions, and handling complex queries. Supabase provides real-time data sync and easy integrations.
-   **Sharding and Replication**: PostgreSQL databases are sharded for performance optimization and replicated to ensure high availability and resilience to failure.

#### 4\. **Caching and Queue Management**

-   **Redis**: Used to cache frequently requested data (e.g., product catalogs, user session data), improving performance and reducing load on the PostgreSQL database. Redis is also used for distributed task queues and background job processing.

#### 5\. **DevOps and Containerization**

-   **Docker**: For containerizing services and ensuring consistent development, testing, and production environments.
-   **Kubernetes**: For orchestrating containers, scaling services automatically based on traffic, and providing fault-tolerant deployments. It also handles load balancing and manages rolling updates for zero downtime.

#### 6\. **Real-Time Communication**

-   **WebSockets**: Enables real-time data push for functionalities such as live updates on kiosk statuses, notifications, and user actions without constant polling.

#### 7\. **Authentication and Authorization**

-   **JWT (JSON Web Tokens)**: Secures API routes by authenticating users through tokens. JWTs are used for stateless authentication, ensuring a scalable and secure method to authorize requests.
-   **Role-Based Access Control (RBAC)**: Implemented to restrict access to specific functionalities based on the user's roles within the system.

#### 8\. **Monitoring, Logging, and Alerts**

-   **Prometheus & Grafana**: For monitoring system health, performance metrics, and generating alerts based on defined thresholds.
-   **PagerDuty**: Used for incident management, sending alerts in case of downtime or critical service failures, ensuring rapid response and recovery.

#### 9\. **Offline Mode (For Kiosk)**

-   **Local Storage (IndexedDB, Service Workers)**: Enables the kiosk system to operate in offline mode by storing temporary data locally on the client side. Data is synced back to the server when the network connection is restored.

#### 10\. **Version Control and Documentation**

-   **GitHub (GitHub Pages)**: Used for version control, with GitHub Pages serving as the platform for project documentation. The documentation includes system architecture, design decisions, diagrams, and API references.

This tech stack ensures the system is resilient, scalable, secure, and capable of handling real-time and offline requirements, making it suitable for the high demands of a multi-kiosk check-in system.
