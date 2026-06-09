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
