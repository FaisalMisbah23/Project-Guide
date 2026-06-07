# Chapter 03 - Data model and migrations

You now have a running React app and a clean repo. The next question is where the portfolio's truth lives. Hard-coded arrays are tempting because they are fast. They are also a dead end once the owner needs admin editing, contact persistence, newsletter subscriptions, comments, or analytics.

## Where we're headed

By the end you will have a Supabase data model, versioned migrations, and seed data for the main portfolio records: `projects`, `articles`, `article_comments`, `contact_messages`, `newsletter_subscribers`, `newsletter_runs`, `page_visits`, and `profile_settings`.

## The tempting model

Bad:

```txt
projects.js
articles.js
visitor messages sent only by email
images stored as random URLs
```

Problem: the public site works, but the admin dashboard has nothing durable to edit. If an email notification fails, the contact message disappears. If an article is unpublished, no durable access rule stops public readers from seeing it.

Better:

```txt
projects(status, featured, slug, title, summary, image_path)
articles(status, slug, title, excerpt, body, category, tags)
article_comments(status, article_id, author_name, body)
contact_messages(status, name, email, subject, body)
newsletter_subscribers(status, email)
page_visits(path, referrer, country, city, created_at)
profile_settings(display_name, headline, location, links)
```

This model lets the public site read published content, the owner manage drafts, and server workflows store messages before trying external email.

## Migrations are the source of truth

Creating tables by hand in the Supabase dashboard feels quick. The cost appears later: no history, no repeatable setup, and no reliable way to rebuild the database.

Use migrations. A migration is a committed schema change that can run in order. In Supabase, this usually means using the Supabase CLI and keeping SQL migration files in the repo.

Plan the dependency order:

```txt
profile_settings
projects
articles
article_comments -> articles
contact_messages
newsletter_subscribers
newsletter_runs
page_visits
```

Add useful fields from the beginning:

```txt
id uuid primary key
created_at timestamptz
updated_at timestamptz
status text
slug text unique
```

For money or historical values, snapshot the value at the time it matters. This portfolio does not sell products, but the habit matters: if a future app stores orders, do not rely only on the current product price. Save the purchased price inside the order item so old orders stay true when product prices change.

## Build it

Create the migrations for the tables above. Add constraints where they protect meaning: required titles, unique slugs, allowed statuses, and foreign keys from comments to articles.

Seed one published project, one draft project, one published article, one draft article, and one sample contact message. The draft rows are important because RLS will prove public users cannot read them.

## Mandatory read

Read a database migration guide for the Supabase CLI and one short article on database normalization. Required: the next chapter adds RLS, and policies only make sense when table ownership and public/private fields are clear.

## Definition of Done

- [ ] Tables exist through committed migrations, not manual dashboard-only changes.
- [ ] Published and draft seed rows exist.
- [ ] Slugs are unique where needed.
- [ ] Comments reference articles with a foreign key.
- [ ] You can explain why contact messages belong in the database before email is sent.
- [ ] You committed the migration files.

> **Log it.** In `learning-log/03-data-model-and-migrations.md`, explain why migrations beat hand-created tables. Then choose one field that should be a column, not hidden in a blob, and explain why.

Next: the data exists. Now stop the wrong people from reading or changing it. -> **[Chapter 04 - RLS and security basics](04-rls-and-security-basics.md)**
