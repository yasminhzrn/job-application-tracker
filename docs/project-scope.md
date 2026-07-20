# Careera Project Scope

**Version:** 1.0  
**Author:** Shafiqah Azzahrah Binti Amiruddin  
**Project Type:** Full Stack Web Application  
**Target Users:** University Students and Recent Graduates

---

# 1. Introduction

## 1.1 Project Overview

Careera is a full-stack web application that helps university students and recent graduates manage their job search in one centralized platform.

Instead of relying on spreadsheets, notebooks, or multiple job websites, users can securely store and organize their job applications, upload tailored resumes, monitor application progress, and receive automated resume feedback based on job descriptions.

The application combines modern web technologies with cloud computing to provide an efficient and scalable platform for managing the recruitment process.

The project will initially be developed locally using Docker to minimize infrastructure costs before being deployed to Amazon Web Services (AWS) as the final production version.

---

## 1.2 Background

Finding a graduate job often requires applying to dozens or even hundreds of companies.

Students typically experience several common problems:

- Applications are stored across multiple job portals.
- It is difficult to remember deadlines.
- Resume versions become disorganized.
- There is no simple way to compare resumes against job descriptions.
- Tracking interviews and offers becomes increasingly difficult.

Many students resort to spreadsheets, which provide limited functionality and no automation.

Careera addresses these issues by providing an integrated platform that combines job tracking, resume management, data visualization, and cloud deployment into a single application.

---

# 2. Problem Statement

University students and recent graduates frequently submit applications through multiple recruitment platforms.

Managing these applications manually often leads to:

- missed deadlines,
- duplicated applications,
- poorly organised resumes,
- limited visibility of application progress,
- and difficulty evaluating resume quality.

Current solutions, such as spreadsheets or note-taking applications, require significant manual effort and provide little analytical insight.

Careera aims to solve these challenges by providing a centralized, secure, and intelligent job application management platform.

---

# 3. Project Aim

The aim of this project is to design, develop, and deploy a secure cloud-based web application that enables users to manage job applications, organize resumes, monitor recruitment progress, and receive automated resume analysis.

---

# 4. Project Objectives

The project has the following objectives:

- Develop a secure user authentication system.
- Allow users to create and manage job applications.
- Enable users to upload and organize resumes.
- Compare resumes with job descriptions using keyword analysis.
- Generate simple resume recommendations.
- Visualize application progress through dashboards.
- Deploy the application using AWS cloud services.
- Demonstrate modern software engineering and cloud computing practices.

---

# 5. Target Users

The primary users are:

- University students
- Final-year students
- Recent graduates
- Internship applicants
- Graduate programme applicants
- Entry-level job seekers

Future versions may support:

- Career advisors
- University career centres
- Recruiters
- Human resource departments

These users are outside the scope of Version 1.

---

# 6. Minimum Viable Product (MVP)

The first release of Careera will include the following core functionality.

## User Management

- User registration
- Secure login
- JWT authentication
- User profile

## Job Applications

- Create applications
- Edit applications
- Delete applications
- View applications
- Track application status

## Resume Management

- Upload PDF resumes
- Store resume information
- Associate resumes with applications

## Resume Analysis

- Extract resume text
- Compare resume against job description
- Calculate keyword match percentage
- Display missing keywords
- Generate basic recommendations

## Dashboard

- Total applications
- Interview count
- Offer count
- Rejection count
- Monthly applications
- Applications by status

---

# 7. Project Scope

## Included

Version 1 includes:

- User authentication
- Job application management
- Resume upload
- Resume analysis
- Dashboard analytics
- AWS deployment
- Cloud monitoring
- Docker containerization

## Excluded

Version 1 does not include:

- Mobile application
- Calendar integration
- Email notifications
- LinkedIn integration
- Recruiter portal
- Salary prediction
- AI interview simulator
- Cover letter generation
- Automatic job applications
- Social login

These features are planned for future releases.

---

# 8. Functional Requirements

The system shall allow users to:

- Register an account.
- Log in securely.
- Manage job applications.
- Upload PDF resumes.
- Track recruitment stages.
- View dashboard analytics.
- Analyze resumes against job descriptions.
- Store user data securely.
- Access only their own data.

---

# 9. Non-Functional Requirements

## Security

The system shall:

- Hash passwords before storage.
- Protect all authenticated endpoints.
- Prevent unauthorized data access.
- Store secrets using environment variables.
- Validate uploaded files.

---

## Performance

The application should:

- Load dashboard pages quickly.
- Handle multiple concurrent users.
- Process resume uploads efficiently.
- Respond to API requests with minimal latency.

---

## Reliability

The application should:

- Handle invalid input gracefully.
- Maintain database consistency.
- Prevent data corruption.
- Log application errors.

---

## Scalability

The architecture should support future deployment to larger AWS infrastructure without major redesign.

---

## Maintainability

The project should:

- Use modular architecture.
- Follow RESTful API principles.
- Use Git version control.
- Include automated testing.
- Follow clean coding practices.

---

# 10. Technology Stack

## Frontend

- React
- TypeScript
- Tailwind CSS
- React Router

## Backend

- Python
- FastAPI
- SQLAlchemy
- Alembic
- Pydantic

## Database

- PostgreSQL

## Authentication

- JWT

## Development

- Docker
- Docker Compose
- Git
- GitHub

## Cloud

- AWS EC2
- AWS RDS
- AWS S3
- AWS IAM
- AWS CloudWatch

## CI/CD

- GitHub Actions

---

# 11. Development Strategy

## Development Environment

During development the project will use:

- React running locally
- FastAPI running locally
- PostgreSQL inside Docker
- GitHub Actions
- Docker Compose

This keeps development costs at approximately **RM0**.

---

## Production Environment

The production deployment will consist of:

Frontend
- Vercel

Backend
- AWS EC2

Database
- AWS RDS PostgreSQL

Storage
- AWS S3

Authentication
- JWT

Monitoring
- AWS CloudWatch

Permissions
- AWS IAM

The AWS deployment will remain active during portfolio demonstrations and interviews before resources are removed to minimize cloud costs.

---

# 12. Success Criteria

The project will be considered successful if users can:

- Register successfully.
- Log in securely.
- Create job applications.
- Update application status.
- Upload resumes.
- Receive resume analysis.
- View dashboard statistics.
- Log out securely.

From a technical perspective, success also includes:

- Successful Docker deployment.
- Successful AWS deployment.
- Secure API authentication.
- Persistent PostgreSQL storage.
- Resume storage in Amazon S3.
- Monitoring through AWS CloudWatch.

---

# 13. Assumptions

This project assumes that:

- Users upload valid PDF resumes.
- Users manually provide job descriptions.
- Internet access is available.
- AWS services remain available during deployment.
- Resume analysis provides recommendations rather than hiring decisions.

---

# 14. Constraints

The project is subject to the following constraints:

- Limited cloud budget.
- Limited development time.
- Single developer.
- Basic keyword analysis rather than advanced AI.
- AWS free-tier and short-term deployment strategy.

---

# 15. Future Expansion

Future versions of Careera may include:

- AI-powered resume rewriting
- AI interview preparation
- Cover letter generation
- Email integration
- Calendar reminders
- LinkedIn integration
- Resume version comparison
- Recruiter dashboard
- Mobile application
- Advanced analytics
- Multi-language support

These features are documented separately in **future-features.md**.

---

# 16. Conclusion

Careera aims to provide a practical, secure, and scalable solution for managing graduate job applications.

By combining modern web development practices with cloud technologies, the project demonstrates both software engineering principles and cloud deployment skills while solving a genuine problem faced by university students and graduates.