# Chapter 5 - RLS and security basics

Supabase can expose database tables directly to the frontend, but that is only safe when Row Level Security controls what each user can do.

> **Principle.** A public API key is acceptable only when the database enforces the rules.

## Where we're headed

By the end, published projects and articles are public, drafts are hidden, and only the signed-in owner can manage content and messages.

## Before you build

> **Mandatory read.** Read Supabase Row Level Security docs: https://supabase.com/docs/guides/auth/auth-deep-dive/auth-row-level-security. Focus on policies, `using`, and `with check`.

> **Apply this habit.** Read "Design for Failure" in [Daily_Software_Development_Guidelines.md](../Daily_Software_Development_Guidelines.md), then write what should happen when a user tries to access draft content.

## Step 1 - Turn on RLS

Enable RLS on:

```txt
projects
articles
contact_messages
profile_settings
```

No table should depend on hope. If the table matters, RLS should be deliberate.

## Step 2 - Public read policies

Public visitors can read only:

```txt
projects where status = 'published'
articles where status = 'published'
safe profile_settings fields
```

Bad:

```txt
Allow public select on all projects.
```

Problem:

```txt
Drafts, private notes, and unfinished content can leak.
```

Better:

```txt
Allow public select only where status = 'published'.
```

## Step 3 - Owner write policies

Only the authenticated owner can insert, update, or delete projects and articles.

For this course, define one owner identity and document how the policies recognize that owner. Keep it simple and explicit.

## Step 4 - Contact message policies

Public visitors should not directly browse contact messages.

The contact Edge Function will insert messages using server-side privileges or a controlled RPC/function path. Admin reads should require the owner.

## Step 5 - Test blocked access

Test the uncomfortable cases:

- public visitor cannot see drafts;
- public visitor cannot update projects;
- public visitor cannot read contact messages;
- signed-in owner can manage content;
- signed-out admin route does not expose data.

## What your screen should show

Published content is visible publicly. Draft and admin-only data is blocked unless the owner is signed in.

## Small challenge

Write one RLS policy in plain English before writing SQL.

Suggested commit:

```bash
git commit -m "feat: add supabase rls policies"
```

## Definition of Done

- [ ] RLS is enabled on all app tables.
- [ ] Public reads are limited to published content.
- [ ] Owner writes are protected.
- [ ] Contact messages are not publicly readable.
- [ ] Draft access is tested.
- [ ] You can explain why anon key plus RLS is not the same as "no security."

> **Log it.** In `learning-log/05-rls-and-security-basics.md`: What can an anonymous visitor do? What can the owner do? Which policy was easiest to misunderstand?

Next: build the public frontend shell. -> **[Chapter 6 - Public layout and routing](06-public-layout-and-routing.md)**
