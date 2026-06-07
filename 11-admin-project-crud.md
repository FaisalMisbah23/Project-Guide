# Chapter 11 - Admin project CRUD

The owner should not edit SQL rows by hand forever. This chapter creates admin tools for managing project content.

> **Principle.** Admin tools should make correct content easier than messy content.

## Where we're headed

By the end, the owner can create, edit, publish, unpublish, and delete projects from the admin area.

## Before you build

> **Reading before this step.** Read Supabase JavaScript database docs: https://supabase.com/docs/reference/javascript/select. Focus on insert, update, delete, and error handling.

> **Apply this habit.** Read "Keep Components Focused" in [Daily_Software_Development_Guidelines.md](../Daily_Software_Development_Guidelines.md), then split form, table, and API responsibilities.

## Step 1 - Create project admin page

Create:

```txt
src/pages/admin/
  AdminProjects.jsx
```

Show all projects, including drafts.

## Step 2 - Create project form

Fields should match the data model. Required fields:

```txt
title
slug
summary
status
```

Long case-study fields can be optional at first, but the Definition of Done requires at least one complete project.

## Step 3 - Add create and update

Create and update should show success and error states.

Bad:

```txt
Save button does nothing visible.
```

Better:

```txt
Save button shows loading, then success or a specific error.
```

## Step 4 - Add publish/unpublish

Publishing should require enough public content:

- title;
- slug;
- summary;
- at least one case-study field.

## Step 5 - Add delete with caution

Use a confirmation step. Deleting content is destructive.

## What your screen should show

Admin can manage projects. Public pages update when a project is published.

## Small challenge

Add a "preview public page" link for published projects.

Suggested commit:

```bash
git commit -m "feat: add admin project crud"
```

## Definition of Done

- [ ] Admin project list shows drafts and published projects.
- [ ] Create works.
- [ ] Edit works.
- [ ] Publish/unpublish works.
- [ ] Delete requires confirmation.
- [ ] Public page reflects published changes.
- [ ] RLS blocks writes when signed out.

> **Log it.** In `learning-log/11-admin-project-crud.md`: What validation protects project quality? Which errors did you test?

Next: manage articles. -> **[Chapter 12 - Admin article CRUD](12-admin-article-crud.md)**
