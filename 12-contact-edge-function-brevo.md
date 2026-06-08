# Chapter 12 - Contact Edge Function and Brevo

The contact form is where a visitor tries to start a conversation. The worst failure is silent: the visitor submits, an email API fails, and the message is gone. This chapter prevents that by storing the message first and sending the notification second.

## Where we're headed

By the end, the contact form submits to a Supabase Edge Function, validates input, inserts into `contact_messages`, and sends a Brevo email notification without exposing Brevo credentials to the frontend.

## The email trap

Bad:

```txt
React form -> Brevo API directly
```

Problem: the Brevo API key would be exposed in the browser. Anyone could steal it and send mail as your account.

Better:

```txt
React form -> Supabase Edge Function -> contact_messages -> Brevo
```

The Edge Function is server-side. It can use secrets safely.

### Edge Functions

**Real-life analogy:** a front desk clerk receives a visitor message, writes it down, and calls the right person. The visitor never sees the private phone list.

**General idea:** an Edge Function runs server-side code. Use it when work needs secrets or protected database access.

```txt
React form -> Supabase Edge Function -> database + Brevo
```

Study more: [AWS Core Concepts - Compute and Security Basics](https://resources.devweekends.com/aws/core-concepts)

## Store first, email second

Bad:

```txt
send email
if email succeeds, save message
```

Problem: if email fails, the message may disappear.

Better:

```txt
validate input
insert contact message
send Brevo notification
if Brevo succeeds: mark notification_sent
if Brevo fails: keep message and mark notification_failed
return a response that tells the frontend what happened
```

Email is a notification. The database is the source of truth.

### Source of truth

**Real-life analogy:** write a message in the logbook before trying to call someone. If the call fails, the message still exists.

**General idea:** the database should keep the contact message. Brevo only notifies the owner that a message arrived.

```ts
await saveContactMessage(input);
await sendBrevoNotification(input);
```

Study more: [Audit Logging for HIPAA - Why Logs Matter](https://resources.devweekends.com/courses/hipaa-compliance/audit-logging)

## Daily guideline

From `Daily_Software_Development_Guidelines.md`: **protect sensitive information** and **use logging wisely**. Log enough to debug contact failures, but never log Brevo keys, service-role keys, or full private message bodies unnecessarily. A log file can leak data just like committed code can.

## Build it

Create a contact Edge Function. It should accept name, email, subject, message, and optional metadata. Validate required fields, lengths, and email format. Reject suspicious empty or oversized submissions.

Store `BREVO_API_KEY`, sender email, and recipient email as Supabase secrets. Never put them in `VITE_` env vars.

After insertion, call Brevo's transactional email API. The message should include enough context for the owner to reply quickly: visitor name, email, subject, message, and page/source if available.

Use a precise response contract:

```txt
201 Created
{ "ok": true, "messageStored": true, "notificationSent": true }

202 Accepted
{ "ok": true, "messageStored": true, "notificationSent": false }

400 Bad Request
{ "ok": false, "error": "validation_failed" }

500 Internal Server Error
{ "ok": false, "error": "message_not_stored" }
```

If Brevo fails after the message is stored, do not lose the message and do not pretend the email succeeded. Store `notification_status = 'failed'` or an `email_error` field so the admin inbox can surface the problem.

## Mandatory read

Read Brevo's transactional email API docs and Supabase Edge Function secrets docs. Required: this chapter depends on knowing where provider credentials belong.

## Definition of Done

- [ ] Contact form submits to an Edge Function.
- [ ] Input is validated server-side.
- [ ] Contact message is saved before email is attempted.
- [ ] Brevo sends an owner notification.
- [ ] Brevo failure after storage returns a degraded-but-saved response.
- [ ] Notification success or failure is stored for owner visibility.
- [ ] Brevo key is stored as a Supabase secret.
- [ ] Brevo key is not present in frontend code or Vite env vars.
- [ ] Failure states tell the visitor what happened.

> **Log it.** In `learning-log/12-contact-edge-function-brevo.md`, explain why the database is the source of truth and Brevo is only the notification channel.

## Between chapters

Optional pause. Pick **one or two**, not all of them. Skip the rest without guilt if your Definition of Done is complete.

**Blog links:** read [MDN - Overview of HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Overview) again with Edge Functions in mind, then read [Cloudflare - DNS Encryption Explained](https://blog.cloudflare.com/dns-encryption-explained/) to see how much infrastructure sits underneath one "send contact form" action.

**Incident exercise:** imagine Brevo is down for one hour. What does the visitor see? What does the owner see later? What data is still saved?

**Quick quiz:** why is calling Brevo directly from React dangerous? Name the exact secret that would leak.

**Failure exercise:** temporarily make the Brevo call fail in development. Confirm the contact message is still stored and the UI explains the notification problem.

**Validation exercise:** submit missing name, invalid email, empty message, and oversized message. The Edge Function should reject bad input even if the frontend misses it.

**Comparison:** source of truth vs notification: the database is the source of truth because it stores the message. Brevo is a notification channel because it tells the owner that the message exists.

**Big word alert:** **server-side** means code runs on a server or platform function, not in the visitor's browser. Server-side code can safely use secrets when configured correctly.

**Diagram:**

```txt
Contact form
  -> Supabase Edge Function
  -> validate input
  -> insert contact_messages row
  -> send Brevo notification
  -> return result to visitor
```

**Motivation pause:** from `Software_Engineering_Community_Affirmations.md`: "Every bug solved is a lesson earned." Contact forms are full of edge cases; each one you handle makes the system more trustworthy.

Next: messages are stored. Now give the owner a place to read and manage them. -> **[Chapter 13 - Contact inbox and Realtime](13-contact-inbox-realtime.md)**
