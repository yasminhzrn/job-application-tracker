# Auth Flow

## Authentication Design

Careera uses email-and-password authentication. Passwords are hashed before being stored, and authenticated users receive a JSON Web Token (JWT).

In the final production design, the JWT will be stored in a secure HTTP-only cookie. Protected backend endpoints will validate the token and identify the current user before retrieving or modifying data.

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
    API->>DB: Check whether email exists
    DB-->>API: Email availability result

    alt Email available
        API->>API: Hash password
        API->>DB: Create user
        DB-->>API: User created
        API-->>Frontend: 201 Created
        Frontend-->>User: Registration successful
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
    DB-->>API: User record
    API->>API: Verify password hash

    alt Valid credentials
        API->>API: Generate JWT
        API-->>Frontend: Store JWT in HTTP-only cookie
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
    Frontend->>API: GET /api/v1/applications with authentication cookie
    API->>API: Decode and validate JWT

    alt Token valid
        API->>DB: Retrieve applications for current user
        DB-->>API: Application records
        API-->>Frontend: 200 OK with application data
        Frontend-->>User: Display applications
    else Token invalid or expired
        API-->>Frontend: 401 Unauthorized
        Frontend-->>User: Redirect to login
    end
```

### Authorisation Rule

Authentication proves the identity of the user. Authorisation determines which records the authenticated user may access.

Every application query must include the authenticated user's ID. For example:

```text
application_id = requested application ID
user_id = authenticated user ID
```

This prevents one user from viewing or modifying another user's applications by changing the application ID in the URL.
