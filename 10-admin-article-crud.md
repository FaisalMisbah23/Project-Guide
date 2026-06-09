# Chapter 10 - Admin article CRUD

Article admin looks like project admin until you notice the dangerous part: bodies and comments are content that become HTML on a page. The editor decision is a security decision wearing a writing-tool costume.

## The point of this chapter

Owner-only article drafts, editing, preview, publishing, unpublishing, tag/category management, safe rendering, and comment moderation.

## Before you touch code

- Public article pages exist.
- Markdown renderer is chosen or an alternative is documented.
- Owner auth works.
- Comment statuses exist.

## Vocabulary for this chapter

- **Preview.** Admin view of how content will render publicly.
- **Sanitize.** Remove unsafe HTML before rendering.
- **Shared renderer.** One component used by preview and public page.
- **Moderation action.** Approve, hide, archive, or delete a comment.

## Guided snippet or contract

This is a shape to aim for, not a finished solution to paste blindly:

```txt
Admin article contract
  create draft
  edit draft or published article
  preview using public renderer
  publish/unpublish
  edit category and tags
  moderate pending comments
```

## Step 1 - Choose Markdown first

Markdown is the required beginner choice for this course unless you deliberately document another path. It stores readable text and can be rendered without raw HTML.

## Step 2 - Make preview honest

Preview must use the same renderer as the public page. A preview that lies is worse than no preview because it hides publication bugs.

## Step 3 - Keep draft visibility boring

Draft means private. Published means public. Queries and RLS should agree. Do not invent extra visibility rules in the UI.

## Step 4 - Moderate comments in admin

Pending comments can be approved, hidden, archived, or deleted. Only approved comments render publicly.

## Step 5 - Define the admin article feature folder

```txt
src/features/adminArticles/
  adminArticleTypes.ts
  adminArticleApi.ts
  validateArticleInput.ts
  ArticleEditor.tsx
  ArticlePreview.tsx
  CommentModerationPanel.tsx
```

The editor, preview, and public renderer should agree on the body format.

## Step 6 - Write the article lifecycle

```txt
draft -> preview -> publish -> public read
published -> edit -> republish
published -> unpublish -> draft/private
comments: pending -> approved or hidden
```

This lifecycle is why `status` exists. Do not replace it with scattered booleans.

## Step 7 - Do it on your project

Build in this order:

1. Admin article list.
2. Draft create form.
3. Markdown editor textarea.
4. Shared safe preview renderer.
5. Publish/unpublish actions.
6. Tag and category fields.
7. Comment moderation table.
8. Suspicious content test.

## Prove it before moving on

Write one article containing Markdown headings, a link, code, and suspicious HTML. Preview it, publish it, and open the public article. The preview and public page should match, and suspicious HTML should not execute.

## If it breaks

| Symptom | Likely cause | Smallest next test |
|---|---|---|
| Preview differs from public page | Different renderers or plugins are used | Make preview call the same `ArticleBody` component. |
| Raw HTML executes | Unsafe renderer settings | Disable raw HTML or sanitize before render. |
| Draft leaks | Query or RLS missing published filter | Open draft slug while signed out. |
| Tag list becomes messy | Tags are free-form without limits | Add validation for count, length, and duplicates. |

## What you should be able to explain

- Why the editor format is a security decision.
- Why Markdown is the recommended beginner default.
- Why comment moderation belongs in admin.

## The slower beginner path

If this chapter feels too large, split the admin article CRUD feature into one sitting per checkpoint. The goal is not to finish fast; the goal is to finish with proof.

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
