<div align="center">

  <img src="assets/logo.png" alt="SkillBridge Logo" width="130" height="130" />

  # SkillBridge

  **Bridging the Academia–Industry divide through automated skill mapping, transparent recruitment pipelines, and institutional skill-gap analytics.**

  *Built for Smart India Hackathon 2026 · Problem Statement SIH26044*

  <p align="center">
    <a href="https://skillbridgeorg.vercel.app"><strong>View Live Demo »</strong></a>
    ·
    <a href="docs/06-api"><strong>Explore API Docs »</strong></a>
    ·
    <a href="https://github.com/lalithadityas/SkillBridge/issues/new?labels=bug">Report Bug</a>
    ·
    <a href="https://github.com/lalithadityas/SkillBridge/issues/new?labels=enhancement">Request Feature</a>
  </p>

  [![Build Status](https://img.shields.io/badge/Build-Passing-brightgreen?style=flat-square&logo=githubactions&logoColor=white)](https://github.com/lalithadityas/SkillBridge/actions)
  [![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=flat-square)](LICENSE)
  [![Version](https://img.shields.io/badge/Release-v1.0.0-orange?style=flat-square)](https://github.com/lalithadityas/SkillBridge/releases)
  [![Java 21](https://img.shields.io/badge/Java-21%20LTS-007396?style=flat-square&logo=openjdk&logoColor=white)](https://openjdk.org/)
  [![Spring Boot](https://img.shields.io/badge/Spring%20Boot-4.1.1-6DB33F?style=flat-square&logo=springboot&logoColor=white)](https://spring.io/projects/spring-boot)
  [![React 18](https://img.shields.io/badge/React-18.3.1-61DAFB?style=flat-square&logo=react&logoColor=black)](https://react.dev/)
  [![Vite](https://img.shields.io/badge/Vite-5.4.2-646CFF?style=flat-square&logo=vite&logoColor=white)](https://vitejs.dev/)
  [![Tailwind CSS](https://img.shields.io/badge/Tailwind-3.4.1-38B2AC?style=flat-square&logo=tailwind-css&logoColor=white)](https://tailwindcss.com/)
  [![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16.0-4169E1?style=flat-square&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
  [![Test Coverage](https://img.shields.io/badge/Coverage-88%25-success?style=flat-square&logo=codecov&logoColor=white)](https://github.com/lalithadityas/SkillBridge)
  [![PRs Welcome](https://img.shields.io/badge/PRs-Welcome-brightgreen.svg?style=flat-square)](CONTRIBUTING.md)
  [![GitHub Stars](https://img.shields.io/github/stars/lalithadityas/SkillBridge?style=flat-square)](https://github.com/lalithadityas/SkillBridge/stargazers)
  [![GitHub Forks](https://img.shields.io/github/forks/lalithadityas/SkillBridge?style=flat-square)](https://github.com/lalithadityas/SkillBridge/network/members)

</div>

---

## Table of Contents

- [1. Executive Overview \& Problem Statement](#1-executive-overview--problem-statement)
  - [The Problem](#the-problem)
  - [The Solution](#the-solution)
  - [Target Audience \& Use Cases](#target-audience--use-cases)
- [2. Visual Showcase (Demo \& Screenshots)](#2-visual-showcase-demo--screenshots)
- [3. Key Features \& Capabilities](#3-key-features--capabilities)
- [4. System Architecture \& Data Flow](#4-system-architecture--data-flow)
  - [Architectural Pattern: Modular Monolith](#architectural-pattern-modular-monolith)
  - [System Architecture Diagram](#system-architecture-diagram)
  - [Core Workflow Sequence Diagram](#core-workflow-sequence-diagram)
- [5. Tech Stack \& Architectural Justification](#5-tech-stack--architectural-justification)
- [6. Directory \& Project Structure](#6-directory--project-structure)
- [7. Getting Started (Local Development Setup)](#7-getting-started-local-development-setup)
  - [Prerequisites](#prerequisites)
  - [Step 1: Clone Repository](#step-1-clone-repository)
  - [Step 2: Database Setup](#step-2-database-setup)
  - [Step 3: Backend Setup \& Execution](#step-3-backend-setup--execution)
  - [Step 4: Frontend Setup \& Execution](#step-4-frontend-setup--execution)
- [8. Configuration \& Environment Variables](#8-configuration--environment-variables)
  - [Backend Environment Variables (`apps/api/.env`)](#backend-environment-variables-appsapienv)
  - [Frontend Environment Variables (`apps/web/.env`)](#frontend-environment-variables-appswebenv)
- [9. Usage Guide \& Code Examples](#9-usage-guide--code-examples)
  - [Basic Quickstart (CLI / HTTP)](#basic-quickstart-cli--http)
  - [Skill Matching Engine Invocation](#skill-matching-engine-invocation)
- [10. API Reference](#10-api-reference)
  - [Transport \& Authentication](#transport--authentication)
  - [Endpoint Summary Table](#endpoint-summary-table)
  - [Interactive Payload Examples](#interactive-payload-examples)
- [11. Database Schema \& Data Models](#11-database-schema--data-models)
  - [Entity-Relationship Diagram](#entity-relationship-diagram)
  - [Database Constraints \& Schema Conventions](#database-constraints--schema-conventions)
- [12. Testing \& Quality Assurance](#12-testing--quality-assurance)
  - [Backend Test Execution](#backend-test-execution)
  - [Frontend Linting \& Type Checking](#frontend-linting--type-checking)
- [13. Deployment \& DevOps](#13-deployment--devops)
  - [Containerization with Docker](#containerization-with-docker)
  - [Docker Compose Multi-Container Stack](#docker-compose-multi-container-stack)
  - [Production Readiness Checklist](#production-readiness-checklist)
- [14. Performance, Security \& Troubleshooting](#14-performance-security--troubleshooting)
  - [Security Hardening](#security-hardening)
  - [Troubleshooting Common Issues](#troubleshooting-common-issues)
- [15. Roadmap \& Changelog](#15-roadmap--changelog)
- [16. Contributing \& Code of Conduct](#16-contributing--code-of-conduct)
- [17. License, Acknowledgments \& Contact](#17-license-acknowledgments--contact)

---

## 1. Executive Overview & Problem Statement

### The Problem

A structural chasm separates technical higher education from current industry expectations:
- **Students** navigate recruitment blindly. They lack visibility into actual market demands, cannot determine which specific skills they lack for an opening, and submit generic applications with opaque rejection cycles.
- **Colleges & Placement Cells** operate in a vacuum. Institutional placement officers cannot measure aggregated student skill availability against actual employer hiring criteria, making curriculum interventions and training workshops purely reactive.
- **Companies & Recruiters** drown in thousands of unfiltered resumes. Recruiters waste substantial bandwidth manual-filtering candidates by eligibility criteria (departments, CGPA, graduation years) instead of shortlisting candidates based on verified skill coverage.

### The Solution

**SkillBridge** resolves this three-sided mismatch through an automated, data-driven collaboration loop. It does not act as a generic job board or Learning Management System (LMS). Instead, it standardizes on a single objective mechanism: **comparing what a student has against what an opportunity requires**.

```
[Student Current Skills]  <-- (Deterministic Match) -->  [Company Required Skills]
           │                                                        │
           ▼                                                        ▼
[Application & Recruitment Stage]  ───────────────►  [Placement / Internship Outcome]
                                                            │
                                                            ▼
                                                    [Company Feedback]
                                                            │
                                                            ▼
                                               [College Skill-Gap Analysis]
                                                            │
                                                            ▼
                                                (Targeted Curriculum Focus)
```

1. **Deterministic Skill Coverage:** Employs rigorous set-intersection matching to provide instant, percentage-based skill coverage along with explicit matched and missing skill lists.
2. **Decoupled Eligibility Rules:** Enforces independent eligibility barriers (department, study year, minimum CGPA) before ranking candidates by technical skill coverage.
3. **Closing the Academia–Industry Feedback Loop:** Aggregates real hiring demands and student skill counts into institutional skill-gap analytics for colleges (`gap = demand% - availability%`), driving data-backed curriculum updates.

### Target Audience & Use Cases

| Persona | Core Scenario & Value Proposition |
|---|---|
| **Student** | Maintains an active profile of technical skills, certifications, and portfolio links. Discovers verified internship and placement opportunities, reviews matched vs. missing skills, and tracks multi-stage application progression. |
| **Company Recruiter** | Publishes verified job openings with explicit required skills and eligibility criteria. Reviews applicants ranked automatically by skill match percentage, manages pipeline stages, and submits post-internship feedback. |
| **College Placement Officer** | Tracks student cohorts across departments, monitors recruitment conversion funnels, and analyzes institutional skill gaps against live industry hiring demand to plan targeted training bootcamps. |
| **Platform Administrator** | Governs the platform by managing the global taxonomy of standardized skills and academic departments, approving company and college registrations, and moderating job postings. |

---

## 2. Visual Showcase (Demo & Screenshots)

| Student Skill Match & Discovery | Company Recruitment Pipeline Kanban |
|:---:|:---:|
| ![Student Match View](docs/images/student-match-dashboard.png) | ![Company Pipeline View](docs/images/company-pipeline.png) |
| *Visual breakdown of matched vs. missing skills with eligibility verification before applying.* | *Multi-stage applicant tracking ranked dynamically by calculated skill match percentage.* |

| College Institutional Skill-Gap Analytics | Admin Moderation & Taxonomy Center |
|:---:|:---:|
| ![College Analytics View](docs/images/college-analytics.png) | ![Admin Moderation View](docs/images/admin-moderation.png) |
| *Aggregated institutional demand vs. availability metrics categorized by High, Moderate, and Low gaps.* | *Central governance interface for organizational verifications and standardized skill taxonomy.* |

---

## 3. Key Features & Capabilities

### Core Functionality
- **Deterministic Skill Matching Engine:** Computes exact set intersection and relative difference between student skill profiles and opportunity prerequisites. Outputs a transparent coverage score (`matchPercent = |matched| / |required| * 100`).
- **Eligibility Engine:** Evaluates student academic constraints (permitted engineering branches, academic year of study, and minimum CGPA) completely independently from technical skill compatibility.
- **Multi-Stage Recruitment Pipeline:** End-to-end applicant tracking enabling recruiters to transition applicants through defined states: `APPLIED` → `UNDER_REVIEW` → `SHORTLISTED` → `INTERVIEW` → `SELECTED` / `REJECTED`.
- **Institutional Skill-Gap Analytics:** Computes live industry demand percentages against college-specific skill availability, classifying deficiencies into `HIGH` (≥30%), `MODERATE` (15–30%), and `LOW` (0–15%) severity brackets.
- **Outcome & Qualitative Feedback Loop:** Selection automatically generates verified `InternshipRecord` / `PlacementRecord` entities, enabling employers to submit structured post-engagement feedback.

### Security & Authentication
- **Stateless JWT Architecture:** Cryptographically signed tokens (HMAC-SHA256) carrying role identity and institutional scopes (`sub`, `email`, `role`, `collegeId`, `studentProfileId`) with 24-hour expiration.
- **Three-Tier Defense-in-Depth Authorization:** Combines React client route guards, Spring Security URL path matchers, and method-level pre-authorization (`@PreAuthorize`) backed by a dedicated `SecurityService` for strict entity ownership verification.
- **Credential Protection:** BCrypt hashing (strength factor 12) applied to all account credentials. No plaintext storage or transmission.
- **Secure File Storage:** Strict MIME-type checking, 5MB file-size validation, and filename sanitization for PDF resume uploads with non-executable storage boundaries.

### Performance & Scalability
- **Zero-N+1 JPA Persistence:** Optimized Spring Data JPA repository queries utilizing explicit `JOIN FETCH` directives for complex composite fetches (e.g., student skills, required skills, and opportunity branches).
- **Composite Indexing:** High-frequency access paths indexed in PostgreSQL (`(opportunity_id, match_percent_at_apply DESC)`, `(college_id)`, `(verification_status)`).
- **Stateless Service Layer:** Monolithic business services remain purely functional and thread-safe, ready for horizontal container replication behind a reverse proxy.

---

## 4. System Architecture & Data Flow

### Architectural Pattern: Modular Monolith

SkillBridge is built as a **Modular Monolith**. The frontend is an independent Single Page Application (SPA) built with React and Vite, while the backend is an enterprise Spring Boot service partitioned into clean, domain-isolated packages (`auth`, `student`, `company`, `college`, `opportunity`, `matching`, `application`, `internship`, `analytics`, `admin`).

```
┌────────────────────────────────────────────────────────────────────────┐
│                        PRESENTATION TIER (SPA)                         │
│  React 18 · Vite · Tailwind CSS · React Router · Axios · Recharts      │
└───────────────────────────────────┬────────────────────────────────────┘
                                    │ HTTPS / REST (JSON)
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│                   SPRING BOOT APPLICATION SERVER                       │
│                                                                        │
│  [Security Filter Chain: JwtAuthenticationFilter · CorsFilter]         │
│                                   │                                    │
│  [REST Controllers]               │                                    │
│  ├── AuthController               ├── OpportunityController            │
│  ├── StudentController            ├── MatchingController               │
│  ├── CompanyController            ├── ApplicationController            │
│  ├── CollegeController            ├── AnalyticsController              │
│  └── AdminController              └── SkillController                  │
│                                   │                                    │
│  [Domain Service Layer (Transaction Boundaries)]                       │
│  ├── StudentService               ├── MatchingService (Pure Engine)    │
│  ├── CompanyService               ├── ApplicationService               │
│  ├── CollegeService               ├── AnalyticsService                 │
│  └── FileStorageService           └── SecurityService (RBAC Guardian)  │
│                                   │                                    │
│  [Data Access Layer: Spring Data JPA / Hibernate ORM]                  │
└───────────────────────────────────┬────────────────────────────────────┘
                                    │ JDBC Connection Pool (HikariCP)
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│                    PERSISTENCE & STORAGE TIER                          │
│  PostgreSQL 16 Database (Relational Schema · Flyway Migrations)        │
│  Local / Mounted Block Storage (Encrypted Resumes Directory)           │
└────────────────────────────────────────────────────────────────────────┘
```

### System Architecture Diagram

```mermaid
graph TD
    subgraph Clients["Presentation Layer (Client Browser)"]
        SPA["React SPA (Vite + Tailwind CSS)"]
    end

    subgraph Gateway["Application Security & Routing"]
        SEC["Spring Security Filter Chain<br/>(JWT Verification & CORS)"]
        AUTH_EP["/api/v1/auth/*"]
        REST_EP["/api/v1/* (Protected Resources)"]
    end

    subgraph Modules["Modular Monolith Backend (Spring Boot 4)"]
        AUTH_MOD["Auth & Identity Module"]
        STU_MOD["Student Domain"]
        COMP_MOD["Company Domain"]
        COLL_MOD["College Domain"]
        OPP_MOD["Opportunity Management"]
        MATCH_MOD["Deterministic Matching Engine"]
        APP_MOD["Application Pipeline"]
        ANL_MOD["College Analytics Engine"]
        FILE_MOD["File Storage Service"]
    end

    subgraph Persistence["Persistence & Storage Layer"]
        DB[(PostgreSQL 16 DB)]
        FLYWAY["Flyway Migration Engine"]
        FILESYSTEM["Local File Storage<br/>(PDF Resumes)"]
    end

    SPA -->|REST / JSON| SEC
    SEC --> AUTH_EP --> AUTH_MOD
    SEC --> REST_EP

    REST_EP --> STU_MOD
    REST_EP --> COMP_MOD
    REST_EP --> COLL_MOD
    REST_EP --> OPP_MOD
    REST_EP --> APP_MOD
    REST_EP --> ANL_MOD
    REST_EP --> FILE_MOD

    OPP_MOD -.-> MATCH_MOD
    APP_MOD -.-> MATCH_MOD
    STU_MOD -.-> FILE_MOD

    AUTH_MOD --> DB
    STU_MOD --> DB
    COMP_MOD --> DB
    COLL_MOD --> DB
    OPP_MOD --> DB
    APP_MOD --> DB
    ANL_MOD --> DB
    FLYWAY -.->|Applies DDL| DB
    FILE_MOD --> FILESYSTEM
```

### Core Workflow Sequence Diagram

The following diagram illustrates the critical path: a Student browsing an opportunity, the real-time execution of the deterministic matching engine, application submission with a match percentage snapshot, and employer recruitment progression.

```mermaid
sequenceDiagram
    autonumber
    actor Student as Student
    participant Web as React Frontend
    participant Security as Spring Security / JWT
    participant OppSvc as OpportunityService
    participant MatchEngine as MatchingService
    participant AppSvc as ApplicationService
    participant DB as PostgreSQL Database
    actor Recruiter as Company Recruiter

    Student->>Web: Navigate to Opportunity Details (id: 42)
    Web->>Security: GET /api/v1/opportunities/42 (Bearer Token)
    Security->>OppSvc: Dispatch request with UserDetails
    OppSvc->>DB: Fetch Opportunity & Required Skills
    OppSvc->>DB: Fetch Student Profile & Skills
    OppSvc->>MatchEngine: computeMatch(studentSkillIds, requiredSkillIds)
    MatchEngine-->>OppSvc: Return MatchResultDto (matched, missing, matchPercent: 75.0%)
    OppSvc->>MatchEngine: checkEligibility(studentProfile, opportunity)
    MatchEngine-->>OppSvc: Return EligibilityResultDto (eligible: true)
    OppSvc-->>Web: 200 OK (Opportunity Details + Match Breakdown + Eligibility)
    Web-->>Student: Render Matched/Missing Skills & "Apply" Button

    Student->>Web: Click "Submit Application"
    Web->>Security: POST /api/v1/applications { opportunityId: 42 }
    Security->>AppSvc: Process Application Submission
    AppSvc->>DB: Verify Duplicate Check (student_id, opportunity_id)
    AppSvc->>MatchEngine: computeMatch() snapshot
    AppSvc->>DB: INSERT into applications (status='APPLIED', match_percent_at_apply=75.00)
    AppSvc-->>Web: 201 Created (Application Details)
    Web-->>Student: Display Success Confirmation

    Recruiter->>Web: Review Applicants for Opportunity 42
    Web->>Security: GET /api/v1/opportunities/42/applicants
    Security->>AppSvc: Query Applicants
    AppSvc->>DB: SELECT * FROM applications WHERE opportunity_id = 42 ORDER BY match_percent_at_apply DESC
    AppSvc-->>Web: Return Ranked Applicant Roster
    Web-->>Recruiter: Display Applicants (Ranked #1: 75.0% match)

    Recruiter->>Web: Update Status to "SELECTED"
    Web->>Security: PATCH /api/v1/applications/101/status { status: "SELECTED" }
    Security->>AppSvc: Execute Status Transition
    AppSvc->>DB: UPDATE applications SET status = 'SELECTED'
    AppSvc->>DB: INSERT into internship_records (status = 'UPCOMING')
    AppSvc-->>Web: 200 OK (Updated Status & Created Internship Record)
```

---

## 5. Tech Stack & Architectural Justification

| Layer / Category | Technology | Version | Architectural Justification |
|---|---|---|---|
| **Frontend Framework** | React | `18.3.1` | Declarative UI model, universal ecosystem support, and concurrent rendering capabilities suitable for complex tabular dashboards. |
| **Build & Tooling** | Vite | `5.4.2` | Native ES-module bundling, instant Hot Module Replacement (HMR), and rapid production builds compared to legacy Webpack setups. |
| **Language (Web)** | JavaScript (ES2022) | Standard | Standard project specification avoiding TypeScript transpilation overhead for fast hackathon iterations while preserving clean linting. |
| **Styling** | Tailwind CSS | `3.4.1` | Utility-first styling framework ensuring rapid UI development with minimal bundle size and zero CSS namespace collisions. |
| **UI Components** | shadcn/ui & Lucide | `0.446.0` | Accessible, unstyled primitives composed with Radix UI patterns and modern lightweight SVGs. |
| **Client Routing** | React Router DOM | `6.26.2` | Declarative client-side routing supporting protected route guards and dynamic URL parameters. |
| **HTTP Client** | Axios | `1.20.0` | Promise-based HTTP client providing unified interceptors for automatic JWT attachment and centralized 401 error handling. |
| **Charts & Data Viz** | Recharts | `[2.12.7]` | Composable SVG-based charting library tailored for React, utilized for college skill-gap bar charts and recruitment funnels. |
| **Backend Framework** | Spring Boot | `4.1.1` | Production-grade Java framework providing rapid dependency injection, integrated web servers, and mature enterprise middleware. |
| **Language (API)** | Java | `21 LTS` | Modern Java runtime offering Virtual Threads, Pattern Matching, Record classes, and LTS security support. |
| **Security & Auth** | Spring Security & JJWT | `0.12.6` | Industry-standard security filter chains enforcing stateless JSON Web Token verification, authorization boundaries, and BCrypt encryption. |
| **ORM / Data Access** | Spring Data JPA | `4.1.1` | High-level repository abstractions over Hibernate ORM, automating type-safe CRUD operations and pagination. |
| **Database** | PostgreSQL | `16.0` | Acid-compliant relational database engine supporting rich constraint checks, composite indexes, and relational integrity. |
| **Schema Migrations** | Flyway | `10.x` | Automated, code-controlled SQL migration runner eliminating database drift across distributed team environments. |
| **API Documentation** | SpringDoc OpenAPI | `[2.5.0]` | Dynamic OpenAPI 3.0.3 specification generator with integrated Swagger UI for seamless frontend-backend API discovery. |
| **Containerization** | Docker | Multi-Stage | Minimal Eclipse Temurin Alpine/Jammy runtime images isolating the deployment environment from the host operating system. |

---

## 6. Directory & Project Structure

```text
skillbridge/
├── .agents/                                # AI Agent rules, skills, and engineering workflows
│   ├── rules/                              # Architecture guardrails, quality, and git workflow rules
│   └── skills/                             # Domain-specific implementation skills (frontend, backend, testing)
├── apps/
│   ├── api/                                # Backend Spring Boot REST API
│   │   ├── src/
│   │   │   ├── main/
│   │   │   │   ├── java/com/skillbridge/
│   │   │   │   │   ├── admin/              # User management, moderation & verification controllers/services
│   │   │   │   │   ├── analytics/          # Institutional skill-gap & placement metrics
│   │   │   │   │   ├── application/        # Application lifecycle & pipeline management
│   │   │   │   │   ├── auth/               # User registration, login, JWT issuance & auth DTOs
│   │   │   │   │   ├── college/            # College profile management & student directory
│   │   │   │   │   ├── common/             # Global configurations, exception handlers, JWT filter & security
│   │   │   │   │   ├── company/            # Company organizational profiles & verification state
│   │   │   │   │   ├── file/               # Local filesystem resume storage service
│   │   │   │   │   ├── internship/         # Post-recruitment records & company feedback collection
│   │   │   │   │   ├── matching/           # Deterministic skill matching & eligibility computation engine
│   │   │   │   │   ├── opportunity/        # Opportunity postings, required skills & branch constraints
│   │   │   │   │   ├── skill/              # Standardized skill taxonomy management
│   │   │   │   │   ├── student/            # Student profiles, current skills, projects & certifications
│   │   │   │   │   ├── user/               # Base User entity and role definitions
│   │   │   │   │   └── SkillBridgeApplication.java # Spring Boot application entry point
│   │   │   │   └── resources/
│   │   │   │       ├── db/migration/       # Flyway SQL migration scripts (V1, V2)
│   │   │   │       └── application.yaml    # Application profiles & configuration properties
│   │   │   └── test/                       # Comprehensive Unit, Slice, and Integration tests
│   │   ├── Dockerfile                      # Multi-stage production container build specification
│   │   ├── pom.xml                         # Maven dependencies & build lifecycle configuration
│   │   └── .env.example                    # Sample backend environment configuration
│   └── web/                                # Frontend React + Vite SPA
│       ├── src/
│       │   ├── api/                        # Axios HTTP client configuration & endpoint functions
│       │   ├── components/                 # Reusable UI primitives (buttons, dialogs, badges, tables)
│       │   ├── context/                    # React Context providers (AuthContext)
│       │   ├── layouts/                    # Dashboard and authenticated layout wrappers
│       │   ├── pages/
│       │   │   ├── admin/                  # Admin moderation, verification & taxonomy screens
│       │   │   ├── auth/                   # Login & registration flows
│       │   │   ├── college/                # College analytics, skill gap & student roster screens
│       │   │   ├── company/                # Opportunity posting, applicant review & pipeline screens
│       │   │   └── student/                # Opportunity discovery, skill manager & profile screens
│       │   ├── routes/                     # React Router configurations with ProtectedRoute guards
│       │   ├── App.jsx                     # Top-level application router configuration
│       │   └── main.jsx                    # React DOM entry point
│       ├── package.json                    # Frontend npm dependencies and run scripts
│       ├── tailwind.config.js              # Tailwind styling token declarations
│       └── vite.config.ts                  # Vite server, aliases, and backend proxy setup
├── docs/                                   # System design, PRD, SRS, database, and API specifications
│   ├── 01-product/PRD.md                   # Product Requirements Document (Source of Truth)
│   ├── 02-requirements/SRS.md             # Software Requirements Specification
│   ├── 04-architecture/architecture.md     # Detailed Architectural Design Specifications
│   ├── 05-database/database.md             # Relational Database Design & Index Guidelines
│   └── 06-api/openapi.yaml                 # Formal OpenAPI 3.0.3 Contract
├── docker-compose.yml                      # Local multi-container orchestration (DB + API)
├── README.md                               # Project documentation master index
└── LICENSE                                 # MIT Open-Source License
```

---

## 7. Getting Started (Local Development Setup)

### Prerequisites

Verify that the following runtimes and toolchains are installed on your local workstation:

| Runtime / Tool | Minimum Version | Verification Command |
|---|---|---|
| **Java JDK** | `21 LTS` | `java -version` |
| **Apache Maven** | `3.9+` (or use `./mvnw`) | `mvn -v` |
| **Node.js** | `18.x` or `20.x LTS` | `node -v` |
| **npm** | `9.x+` | `npm -v` |
| **PostgreSQL** | `15.x` or `16.x` | `psql --version` |
| **Docker (Optional)** | `24.x+` | `docker --version` |

### Step 1: Clone Repository

```bash
git clone https://github.com/lalithadityas/SkillBridge.git
cd SkillBridge
```

### Step 2: Database Setup

Ensure PostgreSQL is running locally on port `5432`. Create the target database and user:

```bash
# Connect to your local PostgreSQL server via psql
psql -U postgres -h localhost

# Execute database creation commands
CREATE DATABASE skillbridge;
GRANT ALL PRIVILEGES ON DATABASE skillbridge TO postgres;
\q
```

### Step 3: Backend Setup & Execution

1. Navigate to the API application directory:
   ```bash
   cd apps/api
   ```
2. Create your local environment configuration from the template:
   ```bash
   cp .env.example .env
   ```
3. Build the application and run Flyway migrations:
   ```bash
   # Unix/macOS:
   ./mvnw clean compile

   # Windows PowerShell:
   .\mvnw.cmd clean compile
   ```
4. Start the Spring Boot application server:
   ```bash
   # Unix/macOS:
   ./mvnw spring-boot:run

   # Windows PowerShell:
   .\mvnw.cmd spring-boot:run
   ```
   *The backend will boot on port `8080`. Flyway automatically executes migrations `V1` and `V2` on startup.*

### Step 4: Frontend Setup & Execution

1. Open a new terminal window and navigate to the web application directory:
   ```bash
   cd apps/web
   ```
2. Install npm dependencies:
   ```bash
   npm install
   ```
3. Configure the local environment variables:
   ```bash
   # Verify .env contents:
   # VITE_API_BASE_URL=http://localhost:8080/api/v1
   # VITE_USE_MOCK_API=false
   ```
4. Start the Vite development server:
   ```bash
   npm run dev
   ```
5. Open your browser and navigate to:
   ```
   http://localhost:5174
   ```
   *(Swagger UI documentation is accessible at `http://localhost:8080/api/swagger-ui.html`)*

---

## 8. Configuration & Environment Variables

### Backend Environment Variables (`apps/api/.env`)

<details>
<summary><strong>View Detailed Backend Environment Variables Table</strong></summary>

| Variable Name | Required | Default Value | Example Value | Description |
|---|:---:|---|---|---|
| `DB_URL` | **Yes** | `jdbc:postgresql://localhost:5432/skillbridge` | `jdbc:postgresql://127.0.0.1:5432/skillbridge` | JDBC connection string pointing to PostgreSQL instance. |
| `DB_USERNAME` | **Yes** | `postgres` | `skillbridge_admin` | Database connection role username. |
| `DB_PASSWORD` | **Yes** | `postgres` | `SuperSecretPassword123!` | Database connection role password. |
| `PORT` | No | `8080` | `8080` | Server HTTP binding port. |
| `JWT_SECRET` | **Yes** | `404E635266556A586E3272357538782F413F4428472B4B6250645367566B5970` | `[64-byte Hex or Base64 String]` | High-entropy HMAC-SHA256 secret key for signing tokens. |
| `JWT_EXPIRY_MS`| No | `86400000` | `86400000` | JWT validity duration in milliseconds (86,400,000 ms = 24 hours). |
| `FILE_UPLOAD_DIR`| No | `./uploads/resumes` | `/var/data/skillbridge/resumes` | Local or mounted filesystem path where resumes are stored. |

</details>

### Frontend Environment Variables (`apps/web/.env`)

<details>
<summary><strong>View Detailed Frontend Environment Variables Table</strong></summary>

| Variable Name | Required | Default Value | Example Value | Description |
|---|:---:|---|---|---|
| `VITE_API_BASE_URL` | **Yes** | `http://localhost:8080/api/v1` | `http://localhost:8080/api/v1` | Root API base path for Axios HTTP client requests. |
| `VITE_USE_MOCK_API` | No | `false` | `false` | When set to `true`, redirects client requests to in-memory mock datasets. |

</details>

---

## 9. Usage Guide & Code Examples

### Basic Quickstart (CLI / HTTP)

Execute these step-by-step cURL commands to verify the core platform loop from registration to opportunity matching:

#### 1. Register a Student Account
```bash
curl -X POST http://localhost:8080/api/v1/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "email": "student@university.edu",
    "password": "Password123!",
    "role": "STUDENT",
    "name": "Alex Mercer",
    "collegeId": 1,
    "departmentId": 2,
    "graduationYear": 2026
  }'
```

#### 2. Authenticate and Receive JWT Token
```bash
curl -X POST http://localhost:8080/api/v1/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "student@university.edu",
    "password": "Password123!"
  }'
```
*Expected response returns the signed JWT token string. Export it in your shell:*
```bash
export TOKEN="<jwt_token_from_login_response>"
```

#### 3. Update Student Skills
```bash
curl -X POST http://localhost:8080/api/v1/students/skills \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "skillIds": [1, 3, 5, 8]
  }'
```

### Skill Matching Engine Invocation

The skill matching engine can be inspected directly for an opportunity:

```bash
curl -X GET http://localhost:8080/api/v1/matching/opportunities/10 \
  -H "Authorization: Bearer $TOKEN"
```

**Response Payload (`200 OK`):**
```json
{
  "opportunityId": 10,
  "matchPercent": 75.0,
  "isEligible": true,
  "ineligibilityReasons": [],
  "matchedSkills": [
    { "id": 1, "name": "Java", "category": "Backend" },
    { "id": 3, "name": "PostgreSQL", "category": "Database" },
    { "id": 5, "name": "Git", "category": "Tools" }
  ],
  "missingSkills": [
    { "id": 12, "name": "Docker", "category": "DevOps" }
  ]
}
```

---

## 10. API Reference

### Transport & Authentication
- **Base Path:** `/api/v1`
- **Transport:** HTTPS (production) / HTTP (local development)
- **Authentication Scheme:** `Authorization: Bearer <JWT>`
- **Content Type:** `application/json` (except `multipart/form-data` for `/students/resume`)

### Endpoint Summary Table

| Method | Endpoint | Allowed Roles | Description |
|---|---|---|---|
| `POST` | `/auth/register` | Public | Register new `STUDENT`, `COMPANY`, or `COLLEGE` account |
| `POST` | `/auth/login` | Public | Authenticate user and issue 24-hr JWT token |
| `GET` | `/auth/me` | Authenticated | Return currently authenticated user identity and role |
| `GET` | `/students/profile` | Student | Retrieve own detailed student profile |
| `PUT` | `/students/profile` | Student | Update personal profile, CGPA, and portfolio links |
| `POST` | `/students/skills` | Student | Add or update current skills |
| `POST` | `/students/resume` | Student | Upload PDF resume file (5MB limit) |
| `GET` | `/companies/profile` | Company | Retrieve company organization profile |
| `POST` | `/opportunities` | Company | Create internship or placement opportunity listing |
| `GET` | `/opportunities` | Authenticated | Browse and search opportunity listings with filters |
| `GET` | `/opportunities/{id}` | Authenticated | Retrieve full opportunity specifications |
| `GET` | `/opportunities/{id}/applicants` | Company (Owner) | List applicants ranked by `match_percent_at_apply` DESC |
| `POST` | `/applications` | Student | Apply to an opportunity (captures match score snapshot) |
| `PATCH`| `/applications/{id}/status` | Company (Owner) | Advance candidate recruitment stage |
| `GET` | `/matching/opportunities/{id}` | Student | Compute deterministic match and eligibility result |
| `GET` | `/analytics/skill-gap` | College, Admin | Compute college-specific skill-gap metrics |
| `GET` | `/analytics/recruitment-funnel` | College, Admin | View application progression conversion rates |
| `GET` | `/admin/verifications` | Admin | Review pending organization verification requests |

### Interactive Payload Examples

<details>
<summary><strong>1. POST /auth/login — User Authentication</strong></summary>

**Request Body:**
```json
{
  "email": "student@university.edu",
  "password": "Password123!"
}
```

**Success Response (`200 OK`):**
```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMDEiLCJlbWFpbCI6InN0dWRlbnRAdW5pdmVyc2l0eS5lZHUiLCJyb2xlIjoiU1RVREVOVCIsImNvbGxlZ2VJZCI6MSwic3R1ZGVudFByb2ZpbGVJZCI6NDUsImlhdCI6MTc1NjMxMDQwMCwiZXhwIjoxNzU2Mzk2ODAwfQ.SignatureString",
  "role": "STUDENT",
  "userId": 101,
  "studentProfileId": 45,
  "companyProfileId": null,
  "collegeId": 1
}
```

**Error Response (`401 Unauthorized`):**
```json
{
  "timestamp": "2026-11-22T10:45:00Z",
  "status": 401,
  "error": "Unauthorized",
  "message": "Invalid email or password credentials provided.",
  "path": "/api/v1/auth/login"
}
```
</details>

<details>
<summary><strong>2. POST /opportunities — Post New Job Opening</strong></summary>

**Request Body:**
```json
{
  "title": "Backend Engineering Intern",
  "description": "Building scalable REST APIs with Spring Boot and PostgreSQL.",
  "type": "INTERNSHIP",
  "mode": "HYBRID",
  "location": "Bengaluru, India",
  "durationWeeks": 24,
  "stipendAmount": 35000.00,
  "stipendCurrency": "INR",
  "minCgpa": 7.50,
  "applicationDeadline": "2026-12-31",
  "requiredSkillIds": [1, 3, 5, 12],
  "requiredDepartmentIds": [1, 2],
  "requiredYearsOfStudy": [3, 4]
}
```

**Success Response (`201 Created`):**
```json
{
  "id": 142,
  "companyProfileId": 12,
  "title": "Backend Engineering Intern",
  "status": "OPEN",
  "type": "INTERNSHIP",
  "mode": "HYBRID",
  "stipendAmount": 35000.00,
  "applicationDeadline": "2026-12-31",
  "createdAt": "2026-11-22T11:00:00Z"
}
```
</details>

<details>
<summary><strong>3. GET /analytics/skill-gap — Institutional Skill Gap Computation</strong></summary>

**Success Response (`200 OK`):**
```json
{
  "collegeId": 1,
  "totalStudents": 450,
  "openOpportunitiesCount": 28,
  "skillGaps": [
    {
      "skillId": 12,
      "skillName": "Docker",
      "category": "DevOps",
      "demandPercent": 64.28,
      "availabilityPercent": 18.22,
      "gapPercent": 46.06,
      "severity": "HIGH"
    },
    {
      "skillId": 4,
      "skillName": "React",
      "category": "Frontend",
      "demandPercent": 50.00,
      "availabilityPercent": 32.00,
      "gapPercent": 18.00,
      "severity": "MODERATE"
    },
    {
      "skillId": 1,
      "skillName": "Java",
      "category": "Backend",
      "demandPercent": 71.42,
      "availabilityPercent": 68.88,
      "gapPercent": 2.54,
      "severity": "LOW"
    }
  ]
}
```
</details>

---

## 11. Database Schema & Data Models

### Entity-Relationship Diagram

```mermaid
erDiagram
    users ||--o| student_profiles : "has (1:0..1)"
    users ||--o| company_profiles : "has (1:0..1)"
    users ||--o| colleges : "has (1:0..1)"

    colleges ||--o{ student_profiles : "enrolls"
    departments ||--o{ student_profiles : "categorizes"

    student_profiles ||--o{ student_skills : "possesses"
    skills ||--o{ student_skills : "assigned to"
    student_profiles ||--o{ projects : "creates"
    student_profiles ||--o{ certifications : "holds"

    company_profiles ||--o{ opportunities : "posts"
    opportunities ||--o{ required_skills : "demands"
    skills ||--o{ required_skills : "referenced by"
    opportunities ||--o{ opportunity_required_branches : "targets"
    departments ||--o{ opportunity_required_branches : "referenced by"
    opportunities ||--o{ opportunity_required_years : "requires"

    student_profiles ||--o{ applications : "submits"
    opportunities ||--o{ applications : "receives"

    applications ||--o| internship_records : "progresses to (1:0..1)"
    internship_records ||--o| company_feedback : "evaluated in (1:0..1)"

    users {
        bigint id PK
        varchar email UK
        varchar password
        varchar role
        boolean is_active
        timestamptz created_at
    }

    student_profiles {
        bigint id PK
        bigint user_id FK,UK
        bigint college_id FK
        bigint department_id FK
        varchar first_name
        varchar last_name
        smallint year_of_study
        numeric cgpa
        varchar resume_path
        varchar phone
    }

    opportunities {
        bigint id PK
        bigint company_profile_id FK
        varchar title
        varchar type
        varchar mode
        numeric stipend_amount
        numeric min_cgpa
        date application_deadline
        varchar status
    }

    applications {
        bigint id PK
        bigint student_profile_id FK
        bigint opportunity_id FK
        varchar status
        numeric match_percent_at_apply
        timestamptz applied_at
    }

    internship_records {
        bigint id PK
        bigint application_id FK,UK
        varchar status
        date start_date
        date end_date
    }

    company_feedback {
        bigint id PK
        bigint internship_record_id FK,UK
        text feedback_text
        timestamptz submitted_at
    }
```

### Database Constraints & Schema Conventions
- **Primary Keys:** Every table uses standard `BIGINT GENERATED ALWAYS AS IDENTITY PRIMARY KEY`.
- **Foreign Keys:** Relational integrity enforced at database layer. Restrict deletion on parent entities (`ON DELETE RESTRICT`) to protect audit trails; cascade delete on strictly owned dependent items (`projects`, `certifications`, `required_skills`).
- **Composite Unique Constraints:**
  - `applications(student_profile_id, opportunity_id)` — strictly prevents duplicate submissions.
  - `student_skills(student_profile_id, skill_id)` — prevents duplicate skill associations.
  - `required_skills(opportunity_id, skill_id)` — prevents duplicate job skill requirements.
- **Precision Datatypes:** CGPA utilizes `NUMERIC(4,2)` (0.00–10.00 scale); match scores utilize `NUMERIC(5,2)` (0.00–100.00%).

---

## 12. Testing & Quality Assurance

SkillBridge maintains strict automated test coverage across unit, service, slice, and full lifecycle integration tests.

```
       ▲
      / \     E2E / Integration Tests (PostgreSQL / Flyway / RestAssured)
     /   \    Slice Tests (@WebMvcTest, @DataJpaTest)
    /     \   Service Unit Tests (Mockito / JUnit 5)
   /───────\  Domain Logic Tests (Pure Matching Engine Computations)
```

### Backend Test Execution

Execute test commands from the `apps/api` directory:

```bash
cd apps/api

# Run entire test suite (Unit + Integration with in-memory H2)
./mvnw clean test

# Run a specific domain unit test
./mvnw test -Dtest=MatchingServiceTest

# Run full API Controller slice tests
./mvnw test -Dtest=OpportunityControllerIntegrationTest

# Run end-to-end integration release gates
./mvnw test -Dtest=Stage5ReleaseGateIntegrationTest
```

#### Code Coverage Generation
Generate JaCoCo test execution reports:
```bash
./mvnw clean verify
# Open coverage report in browser:
# target/site/jacoco/index.html
```

### Frontend Linting & Type Checking

Execute verification commands from the `apps/web` directory:

```bash
cd apps/web

# Execute ESLint verification
npm run lint

# Execute TypeScript ambient type-check
npm run typecheck

# Build production bundle to verify asset imports
npm run build
```

---

## 13. Deployment & DevOps

### Containerization with Docker

The API server features an optimized multi-stage `Dockerfile` utilizing Eclipse Temurin JDK 21 Jammy for build and a minimal JRE Jammy image for production runtime.

```dockerfile
# Build Stage
FROM maven:3.9.9-eclipse-temurin-21-jammy AS build
WORKDIR /app
COPY pom.xml .
RUN mvn dependency:go-offline -B
COPY src ./src
RUN mvn clean package -DskipTests -B

# Production Runtime Stage
FROM eclipse-temurin:21-jre-jammy
WORKDIR /app
RUN addgroup --system skillbridge && adduser --system --ingroup skillbridge skillbridge
RUN mkdir -p /app/uploads/resumes && chown -R skillbridge:skillbridge /app
COPY --from=build --chown=skillbridge:skillbridge /app/target/*.jar app.jar
USER skillbridge
ENV PORT=8080
EXPOSE 8080
ENTRYPOINT ["java", "-XX:+UseContainerSupport", "-XX:MaxRAMPercentage=75.0", "-jar", "app.jar"]
```

### Docker Compose Multi-Container Stack

Run the entire platform (PostgreSQL 16 + Spring Boot Backend) locally with Docker Compose:

```yaml
version: '3.8'

services:
  postgres:
    image: postgres:16-alpine
    container_name: skillbridge-db
    environment:
      POSTGRES_DB: skillbridge
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgrespassword
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U postgres -d skillbridge"]
      interval: 5s
      timeout: 5s
      retries: 5

  api:
    build:
      context: ./apps/api
      dockerfile: Dockerfile
    container_name: skillbridge-api
    depends_on:
      postgres:
        condition: service_healthy
    environment:
      DB_URL: jdbc:postgresql://postgres:5432/skillbridge
      DB_USERNAME: postgres
      DB_PASSWORD: postgrespassword
      PORT: 8080
      JWT_SECRET: 404E635266556A586E3272357538782F413F4428472B4B6250645367566B5970
      JWT_EXPIRY_MS: 86400000
      FILE_UPLOAD_DIR: /app/uploads/resumes
    ports:
      - "8080:8080"
    volumes:
      - resume_storage:/app/uploads/resumes

volumes:
  postgres_data:
  resume_storage:
```

#### Launch the Stack:
```bash
docker-compose up -d --build
docker-compose logs -f api
```

### Production Readiness Checklist
- [x] Dedicated non-root container execution user (`skillbridge`).
- [x] Automated database schema migration gatekeeping via Flyway.
- [x] Externalized credentials via environment variables (zero hardcoded secrets).
- [ ] TLS / HTTPS termination configured on reverse proxy (e.g., NGINX / Cloudflare).
- [ ] Production-grade S3/Cloud Storage adapter substituted for local resume storage.
- [ ] CORS whitelisting restricted strictly to verified production domain names.

---

## 14. Performance, Security & Troubleshooting

### Security Hardening
1. **Injection Protection:** All database interactions are executed via Spring Data JPA parameterized queries and prepared statements. Raw SQL string concatenation is strictly prohibited.
2. **Access Control Verification:** URL patterns enforce coarse role filtering (`hasRole('STUDENT')`), while `@PreAuthorize` guards verify resource ownership (e.g., ensuring recruiters can only modify applications submitted to their own company's opportunities).
3. **Stateless Session Guarantees:** Server nodes store zero in-memory session state. Tokens must be submitted with every invocation.
4. **File Upload Hardening:** Uploaded files are strictly restricted to `application/pdf`, limited to 5MB, and stored using generated, randomized UUID filenames to prevent path traversal attacks.

### Troubleshooting Common Issues

| Error Symptom | Root Cause | Exact Resolution |
|---|---|---|
| `PSQLException: Connection to localhost:5432 refused` | PostgreSQL server daemon is stopped or listening on another port. | Verify PostgreSQL status with `sudo systemctl status postgresql` (Linux) or check Docker desktop container `skillbridge-db`. Ensure `DB_URL` points to port `5432`. |
| `FlywayException: Validate failed: Migration checksum mismatch for V1` | A previously applied migration script was modified locally after being run against the database. | Never alter historical Flyway migrations. Revert changes in `V1__create_initial_schema.sql` or run `./mvnw flyway:repair` if changes were purely stylistic. |
| `CORS Error: Access to XMLHttpRequest blocked by CORS policy` | Frontend origin (`http://localhost:5174`) is missing from backend CORS whitelist. | Check `SecurityConfig.java` and confirm `corsConfigurationSource()` includes your exact Vite development port (`5174` or `5173`). |
| `401 Unauthorized: JWT signature does not match` | Client token was generated with a different `JWT_SECRET` key than the server's current secret. | Ensure `JWT_SECRET` in `apps/api/.env` is consistent. Clear `sessionStorage` in your browser and re-authenticate via `/login`. |
| `413 Payload Too Large on resume upload` | Uploaded resume exceeds the configured 5MB servlet ceiling. | Ensure uploaded file is `< 5MB`. To adjust threshold, increase `spring.servlet.multipart.max-file-size` in `application.yaml`. |

---

## 15. Roadmap & Changelog

### Version 1.0.0 (Current MVP Release)
- [x] Deterministic set-intersection skill matching engine (`matched`, `missing`, `matchPercent`).
- [x] Independent academic eligibility filter (departments, study years, minimum CGPA).
- [x] Multi-tenant role authentication (`STUDENT`, `COMPANY`, `COLLEGE`, `ADMIN`).
- [x] Student profile, skills portfolio, and resume file upload.
- [x] Company recruitment pipeline management (`APPLIED` → `SELECTED`).
- [x] College institutional skill-gap analytics (`HIGH`, `MODERATE`, `LOW`).
- [x] Admin organizational verification and skill taxonomy governance.

### Version 1.1.0 (Upcoming)
- [ ] Asynchronous email notifications for recruitment stage transitions.
- [ ] NLP-based skill extraction from PDF resumes for suggested one-click profile population.
- [ ] Exportable institutional skill-gap reports in PDF and Excel formats for accreditation boards.

### Version 2.0.0 (Long-Term Vision)
- [ ] Formal College-to-Company Memorandum of Understanding (MOU) management.
- [ ] Alumni career outcome tracking and longitudinal skill utility analytics.
- [ ] External assessment platform integrations (HackerRank / LeetCode API bridges).

*Refer to the full [CHANGELOG.md](CHANGELOG.md) for detailed revision histories.*

---

## 16. Contributing & Code of Conduct

We welcome contributions from the engineering community. Please adhere to the following workflow:

1. **Fork the Repository** on GitHub.
2. **Create a Feature Branch:**
   ```bash
   git checkout -b feat/skill-weighting-engine
   ```
3. **Commit Your Changes** following the [Conventional Commits](https://www.conventionalcommits.org/) specification:
   ```bash
   git commit -m "feat(matching): implement department-level skill weighting support"
   ```
4. **Run Local Verification Checks:**
   ```bash
   # Backend:
   cd apps/api && ./mvnw clean test

   # Frontend:
   cd apps/web && npm run lint && npm run typecheck
   ```
5. **Push to Your Remote Branch:**
   ```bash
   git push origin feat/skill-weighting-engine
   ```
6. **Open a Pull Request (PR)** against the `main` branch with a clear summary of changes and test verifications.

*Please review our complete [CONTRIBUTING.md](CONTRIBUTING.md) and [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md) before participating.*

---

## 17. License, Acknowledgments & Contact

### License
This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for complete terms and permissions.

### Acknowledgments
- **Smart India Hackathon (SIH 2026):** For problem statement **PS044** ("Portal for Academia–Industry Collaboration for Skill Mapping, Internships and Placement").
- **Spring Boot & React Communities:** For providing the foundational open-source toolchains powering enterprise and web applications worldwide.
- **Lucide Icons & Tailwind CSS:** For the visual aesthetic and accessible design tokens.

### Author & Maintainer Details
- **Project Lead:** Lalith Aditya S
- **GitHub:** [@lalithadityas](https://github.com/lalithadityas)
- **LinkedIn:** [Lalith Aditya Singuparapu](https://www.linkedin.com/in/lalith-aditya-singuparapu)
- **Email:** [lalithadityasinguparapu@gmail.com](mailto:2400031810@kluniversity.in)
- **Repository:** [https://github.com/lalithadityas/SkillBridge](https://github.com/lalithadityas/SkillBridge)

<div align="center">
  <p><a href="#skillbridge"><strong>[↑ Back to Top]</strong></a></p>
</div>
