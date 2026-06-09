# Chapter 06 - Projects from Supabase

The projects page is where the portfolio starts proving skill. Hard-coded cards are useful for sketching, but the finished app should read published work from the database while keeping drafts private.

## The point of this chapter

Published projects load from Supabase into public list and detail pages, with loading, empty, error, filter, and missing-project states.

## Before you touch code

- Projects table has published and draft seed rows.
- RLS public read policy exists for published projects only.
- Public routes from Chapter 05 work.
- You can run the app and inspect browser network requests.

## Vocabulary for this chapter

- **Data module.** A file that owns Supabase queries for a feature.
- **Mapper.** A function that converts database row shape into UI shape.
- **Loading state.** UI shown while async work is unfinished.
- **Empty state.** UI shown when the request succeeds with no rows.
- **Not-found state.** UI shown when one requested item does not exist or is not public.

## Guided snippet or contract

This is a shape to aim for, not a finished solution to paste blindly:

```ts
// contract shape, not final code
type Project = {
  id: string;
  slug: string;
  title: string;
  summary: string;
  technologies: string[];
  featured: boolean;
  imagePath: string | null;
  imageAlt: string | null;
};

getPublishedProjects(): Promise<Project[]>;
getPublishedProjectBySlug(slug: string): Promise<Project | null>;
```

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

## If it breaks

| Symptom | Likely cause | Smallest next test |
|---|---|---|
| No projects appear | RLS blocks everything or seed status is not `published` | Run the Supabase query for one known published slug. |
| Draft appears publicly | Query selected all rows or RLS policy is too broad | Test signed-out query for the draft slug. |
| Filter reveals unexpected data | Filtering happens after fetching too much | Confirm fetched rows are public before filter state runs. |
| Detail page spins forever | Loading flag is never cleared on error or null result | Force a missing slug and inspect state transitions. |

## What you should be able to explain

- Why project cards should not query Supabase themselves.
- Why database rows are mapped before UI rendering.
- Why filters must not be responsible for hiding drafts.
- How you tested a draft slug.

## The slower beginner path

If this chapter feels too large, split the projects feature into one sitting per checkpoint. The goal is not to finish fast; the goal is to finish with proof.

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
