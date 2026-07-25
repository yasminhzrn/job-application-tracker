# Flow Description and Diagrams

## Authentication Design

Careera uses email-and-password authentication. Passwords are hashed before being stored, and authenticated users receive a JSON Web Token (JWT).

In the final production design, the JWT will be stored in a secure HTTP-only cookie. The backend will set the cookie in the login response, and the browser will automatically include it in later requests.

Protected backend endpoints will validate the JWT, identify the authenticated user, and verify that the user is authorised to access or modify the requested data.

### Registration Flow

```mermaid
sequenceDiagram
    actor User
    participant Frontend
    participant API as FastAPI
    participant DB as PostgreSQL

    User->>Frontend: Enter name, email and password
    Frontend->>API: POST /api/v1/auth/register
    API->>API: Validate input
    API->>DB: Check whether email already exists
    DB-->>API: Email availability result

    alt Email available
        API->>API: Hash password
        API->>DB: Create user account
        DB-->>API: User created
        API-->>Frontend: 201 Created
        Frontend-->>User: Display registration success
    else Email already registered
        API-->>Frontend: 409 Conflict
        Frontend-->>User: Display registration error
    end
```

### Login Flow

```mermaid
sequenceDiagram
    actor User
    participant Frontend
    participant API as FastAPI
    participant DB as PostgreSQL

    User->>Frontend: Enter email and password
    Frontend->>API: POST /api/v1/auth/login
    API->>DB: Find user by email
    DB-->>API: User record or no result
    API->>API: Verify user exists and password is correct

    alt Valid credentials
        API->>API: Generate JWT
        API-->>Frontend: 200 OK with secure HTTP-only authentication cookie
        Frontend-->>User: Open dashboard
    else Invalid credentials
        API-->>Frontend: 401 Unauthorized
        Frontend-->>User: Display login error
    end
```

### Protected Request Flow

```mermaid
sequenceDiagram
    actor User
    participant Frontend
    participant API as FastAPI
    participant DB as PostgreSQL

    User->>Frontend: Open applications page
    Frontend->>API: GET /api/v1/applications
    Note over Frontend,API: Browser automatically includes authentication cookie
    API->>API: Read, decode and validate JWT

    alt Token valid
        API->>DB: Retrieve applications for authenticated user
        DB-->>API: Application records
        API-->>Frontend: 200 OK with application data
        Frontend-->>User: Display applications
    else Token invalid or expired
        API-->>Frontend: 401 Unauthorized
        Frontend-->>User: Redirect to login
    end
```

### Authorisation Rule

Authentication confirms the identity of the user. Authorisation determines which records the authenticated user is permitted to access or modify.

Every application query must be restricted using the user ID extracted from the validated JWT. The backend must not rely on a user ID supplied by the frontend.

For example:

```text
application_id = requested application ID
user_id = authenticated user ID extracted from the JWT
```

The backend should query using both values:

```text
Find the application where:

application.id = requested application ID
AND
application.user_id = authenticated user ID
```

This prevents one user from viewing, updating, or deleting another user's application by changing the application ID in the URL.

## Job Application Flow

### Create Application Flow

```mermaid
sequenceDiagram
    actor User
    participant Frontend
    participant API as FastAPI
    participant DB as PostgreSQL

    User->>Frontend: Complete application form
    Frontend->>API: POST /api/v1/applications
    API->>API: Validate authentication cookie
    API->>API: Identify authenticated user
    API->>API: Validate application fields

    alt Input valid
        API->>DB: Insert application with authenticated user_id
        DB-->>API: Created application
        API-->>Frontend: 201 Created with application data
        Frontend-->>User: Display saved application
    else Input invalid
        API-->>Frontend: 422 Unprocessable Entity
        Frontend-->>User: Display validation errors
    end
```

### View Applications Flow

```mermaid
sequenceDiagram
    actor User
    participant Frontend
    participant API as FastAPI
    participant DB as PostgreSQL

    User->>Frontend: Open applications page
    Frontend->>API: GET /api/v1/applications
    API->>API: Validate JWT and identify user
    API->>DB: Retrieve records belonging to authenticated user
    DB-->>API: Application records
    API-->>Frontend: 200 OK with application list
    Frontend-->>User: Display applications
```

### View Single Application Flow

```mermaid
sequenceDiagram
    actor User
    participant Frontend
    participant API as FastAPI
    participant DB as PostgreSQL

    User->>Frontend: Select an application
    Frontend->>API: GET /api/v1/applications/{application_id}
    API->>API: Validate JWT and identify user
    API->>DB: Find application by ID and authenticated user_id
    DB-->>API: Application record or no result

    alt Application found and owned by user
        API-->>Frontend: 200 OK with application data
        Frontend-->>User: Display application details
    else Application not found or not owned by user
        API-->>Frontend: 404 Not Found
        Frontend-->>User: Display not-found error
    end
```

### Update Application Flow

```mermaid
sequenceDiagram
    actor User
    participant Frontend
    participant API as FastAPI
    participant DB as PostgreSQL

    User->>Frontend: Edit application details
    Frontend->>API: PATCH /api/v1/applications/{application_id}
    API->>API: Validate JWT and identify user
    API->>API: Validate updated fields
    API->>DB: Find application by ID and authenticated user_id
    DB-->>API: Application record or no result

    alt Application found and input valid
        API->>DB: Update application
        DB-->>API: Updated application
        API-->>Frontend: 200 OK with updated data
        Frontend-->>User: Display updated application
    else Application not found
        API-->>Frontend: 404 Not Found
        Frontend-->>User: Display not-found error
    else Input invalid
        API-->>Frontend: 422 Unprocessable Entity
        Frontend-->>User: Display validation errors
    end
```

### Delete Application Flow

```mermaid
sequenceDiagram
    actor User
    participant Frontend
    participant API as FastAPI
    participant DB as PostgreSQL

    User->>Frontend: Select delete application
    Frontend-->>User: Request deletion confirmation
    User->>Frontend: Confirm deletion
    Frontend->>API: DELETE /api/v1/applications/{application_id}
    API->>API: Validate JWT and identify user
    API->>DB: Find application by ID and authenticated user_id
    DB-->>API: Application record or no result

    alt Application found and owned by user
        API->>DB: Delete application
        DB-->>API: Deletion confirmed
        API-->>Frontend: 204 No Content
        Frontend-->>User: Remove application from display
    else Application not found or not owned by user
        API-->>Frontend: 404 Not Found
        Frontend-->>User: Display not-found error
    end
```

## Resume Upload Flow

```mermaid
sequenceDiagram
    actor User
    participant Frontend
    participant API as FastAPI
    participant Storage as File Storage
    participant DB as PostgreSQL

    User->>Frontend: Select PDF resume
    Frontend->>API: POST /api/v1/applications/{application_id}/resume
    API->>API: Validate JWT and identify user
    API->>DB: Verify application belongs to authenticated user
    DB-->>API: Application record or no result

    alt Application found and owned by user
        API->>API: Validate file extension, MIME type, signature and size

        alt Resume valid
            API->>API: Generate safe unique filename
            API->>Storage: Upload PDF
            Storage-->>API: Return storage key
            API->>DB: Save resume metadata
            DB-->>API: Resume record created
            API-->>Frontend: 201 Created with resume metadata
            Frontend-->>User: Display upload success
        else Resume invalid
            API-->>Frontend: 400 Bad Request
            Frontend-->>User: Display file validation error
        end
    else Application not found or not owned by user
        API-->>Frontend: 404 Not Found
        Frontend-->>User: Display not-found error
    end
```

## Resume Analysis Flow

```mermaid
sequenceDiagram
    actor User
    participant Frontend
    participant API as FastAPI
    participant DB as PostgreSQL
    participant Storage as File Storage
    participant Analysis as Analysis Service

    User->>Frontend: Select Run Analysis
    Frontend->>API: POST /api/v1/applications/{application_id}/analysis
    API->>API: Validate JWT and identify user
    API->>DB: Retrieve application, job description and resume metadata
    DB-->>API: Application data or no result

    alt Application and resume found
        API->>Storage: Retrieve resume PDF
        Storage-->>API: Resume file
        API->>Analysis: Extract resume text
        Analysis->>Analysis: Clean and normalise text
        Analysis->>Analysis: Extract job-description keywords
        Analysis->>Analysis: Compare resume with job description
        Analysis->>Analysis: Calculate score and recommendations
        Analysis-->>API: Analysis results
        API->>DB: Save analysis results
        DB-->>API: Analysis record saved
        API-->>Frontend: 200 OK with analysis results
        Frontend-->>User: Display score, keywords and recommendations
    else Application or resume not found
        API-->>Frontend: 404 Not Found
        Frontend-->>User: Display analysis error
    end
```

## Dashboard Flow

```mermaid
sequenceDiagram
    actor User
    participant Frontend
    participant API as FastAPI
    participant DB as PostgreSQL

    User->>Frontend: Open dashboard
    Frontend->>API: GET /api/v1/dashboard/summary
    API->>API: Validate JWT and identify user
    API->>DB: Calculate statistics for authenticated user
    DB-->>API: Aggregated dashboard data
    API-->>Frontend: 200 OK with summary and chart data
    Frontend-->>User: Display dashboard cards and charts
```

## Logout Flow

```mermaid
sequenceDiagram
    actor User
    participant Frontend
    participant API as FastAPI

    User->>Frontend: Select logout
    Frontend->>API: POST /api/v1/auth/logout
    API->>API: Clear authentication cookie
    API-->>Frontend: 204 No Content
    Frontend-->>User: Redirect to login page
```
