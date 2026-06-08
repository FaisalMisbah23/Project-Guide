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

## New ideas before you build

### Rich text storage

**Real-life analogy:** the same document can be saved as plain text, Markdown, HTML, or a design file. The format decides how easy it is to edit and safely display.

**General idea:** choose how article bodies are stored before choosing the editor. Markdown is simpler. HTML must be sanitized. Structured JSON is powerful but more complex.

```txt
Markdown: ## Heading
HTML: <h2>Heading</h2>
JSON: { "type": "heading", "level": 2 }
```

Study more: [Frontend Interview Questions - HTML and React](https://resources.devweekends.com/resources/frontend-interview-qs)

### Draft and published states

**Real-life analogy:** writers keep drafts private until the article is ready.

**General idea:** status fields let the owner save unfinished work without showing it publicly. Queries and RLS should both respect the status.

```ts
await supabase
  .from("articles")
  .select("*")
  .eq("status", "published");
```

Study more: [Database Engineering - Case Studies](https://resources.devweekends.com/courses/database-engineering/case-studies)

## Daily guideline

From `Daily_Software_Development_Guidelines.md`: **design for failure**. Assume a draft save can fail, an article preview can render badly, and moderation actions can be clicked by mistake. Preserve the owner's text while showing the error, and require confirmation for destructive comment actions.

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

## Between chapters

Optional pause. Pick **one or two**, not all of them. Skip the rest without guilt if your Definition of Done is complete.

**Reading:** review [Frontend Interview Questions](https://resources.devweekends.com/resources/frontend-interview-qs), focusing on HTML, React, and security questions.

**Quiz:** what is safer to render by default: raw HTML from a user, sanitized HTML, Markdown through a trusted renderer, or plain text? Explain the tradeoff.

**Content exercise:** create an article with headings, links, code, and an intentionally suspicious HTML snippet. Confirm the final rendering is readable and safe.

**Moderation exercise:** submit three comments: helpful, empty, and abusive. Confirm only approved comments appear publicly.

**Comparison:** Markdown vs HTML: Markdown is easier for writing and can be rendered safely with the right tools. HTML is more flexible but dangerous if user-submitted content is injected without sanitizing.

**Big word alert:** **XSS** means cross-site scripting. It is when unsafe content lets an attacker run JavaScript in someone else's browser.

**Diagram:**

```txt
Article draft
  -> safe body format
  -> preview renderer
  -> publish action
  -> public article page

Comment submit
  -> pending
  -> owner moderates
  -> approved comments render
```

Next: content exists, but it needs images that do not live in database rows. -> **[Chapter 11 - Image storage](11-image-storage.md)**
