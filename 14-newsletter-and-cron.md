# Chapter 14 - Newsletter and Cron

Newsletter signup sounds tiny until you treat an email address like trusted user data. You need validation, duplicate protection, server-side provider calls, unsubscribe-ready status, and a log of scheduled sends.

## The point of this chapter

Newsletter signup through an Edge Function, normalized unique subscribers, friendly duplicate behavior, `newsletter_runs`, and a dry-run-first scheduled digest plan using Supabase Cron and Brevo.

## Before you touch code

- Newsletter table exists.
- Edge Function pattern from Chapter 12 is understood.
- Brevo secrets are server-side only.
- You know whether Cron is implemented now or planned as advanced.

## Vocabulary for this chapter

- **Normalize.** Convert email into a consistent stored form.
- **Unique constraint.** Database rule preventing duplicate subscriber rows.
- **Cron.** Scheduled work triggered by time.
- **Dry run.** Report what would happen without sending.
- **Run log.** Stored record of a scheduled job attempt.

## Guided snippet or contract

This is a shape to aim for, not a finished solution to paste blindly:

```txt
Newsletter contract
  signup: validate -> normalize -> insert or friendly duplicate
  subscriber status: active/unsubscribed/bounced if supported
  digest dry run: find recipients and content, send nothing
  real run: send via Brevo, record newsletter_runs
```

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

## If it breaks

| Symptom | Likely cause | Smallest next test |
|---|---|---|
| Duplicate rows appear | No unique normalized email constraint | Submit same email twice and inspect table. |
| Duplicate error scares user | Database error not mapped | Return friendly already-subscribed response. |
| Cron sends unexpectedly | Dry-run gate skipped | Disable schedule until dry-run output is reviewed. |
| Brevo key leaks | Provider secret placed in frontend env | Move it to Supabase secrets and rotate it. |

## What you should be able to explain

- Why duplicate prevention belongs in the database.
- Why dry-run comes before real scheduled sends.
- Why subscriber status matters for future unsubscribe behavior.

## The slower beginner path

If this chapter feels too large, split the newsletter and Cron workflow into one sitting per checkpoint. The goal is not to finish fast; the goal is to finish with proof.

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
