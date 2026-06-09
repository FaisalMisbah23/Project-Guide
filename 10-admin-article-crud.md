# Chapter 10 - Admin article CRUD

Article admin looks like project admin until you notice the dangerous part: bodies and comments are content that become HTML on a page. The editor decision is a security decision wearing a writing-tool costume.

## The point of this chapter

Owner-only article drafts, editing, preview, publishing, unpublishing, tag/category management, safe rendering, and comment moderation.

## Step 1 - Choose Markdown first

Markdown is the required beginner choice for this course unless you deliberately document another path. It stores readable text and can be rendered without raw HTML.

## Step 2 - Make preview honest

Preview must use the same renderer as the public page. A preview that lies is worse than no preview because it hides publication bugs.

## Step 3 - Keep draft visibility boring

Draft means private. Published means public. Queries and RLS should agree. Do not invent extra visibility rules in the UI.

## Step 4 - Moderate comments in admin

Pending comments can be approved, hidden, archived, or deleted. Only approved comments render publicly.

> **📖 Mandatory read.** Read [react-markdown](https://github.com/remarkjs/react-markdown), [DOMPurify](https://github.com/cure53/DOMPurify) if considering HTML, [Supabase updates](https://supabase.com/docs/reference/javascript/update), and [MDN XSS](https://developer.mozilla.org/en-US/docs/Glossary/Cross-site_scripting). Required: the body format must be a deliberate safety choice.

> **💡 Hint.** Use the same `ArticleBody` component in preview and public detail. Duplication here is how unsafe rendering sneaks in.

## Definition of Done

- [ ] Owner can create and edit article drafts.
- [ ] Owner can publish and unpublish articles.
- [ ] Markdown-first or another documented safe body strategy is used.
- [ ] Preview and public pages share the same safe renderer.
- [ ] Tags and category are editable.
- [ ] Comments can be moderated.
- [ ] Draft articles remain hidden from public reads.

> **✍️ Log it (mandatory).** In `learning-log/10-admin-article-crud.md`: explain why raw HTML is risky, why Markdown is the beginner default, and why preview must match public rendering.

All boxes ticked? Then continue. The next chapter builds on this gate, not around it.

---

Next: content exists; now add images without stuffing files into database rows. -> **[Chapter 11 - Image storage](11-image-storage.md)**
