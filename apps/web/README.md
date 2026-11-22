# SkillBridge — Frontend

The SkillBridge frontend is a role-based web application connecting students, companies, colleges, and administrators around skill mapping, internships, placements, and recruitment. This README documents the frontend architecture, user journeys, local setup, API configuration, quality checks, and deployment workflow.

> **Project:** SIH 2026 PS26044 — Portal for Academia–Industry Collaboration for Skill Mapping, Internships and Placement  
> **Live application:** [skillbridgeorg.vercel.app](https://skillbridgeorg.vercel.app/)  
> **Repository:** [lalithadityas/skillbridge](https://github.com/lalithadityas/skillbridge)

## Contents

- [Product overview](#product-overview)
- [Frontend features](#frontend-features)
- [Technology stack](#technology-stack)
- [Architecture](#architecture)
- [End-to-end user flows](#end-to-end-user-flows)
- [Prerequisites](#prerequisites)
- [Run locally](#run-locally)
- [Configuration](#configuration)
- [Scripts and quality checks](#scripts-and-quality-checks)
- [Project structure](#project-structure)
- [API integration](#api-integration)
- [Build and deployment](#build-and-deployment)
- [Troubleshooting](#troubleshooting)
- [Security notes](#security-notes)
- [Contributing](#contributing)
- [Related documentation](#related-documentation)

## Product overview

SkillBridge is a portal for collaboration between academia and industry. The frontend presents workflows for four user roles:

| Role | Primary workflows |
| --- | --- |
| **Student** | Maintain academic and skills profiles, discover opportunities, apply, track applications, and review skill-gap information. |
| **Company** | Maintain a company profile, publish opportunities, review candidates, and manage recruitment stages. |
| **College / placement cell** | View students and departments, skill availability, industry demand, skill gaps, and recruitment analytics. |
| **Administrator** | Manage accounts, organization verifications, the skills taxonomy, and opportunity moderation. |

Matching and skill-coverage values shown in the UI depend on data returned by the API; they should not be interpreted as verified assessments unless the backend explicitly provides that guarantee.

## Frontend features

- Public landing, sign-in, and registration pages.
- Role-aware dashboards, navigation, and protected routes.
- Student, company, college, and admin areas.
- Shared API client and feature-level API modules.
- Server-state fetching and caching with TanStack Query.
- Optional mock API mode for local UI development and demos.
- Responsive styling with Tailwind CSS and shared global styles.

The frontend route guards provide navigation and user experience. They are **not** a substitute for authorization checks in the backend.

## Technology stack

| Concern | Technology |
| --- | --- |
| UI | React 18, JavaScript (ES modules and JSX) |
| Development server and build | Vite 5 |
| Routing | React Router 6 |
| Server state and caching | TanStack React Query 5 |
| HTTP client | Axios |
| Styling | Tailwind CSS 3, PostCSS, Autoprefixer, global CSS |
| Icons | Lucide React |
| Linting and type checking | ESLint 9, TypeScript tooling |
| Backend integration | Spring Boot REST API, Java, Spring Security, JWT |
| Backend data store | PostgreSQL |

React, Vite, Tailwind CSS, React Router, Axios, and the other frontend packages are defined in `apps/web/package.json`. shadcn/ui and Recharts may be mentioned in broader project planning, but are not direct dependencies in the current frontend package manifest.

## Architecture

The frontend is a single-page application (SPA). Vite serves it during development and creates static assets for deployment.

```text
Browser
└── React SPA
    ├── React Router — public pages and role-protected dashboards
    ├── Auth context — signed-in user and role-aware navigation
    ├── Shared layouts/components — reusable dashboard and UI elements
    ├── TanStack Query — API-backed server state and caching
    └── Feature API modules
        └── Shared Axios client — /api/v1
            └── Spring Boot REST API — authentication, authorization, business rules
                └── PostgreSQL
```

### Request lifecycle

1. `src/main.jsx` mounts the React application and global stylesheet.
2. `src/App.jsx` composes application providers and declares public and role-protected routes.
3. Pages and reusable components call feature API modules under `src/api`.
4. The shared Axios client sends requests to the configured API base URL. It adds the session JWT as a bearer token when present and uses a 15-second timeout.
5. TanStack Query manages server-state caching and request behavior.
6. In development, Vite proxies `/api/v1` to `http://localhost:8080`.
7. A `401` response clears the stored session and redirects the browser to the login page. Backend authorization remains authoritative.

## End-to-end user flows

### Authentication (shared)

1. The user opens the public landing page and chooses sign-in or registration.
2. The frontend submits the form to the authentication API.
3. On success, the session JWT is stored in browser `sessionStorage`; the frontend obtains the current user profile when supported by the API.
4. The user's role determines the destination dashboard and the navigation options displayed.
5. Protected routes verify the session, redirect signed-out visitors to sign-in, and route users without the required role to an unauthorized page.
6. Sign-out clears session data. An expired or invalid session is cleared after an API `401` response.

### Student

1. Complete or update the academic profile and skills.
2. Browse opportunities and inspect their details, requirements, and eligibility information.
3. Review match or skill-coverage details where the API provides them.
4. Apply to a suitable opportunity.
5. Follow application stages and, where applicable, internship or placement progress.
6. Review recommendations and skill-gap information.

### Company

1. Create or update the company profile.
2. Create and manage opportunity postings, including required skills and eligibility criteria.
3. Review applicants and candidate profiles.
4. Manage recruitment stages and track outcomes.

### College / placement cell

1. Review the institution profile, students, and departments.
2. Explore student skill availability alongside industry demand.
3. Review skill-gap and recruitment analytics.

### Administrator

1. Review platform activity and user accounts.
2. Process organization verification requests.
3. Maintain the skills taxonomy and moderate opportunities.

> These describe product workflows and frontend areas. The availability and behavior of each action depends on its API integration and backend configuration.

## Prerequisites

- Git
- Node.js 18 or newer and npm
- For API-backed workflows: Java/Maven as required by `apps/api`, plus a running PostgreSQL instance

Check your local versions:

```bash
node --version
npm --version
```

## Run locally

### 1. Clone the repository

```bash
git clone https://github.com/lalithadityas/skillbridge.git
cd skillbridge
```

### 2. Install frontend dependencies

```bash
cd apps/web
npm ci
```

`npm ci` installs the locked dependencies from `package-lock.json`. Run this from `apps/web`.

### 3. Start the frontend

```bash
npm run dev
```

Open [http://localhost:5174](http://localhost:5174). The Vite server listens on port `5174`; requests under `/api/v1` are proxied to `http://localhost:8080`.

### 4. Start the backend for API-backed workflows

In another terminal, from the repository root:

1. Create or select a PostgreSQL database for SkillBridge.
2. Configure the backend using [`apps/api/.env.example`](../api/.env.example). Set the database connection details, application port, JWT secret, and token expiry for your local environment.
3. Start the API with the Maven wrapper:

```bash
cd apps/api
./mvnw spring-boot:run
```

On Windows PowerShell or Command Prompt:

```powershell
cd apps/api
.\mvnw.cmd spring-boot:run
```

The frontend development proxy targets port `8080`. If the API uses another port, update the proxy target in `apps/web/vite.config.ts`.

### 5. Optional: run without a local API

For local UI development or a demo, create `apps/web/.env.local` with:

```dotenv
VITE_USE_MOCK_API=true
```

Restart Vite after changing environment variables. Mock mode is intended for development; it does not replace the backend or production services. Remove the setting or set it to `false` to use the real API.

## Configuration

Vite exposes frontend variables prefixed with `VITE_`. Local overrides belong in `apps/web/.env.local`.

| Variable | Default | Description |
| --- | --- | --- |
| `VITE_API_BASE_URL` | `/api/v1` | API base URL. Keep the default for same-origin requests and the local Vite proxy. |
| `VITE_USE_MOCK_API` | `false` | Enables the frontend mock data layer when set to `true`. |

Example for a separately hosted API:

```dotenv
VITE_API_BASE_URL=https://api.example.com/api/v1
VITE_USE_MOCK_API=false
```

The API host must allow requests from the deployed frontend origin (CORS). Use HTTPS in production. **Do not put secrets in frontend environment variables**: `VITE_*` values are included in code delivered to the browser and are publicly observable.

## Scripts and quality checks

Run commands from `apps/web`:

| Command | Description |
| --- | --- |
| `npm run dev` | Start the Vite development server. |
| `npm run lint` | Run ESLint. |
| `npm run typecheck` | Run the configured TypeScript check. |
| `npm run build` | Create the optimized production build in `dist/`. |
| `npm run preview` | Preview the production build locally; run the build first. |

There is currently no frontend test script defined in `apps/web/package.json`.

Before submitting frontend changes, run:

```bash
npm run lint
npm run typecheck
npm run build
```

## Project structure

```text
apps/web/
├── index.html                 # SPA HTML entry point
├── package.json               # Dependencies and npm scripts
├── package-lock.json          # Reproducible dependency lockfile
├── vite.config.ts             # Vite config, alias, port, and API proxy
├── tailwind.config.js         # Tailwind content and theme configuration
├── vercel.json                # SPA route rewrite for Vercel
└── src/
    ├── main.jsx               # React entry point
    ├── App.jsx                # Providers and route definitions
    ├── api/                   # API client, feature APIs, and mock layer
    ├── components/            # Shared UI and navigation components
    ├── context/               # Authentication context
    ├── hooks/                 # Reusable React hooks
    ├── layouts/               # Dashboard layouts and navigation config
    ├── pages/                 # Public and role-specific pages
    ├── routes/                # Protected route handling
    ├── styles/                # Global styles
    └── utils/                 # Auth helpers and shared constants
```

Use the `@/` alias for imports from `src` (for example, `@/api`). Keep role-specific screens in their corresponding `src/pages/<role>` area and shared UI in `src/components`.

## API integration

- API endpoints are versioned under `/api/v1`.
- The API contract is documented in [`docs/06-api/openapi.yaml`](../../docs/06-api/openapi.yaml).
- Feature-specific API modules use the shared Axios client.
- The client sets JSON headers, uses a 15-second timeout, attaches the bearer token from `sessionStorage`, and normalizes API errors.
- TanStack Query is configured in `src/App.jsx` for server-state caching and retry behavior.
- Session information is kept in browser `sessionStorage`, rather than long-lived `localStorage`.
- Authentication, authorization, input validation, and resource ownership must be enforced by the API, regardless of frontend route guards or hidden UI controls.

## Build and deployment

### Verify a production build locally

```bash
cd apps/web
npm ci
npm run lint
npm run typecheck
npm run build
npm run preview
```

The production assets are generated in `apps/web/dist`. For a static hosting provider, configure the project root as `apps/web`, install dependencies with `npm ci`, and build with `npm run build`. Configure SPA fallback/rewrite behavior so direct navigation to client-side routes serves `index.html`; `vercel.json` provides the Vercel rewrite configuration.

Before deploying:

- Set `VITE_API_BASE_URL` to the intended API endpoint if the API is not same-origin.
- Ensure `VITE_USE_MOCK_API=false` for production.
- Configure backend CORS for the deployed frontend origin.
- Verify HTTPS, backend authentication/authorization, and production environment settings.
- Never include secrets in frontend configuration.

## Troubleshooting

| Problem | Checks |
| --- | --- |
| `npm ci` fails | Confirm Node/npm versions and that the command is run in `apps/web`, where the lockfile is located. |
| API requests fail locally | Confirm the API is running on port `8080`, the database is available, and Vite's `/api/v1` proxy target is correct. |
| Requests go to the wrong API host | Check `VITE_API_BASE_URL` in `apps/web/.env.local`; restart Vite after changing environment variables. |
| Sign-in returns to the login page | Check API availability, credentials, token validity, and the browser's network response. A `401` clears the stored session. |
| Nested route returns 404 after deployment | Configure the hosting provider to rewrite application routes to `index.html`. |
| Mock/demo data appears unexpectedly | Check `VITE_USE_MOCK_API` and restart the development server after changing it. |

## Security notes

- Treat all `VITE_*` variables and frontend-delivered content as public.
- Use HTTPS and a strong, unique backend JWT secret in deployed environments. Do not reuse sample secrets from environment examples.
- `sessionStorage` reduces persistence across browser sessions but does not eliminate XSS risk. Continue to apply dependency hygiene, safe rendering, and appropriate content security practices.
- Frontend role-based navigation is a usability feature, not a security boundary. Enforce roles and data access on the API.
- Do not log tokens, passwords, or sensitive profile information in browser logs or analytics.

## Contributing

1. Create a focused branch from the default branch.
2. Keep changes scoped to the frontend unless an API contract change is needed.
3. Follow the existing `src` organization and reuse shared components and API modules.
4. Run `npm run lint`, `npm run typecheck`, and `npm run build` from `apps/web`.
5. In your pull request, summarize the change and include screenshots for UI changes, along with any configuration or API contract updates.

## Related documentation

- [Repository README](../../README.md)
- [Product requirements](../../docs/01-product/PRD.md)
- [Architecture](../../docs/04-architecture/architecture.md)
- [REST API design](../../docs/06-api/api-design.md)
- [OpenAPI contract](../../docs/06-api/openapi.yaml)
- [Backend environment example](../api/.env.example)

---

**License:** No license is currently specified in the repository. Contact the repository maintainers before redistributing or reusing this project.
