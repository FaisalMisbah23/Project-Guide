# Chapter 04 - RLS And Security Basics

Now that tables exist, you must decide who can read and change each row. Hiding buttons in React is not security. Supabase Row Level Security protects data at the database layer.

## Goal

By the end, public users can read only public content, and the owner can manage private content.

## What You Will Build

- RLS enabled on important tables.
- Public read policies for published content.
- Owner policies for admin workflows.
- Manual tests that prove drafts and messages are private.

## Beginner Concepts

- **RLS:** Row Level Security, database rules checked for each row.
- **Policy:** the rule that says who may select, insert, update, or delete.
- **Anon user:** signed-out browser visitor using the public anon key.
- **Authenticated user:** signed-in Supabase Auth user.
- **Owner:** the one authenticated user listed in `owner_profile`.

## Step By Step

### Step 1 - Mark Public And Private Data

Write this table:

```txt
Public when published:
  projects
  articles
  approved article_comments
  published work_experience if database-backed

Owner-only:
  drafts
  contact_messages
  newsletter_subscribers
  newsletter_runs
  page_visits summaries
  owner_profile
```

### Step 2 - Enable RLS

Enable RLS on every table that stores app data. A table without RLS can accidentally expose more than intended.

### Step 3 - Add Public Read Policies

Allow signed-out visitors to read:

```txt
projects where status = 'published'
articles where status = 'published'
article_comments where status = 'approved'
work_experience where status = 'published', if table-backed
```

Do not allow public users to read drafts, contact messages, subscribers, or owner identity.

### Step 4 - Add Owner Policies

Use `owner_profile.user_id` to decide who the owner is. The owner may read and write admin-managed tables.

The rule should live in the database, not in React.

### Step 5 - Test With The Anon Client

Run or simulate signed-out queries:

```txt
published project -> visible
draft project -> blocked or not returned
published article -> visible
draft article -> blocked or not returned
contact message -> blocked
subscriber row -> blocked
```

### Step 6 - Test As The Owner

Sign in as the owner and confirm the owner can read drafts and admin-only rows.

## Common Mistakes

| Mistake | Why it hurts | Fix |
|---|---|---|
| Hiding draft links in React only | Draft rows can still leak through queries | Add RLS policies |
| Making any authenticated user an owner | Any login can edit content | Check against `owner_profile` |
| Forgetting contact messages | Private visitor data leaks | Make messages owner-only |
| Not testing signed out | You only tested the happy path | Use anon queries deliberately |

## Checks Before Moving On

- RLS is enabled on app tables.
- Public policies read only published/approved content.
- Owner policies use owner identity.
- Drafts are blocked from signed-out users.
- Contact messages are owner-only.

## Learning Log

In `learning-log/04-rls-and-security.md`, answer:

```txt
Why is hiding UI not security?
Which data is public?
Which data is owner-only?
How did you prove a draft row stays private?
```

## Definition Of Done

- [ ] RLS is enabled.
- [ ] Public read policies are narrow.
- [ ] Owner policies are based on `owner_profile`.
- [ ] Signed-out tests cannot read private rows.
- [ ] Owner tests can access owner workflows.

Next: design public layout and routes. -> **[Chapter 05 - Public Layout And Routing](05-public-layout-and-routing.md)**
