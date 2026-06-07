# Chapter 3 - Supabase project and environment

The frontend exists. Now it needs a backend home: a Supabase project with a database, Auth, Storage, Edge Functions, and environment values that are separated by trust level.

> **Principle.** Environment setup is part of application design, not clerical work.

## Where we're headed

By the end, you have a Supabase project, frontend environment variables, local CLI awareness, and a clear line between browser-safe values and server-only secrets.

## Before you build

> **Mandatory read.** Read Supabase project docs from the official docs index: https://supabase.com/docs. Focus on what Supabase provides: database, auth, storage, and functions.

> **Apply this habit.** Read "Understand Before Coding" in [Daily_Software_Development_Guidelines.md](../Daily_Software_Development_Guidelines.md), then list each service you are about to use.

## Step 1 - Create the Supabase project

Create a Supabase project for the portfolio. Choose a project name that matches the portfolio, and save the project URL and anon key.

Do not use the service role key in the frontend. The browser gets the anon key; RLS decides what that key can do.

```txt
Frontend-safe:
VITE_SUPABASE_URL
VITE_SUPABASE_ANON_KEY

Server-only:
SUPABASE_SERVICE_ROLE_KEY
BREVO_API_KEY
CONTACT_TO_EMAIL
CONTACT_FROM_EMAIL
```

## Step 2 - Create the Supabase client

Create:

```txt
src/lib/
  supabaseClient.js
```

The file should initialize the Supabase JavaScript client using `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY`.

Do not scatter `import.meta.env` across the app. One client file makes configuration easier to inspect.

## Step 3 - Install needed packages

Install the Supabase client:

```bash
npm install @supabase/supabase-js
```

Later chapters may add form helpers or UI libraries only if they solve a real problem. Start small.

## Step 4 - Decide local versus hosted workflow

For this course, use the hosted Supabase dashboard for the beginner path, and use SQL migrations in the Supabase SQL editor or CLI as the source of truth.

If you use the CLI locally, keep generated local artifacts out of unrelated commits and document the commands you used.

## Step 5 - Verify the connection path

Before creating tables, add a tiny connection note to the learning log:

```txt
Supabase URL:
Anon key location:
Service role key location:
Where RLS policies will live:
Where Brevo key will live:
```

## What your screen should show

The app still runs. Supabase is ready, the client file exists, and env values are documented without secrets being committed.

## Small challenge

Write a short comment in `.env.example` explaining that `VITE_` values are browser-visible.

Suggested commit:

```bash
git commit -m "chore: connect supabase environment"
```

## Definition of Done

- [ ] Supabase project exists.
- [ ] `@supabase/supabase-js` is installed.
- [ ] `src/lib/supabaseClient.js` exists.
- [ ] `.env.example` includes only frontend-safe variable names.
- [ ] No service role or Brevo key is in the frontend.
- [ ] You can explain anon key plus RLS in one sentence.

> **Log it.** In `learning-log/03-supabase-project-and-environment.md`: What is safe to expose to the browser? What must stay server-side? Why does RLS matter if the anon key is public?

Next: design the database. -> **[Chapter 4 - Data model and migrations](04-data-model-and-migrations.md)**
