# Chapter 18 - Deploy with Vercel and Supabase

Deployment is where local assumptions meet reality. A green Vercel build proves only that the frontend compiled. It does not prove RLS, Edge Function secrets, Storage policies, Brevo, Cron, or production routes work.

## The point of this chapter

A production deployment where Vercel hosts the Vite frontend, Supabase hosts backend pieces, secrets live in the right platform, and a production smoke test proves critical workflows.

## Step 1 - Build locally first

Run the production build before deploying. If it fails locally, it will not magically become clearer in Vercel logs.

## Step 2 - Add a small CI gate

A basic GitHub Actions workflow should install dependencies, run tests if configured, and build. CI catches mistakes before deployment.

## Step 3 - Deploy Supabase pieces

Deploy migrations, storage buckets/policies, Edge Functions, and scheduled jobs or planned Cron pieces. Set Supabase function secrets there.

## Step 4 - Keep env boundaries strict

Vercel gets browser-safe values: `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY`. Supabase Edge Functions get server secrets such as Brevo keys. Service-role belongs only in controlled server-side code when truly required, because it bypasses RLS.

## Step 5 - Smoke test production

Test public pages, admin login, CRUD, image upload, contact, Brevo, inbox, newsletter, analytics, direct route refresh, and RLS blocked cases on the production URL.

## Step 6 - Write the deployment matrix

Before deploying, write the ownership of every production thing:

| Item | Lives in | Browser-visible? |
|---|---|---:|
| `VITE_SUPABASE_URL` | Vercel | yes |
| `VITE_SUPABASE_ANON_KEY` | Vercel | yes, limited by RLS |
| `BREVO_API_KEY` | Supabase function secret | no |
| service-role key, if needed | Supabase function secret only | no |
| migrations | Supabase database | no |
| Edge Functions | Supabase | called by browser, code runs server-side |

If you cannot place a value in this matrix, do not deploy it yet.

## Step 7 - Build the production smoke test

Create a checklist you can run on the production URL:

```txt
home/about routes load
projects/articles show published only
admin login works
project create/edit/publish/archive works
article preview/publish works
image upload works
contact stores message and sends/records notification
inbox shows message
newsletter signup handles duplicate
analytics counts public route only
RLS blocked cases still block
```

## Step 8 - Do it on your project

Deploy in this order:

1. Local production build.
2. CI build check.
3. Supabase migrations.
4. Storage buckets and policies.
5. Edge Functions.
6. Supabase secrets.
7. Vercel env vars.
8. Vercel deployment.
9. Production smoke test.

## Prove it before moving on

Open browser devtools on production and inspect shipped config. You should see public Vite values, not Brevo keys, service-role keys, database passwords, or private tokens. Then run the blocked RLS tests against production data.

> **📖 Mandatory read.** Read [Vercel Vite deployment](https://vercel.com/docs/frameworks/vite), [Vercel environment variables](https://vercel.com/docs/environment-variables), [Supabase CLI](https://supabase.com/docs/guides/cli), [Supabase Edge Functions](https://supabase.com/docs/guides/functions), [Supabase function secrets](https://supabase.com/docs/guides/functions/secrets), and [GitHub Actions quickstart](https://docs.github.com/en/actions/writing-workflows/quickstart). Required: deployment is frontend, backend, secrets, and checks together.

> **💡 Hint.** If an admin write fails in production, inspect RLS and owner identity before reaching for service-role. Service-role is power, not a bandage.

## Definition of Done

- [ ] Production frontend is deployed.
- [ ] Supabase migrations are deployed.
- [ ] Storage buckets and policies are deployed.
- [ ] Edge Functions and secrets are deployed.
- [ ] Vercel contains only browser-safe Vite variables.
- [ ] Brevo keys and service-role keys are not in frontend variables or shipped assets.
- [ ] Production smoke test covers public, admin, contact, newsletter, analytics, and RLS blocked cases.
- [ ] Direct route refresh works.

> **✍️ Log it (mandatory).** In `learning-log/18-deploy-vercel-supabase.md`: list which values live in Vercel, which live in Supabase secrets, and why service-role is dangerous.

All boxes ticked? Then continue. The next chapter builds on this gate, not around it.

---

Next: the app is deployed; now prove you understand it and can keep it alive. -> **[Chapter 19 - Final review and maintenance](19-final-review-maintenance.md)**
