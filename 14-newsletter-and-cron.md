# Chapter 14 - Newsletter and Cron

Newsletter subscriptions sound small until you treat them like production data. A subscriber is trusting you with their email. Store it carefully, avoid duplicate rows, and send updates only from server-side scheduled work.

## Where we're headed

By the end, visitors can subscribe, subscriber emails are stored in Supabase, and a scheduled newsletter function is planned or implemented with Supabase Cron and Brevo.

## The newsletter trap

Bad:

```txt
newsletter form -> frontend calls email provider
```

Problem: provider keys leak, duplicates grow, and unsubscribes become messy.

Better:

```txt
newsletter form -> Edge Function -> newsletter_subscribers
scheduled function -> query new content -> Brevo send
newsletter_runs records result
```

## Build it

Create a newsletter signup Edge Function. Validate email, normalize casing, prevent duplicates, and store status such as `active`, `unsubscribed`, or `bounced` if you support it.

Create `newsletter_runs` to track scheduled sends:

```txt
id
started_at
finished_at
status
article_count
subscriber_count
error_message
```

If implementing Cron now, schedule a Supabase function that looks for new published articles or projects and sends a digest through Brevo. If this is too much for the first pass, write the contract and leave the function as a planned advanced feature, but keep the schema ready.

## Definition of Done

- [ ] Newsletter signup stores validated emails.
- [ ] Duplicate emails are handled.
- [ ] Brevo keys remain server-side.
- [ ] `newsletter_runs` exists or is clearly planned.
- [ ] Cron workflow is documented.
- [ ] The owner can explain what triggers an update email.

> **Log it.** In `learning-log/14-newsletter-and-cron.md`, explain why newsletters should be sent by scheduled server work, not by browser code.

Next: the owner has content and messages. Now add lightweight visit insights without building a surveillance machine. -> **[Chapter 15 - Analytics and Realtime insights](15-analytics-realtime-insights.md)**
