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
return success if message is stored
record email failure separately if needed
```

Email is a notification. The database is the source of truth.

## Build it

Create a contact Edge Function. It should accept name, email, subject, message, and optional metadata. Validate required fields, lengths, and email format. Reject suspicious empty or oversized submissions.

Store `BREVO_API_KEY`, sender email, and recipient email as Supabase secrets. Never put them in `VITE_` env vars.

After insertion, call Brevo's transactional email API. The message should include enough context for the owner to reply quickly: visitor name, email, subject, message, and page/source if available.

## Mandatory read

Read Brevo's transactional email API docs and Supabase Edge Function secrets docs. Required: this chapter depends on knowing where provider credentials belong.

## Definition of Done

- [ ] Contact form submits to an Edge Function.
- [ ] Input is validated server-side.
- [ ] Contact message is saved before email is attempted.
- [ ] Brevo sends an owner notification.
- [ ] Brevo key is stored as a Supabase secret.
- [ ] Brevo key is not present in frontend code or Vite env vars.
- [ ] Failure states tell the visitor what happened.

> **Log it.** In `learning-log/12-contact-edge-function-brevo.md`, explain why the database is the source of truth and Brevo is only the notification channel.

Next: messages are stored. Now give the owner a place to read and manage them. -> **[Chapter 13 - Contact inbox and Realtime](13-contact-inbox-realtime.md)**
