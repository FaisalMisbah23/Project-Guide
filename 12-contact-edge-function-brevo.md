# Chapter 12 - Contact Edge Function and Brevo

The contact form is where a visitor says, 'I want to talk.' The worst version of this feature sends an email, the email provider fails, and the message disappears. That is not a contact form; that is a trapdoor.

## The point of this chapter

A contact form calls a Supabase Edge Function that handles CORS, validates input, stores the message first, sends Brevo notification second, records notification outcome, and returns an honest response.

## Step 1 - Keep Brevo out of React

Calling Brevo from the browser exposes the API key. Provider keys are server-only. The Edge Function is the boundary where secrets can be used safely.

## Step 2 - Validate on the server

Frontend validation helps the visitor, but the function must validate name, email, subject, message length, and suspicious empty submissions. Never trust the browser alone.

## Step 3 - Store first, email second

Insert the contact message before calling Brevo. If Brevo fails, the owner can still read the message in the admin inbox.

## Step 4 - Return a precise outcome

Use `201` for stored and notified, `202` for stored but notification failed, `400` for validation failure, and `500` only when the message was not stored.

## Step 5 - Handle CORS deliberately

Browser calls to Edge Functions may need CORS headers and preflight handling. Add them as part of the function, not after panic-debugging.

## Step 6 - Write the function contract

The frontend should be able to depend on a precise response shape:

```txt
201 Created
{ ok: true, messageStored: true, notificationSent: true }

202 Accepted
{ ok: true, messageStored: true, notificationSent: false }

400 Bad Request
{ ok: false, error: "validation_failed" }

500 Internal Server Error
{ ok: false, error: "message_not_stored" }
```

This contract keeps the UI honest. A stored message with failed email is not the same as a lost message.

## Step 7 - Define the Edge Function responsibilities

The function owns server-side work:

```txt
handle CORS preflight
parse JSON safely
validate name/email/subject/message
insert contact_messages row
call Brevo with server-side secret
update notification_status
return precise JSON
avoid logging secrets or full private message bodies
```

React owns the form and user feedback. Brevo owns email delivery. The database owns truth.

## Step 8 - Do it on your project

Create:

```txt
supabase/functions/contact/index.ts
contact form submit helper
contact_messages notification fields
Supabase secrets for BREVO_API_KEY, sender, recipient
frontend messages for 201, 202, 400, 500
```

Do not put Brevo secrets in `.env` for Vite.

## Prove it before moving on

Run four tests:

```txt
valid message + Brevo works       -> 201 and inbox row
valid message + Brevo forced fail -> 202 and inbox row with failed notification
invalid email                     -> 400 and no row
forced database failure           -> 500 and no false success
```

If email failure loses the message, the feature is backwards.

> **📖 Mandatory read.** Read [Supabase Edge Functions](https://supabase.com/docs/guides/functions), [Supabase function secrets](https://supabase.com/docs/guides/functions/secrets), [Brevo transactional email](https://developers.brevo.com/docs/send-a-transactional-email), [MDN CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/CORS), and [MDN form validation](https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Forms/Form_validation). Required: this feature crosses browser, server, database, and provider boundaries.

> **💡 Hint.** Temporarily force Brevo failure in development. The message should still exist, and the UI should say the message was saved but notification failed.

## Definition of Done

- [ ] Contact form calls an Edge Function.
- [ ] Function handles CORS and preflight requests.
- [ ] Input is validated server-side.
- [ ] Message is saved before Brevo is called.
- [ ] Brevo success or failure is recorded on the message.
- [ ] Frontend distinguishes stored-and-notified from stored-but-email-failed.
- [ ] Brevo key and service-role key are not in React, Vite env vars, committed files, or logs.

> **✍️ Log it (mandatory).** In `learning-log/12-contact-edge-function-brevo.md`: explain why the database is the source of truth and Brevo is only a notification channel. Include what the visitor and owner see when Brevo fails.

All boxes ticked? Then continue. The next chapter builds on this gate, not around it.

---

Next: messages are stored; now give the owner a durable inbox. -> **[Chapter 13 - Contact inbox and Realtime](13-contact-inbox-realtime.md)**
