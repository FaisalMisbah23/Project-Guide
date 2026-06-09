# Chapter 14 - Newsletter and Cron

Newsletter signup sounds tiny until you treat an email address like trusted user data. You need validation, duplicate protection, server-side provider calls, unsubscribe-ready status, and a log of scheduled sends.

## The point of this chapter

Newsletter signup through an Edge Function, normalized unique subscribers, friendly duplicate behavior, `newsletter_runs`, and a dry-run-first scheduled digest plan using Supabase Cron and Brevo.

## Step 1 - Signup goes through the server

The browser should not call Brevo or write messy subscriber rows directly. Use an Edge Function to validate and normalize email.

## Step 2 - Let the database stop duplicates

The UI can try to prevent double submits. Only a unique normalized email constraint can protect against two requests arriving at nearly the same time.

## Step 3 - Store subscriber status

Use statuses such as active, unsubscribed, and bounced if supported. A newsletter table without status becomes painful the first time someone opts out.

## Step 4 - Dry run before real Cron

A scheduled job should first report who would receive the digest and what content it would include. Only after that should it send real email.

## Step 5 - Record every run

`newsletter_runs` is how you inspect success, failure, counts, and errors later.

## Step 5 - Write the signup response behavior

Duplicate signup behavior should be friendly and privacy-aware. Do not reveal too much, but do not show a scary database error.

```txt
new valid email       -> saved, success message
existing active email -> friendly already-subscribed style success
invalid email         -> validation message
provider unavailable  -> signup still stored if provider is only notification
```

For the first version, signup does not need to send a provider email unless you choose confirmation. It must store clean subscriber data.

## Step 6 - Plan the scheduled digest

A digest job needs a contract before Cron:

```txt
input: dryRun boolean
find: published articles/projects since last successful run
send: Brevo email to active subscribers
record: newsletter_runs status, counts, error
retry: safe because run records exist
```

Dry-run is mandatory before real sending.

## Step 7 - Do it on your project

Create:

```txt
newsletter signup Edge Function
newsletter_subscribers unique normalized email
newsletter_runs table usage
optional digest Edge Function
Cron schedule only after dry-run proof
admin view or log path for recent runs
```

## Prove it before moving on

Submit the same email twice quickly. Inspect the table. There should be one normalized subscriber row. Then run the digest in dry-run mode and confirm it reports recipients and content without sending.

> **📖 Mandatory read.** Read [Supabase Edge Functions](https://supabase.com/docs/guides/functions), [Supabase Cron](https://supabase.com/docs/guides/cron), [Supabase function secrets](https://supabase.com/docs/guides/functions/secrets), and [Brevo transactional email](https://developers.brevo.com/docs/send-a-transactional-email). Required: signup and scheduled sending both need server-side boundaries.

> **💡 Hint.** Submit the same email twice quickly. The database should end with one row, and the UI should still feel friendly.

## Definition of Done

- [ ] Newsletter signup uses an Edge Function.
- [ ] Email is validated and normalized server-side.
- [ ] Duplicate signups do not create duplicate rows.
- [ ] Subscriber status exists.
- [ ] `newsletter_runs` records scheduled send attempts or planned run output.
- [ ] Dry-run behavior exists before real sending.
- [ ] Brevo secrets remain server-side.

> **✍️ Log it (mandatory).** In `learning-log/14-newsletter-and-cron.md`: explain why duplicate prevention belongs in the database, not only in React.

All boxes ticked? Then continue. The next chapter builds on this gate, not around it.

---

Next: newsletter data is controlled; now add useful analytics without building a surveillance machine. -> **[Chapter 15 - Analytics and Realtime insights](15-analytics-realtime-insights.md)**
