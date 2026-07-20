# Careera Minimum Viable Product (MVP)

**Version:** 1.0

---

# 1. Introduction

## 1.1 Purpose

This document defines the Minimum Viable Product (MVP) for Careera.

The MVP represents the smallest complete version of the application that delivers value to users while demonstrating full-stack software engineering and cloud deployment skills.

All development throughout Version 1 must follow this document. New features should not be added unless they replace an existing feature or are moved into **future-features.md**.

---

# 2. MVP Goals

Version 1 of Careera aims to allow users to:

- Create an account.
- Log in securely.
- Manage job applications.
- Upload resumes.
- Compare resumes against job descriptions.
- View application statistics.
- Deploy the application using AWS.

---

# 3. Feature Priorities

The project follows the **MoSCoW prioritisation method**.

| Priority | Description |
|----------|-------------|
| Must Have | Required for Version 1 |
| Should Have | Important but can be postponed |
| Could Have | Nice-to-have improvements |
| Won't Have | Deliberately excluded from Version 1 |

---

# 4. Must Have Features

---

## 4.1 User Authentication

### Description

Users must be able to create an account and log in securely.

### Functions

- Register account
- Login
- Logout
- JWT Authentication
- Password hashing

### Validation Rules

- Email must be unique.
- Email format must be valid.
- Password minimum length: 8 characters.
- Passwords must be hashed before storage.

### Success Criteria

✔ User can register.

✔ User can login.

✔ User stays authenticated.

✔ User can logout.

---

## 4.2 User Profile

Each user owns their own data.

Profile contains:

- Full Name
- Email
- Account Created Date

Users can:

- View profile

(Profile editing will be added later.)

---

## 4.3 Job Application Management

Users can perform full CRUD (Create, Read, Update, Delete) operations on job applications.

### Required Fields

- Company Name
- Job Title

### Optional Fields

- Location
- Salary Range
- Notes
- Deadline
- Job Description
- Application Date
- Resume
- **Application Source**

### Application Sources

Users can select where they found the job from the following predefined list:

- LinkedIn
- Indeed
- Glassdoor
- Gradcracker
- Bright Network
- Company Website
- University Careers Portal
- Referral
- Recruitment Agency
- Other

The predefined list ensures consistent data for filtering and analytics.

Users cannot create custom sources in Version 1.

---

## 4.4 Application Status Tracking

Each application has one status.

Allowed statuses:

- Interested
- Preparing
- Applied
- Online Assessment
- Interview
- Offer
- Rejected
- Withdrawn

Users cannot create custom statuses in Version 1.

---

## 4.5 Resume Upload

Each application can contain one active resume.

Requirements:

- PDF only
- Maximum size: 5 MB
- One resume per application
- Replace existing resume

The uploaded file will later be stored inside AWS S3.

---

## 4.6 Resume Text Extraction

The backend extracts readable text from uploaded PDFs.

The system should:

- Validate PDF
- Extract text
- Store extracted text
- Handle unreadable PDFs gracefully

---

## 4.7 Resume Analysis

Users can compare their resume against the job description.

Version 1 performs:

- Keyword matching
- Missing keyword detection
- Resume section detection
- Contact information check

Output includes:

- Match Score
- Matched Keywords
- Missing Keywords
- Recommendations

Example:

```
Match Score

78%

Matched Skills

Python
SQL
Excel

Missing Skills

Power BI
AWS
Git

Recommendation

Consider including evidence of SQL projects.
```

Version 1 **does not use LLMs**.

The analysis is keyword-based.

---

## 4.8 Dashboard

The dashboard provides an overview of the user's job search activity.

### Summary Cards

- Total Applications
- Applications This Month
- Interviews
- Offers
- Rejections
- Interview Rate
- Offer Rate

### Charts

- Applications by Status
- Applications by Month
- **Applications by Source**

### Recent Activity

Display the five most recently updated applications.

---

## 4.9 Search

Users can search by:

- Company
- Job Title

---

## 4.10 Filter

Users can filter applications by:

- Status
- Application Source

Example:

Status:
✓ Applied

Source:
✓ LinkedIn

---

## 4.11 Responsive Design

The application must support:

- Desktop
- Tablet
- Mobile

---

# 5. Should Have Features

These features are desirable but may be postponed.

## Resume Download

Users can download uploaded resumes.

---

## Application Sorting

Sort by:

- Company
- Date
- Deadline
- Status

---

## Status History

Store previous statuses.

Example:

Applied

↓

Interview

↓

Offer

---

## Interview Details

Store:

- Interview Date
- Interview Type
- Notes

---

# 6. Could Have Features

If development finishes early.

- Dark Mode
- Export CSV
- Better Charts
- Resume Version History
- User Settings
- Profile Picture

---

# 7. Won't Have (Version 1)

The following features are intentionally excluded.

## AI

- GPT Resume Rewrite
- AI Cover Letter
- AI Interview Coach

---

## Integrations

- LinkedIn
- Gmail
- Outlook
- Google Calendar

---

## Recruitment

- Recruiter Dashboard
- HR Accounts
- Applicant Matching

---

## Mobile

Native mobile applications.

---

## Authentication

- Google Login
- Microsoft Login
- Two Factor Authentication

---

# 8. User Workflow

A normal user journey:

Register

↓

Login

↓

Dashboard

↓

Create Application

↓

Paste Job Description

↓

Upload Resume

↓

Run Analysis

↓

Receive Results

↓

Update Status

↓

Dashboard Updates

↓

Logout

---

# 9. Technical Boundaries

## Frontend

React

TypeScript

Tailwind CSS

---

## Backend

Python

FastAPI

SQLAlchemy

Pydantic

Alembic

---

## Database

PostgreSQL

---

## Authentication

JWT

---

## Local Development

Docker

Docker Compose

GitHub Actions

---

## Production

Frontend

Vercel

Backend

AWS EC2

Database

AWS RDS

Storage

AWS S3

Monitoring

CloudWatch

Permissions

IAM

---

# 10. Acceptance Criteria

The MVP is complete only if all conditions below are met.

Authentication

- Users can register.
- Users can login.
- Passwords are hashed.
- Protected routes work.

Applications

- Create
- Read
- Update
- Delete

Status

- Update status
- Filter by status

Resume

- Upload PDF
- Extract text
- Compare with job description

Dashboard

- Statistics display correctly.
- Charts update automatically.

Security

- User cannot access another user's data.
- Invalid files rejected.
- Invalid JWT rejected.

Deployment

- Frontend deployed.
- Backend deployed.
- Database connected.
- Resume stored in AWS.
- CloudWatch logging enabled.

---

# 11. MVP Completion Checklist

## Authentication

- [ ] Register
- [ ] Login
- [ ] Logout
- [ ] JWT
- [ ] Password Hashing

## Applications

- [ ] Create
- [ ] View
- [ ] Edit
- [ ] Delete

## Resume

- [ ] Upload
- [ ] Validation
- [ ] Extraction
- [ ] Analysis

## Dashboard

- [ ] Statistics
- [ ] Charts

## AWS

- [ ] EC2
- [ ] RDS
- [ ] S3
- [ ] IAM
- [ ] CloudWatch

## Testing

- [ ] Backend Tests
- [ ] Frontend Tests

## Documentation

- [ ] README
- [ ] API Docs
- [ ] Screenshots
- [ ] Architecture Diagram

---

# 12. Definition of Done

Version 1 of Careera is considered complete when:

- Every Must Have feature is fully implemented.
- All acceptance criteria are satisfied.
- Core backend tests pass.
- Frontend builds successfully.
- Docker Compose runs without errors.
- GitHub Actions passes all checks.
- The application is deployed to AWS.
- The GitHub repository includes complete documentation and deployment screenshots.

Future improvements should only begin after Version 1 is fully completed.