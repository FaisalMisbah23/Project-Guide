# Chapter 09 - Admin project CRUD

The owner can sign in. Now the admin dashboard needs its first real job: managing portfolio projects. CRUD means create, read, update, and delete, but the production-shaped version includes validation, publish states, confirmations, and public preview checks.

## Where we're headed

By the end, the owner can add, edit, publish, unpublish, and delete portfolio projects from the admin dashboard.

## The CRUD trap

Bad:

```txt
one form
no validation
delete button immediately deletes
all projects public by default
```

Problem: half-written projects leak publicly, destructive actions are too easy, and invalid records create broken public pages.

Better:

```txt
draft first
validate required fields
publish deliberately
confirm delete
preview public result
```

## Build it

Create `/admin/projects`. Load all owner-visible projects, including drafts. Add a project form with title, slug, summary, body/description, technologies, links, featured flag, status, and image path placeholder.

Validation should catch missing title, missing slug, duplicate slug, invalid URLs, and weak summaries. A project summary should say what changed, not only what tech was used.

Add create and edit flows. Add publish/unpublish as a status update. Add delete with confirmation. If you want a safer production habit, use archive or soft delete instead of hard delete.

## Real developer mistake

Mistake: publish automatically after saving.

Why it is bad: the owner may save an incomplete draft while still writing.

Fix: save as draft by default, then publish with a separate deliberate action.

## Definition of Done

- [ ] Admin project list shows owner-visible projects.
- [ ] Owner can create a draft project.
- [ ] Owner can edit project fields.
- [ ] Owner can publish and unpublish.
- [ ] Delete or archive requires confirmation.
- [ ] Signed-out users cannot write projects.
- [ ] Public page shows only published projects.

> **Log it.** In `learning-log/09-admin-project-crud.md`, explain why draft/published status is safer than making every saved project public.

Next: projects are manageable. Now give the owner the same power over articles. -> **[Chapter 10 - Admin article CRUD](10-admin-article-crud.md)**
