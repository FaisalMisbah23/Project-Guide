# Chapter 12 - Contact Edge Function And Brevo

A contact form should not rely only on email. The message should be saved first, then the app can try to send an email notification.

## Goal

By the end, contact messages are validated, saved in Supabase, and followed by a Brevo notification attempt from a server-side Edge Function.

## What You Will Build

- Public contact form.
- Supabase Edge Function.
- Input validation.
- Database insert.
- Brevo notification call.
- Failure handling.

## Beginner Concepts

- **Edge Function:** server-side code hosted by Supabase.
- **Server-side secret:** private key used outside the browser.
- **Validation:** checking input before trusting it.
- **Source of truth:** the place where data is reliably stored.
- **Notification:** helpful alert, not the permanent record.

## Step By Step

### Step 1 - Build The Contact Form UI

On `/contact`, collect:

```txt
name
email
subject, optional
message
```

Show validation errors before submitting.

### Step 2 - Create The Edge Function

Create a Supabase Edge Function such as:

```txt
send-contact-message
```

The browser should call this function instead of calling Brevo directly.

### Step 3 - Validate In The Function

Validate:

```txt
name is present
email looks like email
message is present
message length is reasonable
```

Frontend validation is friendly. Function validation is required.

### Step 4 - Save Message First

Insert into `contact_messages` before calling Brevo.

Use fields such as:

```txt
name
email
subject
message
status = unread
notification_status = pending
```

### Step 5 - Send Brevo Notification

Use the Brevo API key only inside the Edge Function environment. Never put it in React.

If Brevo succeeds, update `notification_status` to `sent`.

If Brevo fails, update `notification_status` to `failed` but keep the saved message.

### Step 6 - Return A Friendly Response

The visitor should see a calm success message if the database saved the message, even if email notification failed.

### Step 7 - Test Failures

Try:

```txt
missing email
empty message
Brevo key missing
Brevo request failure
signed-out direct table insert, if not allowed
```

## Common Mistakes

| Mistake | Why it hurts | Fix |
|---|---|---|
| Calling Brevo from React | Exposes the API key | Use Edge Function |
| Email before database insert | Message can be lost | Save first |
| Treating email as storage | Inbox can miss messages | Use database as source of truth |
| No function validation | Browser checks can be bypassed | Validate server-side |

## Checks Before Moving On

- Contact form submits to Edge Function.
- Function validates input.
- Message saves before email.
- Brevo key is server-only.
- Failed email does not delete the message.
- Visitor sees understandable feedback.

## Learning Log

In `learning-log/12-contact-edge-function-brevo.md`, answer:

```txt
Why should contact messages be saved before email?
Why can Brevo keys not live in React?
What happens if Brevo fails?
Which validations happen in the form and which happen in the function?
```

## Definition Of Done

- [ ] Contact form exists.
- [ ] Edge Function receives submissions.
- [ ] Invalid input is rejected.
- [ ] Messages are inserted into `contact_messages`.
- [ ] Brevo notification is attempted server-side.
- [ ] Email failure keeps the saved message.

Next: build the admin inbox. -> **[Chapter 13 - Contact Inbox And Realtime](13-contact-inbox-realtime.md)**
