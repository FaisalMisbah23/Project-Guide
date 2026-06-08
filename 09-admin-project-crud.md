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

## New ideas before you build

### CRUD

**Real-life analogy:** managing a notebook means you can add a note, read it, edit it, and remove it. CRUD is the software version: create, read, update, delete.

**General idea:** admin project management needs all four operations, plus validation, confirmation, and a draft/published status.

```ts
await supabase.from("projects").insert(projectInput);
await supabase.from("projects").select("*");
await supabase.from("projects").update(changes).eq("id", id);
await supabase.from("projects").delete().eq("id", id);
```

Study more: [Frontend Interview Questions - React Fundamentals](https://resources.devweekends.com/resources/frontend-interview-qs)

### Form state

**Real-life analogy:** a paper form keeps what you wrote in each box until you submit it. React form state stores those boxes in code.

**General idea:** controlled inputs keep form values in state, which lets you validate, save drafts, and show errors.

```tsx
const [title, setTitle] = useState("");

<input
  value={title}
  onChange={(event) => setTitle(event.target.value)}
/>;
```

Study more: [React Crash Course - Components and Props](https://resources.devweekends.com/courses/react-crash-course/02-components-props)

## Daily guideline

From `Daily_Software_Development_Guidelines.md`: **protect against double submissions** and **think about real users**. Disable the save button while a project is being created or updated. Show success or failure clearly. A user who clicks twice because nothing happened should not accidentally create duplicate projects.

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

## Between chapters

**Assignment:** create a manual test checklist for project CRUD: create draft, edit draft, publish, unpublish, delete/archive, invalid URL, duplicate slug, signed-out write attempt.

**Blog prompt:** write three paragraphs on `Why save does not always mean publish`.

**CRUD exercise:** perform the full lifecycle on one project: create draft, preview, publish, edit, unpublish, archive/delete. After each step, check both the admin page and public page.

**Validation exercise:** submit the project form with an empty title, bad URL, duplicate slug, and too-short summary. The form should fail before creating broken public content.

**Comparison:** create vs update: create makes a new row. Update changes an existing row. A form can look similar for both, but the database operation and edge cases are different.

**Big word alert:** **CRUD** means Create, Read, Update, Delete. It is the basic set of actions most admin tools need.

**Motivation pause:** from `Software_Engineering_Community_Affirmations.md`: "Every project teaches something valuable." CRUD looks ordinary, but this is where you learn how real owner workflows are protected.

Next: projects are manageable. Now give the owner the same power over articles. -> **[Chapter 10 - Admin article CRUD](10-admin-article-crud.md)**
