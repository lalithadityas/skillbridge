# SkillBridge — Frontend

The SkillBridge frontend is a role-based web application for connecting students, companies, and colleges around skill discovery, internships, placements, recruitment, and skill-gap insights. This README covers the frontend in `apps/web`; the repository also contains the Spring Boot API in `apps/api`.

> **Project:** SIH 2026 PS26044 — Portal for Academia–Industry Collaboration for Skill Mapping, Internships and Placement  
> **Live application:** [skillbridgeorg.vercel.app](https://skillbridgeorg.vercel.app/)  
> **Repository:** [lalithadityas/skillbridge](https://github.com/lalithadityas/skillbridge)

## Contents

- [Product overview](#product-overview)
- [Frontend capabilities](#frontend-capabilities)
- [Technology stack](#technology-stack)
- [Architecture](#architecture)
- [End-to-end user flows](#end-to-end-user-flows)
- [Prerequisites](#prerequisites)
- [Run locally](#run-locally)
- [Configuration](#configuration)
- [Available scripts](#available-scripts)
- [Project structure](#project-structure)
- [API integration](#api-integration)
- [Build and deployment](#build-and-deployment)
- [Troubleshooting](#troubleshooting)
- [Security and production notes](#security-and-production-notes)
- [Contributing](#contributing)
- [Related documentation](#related-documentation)

## Product overview

SkillBridge is a collaboration portal for four user roles:

- **Students** maintain their academic and skills profiles, explore relevant opportunities, apply, and follow outcomes.
- **Companies** publish opportunities, review candidates, and manage recruitment stages.
- **Colleges / placement cells** view student and department information, skill availability, industry demand, and recruitment analytics.
- **Admins** manage users, organization verifications, the skills taxonomy, and opportunity moderation.

The central matching concept compares skills listed by a student with skills required by an opportunity. Match and availability values represent **skill coverage or presence**, not verified proficiency.

## Frontend capabilities

The application includes public landing, login, and registration pages, and role-specific dashboard areas:

| Role | Main frontend areas |
| --- | --- |
| Student | Dashboard, profile, skills, opportunity browsing and details, recommendations, applications, skill gaps, internships, settings |
| Company | Dashboard, profile, opportunity management and creation, candidates and candidate profiles, applications, internships, settings |
| College | Dashboard, profile, student roster, skill statistics, industry demand, skill-gap analysis, recruitment analytics, settings |
| Admin | Dashboard, users, verifications, skills taxonomy, opportunity moderation |

Protected pages require a signed-in user and the appropriate role. Role authorization must also be enforced by the API; client-side route guards are not a security boundary.

## Technology stack

| Concern | Technology |
| --- | --- |
| UI | React 18, JavaScript (ES modules, JSX) |
| Build and development server | Vite 5 |
| Routing | React Router 6 |
| Server-state and caching | TanStack React Query 5 |
| HTTP | Axios |
| Styling | Tailwind CSS 3, PostCSS, Autoprefixer, global CSS |
| Icons | Lucide React |
| Static analysis | ESLint 9, TypeScript tooling for type checking |
| Backend integration | Spring Boot REST API, Java, Spring Security, JWT |
| Database (backend) | PostgreSQL |

The repository-level product description also lists shadcn/ui and Recharts in the intended project stack. The frontend package manifest currently includes React, Vite, Tailwind CSS, React Router, Axios, TanStack Query, and Lucide React; verify current implementation and installed dependencies before relying on any library not listed in `apps/web/package.json`.

## Architecture

The frontend is a single-page application (SPA):

1. `src/main.jsx` mounts the React application and global stylesheet.
2. `src/App.jsx` composes the providers (React Query, authentication, toast notifications, and browser routing) and declares public and role-protected routes.
3. Shared layouts and navigation provide common dashboard structure; pages are organized by role.
4. Feature API modules in `src/api` call the REST API through a shared Axios client. React Query is configured for server-state caching and retry behavior.
5. The client attaches the JWT from `sessionStorage` to API requests. A `401` response clears local session data and redirects to login.
6. In development, Vite proxies `/api/v1` requests to `http://localhost:8080`. In deployment, configure the API base URL or provide same-origin routing to the backend.

```text
Browser
  └── React SPA (Vite build)
      ├── React Router ── public pages and role-protected dashboards
      ├── AuthContext ── session state and role-aware navigation
      ├── TanStack Query ── server-state cache
      └── Axios API client ── /api/v1 ── Spring Boot REST API ── PostgreSQL
```

## End-to-end user flows

### Shared authentication flow

1. A user opens the landing page and chooses login or registration.
2. The frontend submits credentials or registration details to the authentication API.
3. On success, the JWT is saved in `sessionStorage`; the frontend retrieves the current user profile when available.
4. The user's role determines the dashboard route and navigation items.
5. Protected routes show a session-verification loading state, redirect unauthenticated users to login, and send users with the wrong role to the unauthorized page.
6. Logout clears local session data. Expired or invalid sessions are cleared after an API `401` response.

### Student journey

1. Complete or update the academic profile and add current skills.
2. Browse opportunities and open an opportunity's details.
3. Review the matching skill coverage and eligibility information where provided by the API.
4. Apply to a suitable opportunity.
5. Track application stages and, when selected, view internship or placement progress.
6. Use skill-gap and recommendation areas to explore relevant information.

### Company journey

1. Create or update the company profile.
2. Create and manage opportunity postings, including required skills and eligibility criteria.
3. Review applicants and candidate profiles.
4. Move applications through the recruitment pipeline and track confirmed outcomes.

### College journey

1. Review the institutional profile, students, and departments.
2. Explore student skill availability alongside industry skill demand.
3. Review skill-gap and recruitment analytics to identify areas of focus.

### Admin journey

1. Review platform activity and user accounts.
2. Process organization verification requests.
3. Maintain the skills taxonomy and moderate opportunities.

> The above describes the product journey and frontend route areas. Availability of a particular action depends on its API integration and backend configuration. The frontend also supports a mock API option for local/demo workflows.

## Prerequisites

- Git
- Node.js 18 or newer and npm (the frontend uses Vite 5)
- For live API-backed workflows: Java/Maven as required by the backend, and PostgreSQL

Check installed versions:

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

`npm ci` installs the exact dependency versions recorded in `package-lock.json`. Use `npm install` if you intentionally need to update dependencies and the lockfile.

### 3. Start the frontend

```bash
npm run dev
```

Open [http://localhost:5174](http://localhost:5174). The Vite development server listens on port `5174` and proxies requests under `/api/v1` to `http://localhost:8080`.

### 4. Start the backend for API-backed workflows

In a second terminal, from the repository root:

1. Create a PostgreSQL database named `skillbridge` (or configure the backend to use your database).
2. Configure the backend environment using [`apps/api/.env.example`](../api/.env.example) as a reference. Supply database URL, username, password, application port, JWT secret, token expiry, and upload directory through the mechanism supported by your local environment. Do not use the example JWT secret outside local development.
3. Start the API using the included Maven wrapper:

```bash
cd apps/api
./mvnw spring-boot:run
```

On Windows Command Prompt or PowerShell, use:

```powershell
cd apps/api
.\mvnw.cmd spring-boot:run
```

The frontend's development proxy expects the API on port `8080`. If you change the API port, update the proxy target in `apps/web/vite.config.ts` or configure a frontend API base URL as described below. Consult the backend documentation and application configuration for database migrations, seed data, and required environment variables.

### 5. Optional: use mock API mode

To run the frontend without a local API, create `apps/web/.env.local`:

```dotenv
VITE_USE_MOCK_API=true
```

Restart Vite after changing environment variables. Mock mode is intended for local demos and UI development; it does not replace backend integration or production services. Remove the setting or set it to `false` to use the real API.

## Configuration

Vite exposes frontend environment variables prefixed with `VITE_`. Create `apps/web/.env.local` for local overrides; do not commit secrets in frontend environment files because values bundled into a browser application are public.

| Variable | Default | Purpose |
| --- | --- | --- |
| `VITE_API_BASE_URL` | `/api/v1` | Base URL used by the API client. Leave as default for same-origin requests and the local Vite proxy. |
| `VITE_USE_MOCK_API` | `false` | Set to `true` to use the frontend mock data layer. |

Example for a separately hosted API:

```dotenv
VITE_API_BASE_URL=https://api.example.com/api/v1
VITE_USE_MOCK_API=false
```

The API host must allow requests from the deployed frontend origin (CORS), and production traffic should use HTTPS. Exact backend environment variables are documented in [`apps/api/.env.example`](../api/.env.example).

## Available scripts

Run these from `apps/web`:

| Command | Description |
| --- | --- |
| `npm run dev` | Start the Vite development server. |
| `npm run build` | Create the optimized production build in `dist/`. |
| `npm run preview` | Serve the generated build locally for verification. Run `npm run build` first. |
| `npm run lint` | Run ESLint. |
| `npm run typecheck` | Run the configured TypeScript check. |

There is currently no test script defined in `apps/web/package.json`.

## Project structure

```text
apps/web/
├── index.html                 # SPA HTML entry point
├── package.json               # Dependencies and npm scripts
├── vite.config.ts             # Vite config, alias, port, API proxy
├── tailwind.config.js         # Tailwind content and theme configuration
├── vercel.json                # SPA route rewrite for Vercel
└── src/
    ├── main.jsx               # React entry point
    ├── App.jsx                # Providers and route definitions
    ├── api/                   # API client, feature APIs, mock layer
    ├── components/            # Shared, UI, and navigation components
    ├── context/               # Authentication context
    ├── hooks/                 # Reusable React hooks
    ├── layouts/               # Shared dashboard layouts and nav config
    ├── pages/                 # Public and role-specific pages
    ├── routes/                # Protected route handling
    ├── styles/                # Global styles
    └── utils/                 # Auth helpers and shared constants
```

Use the `@/` import alias for modules under `src` (for example, `@/api`). Keep role-specific screens within the corresponding `src/pages/<role>` directory and shared UI in `src/components`.

## API integration

- API routes are versioned under `/api/v1`; the backend contract is maintained in [`docs/06-api/openapi.yaml`](../../docs/06-api/openapi.yaml).
- The shared Axios client sets JSON headers, uses a 15-second timeout, attaches the bearer token, and normalizes API errors.
- TanStack Query defaults are configured in `src/App.jsx` (including cache timing, retries, and no refetch on window focus).
- Authentication/session data is stored in browser `sessionStorage`, not long-lived `localStorage`.
- API role checks and resource ownership must always be enforced server-side, even when the frontend hides or protects a route.

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

Vite outputs static assets to `apps/web/dist`. Deploy that directory with a static hosting provider. Configure the hosting build root as `apps/web`, install with `npm ci`, and use `npm run build` as the build command. The repository includes a Vercel rewrite to serve `index.html` for SPA routes; configure equivalent history-fallback rewrites on other hosts.

Before deploying, set `VITE_API_BASE_URL` to the intended API endpoint if it is not same-origin, set `VITE_USE_MOCK_API=false`, and verify backend CORS, HTTPS, authentication, and environment configuration. Never put private credentials or server secrets in frontend variables.

## Troubleshooting

| Symptom | Things to check |
| --- | --- |
| `npm ci` fails | Confirm Node/npm versions and that the command is run in `apps/web`, where `package-lock.json` is located. |
| Browser cannot connect to API | Confirm the backend is listening at `localhost:8080`, the database is available, and Vite is running with the configured proxy. |
| API requests go to the wrong host | Check `VITE_API_BASE_URL` in `apps/web/.env.local`; restart Vite after changing it. |
| Login redirects back to login | Check API availability, credentials, token validity, and the browser console/network response. A `401` clears the stored session. |
| Direct navigation to a nested route returns 404 after deployment | Configure the host to rewrite application routes to `index.html`; Vercel rewrite configuration is provided in `vercel.json`. |
| Unexpected demo data appears | Check whether `VITE_USE_MOCK_API=true` is set and restart the development server after changing it. |

## Security and production notes

- Treat all `VITE_*` values and frontend-delivered content as publicly observable.
- Use HTTPS and a strong, unique backend JWT secret in deployed environments. Do not reuse the sample secret from `.env.example`.
- Session storage reduces persistence across browser sessions but does not eliminate XSS risk. Apply standard output-safety, dependency hygiene, and content security practices.
- Frontend role-based navigation improves usability only; the API is responsible for authentication, authorization, input validation, and data scoping.
- Avoid logging tokens, passwords, or sensitive profile data in browser logs or analytics.

## Contributing

1. Create a focused branch from the default branch.
2. Keep changes scoped to the frontend unless an API change is required.
3. Follow the existing `src` organization and reuse shared components and API modules.
4. Run `npm run lint`, `npm run typecheck`, and `npm run build` from `apps/web` before opening a pull request.
5. Include a clear summary, relevant screenshots for UI changes, and any configuration or API contract updates.

## Related documentation

- [Repository README](../../README.md)
- [Product requirements](../../docs/01-product/PRD.md)
- [Architecture](../../docs/04-architecture/architecture.md)
- [REST API design](../../docs/06-api/api-design.md)
- [OpenAPI contract](../../docs/06-api/openapi.yaml)
- [Backend environment example](../api/.env.example)

---

**License:** No license is currently specified in the repository. Contact the repository maintainers before redistributing or reusing this project.
