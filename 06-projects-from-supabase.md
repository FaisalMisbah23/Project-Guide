# Chapter 06 - Projects From Supabase

The projects page can start with a local array, but the finished portfolio should load published projects from Supabase while keeping drafts private.

## Goal

By the end, project list and detail pages read published projects from Supabase and handle loading, empty, error, and not-found states.

## What You Will Build

- Project types.
- Project API functions.
- Project card component.
- Project list page.
- Project detail page.
- Privacy checks for draft projects.

## Beginner Concepts

- **API module:** a file that fetches data.
- **Component:** a reusable UI piece.
- **Mapper:** code that converts database field names into UI-friendly names.
- **Loading state:** what the visitor sees while data is being fetched.
- **Draft:** content that exists but is not public.

## Step By Step

### Step 1 - Start With The Local Array

Before fetching, render project cards from `src/data/starterProjects.ts`. This proves the UI works without database complexity.

Each item should include:

```txt
title
slug
summary
technologies
featured
```

### Step 2 - Create The Feature Folder

Create:

```txt
src/features/projects/
  projectTypes.ts
  projectApi.ts
  ProjectCard.tsx
```

Pages may stay in `src/pages/` or move into the feature folder, but keep fetching code out of visual cards.

### Step 3 - Define The UI Type

In `projectTypes.ts`, define the shape your UI wants:

```ts
export type Project = {
  id: string;
  slug: string;
  title: string;
  summary: string;
  technologies: string[];
  featured: boolean;
  imagePath: string | null;
  imageAlt: string | null;
};
```

### Step 4 - Write Supabase Read Functions

In `projectApi.ts`, create:

```txt
getPublishedProjects()
getPublishedProjectBySlug(slug)
```

Both functions must request only `status = 'published'`. RLS should enforce the same rule.

### Step 5 - Replace Local Data With Supabase Data

Update the projects page:

```txt
start loading
call getPublishedProjects
show cards when rows exist
show empty state when no rows exist
show error state when request fails
```

### Step 6 - Build Detail Fetching

On `/projects/:slug`, read the slug from the route, fetch one published project, and show:

```txt
loading
project details
not found when null
error when request fails
```

### Step 7 - Prove Draft Privacy

Create one published project and one draft project. Check:

```txt
/projects shows only published projects
/projects/draft-slug shows not found
signed-out Supabase query cannot reveal the draft
```

## Common Mistakes

| Mistake | Why it hurts | Fix |
|---|---|---|
| Fetching all rows then filtering in React | Drafts reach the browser | Filter in query and enforce RLS |
| Querying inside the card | UI becomes hard to reuse | Fetch in API/page layer |
| No empty state | Empty database looks broken | Add a friendly empty message |
| Detail page never stops loading | Error/null path does not clear loading | Handle all outcomes |

## Checks Before Moving On

- Local project cards worked first.
- Supabase project list works.
- Project detail works by slug.
- Draft rows are not public.
- Loading, empty, error, and not-found states exist.

## Learning Log

In `learning-log/06-projects-from-supabase.md`, answer:

```txt
Why did the UI start with a local array?
Why should cards not query Supabase?
Why is hiding drafts in React too late?
How did you prove the draft stayed private?
```

## Definition Of Done

- [ ] Published projects load from Supabase.
- [ ] Draft projects do not appear.
- [ ] Detail pages fetch by slug.
- [ ] Missing or draft slug shows not found.
- [ ] UI handles loading, empty, and error states.
- [ ] Data is mapped before rendering.

Next: build articles and comments. -> **[Chapter 07 - Articles, Comments, Search, And Pagination](07-articles-comments-search.md)**
