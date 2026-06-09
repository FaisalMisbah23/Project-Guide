# Chapter 09 - Admin project CRUD

Now the owner gets real power: create, edit, publish, unpublish, and archive projects. CRUD looks basic until you add validation, duplicate slugs, public visibility, ownership policies, and two tabs editing the same row.

## The point of this chapter

An owner-only project management flow with validated forms, draft/published states, safer archive behavior, and a concurrency guard based on reliable `updated_at`.

## Step 1 - Confirm `updated_at` is real

Before using `updated_at` as a guard, prove it changes on update. A stale timestamp gives false confidence and makes concurrency handling theater.

## Step 2 - Validate before saving

Create a form shape for what the owner edits. Validate title, slug, summary, URLs, technologies, status, and featured flag before mutation. Database constraints still stay in place.

## Step 3 - Prefer archive over hard delete

Hard delete is permanent and can break public links. Archive is the safer default because it removes public visibility while preserving history.

## Step 4 - Guard stale edits

When loading an edit form, remember `updated_at`. On save, update only when the row still has that same value. If no row updates, tell the owner to reload because the project changed elsewhere.

> **📖 Mandatory read.** Read [Supabase inserts and updates](https://supabase.com/docs/reference/javascript/insert), [MDN form validation](https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Forms/Form_validation), and [PostgreSQL unique constraints](https://www.postgresql.org/docs/current/ddl-constraints.html#DDL-CONSTRAINTS-UNIQUE-CONSTRAINTS). Required: admin forms need UI validation, database constraints, and clear mutation behavior.

> **💡 Hint.** Test a duplicate slug on purpose. A database error should become a useful field message, not a mysterious red wall.

## Definition of Done

- [ ] Owner can list projects.
- [ ] Owner can create and edit drafts.
- [ ] Owner can publish and unpublish projects.
- [ ] Archive is available and safer than hard delete by default.
- [ ] Invalid URLs, empty titles, short summaries, and duplicate slugs fail clearly.
- [ ] Signed-out writes fail through RLS.
- [ ] Stale `updated_at` updates show a reload-before-saving message.

> **✍️ Log it (mandatory).** In `learning-log/09-admin-project-crud.md`: explain why archive is safer than hard delete, and why the concurrency guard depends on trustworthy `updated_at`.

All boxes ticked? Then continue. The next chapter builds on this gate, not around it.

---

Next: projects are manageable; now give articles the same owner workflow. -> **[Chapter 10 - Admin article CRUD](10-admin-article-crud.md)**
