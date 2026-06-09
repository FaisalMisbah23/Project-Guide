# Chapter 03 - Data model and migrations

A portfolio looks like pages, but it behaves like data. Projects have draft and published states. Articles have bodies, tags, and comments. Contact messages must survive email failure. Newsletter subscribers need duplicate protection. The owner identity must live somewhere trustworthy before RLS can protect anything.

This chapter is where the app stops being a pile of components and becomes a system with a memory.

## The point of this chapter

You design and create the database through committed Supabase migrations: content tables, workflow tables, analytics tables, an owner identity table, constraints, seed rows, indexes, and a reliable `updated_at` strategy.

## Before you touch code

- Finish Chapter 02 and confirm the app builds.
- Read the Supabase CLI docs with migrations in mind.
- Write the table list before opening the SQL editor.
- Decide that dashboard-only schema changes do not count as done.

## Vocabulary for this chapter

- **Migration.** A committed database change that can be rerun in order.
- **Constraint.** A database rule that rejects invalid data.
- **Seed data.** Sample rows used to prove features and policies.
- **Foreign key.** A rule that one row points to a real row elsewhere.
- **Trigger.** Database logic that runs automatically, such as updating `updated_at`.

## Guided snippet or contract

This is a shape to aim for, not a finished solution to paste blindly:

```sql
-- shape, not final migration
owner_profile(user_id uuid unique not null)
projects(slug text unique not null, status text not null, updated_at timestamptz)
articles(slug text unique not null, status text not null, updated_at timestamptz)
article_comments(article_id uuid not null, status text not null)
contact_messages(email text not null, status text not null, notification_status text)
newsletter_subscribers(email text unique not null, status text not null)
page_visits(path text not null, referrer text, created_at timestamptz)
```

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

## Step 6 - Turn the drawing into migration files

Use one or more migration files, but keep the dependency order clear. A beginner-friendly order is:

```txt
owner_profile and profile_settings
projects
articles
article_comments
contact_messages
newsletter_subscribers
newsletter_runs
page_visits
updated_at trigger/helper
indexes
seed data
```

The exact filenames are less important than the rule: migrations are committed, ordered, and repeatable.

## Step 7 - Write constraints as business rules

A constraint is not database decoration. It is a business rule the database refuses to forget:

| Rule | Database protection |
|---|---|
| A project slug should not collide | unique constraint on `projects.slug` |
| A status should not be misspelled | check constraint on `status` |
| A comment belongs to an article | foreign key from `article_comments.article_id` |
| One subscriber email should not duplicate | unique normalized email |
| Editable rows need reliable conflict checks | automatic `updated_at` strategy |

React can help users avoid mistakes. The database prevents corrupted truth.

## Step 8 - Seed for proof, not decoration

Seed rows should create test situations:

```txt
published project   -> should appear publicly later
draft project       -> should not appear publicly later
published article   -> should appear publicly later
draft article       -> should not appear publicly later
pending comment     -> should not appear publicly until approved
contact message     -> should be owner-only later
```

If seed data does not help prove a rule, improve it.

## Step 9 - Do it on your project

Create or update migrations so a reviewer can answer these questions from the SQL:

```txt
Where is owner identity stored?
Which rows can be drafted or published?
Which fields are required?
Which values are unique?
Which tables reference other tables?
Which queries will need indexes later?
How does updated_at stay current?
```

Do not move to RLS with fuzzy answers. RLS policies are only as clear as the model they protect.

## Prove it before moving on

Run the migrations from a clean database if your Supabase workflow allows it, or inspect the migration history and table definitions carefully. Then try one invalid insert per important constraint: duplicate slug, bad status, comment with missing article, duplicate subscriber email. The database should say no.

## If it breaks

| Symptom | Likely cause | Smallest next test |
|---|---|---|
| Migration fails on first run | SQL syntax or dependency order is wrong | Read the first error line and run only that migration after fixing. |
| Seed rows fail | Required field or check constraint missing from seed data | Insert one row manually with all required fields. |
| Duplicate bad data is accepted | A unique or check constraint is missing | Try the bad insert again after adding the constraint. |
| `updated_at` never changes | Trigger/application update strategy is not wired | Update one row and compare timestamp before/after. |

## What you should be able to explain

- Why migrations are better than dashboard-only changes.
- Why `owner_profile` is needed before RLS.
- Why seed data should include private rows.
- Why `updated_at` must be real before Chapter 09.

## The slower beginner path

If this chapter feels too large, split the database model into one sitting per checkpoint. The goal is not to finish fast; the goal is to finish with proof.

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
