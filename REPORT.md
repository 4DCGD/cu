## CuraFinder – Architecture and Build Report

### 1) Overview

**CuraFinder** is a full‑stack web application that helps users discover and review medical clinics. It consists of:

- **Frontend**: React + TypeScript (CRA), Material UI, React Router, i18next.
- **Backend**: Node.js (Express), PostgreSQL via `pg`, JWT auth, security middleware.

The project is organized as a simple two‑app workspace (frontend root + backend subfolder).

Directory layout (relevant parts):

```
Curafinder-feature-auth (1)/Curafinder-feature-auth/
  package.json              # React app (frontend)
  src/                      # React source code
  public/                   # CRA public assets
  backend/                  # Express API (backend)
    package.json
    src/
      app.js               # Express entrypoint
      routes/              # API routes: auth, users, clinics, reviews, stats
      middleware/
      config/
    setup-database.sql     # Initial DB setup
```

---

### 2) Tech Stack

- **Frontend**

  - React 18, TypeScript
  - Material UI (MUI) components and icons
  - React Router v6
  - i18next + react‑i18next for internationalization (English, French)
  - Axios for API calls
  - CRA build tooling (`react-scripts`)

- **Backend**
  - Express 4, `cors`, `helmet`, `morgan`
  - `jsonwebtoken` for JWT auth, `bcryptjs` for password hashing
  - `pg` for PostgreSQL access
  - `dotenv` for environment config
  - `nodemon` for development

---

### 3) Frontend Architecture

- Entry: `src/index.tsx` → `src/App.tsx`.
- Routing: React Router for pages under `src/pages/` (e.g., `HomePage`, `SearchPage`, `LoginPage`, `RegisterPage`, `AdminDashboard`, etc.).
- UI: MUI theming via `src/theme.ts`, shared layout components in `src/layouts/` (`MainLayout`, `UserLayout`, `AdminLayout`).
- State/Context:
  - `contexts/AuthContext.tsx`: authentication state and helper actions.
  - `contexts/LanguageContext.tsx`: i18n language switching.
  - `contexts/ThemeContext.tsx`: light/dark theme toggling.
- Services: `src/services/` contains API clients (`authService.ts`, `adminService.ts`, etc.) and utilities (`googleReviewsService.ts`, `reviewTransformerService.ts`).
- i18n: `src/i18n.ts` bootstraps translations with namespaced JSON files in `src/locales/en/` and `src/locales/fr/`.

Key frontend responsibilities:

- Render public pages (Home, Search, Clinic Reviews) and authenticated areas (User, Admin).
- Handle login/registration flows, store tokens in context/storage, and attach auth headers via Axios where needed.
- Provide multilingual UI and adaptive theme.

---

### 4) Backend Architecture

- Entry: `backend/src/app.js`.
- Ports: defaults to `PORT=3001` (overridable via env).
- Middleware: `helmet`, `cors` (whitelist includes `http://localhost:3000`), `morgan`, `express.json()`.
- Routing: mounted under `/api` via `backend/src/routes/index.js`, composing feature routers:
  - `auth.js` – registration, login, token issuance.
  - `users.js` – user profiles/management (protected).
  - `clinics.js` – clinic search/listing/details.
  - `reviews.js` – clinic reviews CRUD (protected for write).
  - `stats.js` – aggregate metrics for admin dashboards.
- Auth: `middleware/auth.js` verifies JWTs for protected routes.
- Database: PostgreSQL via `pg`. Connection handled in `config/database.js`; schema/bootstrap hints in `setup-database.sql`.

Key backend responsibilities:

- Authenticate users and protect sensitive endpoints via JWT.
- Expose CRUD APIs for clinics, reviews, and admin stats.
- Apply security headers and CORS policy for the frontend origin(s).

---

### 5) Data Flow (High Level)

1. A user interacts with the React UI → triggers an Axios request to the API.
2. API routes in Express validate auth (if required), process input, query PostgreSQL, and return JSON.
3. The frontend normalizes and displays data; on auth actions it stores tokens and updates `AuthContext`.

---

### 6) Environment Configuration

Backend reads from `.env` (via `dotenv`). Typical variables:

- `PORT=3001`
- `DATABASE_URL` or individual PG vars (`PGHOST`, `PGPORT`, `PGDATABASE`, `PGUSER`, `PGPASSWORD`)
- `JWT_SECRET`
- `CORS_ORIGIN=http://localhost:3000`

Frontend (CRA) runtime config is usually static; if needed, use `REACT_APP_*` env vars at build time.

---

### 7) Local Development

Install dependencies:

```bash
# Frontend
cd "Curafinder-feature-auth (1)/Curafinder-feature-auth"
npm install

# Backend
cd backend
npm install
```

Run dev servers (two terminals):

```bash
# Terminal 1 – Frontend
cd "Curafinder-feature-auth (1)/Curafinder-feature-auth"
npm start   # http://localhost:3000

# Terminal 2 – Backend
cd "Curafinder-feature-auth (1)/Curafinder-feature-auth/backend"
npm run dev # or npm start → http://localhost:3001
```

---

### 8) Build & Production

Create a production build of the React app:

```bash
cd "Curafinder-feature-auth (1)/Curafinder-feature-auth"
npm run build
```

This outputs an optimized `build/` directory suitable for static hosting or reverse‑proxying behind the API.

Backend is a standard Node.js service. For production:

- Provide environment variables (.env or platform settings).
- Use a process manager (PM2/systemd) or container.
- Ensure HTTPS termination and correct CORS.

---

### 9) Security Practices

- `helmet` for HTTP headers; `cors` with explicit allowed origins.
- Passwords hashed with `bcryptjs`.
- JWT with strong `JWT_SECRET`; short‑lived access tokens recommended.
- Input validation on API routes (consider `zod`/`joi` for stricter contracts).

---

### 10) Testing & Quality

- CRA test setup (`@testing-library/*`) for UI unit/integration tests.
- Add backend tests with `jest`/`supertest` (recommended).
- ESLint configured via CRA defaults.

---

### 11) Notable Design Decisions

- Separation of concerns: UI/UX in React, API logic in Express.
- Context‑based state for auth/theme/language to avoid heavy global stores.
- i18n wired early with English/French to support multilingual growth.
- Service layer (`services/`) centralizes API access and transformations.

---

### 12) Future Enhancements

- CI/CD pipeline for builds, tests, and deployments.
- Infrastructure as code for DB and app environments.
- Role‑based authorization and audit logging.
- Caching for heavy endpoints; pagination for large lists.
- Error tracking (Sentry) and performance monitoring (Web Vitals backend).

---

### 13) Quick Start (TL;DR)

```bash
# Frontend
cd "Curafinder-feature-auth (1)/Curafinder-feature-auth"
npm install && npm start

# Backend
cd "Curafinder-feature-auth (1)/Curafinder-feature-auth/backend"
npm install && npm start
```

Production build:

```bash
cd "Curafinder-feature-auth (1)/Curafinder-feature-auth"
npm run build
```

This report summarizes how the app is structured, how it runs, and how to build and operate it locally and in production.
