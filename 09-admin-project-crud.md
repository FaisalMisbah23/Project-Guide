# Chapter 09 - Admin project CRUD

Now the owner gets real power: create, edit, publish, unpublish, and archive projects. CRUD looks basic until you add validation, duplicate slugs, public visibility, ownership policies, and two tabs editing the same row.

## The point of this chapter

An owner-only project management flow with validated forms, draft/published states, safer archive behavior, and a concurrency guard based on reliable `updated_at`.

## Before you touch code

- Owner login works.
- Owner can read project rows through RLS.
- `updated_at` changes on update.
- Public project pages already hide drafts.

## Vocabulary for this chapter

- **CRUD.** Create, read, update, delete/archive workflow.
- **Draft.** Saved but not public.
- **Published.** Visible to public routes.
- **Archive.** Hide while preserving history.
- **Concurrency.** Two edits happening close enough to conflict.

## Guided snippet or contract

This is a shape to aim for, not a finished solution to paste blindly:

```ts
// form and mutation contract shapes
type ProjectFormValues = {
  title: string;
  slug: string;
  summary: string;
  description: string;
  technologies: string[];
  demoUrl: string;
  codeUrl: string;
  featured: boolean;
  status: 'draft' | 'published' | 'archived';
};

validateProjectInput(values) -> fieldErrors;
updateProject(id, values, lastSeenUpdatedAt) -> updated row or stale-edit error;
```

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

## If it breaks

| Symptom | Likely cause | Smallest next test |
|---|---|---|
| Duplicate slug creates ugly error | Database error is not mapped to field message | Catch unique violation and show slug-specific message. |
| Public page does not update after publish | Status value or public query mismatch | Inspect row status and public query filter. |
| Stale edit overwrites newer edit | `updated_at` guard missing or timestamp stale | Run the two-tab test again. |
| Signed-out create works | RLS policy too broad | Try insert from anon client and fix policy immediately. |

## What you should be able to explain

- Why archive is safer than hard delete.
- Why validation and database constraints both matter.
- Why `updated_at` must update automatically or consistently.
- How the two-tab stale edit test works.

## The slower beginner path

If this chapter feels too large, split the admin project CRUD feature into one sitting per checkpoint. The goal is not to finish fast; the goal is to finish with proof.

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
