# Chapter 07 - Articles, comments, search, and pagination

Projects prove that you can ship. Articles prove that you can explain decisions. For a software engineer, that matters. A clear article about a bug, tradeoff, or system design decision can be stronger than another decorative section.

## Where we're headed

By the end, the public site has articles with categories, tags, comments, pagination, and search powered by Supabase queries.

## The content trap

Bad:

```txt
private notes
random markdown snippets
no categories
no search
all posts loaded at once
```

Problem: visitors cannot browse the thinking. The owner cannot build a useful writing habit. Loading every article at once also teaches the wrong scaling habit.

Better:

```txt
articles with status, category, tags, excerpt, slug
approved comments only
search and pagination handled by queries
```

Use the word **Articles** throughout the app. "Learning notes" sounds internal. "Articles" sounds publishable.

## Build it

Create article list and detail routes. Query only published articles. Add category and tag filters. Add search as a Supabase query condition rather than filtering only in memory.

Use pagination. Cursor pagination is stronger for large changing lists, but page/limit pagination is acceptable for this portfolio if the learner can explain the tradeoff.

For comments, public visitors may submit a comment as `pending`. Only approved comments render publicly. This is not just moderation; it is abuse control.

## Rich text

Add a rich text editor in the admin chapter, but decide the storage format now. Store article body in a format you can render safely. Do not blindly inject HTML without sanitizing. If you store Markdown, render it with a trusted parser and safe configuration.

## Mandatory read

Read about React lists/keys if not already done in Chapter 06. Read a short article on pagination and one on sanitizing user-generated content. Required: comments and rich article bodies introduce data that can harm readers if rendered carelessly.

## Definition of Done

- [ ] Article list renders published articles from Supabase.
- [ ] Article details load by slug.
- [ ] Categories and tags work.
- [ ] Search uses Supabase queries.
- [ ] Pagination exists.
- [ ] Comments can be submitted as pending and only approved comments render.
- [ ] Draft articles are hidden publicly.

> **Log it.** In `learning-log/07-articles-comments-search.md`, explain why pending comments should not appear immediately and why article search should not require loading every row.

Next: public content works. Now build the private door for the owner. -> **[Chapter 08 - Owner auth and admin dashboard](08-owner-auth-and-admin-dashboard.md)**
