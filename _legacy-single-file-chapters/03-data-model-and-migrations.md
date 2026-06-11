# Chapter 03 - Data Model And Migrations

The portfolio will eventually store content in Supabase. Before writing SQL, you need to decide what kinds of data exist and which tables own them.

## Goal

By the end, you will have a beginner-readable database plan and migrations for the main portfolio data.

## What You Will Build

- A table plan.
- Supabase migration files.
- Seed data for public and private cases.
- Constraints that protect obvious mistakes.

## Beginner Concepts

- **Table:** a database collection for one kind of thing.
- **Row:** one item inside a table.
- **Column:** one field on a row.
- **Migration:** a saved database change that can be rerun.
- **Seed data:** starter rows used for testing.
- **Constraint:** a database rule that rejects bad data.

## Step By Step

### Step 1 - List The Content Types

Write this table list before opening SQL:

```txt
owner_profile
profile_settings
work_experience
projects
articles
article_comments
contact_messages
newsletter_subscribers
newsletter_runs
page_visits
```

Work experience is included because a portfolio should show professional history, internships, freelance work, volunteer work, or serious learning milestones.

### Step 2 - Decide What Starts Local And What Moves To Supabase

Use this rule:

```txt
Local array first:
  skills
  starter work experience
  starter project cards

Supabase later:
  projects managed by admin
  articles managed by admin
  contact messages
  subscribers
  analytics
  optional work_experience if you want admin editing
```

The course documents `work_experience` as a possible table, but you may first render experience from `src/data/experience.ts`.

### Step 3 - Create Migrations

Use the Supabase CLI migration workflow. The files should be committed, not only clicked together in the dashboard.

Create tables in a clear order:

```txt
owner_profile
profile_settings
work_experience
projects
articles
article_comments
contact_messages
newsletter_subscribers
newsletter_runs
page_visits
```

### Step 4 - Add Basic Columns

Most editable tables should have:

```txt
id
created_at
updated_at
status
```

Examples:

```txt
projects: title, slug, summary, description, technologies, status, featured
articles: title, slug, excerpt, body, status, published_at
work_experience: company, role, start_date, end_date, summary, highlights, sort_order, status
contact_messages: name, email, message, status, notification_status
```

### Step 5 - Add Constraints

Add database rules for:

```txt
unique project slugs
unique article slugs
valid status values
comments belonging to real articles
unique subscriber emails
updated_at changing reliably
```

React can guide users. The database must protect truth.

### Step 6 - Add Seed Data

Seed rows should prove behavior:

```txt
published project
draft project
published article
draft article
published work experience item
draft work experience item, if using the table
pending comment
sample contact message
```

Private or draft seed data is not decoration. It lets you test that RLS blocks it later.

## Common Mistakes

| Mistake | Why it hurts | Fix |
|---|---|---|
| Making tables only in the dashboard | No repeatable history | Use migrations |
| No draft seed data | Privacy cannot be tested | Seed both public and private rows |
| No unique slug | Two pages can share one URL | Add unique constraints |
| Treating `updated_at` as decoration | Edit conflict checks become unreliable | Use a real trigger or clear update strategy |

## Checks Before Moving On

- Migration files exist.
- Tables have clear responsibilities.
- Seed data includes public and private examples.
- Constraints reject obvious bad data.
- Work experience has either a local-array plan or a table plan.

## Learning Log

In `learning-log/03-data-model-and-migrations.md`, answer:

```txt
Which data starts local?
Which data belongs in Supabase?
Why do projects and articles need draft rows?
Why are migrations better than dashboard-only changes?
What table would store work experience if admin editing is needed?
```

## Definition Of Done

- [ ] Database model is written before SQL.
- [ ] Migrations create the tables.
- [ ] `owner_profile` exists.
- [ ] `work_experience` is planned or created.
- [ ] Constraints protect slugs, statuses, relationships, and duplicate emails.
- [ ] Seed data includes public and private rows.

Next: protect the data. -> **[Chapter 04 - RLS And Security Basics](04-rls-and-security-basics.md)**
