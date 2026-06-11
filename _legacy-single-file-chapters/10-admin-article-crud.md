# Chapter 10 - Admin Article CRUD

Projects show proof of building. Articles show proof of thinking. The owner needs a private workflow for drafts, previews, publishing, and comment moderation.

## Goal

By the end, the owner can create, edit, preview, publish, and manage articles from the admin dashboard.

## What You Will Build

- Admin article list.
- Article editor form.
- Draft and publish flow.
- Preview route or preview panel.
- Comment moderation controls.

## Beginner Concepts

- **Draft:** article not visible publicly.
- **Preview:** owner-only view before publishing.
- **Markdown:** plain-text writing format that can render as HTML.
- **Moderation:** approving or rejecting visitor comments.
- **XSS:** unsafe script injection through rendered content.

## Step By Step

### Step 1 - Create Admin Article Files

Create:

```txt
src/features/adminArticles/
  adminArticleTypes.ts
  adminArticleApi.ts
  ArticleEditor.tsx
  AdminArticleList.tsx
  CommentModerationList.tsx
```

### Step 2 - Build The Article List

Show all owner-visible articles:

```txt
draft
published
archived, if supported
```

Include title, status, updated date, and edit link.

### Step 3 - Build The Editor

The editor should include:

```txt
title
slug
excerpt
body
tags
status
published_at
```

Start with simple form controls. Fancy editors can wait.

### Step 4 - Add Draft Save

Saving a draft should not make the article public. Confirm `/articles/draft-slug` is still not found when signed out.

### Step 5 - Add Preview

Preview should let the owner read the article before publishing. It must not create a public URL that exposes drafts.

### Step 6 - Add Publish

Publishing should set the correct status and publication date. The public article list should then show the article.

### Step 7 - Add Comment Moderation

Create a moderation screen or section where the owner can:

```txt
see pending comments
approve comments
reject or archive comments
```

Only approved comments should appear publicly.

## Common Mistakes

| Mistake | Why it hurts | Fix |
|---|---|---|
| Preview route is public | Drafts leak | Protect preview routes |
| Raw HTML rendering | XSS risk | Use safe Markdown rendering |
| Publishing without date | Sorting becomes unclear | Set `published_at` |
| Deleting comments immediately | Loses moderation history | Use statuses |

## Checks Before Moving On

- Owner can create drafts.
- Owner can edit drafts.
- Preview is owner-only.
- Published articles appear publicly.
- Draft articles stay private.
- Pending comments can be approved.

## Learning Log

In `learning-log/10-admin-article-crud.md`, answer:

```txt
Why does an article need a draft state?
How is preview different from public detail?
Why should comments be moderated?
How did you prove a draft article stayed private?
```

## Definition Of Done

- [ ] Owner can create articles.
- [ ] Owner can edit articles.
- [ ] Owner can preview safely.
- [ ] Owner can publish.
- [ ] Owner can moderate comments.
- [ ] Public pages show only published/approved content.

Next: add image uploads. -> **[Chapter 11 - Image Storage](11-image-storage.md)**
