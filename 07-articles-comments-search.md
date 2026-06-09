# Chapter 07 - Articles, comments, search, and pagination

Projects show what you built. Articles show how you think. The moment you add article bodies and comments, you also add rendering safety, moderation, search, and pagination decisions.

## The point of this chapter

Published articles render safely, comments enter as pending, approved comments display publicly, and article lists support search and pagination without exposing drafts.

## Before you touch code

- Articles and comments tables exist.
- You have at least one draft and one published article.
- You understand Markdown is the beginner default.
- You have one approved and one pending comment seed row.

## Vocabulary for this chapter

- **Markdown.** Plain text syntax rendered into HTML safely by a renderer.
- **XSS.** Script injection caused by unsafe rendering of untrusted content.
- **Pagination.** Loading a limited page of results.
- **Moderation.** Owner review before public display.
- **Search term.** User input used to filter content and still treated as untrusted.

## Guided snippet or contract

This is a shape to aim for, not a finished solution to paste blindly:

```txt
Article public contract
  list: published articles only, paginated
  detail: one published article by slug
  body: Markdown rendered by shared ArticleBody
  comments: approved only
  comment submit: creates pending comment
```

## Step 1 - Choose a safe article body format

For this beginner build, Markdown is the recommended starting point. It stores readable text and avoids raw HTML by default. If you choose sanitized HTML later, you must own the sanitizing rules.

## Step 2 - Keep drafts private

Article queries should request published rows, and RLS should enforce published-only public reads. Search must not become a side door into drafts.

## Step 3 - Moderate comments

A visitor-submitted comment should start as `pending`. The owner approves it before it becomes public. That is slower than instant display and much safer.

## Step 4 - Paginate before the list grows

Pagination is not only performance polish. It is the habit of never asking the browser or database for more than the screen needs.

## Step 5 - Define the article feature folder

Use a shape like:

```txt
src/features/articles/
  articleTypes.ts
  articleApi.ts
  ArticleBody.tsx
  ArticlesPage.tsx
  ArticleDetailPage.tsx
  CommentForm.tsx
  CommentsList.tsx
```

Keep `ArticleBody` boring and safe. It should be the only place article Markdown becomes rendered UI.

## Step 6 - Compare body formats deliberately

| Format | Beginner fit | Risk |
|---|---|---|
| Markdown | best starting point | plugin choices still matter |
| Sanitized HTML | useful with rich editors | sanitizer must be correct |
| Raw HTML | avoid | XSS risk |
| Structured JSON | powerful later | more renderer work |

The course default is Markdown. If you choose otherwise, document why.

## Step 7 - Do it on your project

Build in this order:

1. Published article list with pagination.
2. Search that still filters to published rows.
3. Detail page by slug.
4. Safe body renderer.
5. Approved comments list.
6. Comment form that inserts pending comments.
7. Owner moderation comes later in admin.

## Prove it before moving on

Create an article body with headings, links, code, and suspicious HTML. Create approved and pending comments. Public pages should render the article safely, show approved comments only, and never expose drafts.

## If it breaks

| Symptom | Likely cause | Smallest next test |
|---|---|---|
| Suspicious HTML renders | Renderer allows raw HTML or unsafe plugin | Disable raw HTML and test the snippet again. |
| Draft appears in search | Search query forgot published filter or RLS too broad | Search for a unique draft word as signed-out user. |
| Pending comments appear | Comment query ignores approved status | Query comments for one article and compare statuses. |
| Pagination repeats/skips rows | Ordering is unstable | Add deterministic order such as `created_at` plus `id`. |

## What you should be able to explain

- Why Markdown is easier than raw HTML for beginners.
- Why pending comments are safer than instant publishing.
- Why search must still obey visibility rules.

## The slower beginner path

If this chapter feels too large, split the articles and comments feature into one sitting per checkpoint. The goal is not to finish fast; the goal is to finish with proof.

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

> **📖 Mandatory read.** Read [react-markdown](https://github.com/remarkjs/react-markdown), [MDN cross-site scripting](https://developer.mozilla.org/en-US/docs/Glossary/Cross-site_scripting), [Supabase JavaScript client](https://supabase.com/docs/reference/javascript/introduction), and [Supabase RLS](https://supabase.com/docs/guides/database/postgres/row-level-security). Required: safe rendering and public/private visibility meet in this chapter.

> **💡 Hint.** Create one article containing a harmless code block and one suspicious HTML snippet. The code should display; the suspicious HTML should not execute.

## Definition of Done

- [ ] Published article list and detail pages work.
- [ ] Draft articles are hidden from public reads and search.
- [ ] Article body uses a documented safe rendering strategy.
- [ ] New comments are pending by default.
- [ ] Only approved comments display publicly.
- [ ] Search and pagination work without loading everything.

> **✍️ Log it (mandatory).** In `learning-log/07-articles-comments-search.md`: explain raw HTML risk, why comments start pending, and why search must still respect published-only visibility.

All boxes ticked? Then continue. The next chapter builds on this gate, not around it.

---

Next: public content works; now build the private door for the owner. -> **[Chapter 08 - Owner auth and admin dashboard](08-owner-auth-and-admin-dashboard.md)**
