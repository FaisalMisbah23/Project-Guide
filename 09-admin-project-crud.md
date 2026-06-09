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

## Step 5 - Define the admin project feature folder

Use a folder that keeps form, validation, and mutations together:

```txt
src/features/adminProjects/
  adminProjectTypes.ts
  adminProjectApi.ts
  validateProjectInput.ts
  AdminProjectsPage.tsx
  ProjectForm.tsx
  ProjectRowActions.tsx
```

This is the admin-side mirror of the public projects feature. Public reads and owner writes should not blur together.

## Step 6 - Write the mutation contract

Use clear functions instead of inline Supabase calls everywhere:

```ts
listOwnerProjects()
createProjectDraft(values)
updateProject(id, values, lastSeenUpdatedAt)
publishProject(id)
unpublishProject(id)
archiveProject(id)
```

The names describe intent. The implementation can use Supabase, but the UI should call verbs the owner understands.

## Step 7 - Compare delete choices

| Action | Public effect | History effect | Beginner default |
|---|---|---|---|
| hard delete | row disappears | history can break | avoid for published work |
| archive | hidden publicly | row remains | use this |
| unpublish | hidden publicly | draft/editable | use for temporary removal |

Hard delete is not evil. It is just rarely the safest first behavior for portfolio work that may have links, images, comments, or analytics.

## Step 8 - Do it on your project

Build this lifecycle in order:

1. Owner list view with status filters.
2. Create draft form.
3. Edit draft form.
4. Publish action.
5. Unpublish action.
6. Archive action with confirmation.
7. Duplicate slug and invalid URL messages.
8. Stale edit guard using `updated_at`.

## Prove it before moving on

Open two tabs on the same project. Save a change in tab A. Try saving older data in tab B. Tab B should not silently overwrite tab A; it should ask the owner to reload.

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
