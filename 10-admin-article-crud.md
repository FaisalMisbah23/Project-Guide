# Chapter 10 - Admin article CRUD

Articles are the portfolio owner's public thinking. Managing them needs more than a title and textarea. Articles need drafts, categories, tags, rich body content, preview, publishing, and comment moderation.

## Where we're headed

By the end, the owner can create, edit, publish, unpublish, tag, categorize, and manage comments for articles.

## The article trap

Bad:

```txt
title + raw HTML body
publish immediately
no preview
comments appear instantly
```

Problem: unsafe rendering can become an XSS risk, drafts can leak, and comments can become an abuse path.

Better:

```txt
draft body stored clearly
safe rendering path
explicit publish action
pending comment moderation
```

## Build it

Create `/admin/articles`. Add list, create, edit, and preview flows. Store title, slug, excerpt, body, category, tags, status, and image path.

Integrate a rich text editor, but do not let the editor decision hide the data decision. Know what format you store: Markdown, sanitized HTML, or structured JSON. The learner should be able to explain how it renders safely.

Add comment moderation. Pending comments can be approved, hidden, or deleted. Approved comments appear publicly; hidden/deleted ones do not.

## Do and don't

Do save drafts.

Don't trust raw HTML from users.

Do make tags useful and limited.

Don't create a tag system that requires editing code.

## Definition of Done

- [ ] Owner can create and edit article drafts.
- [ ] Owner can publish and unpublish articles.
- [ ] Article body uses a clear storage/rendering strategy.
- [ ] Category and tags are editable.
- [ ] Comments can be moderated.
- [ ] Draft articles are hidden from public reads.

> **Log it.** In `learning-log/10-admin-article-crud.md`, explain the risk of rendering article/comment content unsafely and how your approach reduces it.

Next: content exists, but it needs images that do not live in database rows. -> **[Chapter 11 - Image storage](11-image-storage.md)**
