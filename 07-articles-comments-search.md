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

## New ideas before you build

### Search

**Real-life analogy:** asking a librarian for books about React is better than carrying every book home and searching page by page.

**General idea:** let Supabase search the rows. Do not load every article into React just to filter in the browser.

```ts
const { data } = await supabase
  .from("articles")
  .select("*")
  .eq("status", "published")
  .ilike("title", `%${searchTerm}%`);
```

Study more: [Frontend Interview Questions - JavaScript and React](https://resources.devweekends.com/resources/frontend-interview-qs)

### Pagination

**Real-life analogy:** books use pages so you do not read the whole library at once.

**General idea:** pagination loads a smaller set of rows at a time. It keeps the app faster and easier to browse.

```ts
const from = page * pageSize;
const to = from + pageSize - 1;

const { data } = await supabase
  .from("articles")
  .select("*")
  .range(from, to);
```

Study more: [Frontend Interview Questions - Performance](https://resources.devweekends.com/resources/frontend-interview-qs)

### Sanitizing user content

**Real-life analogy:** if visitors can write on a public wall, you still check the writing before displaying it.

**General idea:** never blindly render user-submitted HTML. Comments and rich article bodies can become unsafe if scripts are allowed through.

```tsx
// Prefer safe Markdown rendering or sanitized HTML.
<ArticleBody markdown={article.body} />
```

Study more: [Frontend Interview Questions - Security and React](https://resources.devweekends.com/resources/frontend-interview-qs)

## Daily guideline

From `Daily_Software_Development_Guidelines.md`: **think about scalability** and **test edge cases**. Search and pagination are not only "nice features"; they prevent the app from loading every article forever. Test empty results, long search terms, no comments, many comments, and deleted article slugs.

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

## Between chapters

Optional pause. Pick **one or two**, not all of them. Skip the rest without guilt if your Definition of Done is complete.

**Blog prompt:** draft an article titled `Why I do not load every row into React`. Explain search, pagination, and the difference between database work and browser work.

**Quiz:** why are pending comments hidden? Choose two answers: moderation, performance, abuse control, prettier UI. Defend your choices.

**Performance exercise:** seed at least 30 articles, then compare loading all rows vs loading one page. Write down what changes in query size, UI speed, and mental model.

**Search exercise:** search for a word that matches no articles, one article, and many articles. Verify each result state is clear.

**Comparison:** filtering in React vs filtering in Supabase: React filtering means the browser already received the rows. Supabase filtering means the database returns only the rows the page needs.

**Big word alert:** **pagination** means splitting a large result into smaller pages or chunks so the app does not load everything at once.

**Diagram:**

```txt
Search input + filters + page number
  -> Supabase query
  -> published articles only
  -> limited page of rows
  -> article list UI
```

Next: public content works. Now build the private door for the owner. -> **[Chapter 08 - Owner auth and admin dashboard](08-owner-auth-and-admin-dashboard.md)**
