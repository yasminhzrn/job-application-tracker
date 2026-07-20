# Careera User Stories

**Version:** 1.0

---

# Introduction

This document defines the user stories for Careera.

User stories describe the system from the perspective of the user and provide clear acceptance criteria for development and testing.

Format:

> As a [user], I want [goal] so that [benefit].

---

# Epic 1 — Authentication

## US-001 Register Account

**As a** new user

**I want** to create an account

**So that** I can save my job applications.

### Acceptance Criteria

- User enters name, email and password.
- Email must be unique.
- Password is hashed.
- Registration succeeds.

---

## US-002 Login

**As a** registered user

**I want** to log into my account

**So that** I can access my dashboard.

### Acceptance Criteria

- Valid email/password required.
- JWT token generated.
- Invalid credentials rejected.

---

## US-003 Logout

**As a** logged-in user

**I want** to logout

**So that** nobody else can access my account.

### Acceptance Criteria

- Session terminated.
- Protected pages inaccessible afterwards.

---

# Epic 2 — Job Applications

## US-004 Create Application

As a user,

I want to create a job application,

So that I can track it.

Acceptance Criteria

- Company required.
- Job title required.
- Status assigned.
- Application saved.

---

## US-005 View Applications

As a user,

I want to view all my applications,

So that I know my progress.

Acceptance Criteria

- Only my applications displayed.
- Supports pagination (future).
- Displays latest applications.

---

## US-006 Update Application

As a user,

I want to edit my application,

So that information stays up to date.

Acceptance Criteria

- Editable fields update.
- Validation applied.

---

## US-007 Delete Application

As a user,

I want to remove an application,

So that I can keep my tracker organised.

Acceptance Criteria

- Confirmation dialog.
- Record deleted.

---

# Epic 3 — Application Tracking

## US-008 Update Status

As a user,

I want to change the application status,

So that the dashboard reflects my progress.

Acceptance Criteria

- Status updated.
- Dashboard updates automatically.

---

## US-009 Search Applications

As a user,

I want to search by company or role,

So that I can find applications quickly.

Acceptance Criteria

- Partial matching.
- Case insensitive.

---

## US-010 Filter Applications

As a user,

I want to filter applications,

So that I can view only relevant records.

Acceptance Criteria

Filter by:

- Status
- Application Source

---

# Epic 4 — Resume Management

## US-011 Upload Resume

As a user,

I want to upload a PDF resume,

So that I can analyse it later.

Acceptance Criteria

- PDF only.
- Maximum 5 MB.
- Resume linked to application.

---

## US-012 Replace Resume

As a user,

I want to replace my resume,

So that I always use the latest version.

Acceptance Criteria

- Old file replaced.
- New metadata saved.

---

# Epic 5 — Resume Analysis

## US-013 Extract Resume Text

As a user,

I want Careera to extract text,

So that my resume can be analysed.

Acceptance Criteria

- Readable PDF supported.
- Invalid PDFs handled safely.

---

## US-014 Resume Matching

As a user,

I want my resume compared against a job description,

So that I know how well they match.

Acceptance Criteria

Display:

- Match score
- Matched keywords
- Missing keywords

---

## US-015 Resume Recommendations

As a user,

I want recommendations,

So that I know how to improve my resume.

Acceptance Criteria

Recommendations generated based on keyword comparison.

---

# Epic 6 — Dashboard

## US-016 Dashboard Statistics

As a user,

I want summary statistics,

So that I understand my job search progress.

Acceptance Criteria

Display:

- Total applications
- Interviews
- Offers
- Rejections
- Applications this month

---

## US-017 Dashboard Charts

As a user,

I want visual charts,

So that I can understand my application trends.

Acceptance Criteria

Charts:

- Applications by Status
- Applications by Month
- Applications by Source

---

# Epic 7 — Security

## US-018 Private Data

As a user,

I want my applications to remain private,

So that nobody else can access them.

Acceptance Criteria

- Users only access their own records.

---

## US-019 Secure Upload

As a user,

I want uploaded files validated,

So that malicious files cannot be uploaded.

Acceptance Criteria

- File type validation.
- Size validation.

---

# Epic 8 — Deployment

## US-020 Cloud Deployment

As a developer,

I want Careera deployed to AWS,

So that employers can access a production version.

Acceptance Criteria

- Frontend online
- Backend online
- Database online
- Resume storage works

---

## Definition of Done

A user story is complete when:

- Acceptance criteria satisfied.
- Backend implemented.
- Frontend implemented.
- Tested successfully.
- Documented.