# Chapter 8 - Articles from Supabase

Articles make your thinking visible: decisions, lessons, debugging stories, and project writeups.

> **Principle.** Articles turn hidden learning into inspectable judgment.

## Where we're headed

By the end, the portfolio has an Articles page and article detail pages loaded from Supabase.

## Before you build

> **Mandatory read.** From [Software_Engineering_Community_Affirmations.md](../Software_Engineering_Community_Affirmations.md), keep this motto: "Learn, build, share, repeat."

> **Apply this habit.** Read "Ask Better Questions" in [Daily_Software_Development_Guidelines.md](../Daily_Software_Development_Guidelines.md), then write one article idea from this project.

## Step 1 - Seed one published article

Create one article with:

```txt
title
slug
excerpt
body
tags
status = published
published_at
```

Keep the first article short and real. Example:

```txt
How I protected public portfolio data with Supabase RLS
```

## Step 2 - Fetch article list

Create:

```txt
src/features/articles/
  articlesApi.js
```

Fetch only published articles for public pages.

## Step 3 - Render article cards

Cards should show title, excerpt, tags, and publish date.

Do not make article cards look like project cards if the content is different. Projects prove output; articles prove thinking.

## Step 4 - Render article detail

Use `/articles/:slug`. Missing or draft articles should show not found.

## Step 5 - Add tag filtering or search

Add one simple interaction:

- search by title/excerpt; or
- filter by tag.

Do not store filtered results in state if they can be derived from articles plus the current search/tag.

## What your screen should show

The Articles page shows published articles from Supabase. Detail pages open by slug.

## Small challenge

Write the first paragraph of an article that explains a real decision you made in this course.

Suggested commit:

```bash
git commit -m "feat: add articles from supabase"
```

## Definition of Done

- [ ] Articles page loads published articles.
- [ ] Article detail route works.
- [ ] Draft articles are hidden publicly.
- [ ] Search or tag filtering works.
- [ ] Empty state is clear.
- [ ] The guide and UI use "Articles" consistently.

> **Log it.** In `learning-log/08-articles-from-supabase.md`: Why does a portfolio benefit from articles? How do articles differ from projects?

Next: add owner login. -> **[Chapter 9 - Owner login with Supabase Auth](09-owner-login-with-supabase-auth.md)**
