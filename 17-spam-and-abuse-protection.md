# Chapter 17 - Spam and abuse protection

A public contact form invites real people and bots. You do not need enterprise abuse prevention, but you do need to think beyond the happy path.

> **Principle.** Public inputs deserve suspicion and care.

## Where we're headed

By the end, the contact flow has basic anti-abuse checks, safer validation, and a plan for rate limiting or CAPTCHA if needed.

## Before you build

> **Mandatory read.** Read Supabase Edge Functions docs on deployment and environment: https://supabase.com/docs/guides/functions.

> **Apply this habit.** Read "Design for Failure" in [Daily_Software_Development_Guidelines.md](../Daily_Software_Development_Guidelines.md), then write how spam would affect the owner.

## Step 1 - Add a honeypot field

Add a hidden field that normal users do not fill. If it contains a value, reject or silently accept without sending email.

Do not rely on this alone. It is a speed bump.

## Step 2 - Add length limits

Set limits for:

```txt
name
email
subject
message
```

Long messages can be valid, but unbounded input is a risk.

## Step 3 - Normalize and store source metadata

Store safe metadata such as:

```txt
source
created_at
```

Avoid collecting sensitive data unless you need it and can explain why.

## Step 4 - Plan rate limiting

For this course, document the production choice:

- Supabase Edge Function plus provider/platform limits;
- optional CAPTCHA;
- optional IP-based rate limiting service;
- Brevo monitoring for unusual send volume.

## Step 5 - Test abuse-ish cases

Test:

- empty message;
- huge message;
- invalid email;
- honeypot filled;
- repeated submit click.

## What your screen should show

Normal contact works. Obvious bad submissions do not send noisy Brevo emails.

## Small challenge

Add a disabled submit state that prevents double-click duplicate submissions.

Suggested commit:

```bash
git commit -m "feat: harden contact submission"
```

## Definition of Done

- [ ] Honeypot field exists.
- [ ] Length limits exist.
- [ ] Double submit is prevented.
- [ ] Bad input is rejected safely.
- [ ] Brevo is not called for obvious spam.
- [ ] Rate-limit strategy is documented.

> **Log it.** In `learning-log/17-spam-and-abuse-protection.md`: Which abuse case did you test, and what happened?

Next: polish the experience. -> **[Chapter 18 - Responsive polish and accessibility](18-responsive-polish-and-accessibility.md)**
