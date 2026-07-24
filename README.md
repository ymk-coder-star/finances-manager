# Acme Financial Dashboard

A full-stack financial dashboard built with the [Next.js App Router](https://nextjs.org/docs/app). It demonstrates data fetching, streaming UI, server actions, form validation, and authentication — based on the [Next.js Learn Dashboard App](https://nextjs.org/learn/dashboard-app) course.

Live demo: [finances-manager-six.vercel.app](https://finances-manager-six.vercel.app/)

## Features

- **Dashboard overview** — revenue chart, latest invoices, and summary cards (collected, pending, invoices, customers)
- **Invoices** — search, pagination, create, edit, and delete
- **Customers** — searchable customer table with invoice totals
- **Authentication** — credentials-based login with NextAuth.js; `/dashboard` routes are protected
- **Streaming & loading states** — Suspense boundaries and skeleton UI for a responsive feel
- **Server Actions** — mutations and form handling with Zod validation

## Tech stack

| Technology | Role |
| --- | --- |
| [Next.js](https://nextjs.org/) (App Router) | Framework |
| [React](https://react.dev/) | UI |
| [TypeScript](https://www.typescriptlang.org/) | Typing |
| [Tailwind CSS](https://tailwindcss.com/) | Styling |
| [PostgreSQL](https://www.postgresql.org/) (`postgres` client) | Database |
| [NextAuth.js v5](https://authjs.dev/) | Auth |
| [Zod](https://zod.dev/) | Validation |
| [bcrypt](https://www.npmjs.com/package/bcrypt) | Password hashing |
| [Heroicons](https://heroicons.com/) | Icons |

Package manager: **pnpm**

## Prerequisites

- Node.js 18+ (recommended: current LTS)
- [pnpm](https://pnpm.io/)
- A PostgreSQL database (e.g. [Vercel Postgres](https://vercel.com/docs/storage/vercel-postgres), Neon, Supabase, or local Postgres)

## Getting started

### 1. Clone and install

```bash
git clone <repository-url>
cd financial-dashboard
pnpm install
```

### 2. Environment variables

Create a `.env` (or `.env.local`) file in the project root:

```env
# PostgreSQL connection string (SSL required by the app)
POSTGRES_URL=postgres://USER:PASSWORD@HOST:PORT/DATABASE

# Secret used by NextAuth to sign sessions (generate a random string)
AUTH_SECRET=your-random-secret
```

Generate an `AUTH_SECRET` with:

```bash
npx auth secret
# or
openssl rand -base64 32
```

### 3. Database

The app expects Postgres tables for users, customers, invoices, and revenue (as used in the Next.js Learn course). Seed data — including the demo login user — lives in `app/lib/placeholder-data.ts`.

Ensure your database is migrated and seeded before logging in. If you followed the course, that is typically done via a seed route or script against `POSTGRES_URL`.

### 4. Run the app

```bash
# Development (Turbopack)
pnpm dev

# Production build
pnpm build
pnpm start

# Lint
pnpm lint
```

Open [http://localhost:3000](http://localhost:3000).

## Logging in (protected routes)

Routes under `/dashboard` require authentication. Unauthenticated users are redirected to `/login`.

Use these demo credentials:

| Field | Value |
| --- | --- |
| **Email** | `user@nextmail.com` |
| **Password** | `123456` |

Steps:

1. Go to [http://localhost:3000/login](http://localhost:3000/login) (or click **Log in** on the home page).
2. Enter the email and password above.
3. After a successful sign-in you are redirected to `/dashboard`.

You can then access:

- `/dashboard` — overview
- `/dashboard/invoices` — invoice management
- `/dashboard/customers` — customers list

Sign out from the sidebar when finished.

## Project structure

```
app/
  dashboard/          # Protected dashboard pages (overview, invoices, customers)
  login/              # Login page
  lib/                # Data fetching, server actions, types, placeholder data
  ui/                 # Shared UI components (forms, tables, charts, skeletons)
auth.ts               # NextAuth configuration + credentials provider
auth.config.ts        # Auth pages & authorized callback
proxy.ts              # Auth middleware matcher (protects non-public routes)
```

## Scripts

| Command | Description |
| --- | --- |
| `pnpm dev` | Start the development server with Turbopack |
| `pnpm build` | Create a production build |
| `pnpm start` | Run the production server |
| `pnpm lint` | Run ESLint |

## Learn more

- [Next.js Learn — Dashboard App](https://nextjs.org/learn/dashboard-app)
- [Next.js Documentation](https://nextjs.org/docs)
- [Auth.js / NextAuth](https://authjs.dev/)
