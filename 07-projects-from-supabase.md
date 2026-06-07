# Chapter 7 - Projects from Supabase

Projects are no longer hard-coded arrays. They live in Postgres, are protected by RLS, and render publicly only when published.

> **Principle.** Dynamic content should still feel fast, clear, and trustworthy.

## Where we're headed

By the end, the projects page reads published projects from Supabase, shows project cards, opens detail pages by slug, and handles loading, error, and empty states.

## Before you build

> **Reading before this step.** Read DevWeekends React `useEffect`: https://resources.devweekends.com/courses/react-crash-course/07-useeffect. Focus on loading data after render.

> **Apply this habit.** Read "Test Edge Cases" in [Daily_Software_Development_Guidelines.md](../Daily_Software_Development_Guidelines.md), then plan the empty projects state.

## Step 1 - Seed one published project

Create one published project in Supabase. It should have a slug, summary, problem, solution, and result.

Do not seed fake links unless marked clearly as placeholders.

## Step 2 - Fetch published projects

Create a data function in the projects feature:

```txt
src/features/projects/
  projectsApi.js
```

It should fetch published projects ordered by `published_at` or `featured`.

## Step 3 - Render project cards

Create:

```txt
ProjectCard
ProjectGrid
ProjectStatusMessage
```

Cards should show:

```txt
title
summary
tech_stack
live_url or status
link to details
```

## Step 4 - Build project details

Use the `slug` route to fetch one published project.

If the slug does not exist or the project is a draft, show a friendly not-found state.

## Step 5 - Handle all states

Show:

- loading;
- error;
- empty;
- success;
- not found.

## What your screen should show

The projects page loads real Supabase data. Draft projects do not appear publicly.

## Small challenge

Write a project card that makes someone want to click without opening the detail page.

Suggested commit:

```bash
git commit -m "feat: load projects from supabase"
```

## Definition of Done

- [ ] Published projects load from Supabase.
- [ ] Draft projects are hidden publicly.
- [ ] Project cards render useful summaries.
- [ ] Project detail pages use slugs.
- [ ] Loading, error, empty, and not-found states exist.
- [ ] You tested a draft project.

> **Log it.** In `learning-log/07-projects-from-supabase.md`: How does RLS affect the public project query? What happens when a slug is missing?

Next: publish articles from Supabase. -> **[Chapter 8 - Articles from Supabase](08-articles-from-supabase.md)**
