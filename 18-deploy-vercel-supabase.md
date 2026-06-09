# Chapter 18 - Deploy with Vercel and Supabase

Deployment is where local assumptions meet reality. A green Vercel build proves only that the frontend compiled. It does not prove RLS, Edge Function secrets, Storage policies, Brevo, Cron, or production routes work.

## The point of this chapter

A production deployment where Vercel hosts the Vite frontend, Supabase hosts backend pieces, secrets live in the right platform, and a production smoke test proves critical workflows.

## Before you touch code

- Local build passes.
- Supabase migrations and functions are ready.
- You know all env vars and where they belong.
- You have a smoke-test checklist written before deployment.

## Vocabulary for this chapter

- **Build.** Compile and package frontend assets.
- **Preview deployment.** A non-production deployment used for review.
- **Function secret.** Server-side env value available to Edge Functions.
- **Smoke test.** Small set of critical checks after deployment.
- **SPA fallback.** Rule that sends direct route refreshes back to React.

## Guided snippet or contract

This is a shape to aim for, not a finished solution to paste blindly:

```txt
Deployment contract
  Vercel: frontend build + browser-safe VITE_ variables
  Supabase: database, RLS, storage, Edge Functions, secrets, Realtime/Cron
  Brevo: provider account and transactional email key stored server-side
  CI: install, test if configured, build
  Smoke test: prove critical workflows in production
```

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

## If it breaks

| Symptom | Likely cause | Smallest next test |
|---|---|---|
| Homepage works but contact fails | Edge Function not deployed or secrets missing | Open function logs and verify Supabase secrets. |
| Admin write fails in production | Owner id/RLS mismatch | Check `owner_profile` in production before using service-role. |
| Direct route refresh 404s | SPA fallback missing | Configure Vercel rewrite/fallback. |
| Secret appears in bundle | Private value was put in frontend env | Remove, rotate, redeploy, and inspect bundle again. |

## What you should be able to explain

- Why Vercel gets only browser-safe values.
- Why Supabase secrets hold Brevo/service-role values.
- Why production smoke tests include blocked RLS cases.
- What you do first when production differs from local.

## The slower beginner path

If this chapter feels too large, split the deployment workflow into one sitting per checkpoint. The goal is not to finish fast; the goal is to finish with proof.

### Sitting 1 - Read and translate

- Read the mandatory docs with this chapter open beside you.
- Write five plain-language notes in the learning log.
- Circle any word you cannot define yet.
- Rewrite the point of the chapter in your own words.
- Stop before coding if you cannot explain what you are about to change.

### Sitting 2 - Create the smallest artifact

- Create only the first file, table, route, policy, function, checklist, or note this chapter requires.
- Add placeholder content or a tiny shape before trying to make it complete.
- Run the smallest possible check.
- If it fails, debug that one artifact before adding the next one.

### Sitting 3 - Connect the artifact

- Connect the artifact to the previous chapter's work.
- Keep the connection narrow: one query, one route, one form submit, one policy, or one checklist item.
- Add a visible loading, empty, blocked, or failure state if this chapter touches UI or data.
- Write down what changed in the request flow.

### Sitting 4 - Break it safely

- Try the shortcut this chapter warned you about in a harmless way.
- Try the most likely beginner mistake from the troubleshooting table.
- Confirm the app fails safely, or fix it until it does.
- Record the before/after in the learning log.

## Checkpoints during the work

Use this mini-review after each sitting:

```txt
What did I create or change?
What command, route, query, or click proves it exists?
What private data or failure case did I protect?
What is the next smallest test?
```

If you cannot answer the second question, you do not have proof yet. If you cannot answer the third question, you may have built only the happy path.

## Suggested commit rhythm

Make small commits when code changes. A good commit for this chapter should complete one idea, not the whole universe:

```txt
setup: add safe Supabase client shape
schema: add project and article tables
security: add public published-project policy
ui: add project loading and empty states
admin: add project archive action
ops: add production smoke-test checklist
```

Use the style that fits your repo, but keep the habit: one clear change, one clear reason, one checkpoint you can return to.

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
