# Chapter 14 - Contact Edge Function with Brevo

The contact form should not pretend. It should store the message and notify the portfolio owner.

> **Principle.** Server-only work belongs server-side.

## Where we're headed

By the end, the contact form calls a Supabase Edge Function. The function validates input, stores the message, and sends a Brevo transactional email notification.

## Before you build

> **Mandatory read.** Read Supabase Edge Functions docs: https://supabase.com/docs/guides/functions.

> **Reading before adding secrets.** Read Supabase function secrets docs: https://supabase.com/docs/guides/functions/secrets.

> **Reading before email.** Read Brevo transactional email docs: https://developers.brevo.com/docs/send-a-transactional-email.

> **Apply this habit.** Read "Validate Input Everywhere" in [Daily_Software_Development_Guidelines.md](../Daily_Software_Development_Guidelines.md), then write the contact validation rules before coding.

## Step 1 - Define the contact contract

Request:

```txt
POST /functions/v1/contact-submit
{
  name,
  email,
  subject,
  message
}
```

Response:

```txt
Success: { ok: true }
Failure: { ok: false, error: "safe message" }
```

Do not return stack traces or Brevo details to the visitor.

## Step 2 - Create Edge Function

Create:

```txt
supabase/functions/contact-submit/
  index.ts
```

The function should:

1. accept only `POST`;
2. validate input;
3. insert into `contact_messages`;
4. call Brevo;
5. return a safe response.

## Step 3 - Add secrets

Store these as Supabase secrets, not Vite variables:

```txt
BREVO_API_KEY
CONTACT_TO_EMAIL
CONTACT_FROM_EMAIL
```

Never expose `BREVO_API_KEY` to the frontend.

## Step 4 - Send Brevo notification

Use Brevo's transactional email API endpoint. The notification should include visitor name, email, subject, message, and timestamp.

If Brevo fails after the message is stored, return a careful response and log the failure. The stored message should still exist.

## Step 5 - Connect the frontend form

The contact form should call the Edge Function and show:

- loading;
- success;
- validation error;
- server error.

## What your screen should show

A valid contact form submit creates a database row and sends a Brevo notification to the owner.

## Small challenge

Add a small success message that tells the visitor what happens next.

Suggested commit:

```bash
git commit -m "feat: add contact edge function with brevo"
```

## Definition of Done

- [ ] Edge Function exists.
- [ ] Function validates input.
- [ ] Function stores contact message.
- [ ] Function sends Brevo notification.
- [ ] Brevo key is stored as a Supabase secret.
- [ ] Frontend never sees Brevo key.
- [ ] Contact form handles success and failure.

> **Log it.** In `learning-log/14-contact-edge-function-brevo.md`: Why does the Brevo call belong in an Edge Function? What happens if email fails after the message is stored?

Next: build the contact inbox. -> **[Chapter 15 - Contact inbox](15-contact-inbox.md)**
