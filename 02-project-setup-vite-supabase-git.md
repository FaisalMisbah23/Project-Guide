# Chapter 02 - Project setup with Vite, Supabase, and Git

Last chapter you chose the product: a full-stack portfolio, not a static resume page. Now make the repo real. Setup is not glamorous, but it is where production habits start. A messy setup leaks secrets, hides required commands, and makes every later chapter feel harder than it is.

## Where we're headed

By the end, a Vite React app runs locally, TailwindCSS and shadcn/ui are installed, Supabase client configuration is separated from secrets, `.env` is ignored, `.env.example` is committed, and Git has a clean baseline commit.

## The setup trap

The weak setup puts everything wherever it first fits:

```txt
API keys pasted into components
no .env.example
no folder plan
uncommitted setup changes for days
```

Problem: you cannot tell which values are safe for the browser, a teammate cannot reproduce your setup, and one accidental push can expose private credentials.

The professional setup separates public configuration from private secrets:

```txt
VITE_SUPABASE_URL=public project URL
VITE_SUPABASE_ANON_KEY=public anon key protected by RLS

BREVO_API_KEY=server-only, never in Vite
SUPABASE_SERVICE_ROLE_KEY=server-only, never in Vite
```

Supabase's anon key is allowed in the browser because RLS is the real guard. Brevo and service-role keys are not browser-safe and must live only in Supabase Edge Function secrets.

## Build it

Create the Vite app and install the frontend tools. Use React, TailwindCSS, and shadcn/ui because this course needs a polished public site and repeatable admin UI patterns.

Create a clean source layout:

```txt
src/
  components/
  features/
  lib/
  pages/
  routes/
  styles/
```

Add a Supabase client helper in `src/lib/`. It should read only Vite-safe variables. Do not put service-role keys, Brevo keys, or database passwords in frontend code.

Create:

```txt
.env
.env.example
.gitignore
learning-log/
```

`.env.example` should show the names of required variables without real values. `.gitignore` must ignore `.env`, build output, dependency folders, editor clutter, and local Supabase artifacts that should not be committed.

Commit the baseline once the app starts and builds. Small commits matter because this course will change database schema, policies, Edge Functions, and frontend code. You want rollback points.

## Do and don't

Do commit the first working baseline before adding features.

Don't store Brevo, service-role, or database credentials in any `VITE_` variable.

Do add a clear `.env.example`.

Don't assume a secret is safe because the repo is private.

## Mandatory read

Read the official Vite environment variables guide and Supabase's note on anon keys and RLS. Required: the rest of the course assumes you understand why some browser variables are acceptable and some secrets must stay server-side.

## Definition of Done

- [ ] Vite React app runs locally.
- [ ] TailwindCSS and shadcn/ui are installed.
- [ ] Supabase client helper exists and uses only `VITE_` variables.
- [ ] `.env` is ignored and `.env.example` is committed.
- [ ] `learning-log/` exists.
- [ ] The baseline setup is committed.

> **Log it.** In `learning-log/02-project-setup.md`, explain the difference between a public Vite env var and a server-only secret. Name one mistake that would leak credentials.

Next: the app runs, but it has no durable data. Build the database model that everything else depends on. -> **[Chapter 03 - Data model and migrations](03-data-model-and-migrations.md)**
