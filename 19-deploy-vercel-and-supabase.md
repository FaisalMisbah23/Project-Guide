# Chapter 19 - Deploy to Vercel and Supabase

The project is not finished until someone else can open it and the backend still works.

> **Principle.** Deployment tests whether your assumptions survive outside your machine.

## Where we're headed

By the end, the React app is deployed to Vercel, Supabase tables/policies/functions are deployed, secrets are set, and the production contact flow works with Brevo.

## Before you build

> **Mandatory read.** Read Vercel docs: https://vercel.com/docs. Focus on project deployment and environment variables.

> **Mandatory read.** Revisit Supabase function secrets: https://supabase.com/docs/guides/functions/secrets.

> **Apply this habit.** Read "Monitor Production" in [Daily_Software_Development_Guidelines.md](../Daily_Software_Development_Guidelines.md), then list every production variable.

## Step 1 - Run local production build

Run:

```bash
npm run build
npm run preview
```

Fix build errors before deployment.

## Step 2 - Deploy Supabase database changes

Confirm migrations, RLS policies, Storage buckets, and Edge Functions exist in the Supabase project you will use for production.

## Step 3 - Set Supabase secrets

Production secrets:

```txt
BREVO_API_KEY
CONTACT_TO_EMAIL
CONTACT_FROM_EMAIL
```

Frontend env values in Vercel:

```txt
VITE_SUPABASE_URL
VITE_SUPABASE_ANON_KEY
```

Do not add service role or Brevo keys to Vercel frontend variables.

## Step 4 - Deploy to Vercel

Deploy the Vite app to Vercel.

Build command:

```txt
npm run build
```

Output directory:

```txt
dist
```

## Step 5 - Test production

Test:

- public pages;
- project detail refresh;
- article detail refresh;
- admin login;
- project/article CRUD;
- image upload;
- contact submit;
- Brevo notification;
- contact inbox.

## What your screen should show

The live URL behaves like the local app. Contact stores a message and sends a Brevo notification.

## Small challenge

Send yourself the deployed URL and open it on mobile.

Suggested commit:

```bash
git commit -m "chore: deploy full-stack portfolio"
```

## Definition of Done

- [ ] `npm run build` passes.
- [ ] Vercel deployment works.
- [ ] Supabase database and policies are production-ready.
- [ ] Edge Function is deployed.
- [ ] Brevo secret is set in Supabase.
- [ ] Contact form works in production.
- [ ] Admin login works in production.
- [ ] No secret keys are exposed in the frontend.

> **Log it.** In `learning-log/19-deploy-vercel-and-supabase.md`: Which production issue did you find? Which environment variable would be most dangerous to expose?

Next: finish like an engineer. -> **[Chapter 20 - Final review and maintenance](20-final-review-and-maintenance.md)**
