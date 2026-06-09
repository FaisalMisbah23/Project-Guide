# Chapter 12 - Contact Edge Function and Brevo

The contact form is where a visitor says, 'I want to talk.' The worst version of this feature sends an email, the email provider fails, and the message disappears. That is not a contact form; that is a trapdoor.

## The point of this chapter

A contact form calls a Supabase Edge Function that handles CORS, validates input, stores the message first, sends Brevo notification second, records notification outcome, and returns an honest response.

## Before you touch code

- Contact form route exists.
- contact_messages table exists.
- Supabase Edge Functions workflow is available.
- Brevo account/key is ready or you can fake provider failure in development.

## Vocabulary for this chapter

- **Edge Function.** Server-side code deployed on Supabase.
- **CORS.** Browser rule for cross-origin function calls.
- **Server validation.** Validation that runs outside the browser and cannot be bypassed by editing React.
- **Degraded success.** The important data saved, but a secondary action failed.
- **Notification.** A message sent to alert the owner; not the source of truth.

## Guided snippet or contract

This is a shape to aim for, not a finished solution to paste blindly:

```ts
// Edge Function responsibility shape
request -> CORS -> parse JSON -> validate -> insert contact_messages -> call Brevo -> update notification_status -> response

// response contract
201: stored and notification sent
202: stored and notification failed
400: validation failed
500: message not stored
```

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

## If it breaks

| Symptom | Likely cause | Smallest next test |
|---|---|---|
| Browser shows CORS error | Preflight or allowed origin headers missing | Send an OPTIONS request or inspect function headers. |
| Invalid email stores row | Server validation missing | Call function directly with invalid payload. |
| Brevo failure loses message | Email is attempted before insert | Force provider failure and inspect table. |
| Secret appears in frontend bundle | Brevo key placed in Vite env or React file | Search built/source files and move secret to Supabase. |

## What you should be able to explain

- Why Brevo cannot be called from React.
- Why store-first/email-second protects visitors.
- What 201, 202, 400, and 500 mean in this flow.
- How CORS differs from authentication.

## The slower beginner path

If this chapter feels too large, split the contact function and Brevo workflow into one sitting per checkpoint. The goal is not to finish fast; the goal is to finish with proof.

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
