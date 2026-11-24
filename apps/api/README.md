<div align="center">

# SkillBridge Backend

**Spring Boot REST API for skill mapping, internship and placement workflows, opportunity matching, and institutional analytics.**

[![REST API endpoints](https://img.shields.io/badge/REST%20API-64%20endpoints-2563EB?style=flat-square)](#core-api-surface)
[![Controllers](https://img.shields.io/badge/Controllers-12-0F766E?style=flat-square)](#directory-structure)
[![JPA entities](https://img.shields.io/badge/JPA%20entities-16-7C3AED?style=flat-square)](#database-and-migrations)
[![Matcher competencies](https://img.shields.io/badge/Matcher-18%20competencies-0891B2?style=flat-square)](#matching-and-analytics)
[![Eligibility criteria](https://img.shields.io/badge/Eligibility-4%20criteria-F97316?style=flat-square)](#matching-and-analytics)
[![Analytics categories](https://img.shields.io/badge/Analytics-18%20categories-4F46E5?style=flat-square)](#matching-and-analytics)
[![Gap severity bands](https://img.shields.io/badge/Gap%20severity-4%20bands-DC2626?style=flat-square)](#matching-and-analytics)
[![Test methods](https://img.shields.io/badge/Test%20methods-155-success?style=flat-square)](#testing-and-quality)
[![Java 21](https://img.shields.io/badge/Java-21%20LTS-007396?style=flat-square&logo=openjdk&logoColor=white)](https://openjdk.org/)
[![Spring Boot 4.1.1](https://img.shields.io/badge/Spring%20Boot-4.1.1-6DB33F?style=flat-square&logo=springboot&logoColor=white)](https://spring.io/projects/spring-boot)
[![PostgreSQL 16](https://img.shields.io/badge/PostgreSQL-16-4169E1?style=flat-square&logo=postgresql&logoColor=white)](https://www.postgresql.org/)

</div>

SkillBridge is a modular-monolith backend for the SkillBridge academia–industry collaboration platform. It provides role-aware REST APIs for students, companies, colleges, and administrators with PostgreSQL persistence and JWT-based authentication.

The opportunity matcher is deterministic and rule-based: it compares student skills with opportunity requirements and evaluates branch, year-of-study, and CGPA constraints. College analytics compare opportunity demand with student skill availability across 18 skill categories and classify gaps into four severity bands.

## Contents

- [Architecture](#architecture)
- [Matching and Analytics](#matching-and-analytics)
- [Technology Stack](#technology-stack)
- [Directory Structure](#directory-structure)
- [Local Development](#local-development)
- [Configuration](#configuration)
- [Authentication and Security](#authentication-and-security)
- [Core API Surface](#core-api-surface)
- [Database and Migrations](#database-and-migrations)
- [Testing and Quality](#testing-and-quality)
- [Docker](#docker)
- [Troubleshooting](#troubleshooting)

## Architecture

The backend is a modular monolith. Domain packages separate business capabilities while sharing security infrastructure and PostgreSQL persistence.

```text
React/Vite frontend
  -> HTTP REST/JSON (/api/v1/**)
  -> Spring Security filters
  -> JWT authentication
  -> REST controller
  -> Request validation
  -> Domain service
  -> Spring Data JPA repository
  -> PostgreSQL
```

### Request Lifecycle

1. The client sends `Authorization: Bearer <JWT>` when authentication is required.
2. The CORS and JWT filters process the request.
3. Spring Security resolves the principal and evaluates role requirements.
4. `@PreAuthorize` checks coarse roles and fine-grained resource ownership.
5. Controllers validate request DTOs using Jakarta Validation.
6. Services enforce domain rules and coordinate repositories.
7. Repositories execute parameterized JPA or native database operations.
8. Services return DTOs instead of exposing persistence entities directly.
9. Resume files are written to the configured local storage directory.

### Core Domain Boundaries

- `auth` — Registration, login, JWT issuance, and current-user lookup
- `user` — Shared identity and role definitions
- `student` — Profiles, skills, projects, certificates, and resumes
- `college` — College profiles, departments, rosters, and analytics
- `company` — Company profiles and verification state
- `opportunity` — Internship and placement listings
- `application` — Candidate applications and recruitment stages
- `matching` — Deterministic matching and recommendations
- `internship` — Internship records and outcomes
- `analytics` — Skill-gap and placement-funnel reports
- `admin` — User administration and organization moderation
- `skill` — Standardized skill taxonomy
- `file` — Resume storage

No external email, object-storage, or background-job integration is configured in the inspected service.

## Matching and Analytics

The opportunity matcher evaluates:

- 18 standardized competencies
- Skill coverage
- Branch eligibility
- Year-of-study eligibility
- Minimum CGPA

The matching engine separates eligibility from skill ranking. It returns matched skills, missing skills, match percentage, eligibility status, and ineligibility reasons.

College analytics compare opportunity demand with student skill availability across 18 categories. Gaps are classified into four severity bands and used to generate institutional skill-gap dashboards.

## Technology Stack

| Component | Technology | Version | Responsibility |
|---|---|---:|---|
| Runtime | Java | 21 LTS | Application runtime |
| Framework | Spring Boot | 4.1.1 | REST, dependency injection, configuration |
| Security | Spring Security | Managed by Boot | Authentication and RBAC |
| JWT | JJWT | 0.12.6 | Token creation and verification |
| Persistence | Spring Data JPA / Hibernate | Managed by Boot | ORM and repositories |
| Database | PostgreSQL | 16 | Primary data store |
| Migrations | Flyway | Managed by Boot | Versioned schema management |
| Build | Maven | 3.9+ or included Wrapper | Build, test, package, run |
| Testing | JUnit 5, Spring Boot Test, H2 | Managed by Maven | Unit and integration testing |
| Container | Docker | 24+ | Backend packaging |

The Maven artifact is `com.skillbridge:api:0.0.1-SNAPSHOT`.

## Directory Structure

```text
apps/api/
├── src/main/java/com/skillbridge/
│   ├── SkillBridgeApplication.java
│   ├── admin/          # Administration and moderation
│   ├── analytics/      # Skill-gap and placement analytics
│   ├── application/    # Application lifecycle
│   ├── auth/           # Registration, login, JWT, current user
│   ├── college/        # College profiles and student rosters
│   ├── common/         # Security, DTOs, entities, exceptions
│   ├── company/        # Company profiles
│   ├── file/           # Resume file handling
│   ├── internship/     # Internship records
│   ├── matching/       # Matcher and recommendations
│   ├── opportunity/    # Internship and placement opportunities
│   ├── skill/          # Standardized skill taxonomy
│   ├── student/        # Profiles, skills, projects, certificates
│   └── user/           # Identity and roles
├── src/main/resources/
│   ├── application.yaml
│   └── db/migration/
│       ├── V1__create_initial_schema.sql
│       └── V2__add_student_phone.sql
├── src/test/
│   ├── java/
│   └── resources/
├── .env.example
├── Dockerfile
├── mvnw
├── mvnw.cmd
└── pom.xml
```

The service contains 12 REST controllers and 16 JPA entities.

## Local Development

### Prerequisites

- JDK 21
- PostgreSQL 16 or a compatible PostgreSQL instance
- Git
- Docker is optional

Verify the installation:

```bash
java -version
psql --version
./mvnw -version
```

On Windows:

```powershell
java -version
.\mvnw.cmd -version
```

### 1. Clone the Repository

```bash
git clone https://github.com/lalithadityas/SkillBridge.git
cd SkillBridge/apps/api
```

### 2. Start PostgreSQL

Create a local database:

```sql
CREATE DATABASE skillbridge;
```

Using Docker:

```bash
docker run --name skillbridge-postgres \
  -e POSTGRES_DB=skillbridge \
  -e POSTGRES_USER=postgres \
  -e POSTGRES_PASSWORD=postgres \
  -p 5432:5432 \
  -d postgres:16
```

### 3. Configure Environment Variables

Copy the example file:

```bash
cp .env.example .env
mkdir -p uploads/resumes
```

Export configuration values on Unix or macOS:

```bash
export DB_URL='jdbc:postgresql://localhost:5432/skillbridge'
export DB_USERNAME='postgres'
export DB_PASSWORD='postgres'
export PORT='8080'
export JWT_SECRET='<replace-with-a-long-random-secret>'
export JWT_EXPIRY_MS='86400000'
export FILE_UPLOAD_DIR='./uploads/resumes'
```

Export configuration values on Windows PowerShell:

```powershell
$env:DB_URL='jdbc:postgresql://localhost:5432/skillbridge'
$env:DB_USERNAME='postgres'
$env:DB_PASSWORD='postgres'
$env:PORT='8080'
$env:JWT_SECRET='<replace-with-a-long-random-secret>'
$env:JWT_EXPIRY_MS='86400000'
$env:FILE_UPLOAD_DIR='./uploads/resumes'
```

The example JWT secret must not be used outside local development.

### 4. Build and Run

Unix/macOS:

```bash
./mvnw clean verify
./mvnw spring-boot:run
```

Windows:

```powershell
.\mvnw.cmd clean verify
.\mvnw.cmd spring-boot:run
```

The API is available at:

```text
http://localhost:8080
```

Flyway applies migrations during startup. Hibernate validates entity mappings with `ddl-auto: validate` and does not generate or modify the schema.

## Configuration

| Variable | Required | Default | Description |
|---|---:|---|---|
| `DB_URL` | Yes | `jdbc:postgresql://localhost:5432/skillbridge` | PostgreSQL JDBC URL |
| `DB_USERNAME` | Yes | `postgres` | Database role |
| `DB_PASSWORD` | Yes | `postgres` | Database password |
| `PORT` | No | `8080` | HTTP server port |
| `JWT_SECRET` | Yes | Development value | HMAC signing secret |
| `JWT_EXPIRY_MS` | No | `86400000` | Access-token lifetime in milliseconds |
| `FILE_UPLOAD_DIR` | No | `./uploads/resumes` | Resume storage directory |

For production, use a generated secret and store credentials in a secret manager or deployment platform.

## Authentication and Security

### Token Lifecycle

- `POST /api/v1/auth/register` creates an account and returns an authentication response.
- `POST /api/v1/auth/login` validates credentials and returns a JWT.
- Protected endpoints require `Authorization: Bearer <JWT>`.
- `GET /api/v1/auth/me` returns current-user information.
- `POST /api/v1/auth/logout` exists as a logout endpoint.
- JWT authentication is stateless; clients must remove their local token.
- The configured access-token lifetime is 24 hours.
- A refresh-token flow is not identified in the inspected implementation and has not been documented as available.

### RBAC

| Role | Scope |
|---|---|
| `STUDENT` | Own profile, skills, projects, certificates, resume, applications, and recommendations |
| `COMPANY` | Company profile, owned opportunities, applicants, and recruitment pipeline |
| `COLLEGE` | College profile, student roster, and institutional analytics |
| `ADMIN` | User administration, taxonomy, verification queue, and opportunity moderation |

Authorization combines role checks with resource-ownership checks. For example:

```text
hasRole('COMPANY') and
@securityService.isOpportunityOwner(#id, authentication)
```

Passwords are hashed using BCrypt. Database queries use JPA repositories and parameterized operations. Resume uploads are restricted to PDF files with a 5 MB multipart limit.

Production deployments should add TLS, restricted CORS origins, database TLS, secret rotation, rate limiting, security headers, and centralized audit logging.

## Core API Surface

All endpoints use `/api/v1` unless noted otherwise.

| Method | Endpoint Prefix | Authentication | Responsibility |
|---|---|---|---|
| `POST`, `GET` | `/auth` | Registration/login public; `/me` protected | Authentication and identity |
| `GET`, `PUT`, `POST`, `DELETE` | `/students` | `STUDENT` or institution roles | Student profile and portfolio |
| `GET`, `PUT` | `/companies` | `COMPANY` | Company profile |
| `GET`, `PUT` | `/colleges` | `COLLEGE` or `ADMIN` | College profile and rosters |
| `GET`, `POST`, `PUT`, `DELETE` | `/skills` | Reads public; writes require `ADMIN` | Skill taxonomy |
| `GET`, `POST` | `/departments` | Reads public; writes require `ADMIN` | Academic departments |
| `GET`, `POST`, `PUT`, `PATCH` | `/opportunities` | Mixed; writes require `COMPANY` | Opportunity lifecycle |
| `GET`, `POST`, `PATCH` | `/applications` | Mixed | Application and recruitment pipeline |
| `GET` | `/matching` | `STUDENT` | Match evaluation and recommendations |
| `GET` | `/analytics` | `COLLEGE` or `ADMIN` | Skill-gap and placement analytics |
| `GET`, `PATCH` | `/admin` | `ADMIN` | User and organization administration |

Example login:

```bash
curl -X POST http://localhost:8080/api/v1/auth/login \
  -H 'Content-Type: application/json' \
  -d '{
    "email": "student@university.edu",
    "password": "Password123!"
  }'
```

Example authenticated request:

```bash
curl http://localhost:8080/api/v1/auth/me \
  -H 'Authorization: Bearer <JWT>'
```

OpenAPI or Swagger configuration is not declared in the inspected Maven dependencies. [TODO: Verify whether Swagger/OpenAPI is enabled before publishing Swagger URLs.]

## Database and Migrations

The service defines 16 JPA entities, including users, profiles, departments, skills, opportunities, applications, internships, and feedback.

### Core Relationships

```text
User -> StudentProfile -> Skills
User -> StudentProfile -> Projects
User -> StudentProfile -> Certificates
User -> CompanyProfile -> Opportunities
College -> Departments -> StudentProfiles
StudentProfile + Opportunity -> Application
Application -> InternshipRecord
InternshipRecord -> CompanyFeedback
```

Notable constraints include:

- Unique applications by student and opportunity
- Unique student skill associations
- Unique opportunity skill requirements
- Restricted deletion for critical parent resources
- Cascading deletion for strictly owned dependent resources

### Migrations

Flyway migrations are stored in:

```text
src/main/resources/db/migration
```

Current migrations:

```text
V1__create_initial_schema.sql
V2__add_student_phone.sql
```

Add future migrations by creating a new forward-only SQL file:

```text
V3__<description>.sql
```

Never modify an already-applied migration. Back up production data and test migration changes against a database copy before deployment.

## Testing and Quality

The project reports 155 successful unit, integration, and gate-test methods.

Run the complete verification lifecycle:

```bash
./mvnw clean verify
```

Run tests only:

```bash
./mvnw test
```

Run one test class:

```bash
./mvnw -Dtest=MatchingServiceTest test
```

Windows:

```powershell
.\mvnw.cmd clean verify
.\mvnw.cmd test
```

Generate the JaCoCo report if configured:

```bash
./mvnw clean verify
```

Open:

```text
target/site/jacoco/index.html
```

Before opening a pull request:

```bash
./mvnw clean verify
git diff --check
```

## Docker

Build the image:

```bash
docker build -t skillbridge-api ./apps/api
```

Run the API:

```bash
docker run --rm \
  -p 8080:8080 \
  -e DB_URL='jdbc:postgresql://host.docker.internal:5432/skillbridge' \
  -e DB_USERNAME='postgres' \
  -e DB_PASSWORD='replace-me' \
  -e JWT_SECRET='replace-with-a-random-secret' \
  -e JWT_EXPIRY_MS='86400000' \
  -e FILE_UPLOAD_DIR='/app/uploads/resumes' \
  -v skillbridge-resumes:/app/uploads/resumes \
  skillbridge-api
```

Start the local stack:

```bash
docker-compose up -d --build
docker-compose logs -f api
docker-compose down
```

## Troubleshooting

### PostgreSQL Connection Refused

Verify that PostgreSQL is running and that `DB_URL` uses the correct host and port.

```bash
pg_isready -h localhost -p 5432
```

### Flyway Checksum Mismatch

An applied migration was changed locally.

- Restore the original migration file.
- Add a new migration for the intended change.
- Repair migration metadata only after reviewing database state.

### 401 Unauthorized

Verify:

- The `Bearer` prefix is present.
- `JWT_SECRET` is identical across API instances.
- The token has not expired.
- `JWT_EXPIRY_MS` is a valid millisecond value.
- The client sends the latest token.

### Resume Upload Failure

Verify:

- The file is PDF.
- The file is smaller than 5 MB.
- `FILE_UPLOAD_DIR` exists.
- The application process can write to the directory.
- The container has an appropriate volume mount.
