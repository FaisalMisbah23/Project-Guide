# Chapter 06 - Projects from Supabase

The projects page is where the portfolio starts proving skill. Hard-coded cards are useful for sketching, but the finished app should read published work from the database while keeping drafts private.

## The point of this chapter

Published projects load from Supabase into public list and detail pages, with loading, empty, error, filter, and missing-project states.

## Step 1 - Keep data access out of the card

Create a project feature folder. Put Supabase queries in a data module and rendering in components. A card should display a project; it should not know how to query the database.

## Step 2 - Ask for published rows only

The bad approach is fetching all rows and hiding drafts in React. If the browser receives the draft, the draft leaked. Query `status = 'published'` and let RLS enforce the same rule.

## Step 3 - Map database rows to UI data

Database rows are often snake_case. UI code often wants camelCase. Map deliberately so your components are not coupled to raw table shape.

## Step 4 - Build the states

Show loading while the request runs, a useful empty state when no projects exist, a human error when Supabase fails, and a not-found state when a slug has no published row.

## Step 5 - Define the feature folder

Keep the project feature cohesive:

```txt
src/features/projects/
  projectTypes.ts
  projectApi.ts
  ProjectCard.tsx
  ProjectsPage.tsx
  ProjectDetailPage.tsx
```

The API module knows Supabase. The card knows display. The pages coordinate loading and route state.

## Step 6 - Write the read contract

Your data functions should have simple promises:

```ts
getPublishedProjects() -> Project[]
getPublishedProjectBySlug(slug) -> Project | null
```

They should select only public fields: title, slug, summary, technologies, links, featured flag, image path, and image alt. Do not select owner-only notes or draft-only fields.

## Step 7 - Do it on your project

Build in this order:

1. Render fake project cards from a local array.
2. Add filter state against the fake array.
3. Create Supabase read functions.
4. Replace the data source without rewriting the card.
5. Add detail page fetch by slug.
6. Add loading, empty, error, and not-found states.

This order proves your UI and data boundary are separate.

## Prove it before moving on

Seed a published and draft project with similar tags. Confirm:

```txt
/projects shows published only
filtering by shared tag still shows published only
/projects/draft-slug shows not found
browser console query cannot reveal drafts when signed out
```

> **📖 Mandatory read.** Read [Supabase JavaScript client](https://supabase.com/docs/reference/javascript/introduction), [Supabase RLS](https://supabase.com/docs/guides/database/postgres/row-level-security), and [React effects](https://react.dev/learn/synchronizing-with-effects). Required: this is the first public feature that depends on async data and RLS together.

> **💡 Hint.** Seed a draft and published project with the same technology tag. Filters should never reveal the draft.

## Definition of Done

- [ ] Projects list reads from Supabase.
- [ ] Only published projects render publicly.
- [ ] Project detail fetches by slug and published status.
- [ ] Draft projects do not appear in list, filter, or detail views.
- [ ] Loading, empty, error, and not-found states are visible.
- [ ] Database row shape is mapped before reaching visual components.

> **✍️ Log it (mandatory).** In `learning-log/06-projects-from-supabase.md`: explain why both the query filter and RLS policy matter. Why is hiding drafts in React too late?

All boxes ticked? Then continue. The next chapter builds on this gate, not around it.

---

Next: projects show what you built; now articles show how you think. -> **[Chapter 07 - Articles, comments, search, and pagination](07-articles-comments-search.md)**
