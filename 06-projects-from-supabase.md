# Chapter 06 - Projects from Supabase

You now have public routes. The projects page is where the portfolio starts proving skill. Hard-coded project cards are easy, but they do not exercise the backend you built. This chapter makes the public project experience database-backed.

## Where we're headed

By the end, `/projects` loads published projects from Supabase, orders featured work first, supports useful empty/loading/error states, and `/projects/:slug` loads one published project by slug.

## The public data rule

Bad:

```txt
Fetch all projects and hide drafts in React.
```

Problem: the browser still receives draft data. If the content is private, hiding it after the fetch is too late.

Better:

```txt
Supabase query asks for published projects.
RLS also prevents draft projects from being returned publicly.
React only receives what visitors are allowed to see.
```

## Build it

Create a project data module in `src/features/projects/`. Keep Supabase query logic out of the visual card component. The list query should request published projects, order featured projects first, and then order by a stable display field or creation date.

Render cards that answer:

```txt
What was built?
What problem did it solve?
What technologies were used?
Where can I view code or demo?
What changed because of this project?
```

Do not let the card become a wall of badges. A visitor is scanning for evidence, not collecting buzzwords.

For the detail route, fetch by slug and published status. If no project matches, show a clear missing state.

## Empty, loading, and error states

A blank grid looks broken.

Good:

```txt
No projects match this category yet.
```

Better, when filtering:

```txt
No React projects match this filter yet. Clear filters to see all work.
```

The page should show loading while the request is in progress and a human-readable error if Supabase fails.

## Mandatory read

Read the DevWeekends React material on state, events, and lists/keys only if this is the first chapter where the learner is rendering dynamic lists in React. Required: project cards depend on state, mapped lists, keys, and filter events.

## Definition of Done

- [ ] Published projects render from Supabase.
- [ ] Draft projects do not appear publicly.
- [ ] Featured projects can appear first.
- [ ] Project detail pages load by slug.
- [ ] Missing, loading, error, and empty states are visible and useful.
- [ ] The project card copy explains outcomes, not only tools.

> **Log it.** In `learning-log/06-projects-from-supabase.md`, explain why drafts must be blocked by the database, not only hidden in React.

Next: projects show what you built. Articles show how you think. -> **[Chapter 07 - Articles, comments, search, and pagination](07-articles-comments-search.md)**
