# Chapter 18 - Deploy With Vercel And Supabase

Deployment is where local assumptions meet production. A green Vercel build is not enough. You must also deploy backend pieces, set secrets correctly, and run smoke tests.

## Goal

By the end, the portfolio is deployed with Vercel and Supabase, using correct environment variables and production checks.

## What You Will Build

- Vercel deployment.
- Supabase production setup.
- Environment variable checklist.
- Edge Function deployment.
- Production smoke test.
- Direct route refresh support.

## Beginner Concepts

- **Deployment:** putting the app online.
- **Build:** optimized production files.
- **Environment variable:** config value in local or production.
- **Secret:** private value stored only in trusted platforms.
- **Smoke test:** small set of checks proving critical workflows.
- **SPA fallback:** deployment rule that lets direct route refresh work.

## Step By Step

### Step 1 - Build Locally First

Run:

```bash
npm run build
npm run preview
```

Fix local build errors before deploying.

### Step 2 - Prepare Supabase

Confirm:

```txt
migrations are applied
RLS policies exist
storage bucket exists
Edge Functions are ready
function secrets are configured
owner account exists
seed or production content exists
```

### Step 3 - Configure Vercel

Connect the repository to Vercel. Add only browser-safe variables:

```txt
VITE_SUPABASE_URL
VITE_SUPABASE_ANON_KEY
```

Do not add Brevo keys, service-role keys, or database passwords to frontend variables.

### Step 4 - Deploy Edge Functions

Deploy Supabase Edge Functions used by:

```txt
contact form
newsletter signup or sends, if implemented
Cron tasks, if implemented
```

Store private secrets in Supabase function secrets.

### Step 5 - Handle Direct Route Refresh

Test direct refresh on:

```txt
/projects
/projects/example
/articles
/contact
/admin/login
```

If refresh fails, configure the Vercel rewrite/fallback for a Vite SPA.

### Step 6 - Run Production Smoke Tests

Check:

```txt
homepage loads
projects load
draft project is hidden
article page loads
contact message saves
Brevo failure does not lose message
admin login works
project edit works
image upload works
inbox shows message
analytics records public page
admin pages are protected
```

### Step 7 - Inspect Secrets

Open browser devtools on production. You may see public Vite values. You must not see Brevo keys, service-role keys, database passwords, or private tokens.

## Common Mistakes

| Mistake | Why it hurts | Fix |
|---|---|---|
| Only deploying frontend | Contact/functions fail | Deploy Supabase backend pieces |
| Putting private keys in Vercel frontend env | Secrets leak to browser | Store server secrets in Supabase |
| Not testing direct routes | Shared links break | Add SPA fallback |
| Skipping production RLS tests | Local privacy may not match prod | Retest drafts and messages |

## Checks Before Moving On

- Production URL loads.
- Supabase backend pieces are deployed.
- Function secrets are set.
- Direct refresh works.
- Smoke tests pass.
- No private secrets are visible in browser code.

## Learning Log

In `learning-log/18-deploy-vercel-supabase.md`, answer:

```txt
What lives on Vercel?
What lives on Supabase?
Which env vars are browser-safe?
Which secrets must stay server-side?
What production smoke test failed first?
```

## Definition Of Done

- [ ] Vercel deployment works.
- [ ] Supabase migrations/policies/storage/functions are ready.
- [ ] Browser-safe env vars are configured.
- [ ] Server-only secrets stay server-side.
- [ ] Direct route refresh works.
- [ ] Production smoke tests pass.

Next: review and prepare for maintenance. -> **[Chapter 19 - Final Review And Maintenance](19-final-review-maintenance.md)**
