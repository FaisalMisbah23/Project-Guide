# Chapter 12 - Admin article CRUD

Articles are where the portfolio shows your thinking. Admin tools should make drafting and publishing calm.

> **Principle.** Publishing is a state change, not just a save button.

## Where we're headed

By the end, the owner can create drafts, edit articles, publish them, unpublish them, and delete them.

## Before you build

> **Apply this habit.** Read "Think About Real Users" in [Daily_Software_Development_Guidelines.md](../Daily_Software_Development_Guidelines.md), then define who each article is for.

## Step 1 - Create article admin page

Create:

```txt
src/pages/admin/
  AdminArticles.jsx
```

Show title, status, updated date, and publish date.

## Step 2 - Build article form

Fields:

```txt
title
slug
excerpt
body
tags
status
featured
published_at
```

## Step 3 - Save drafts

Drafts can be incomplete. They should never appear publicly.

## Step 4 - Publish articles

Publishing should require:

- title;
- slug;
- excerpt;
- body;
- publish date.

## Step 5 - Test public visibility

Verify:

- draft article is hidden;
- published article appears;
- unpublishing removes it from public pages.

## What your screen should show

Admin can manage articles. Public Articles page only shows published content.

## Small challenge

Add a "last edited" note in the admin list so stale drafts are obvious.

Suggested commit:

```bash
git commit -m "feat: add admin article crud"
```

## Definition of Done

- [ ] Article list exists in admin.
- [ ] Create draft works.
- [ ] Edit works.
- [ ] Publish/unpublish works.
- [ ] Delete requires confirmation.
- [ ] Public article route hides drafts.
- [ ] The UI says "Articles" consistently.

> **Log it.** In `learning-log/12-admin-article-crud.md`: How does draft status protect unfinished writing?

Next: upload images. -> **[Chapter 13 - Image uploads with Supabase Storage](13-image-uploads-with-supabase-storage.md)**
