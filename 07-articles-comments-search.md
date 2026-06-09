# Chapter 07 - Articles, comments, search, and pagination

Projects show what you built. Articles show how you think. The moment you add article bodies and comments, you also add rendering safety, moderation, search, and pagination decisions.

## The point of this chapter

Published articles render safely, comments enter as pending, approved comments display publicly, and article lists support search and pagination without exposing drafts.

## Step 1 - Choose a safe article body format

For this beginner build, Markdown is the recommended starting point. It stores readable text and avoids raw HTML by default. If you choose sanitized HTML later, you must own the sanitizing rules.

## Step 2 - Keep drafts private

Article queries should request published rows, and RLS should enforce published-only public reads. Search must not become a side door into drafts.

## Step 3 - Moderate comments

A visitor-submitted comment should start as `pending`. The owner approves it before it becomes public. That is slower than instant display and much safer.

## Step 4 - Paginate before the list grows

Pagination is not only performance polish. It is the habit of never asking the browser or database for more than the screen needs.

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
