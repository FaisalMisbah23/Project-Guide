# Chapter 14 - Newsletter And Cron

A newsletter signup lets visitors ask for updates. Cron lets scheduled work happen later. For a beginner portfolio, build the signup carefully and plan scheduled sending before making it complex.

## Goal

By the end, visitors can subscribe safely, duplicate emails are controlled, and the owner has a clear newsletter/Cron plan.

## What You Will Build

- Newsletter signup form.
- Server-side signup handler or safe insert path.
- Duplicate email protection.
- Admin subscriber view.
- Newsletter run log or plan.
- Cron schedule plan.

## Beginner Concepts

- **Subscriber:** a visitor who asked for updates.
- **Duplicate:** same email submitted more than once.
- **Cron:** scheduled work triggered by time.
- **Run log:** record that a scheduled task happened.
- **Privacy-aware response:** message that does not reveal too much about someone else's email.

## Step By Step

### Step 1 - Add Public Signup UI

Add a small signup form, usually near the footer or articles page:

```txt
email input
submit button
success message
error message
```

### Step 2 - Protect Against Duplicates

The database should enforce unique subscriber emails. React can warn, but the database must prevent duplicates.

### Step 3 - Decide The Signup Path

Use one of these safe paths:

```txt
Edge Function validates and inserts subscriber
or
public insert policy allows only safe subscriber fields
```

Do not let visitors set admin-only fields.

### Step 4 - Build Admin Subscriber View

In `/admin/newsletter`, show:

```txt
subscriber email
status
created_at
unsubscribe or archive action, if supported
```

### Step 5 - Add Newsletter Run Planning

Create or document `newsletter_runs` rows:

```txt
subject
status
started_at
finished_at
error
```

This gives scheduled sending a history.

### Step 6 - Plan Cron Carefully

For v1, document the schedule and smoke test. If implementing Cron now, keep it narrow:

```txt
Cron triggers function
function selects eligible content/subscribers
function records run
function handles failures
```

## Common Mistakes

| Mistake | Why it hurts | Fix |
|---|---|---|
| Duplicate prevention only in React | Double submits can still happen | Add unique database rule |
| Revealing subscriber existence | Privacy issue | Use a neutral success response |
| Cron without logs | Hard to debug | Create run records |
| Letting public set status fields | Users can alter workflow | Validate server-side or restrict policy |

## Checks Before Moving On

- Signup form works.
- Duplicate email ends with one subscriber row.
- Admin can view subscribers.
- Public users cannot read subscriber list.
- Cron/send plan is documented or implemented with logs.

## Learning Log

In `learning-log/14-newsletter-and-cron.md`, answer:

```txt
Why does duplicate protection belong in the database?
What should a visitor see after signing up?
Why should scheduled work create logs?
What parts are implemented now and what parts are planned?
```

## Definition Of Done

- [ ] Newsletter signup exists.
- [ ] Duplicate emails are controlled.
- [ ] Subscriber data is private.
- [ ] Admin subscriber view exists.
- [ ] Newsletter run log or plan exists.
- [ ] Cron behavior is documented or implemented safely.

Next: add analytics. -> **[Chapter 15 - Analytics And Realtime Insights](15-analytics-realtime-insights.md)**
