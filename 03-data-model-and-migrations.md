# Chapter 03 - Data model and migrations

A portfolio looks like pages, but it behaves like data. Projects have draft and published states. Articles have bodies, tags, and comments. Contact messages must survive email failure. Newsletter subscribers need duplicate protection. The owner identity must live somewhere trustworthy before RLS can protect anything.

This chapter is where the app stops being a pile of components and becomes a system with a memory.

## The point of this chapter

You design and create the database through committed Supabase migrations: content tables, workflow tables, analytics tables, an owner identity table, constraints, seed rows, indexes, and a reliable `updated_at` strategy.

## Step 1 - Draw the model before SQL

Write the tables on paper first:

```txt
owner_profile
profile_settings
projects
articles
article_comments
contact_messages
newsletter_subscribers
newsletter_runs
page_visits
```

The important beginner move is not memorizing SQL. It is deciding what each table is responsible for. Each table should store one kind of thing. Each column should store one clear fact.

## Step 2 - Use migrations, not dashboard memory

Clicking tables into existence in the Supabase dashboard feels fast. It leaves no reliable history. A migration is a repeatable, committed change. Another machine can run it. Future-you can review it. That is why migrations are mandatory.

> **📖 Mandatory read.** Read [Supabase CLI](https://supabase.com/docs/guides/cli), [Supabase database overview](https://supabase.com/docs/guides/database/overview), [PostgreSQL constraints](https://www.postgresql.org/docs/current/ddl-constraints.html), and [PostgreSQL indexes](https://www.postgresql.org/docs/current/indexes.html). Required: this chapter depends on knowing what migrations, constraints, and indexes are for.

## Step 3 - Add the safety fields early

Most editable tables need:

```txt
id uuid primary key
created_at timestamptz
updated_at timestamptz
status text with a check constraint
```

For `updated_at`, choose one strategy now. This course recommends a database trigger so later concurrency checks in Chapter 09 are not built on a stale timestamp. If `updated_at` does not actually update, it is decoration, not protection.

## Step 4 - Create the owner identity table

Chapter 04 needs to know who the single portfolio owner is. Do not hard-code that in React. Create `owner_profile` or equivalent:

```txt
owner_profile(user_id uuid)
```

That `user_id` points to the Supabase Auth user who owns the portfolio. The table itself must be private once RLS is enabled. Public users should never get to read or edit who counts as owner.

## Step 5 - Add constraints and seeds

Add unique slugs for public pages. Add status checks so `published`, `draft`, `archived`, `pending`, and `approved` cannot be misspelled into new states. Add a foreign key from comments to articles. Add a unique normalized email for subscribers.

Seed at least one published project, one draft project, one published article, one draft article, one pending comment, and one sample contact message. Draft seed data is not filler; it is how you prove RLS later.

> **💡 Hint.** A schema without private seed rows cannot prove privacy. You need something private in the database before you can test that public users cannot see it.

## Definition of Done

- [ ] Tables are created through committed migrations, not dashboard-only changes.
- [ ] `owner_profile` or equivalent owner identity table exists.
- [ ] Editable tables have a reliable `updated_at` strategy.
- [ ] Status fields have check constraints.
- [ ] Slugs and normalized subscriber emails are unique where needed.
- [ ] Comments reference articles with a foreign key.
- [ ] Useful indexes exist for published reads, slug lookups, approved comments, recent messages, and recent visits.
- [ ] Seed data includes both public and private/draft rows.

> **✍️ Log it (mandatory).** In `learning-log/03-data-model-and-migrations.md`: explain why migrations beat dashboard-only changes, why `owner_profile` belongs in the database instead of React, and why `updated_at` must be reliable before it can protect edits.

All boxes ticked? Then the data exists. Now lock the doors.

---

Next: the data exists; now decide who is allowed to see and change it. -> **[Chapter 04 - RLS and security basics](04-rls-and-security-basics.md)**
