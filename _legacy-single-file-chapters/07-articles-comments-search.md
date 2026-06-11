# Chapter 07 - Articles, Comments, Search, And Pagination

Projects show what you built. Articles show how you think. This chapter adds published articles, article details, safe comments, search, and pagination.

## Goal

By the end, visitors can read published articles, submit comments for moderation, search articles, and move through paginated results.

## What You Will Build

- Article list and detail data functions.
- Article cards.
- Safe article rendering.
- Comment submission form.
- Search input.
- Pagination controls.

## Beginner Concepts

- **Published article:** visible to visitors.
- **Draft article:** visible only to the owner.
- **Pending comment:** saved but not shown publicly yet.
- **Search:** narrowing results by user input.
- **Pagination:** loading a page of results instead of everything.
- **Unsafe HTML:** content that can execute unwanted scripts if rendered carelessly.

## Step By Step

### Step 1 - Create The Feature Folder

Create:

```txt
src/features/articles/
  articleTypes.ts
  articleApi.ts
  ArticleCard.tsx
  CommentForm.tsx
```

### Step 2 - Render Article Placeholders First

Use a small local array to render article cards. Confirm the page layout before fetching from Supabase.

### Step 3 - Fetch Published Articles

In `articleApi.ts`, create:

```txt
getPublishedArticles({ search, page })
getPublishedArticleBySlug(slug)
getApprovedComments(articleId)
submitComment(input)
```

Only published articles should be returned publicly. Only approved comments should be shown publicly.

### Step 4 - Add Search

Add a search input on the articles page. Start simple:

```txt
type search text
submit or debounce
request matching published articles
show no-results state when none match
```

Do not load every article and search in React once the database exists.

### Step 5 - Add Pagination

Show a small number of articles per page. Add Previous and Next buttons. Disable buttons when the visitor cannot move further.

### Step 6 - Render Article Body Safely

Choose a safe rendering path such as Markdown with a trusted renderer. Do not dangerously render raw HTML from user-editable content unless you have a sanitizing strategy.

### Step 7 - Submit Comments As Pending

The comment form should collect:

```txt
name
email, optional or private depending on your schema
message
```

New comments should save as `pending`. Public article pages should show only `approved` comments.

## Common Mistakes

| Mistake | Why it hurts | Fix |
|---|---|---|
| Showing pending comments immediately | Spam or unsafe content appears | Require moderation |
| Searching after loading all rows | Does not scale and may leak data | Search published rows in the query |
| Rendering raw HTML casually | Security risk | Use Markdown or sanitize |
| No pagination | Large tables become slow | Request one page at a time |

## Checks Before Moving On

- Published article list works.
- Draft article slug is not public.
- Search returns only published articles.
- Pagination does not load everything.
- New comments save as pending.
- Public page shows approved comments only.

## Learning Log

In `learning-log/07-articles-comments-search.md`, answer:

```txt
Why are articles useful in a portfolio?
Why do comments start as pending?
Why is raw HTML dangerous?
Why should search and pagination happen near the database?
```

## Definition Of Done

- [ ] Published article list renders.
- [ ] Article detail renders by slug.
- [ ] Drafts are private.
- [ ] Search works.
- [ ] Pagination works.
- [ ] Comment submission creates pending comments.
- [ ] Only approved comments are public.

Next: build the owner login and dashboard. -> **[Chapter 08 - Owner Auth And Admin Dashboard](08-owner-auth-and-admin-dashboard.md)**
