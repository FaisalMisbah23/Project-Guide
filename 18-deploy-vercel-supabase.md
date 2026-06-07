# Chapter 18 - Deploy with Vercel and Supabase

Local success is not shipping. Deployment is where environment variables, migrations, storage policies, Edge Functions, and frontend builds meet reality.

## Where we're headed

By the end, the frontend is deployed to Vercel, Supabase backend pieces are deployed, secrets are set in the right places, and the production app works end to end.

## The deployment trap

Bad:

```txt
works locally
push to Vercel
hope Supabase functions and secrets are fine
```

Problem: frontend deployment does not automatically prove database policies, Edge Functions, Storage, Cron, or Brevo secrets are correct.

Better:

```txt
run production build
deploy Supabase migrations/functions
set Supabase secrets
set Vercel public env vars
test every workflow on production
```

## Environment boundary

Vercel should receive:

```txt
VITE_SUPABASE_URL
VITE_SUPABASE_ANON_KEY
```

Supabase Edge Function secrets should receive:

```txt
BREVO_API_KEY
BREVO_SENDER_EMAIL
CONTACT_RECIPIENT_EMAIL
SUPABASE_SERVICE_ROLE_KEY if required server-side
```

Never put Brevo or service-role secrets in Vercel frontend variables.

## Build it

Run a production build locally first. Fix build errors before deployment.

Deploy Supabase migrations, storage buckets/policies, and Edge Functions. Set secrets. Then deploy the Vite app to Vercel.

Test production:

```txt
public pages
project/article reads
admin login
project CRUD
article CRUD
image upload
contact form
Brevo notification
contact inbox
newsletter signup
visit tracking
RLS blocked cases
```

## Definition of Done

- [ ] Vercel deployment succeeds.
- [ ] Supabase migrations are applied.
- [ ] Edge Functions are deployed.
- [ ] Supabase secrets are set.
- [ ] Vercel env vars contain only browser-safe values.
- [ ] Contact form stores messages and triggers Brevo.
- [ ] Admin workflows work in production.
- [ ] RLS blocked cases still block in production.

> **Log it.** In `learning-log/18-deploy-vercel-supabase.md`, explain which secrets live in Vercel and which live in Supabase, and why.

Next: the app is deployed. Now prove you understand it and plan how to keep it alive. -> **[Chapter 19 - Final review and maintenance](19-final-review-maintenance.md)**
