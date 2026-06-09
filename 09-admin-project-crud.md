# Chapter 09 - Admin Project CRUD

The owner can enter the admin area. Now the owner needs to create, edit, publish, unpublish, and archive projects without editing source code.

## Goal

By the end, project content is manageable from the admin dashboard.

## What You Will Build

- Admin project list.
- Project form.
- Create action.
- Edit action.
- Publish/unpublish action.
- Archive action.
- Validation and duplicate-slug handling.

## Beginner Concepts

- **CRUD:** create, read, update, delete. This course usually archives instead of deleting.
- **Validation:** checking input before saving.
- **Mutation:** a database write.
- **Slug:** URL-safe identifier.
- **Archive:** hide from active use without destroying history.

## Step By Step

### Step 1 - Create Admin Project Files

Create:

```txt
src/features/adminProjects/
  adminProjectTypes.ts
  adminProjectApi.ts
  ProjectForm.tsx
  AdminProjectList.tsx
```

### Step 2 - Build The List First

Show all owner-visible projects in `/admin/projects`, including drafts, published, and archived rows. Public pages still show only published rows.

### Step 3 - Build The Form

The form should include:

```txt
title
slug
summary
description
technologies
project link
repository link
featured flag
status
image path / image alt later
```

Start with text inputs and textareas. Improve UI later.

### Step 4 - Add Create

On submit:

```txt
validate required fields
insert project
show success
return to project list or stay on edit page
```

### Step 5 - Add Edit

Load the existing project by id or slug. Fill the form. Save changes with an update mutation.

### Step 6 - Add Status Actions

Add buttons for:

```txt
publish
unpublish to draft
archive
```

Prefer archive over hard delete for v1 because links, images, and analytics may reference old projects.

### Step 7 - Test Errors

Try:

```txt
empty title
duplicate slug
invalid status
signed-out insert
two tabs editing the same row, if using updated_at checks
```

## Common Mistakes

| Mistake | Why it hurts | Fix |
|---|---|---|
| Only validating in React | Bad writes can still happen | Keep database constraints |
| Hard deleting by default | History and links can break | Archive first |
| Duplicate slug shows raw error | Owner cannot fix easily | Convert to a field message |
| Public query sees drafts | RLS or query is too broad | Retest signed-out reads |

## Checks Before Moving On

- Admin project list shows all owner rows.
- Create works.
- Edit works.
- Publish/unpublish works.
- Archive works.
- Duplicate slug is handled.
- Signed-out users cannot write.

## Learning Log

In `learning-log/09-admin-project-crud.md`, answer:

```txt
Why does the admin list show drafts while the public list does not?
Why is archive safer than hard delete for v1?
Which validation belongs in React?
Which validation belongs in the database?
```

## Definition Of Done

- [ ] Owner can create projects.
- [ ] Owner can edit projects.
- [ ] Owner can publish and unpublish.
- [ ] Owner can archive.
- [ ] Validation errors are understandable.
- [ ] RLS blocks unauthorized writes.

Next: add article management. -> **[Chapter 10 - Admin Article CRUD](10-admin-article-crud.md)**
