# Careera System Architecture

## Architecture Overview

Careera uses a client-server architecture with separate frontend, backend, database, and file-storage layers.

The React frontend communicates with the FastAPI backend through HTTPS requests. The FastAPI backend handles authentication, business logic, validation, database access, resume processing, and file-storage operations.

PostgreSQL stores structured application data. Resume PDF files are stored separately in AWS S3 in production.

```mermaid
flowchart LR
    User[User Browser]

    subgraph Frontend
        React[React and TypeScript Frontend]
    end

    subgraph Backend
        API[FastAPI REST API]
        Auth[Authentication Service]
        AppService[Application Service]
        ResumeService[Resume Service]
        AnalysisService[Analysis Service]
        DashboardService[Dashboard Service]
    end

    subgraph Data
        PostgreSQL[(PostgreSQL)]
        S3[(AWS S3)]
    end

    subgraph Monitoring
        CloudWatch[AWS CloudWatch]
    end

    User -->|Uses Careera| React
    React -->|HTTPS and JSON| API

    API --> Auth
    API --> AppService
    API --> ResumeService
    API --> AnalysisService
    API --> DashboardService

    Auth --> PostgreSQL
    AppService --> PostgreSQL
    ResumeService --> PostgreSQL
    ResumeService --> S3
    AnalysisService --> PostgreSQL
    DashboardService --> PostgreSQL

    API --> CloudWatch
```

## Component Responsibilities

### React Frontend

The frontend provides the user interface for registration, authentication, job-application management, resume uploads, analysis results, and dashboards.

### FastAPI Backend

The backend exposes REST API endpoints and handles all business logic, security checks, data validation, resume processing, and communication with external services.

### PostgreSQL

PostgreSQL stores users, job applications, resume metadata, analysis results, and other structured data.

### AWS S3

AWS S3 stores uploaded resume PDF files in the production environment.

### AWS CloudWatch

AWS CloudWatch receives application logs and infrastructure-monitoring information from the production backend.

## Communication Rules

* The frontend communicates only with the FastAPI backend.
* The frontend never connects directly to PostgreSQL or AWS S3.
* The backend validates every protected request.
* The backend verifies that a user owns a resource before returning or modifying it.
* Database credentials and AWS credentials are stored in environment variables.
* Public production communication must use HTTPS.
