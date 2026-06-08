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

## New ideas before you build

This chapter is the first place where the page stops being static. If the learner is new to React, pause here and learn these topics before building the project list.

### `useEffect` for loading data

**Real-life analogy:** imagine opening a shop in the morning. First you unlock the door and turn on the lights. Then, after the shop is open, you check the stock room and bring products to the shelves. `useEffect` is like that second step: it runs after React has shown the page, so the component can go do something outside the first render, such as fetching projects from Supabase.

**General idea:** React components should render UI from current data. When a component needs to talk to something outside React, such as Supabase, the browser, a timer, or a subscription, that work belongs in an effect. The dependency array tells React when to run the effect again. An empty array, `[]`, means "run this once when the component appears."

```tsx
import { useEffect, useState } from "react";

function ProjectsPage() {
  const [projects, setProjects] = useState([]);
  const [isLoading, setIsLoading] = useState(true);
  const [error, setError] = useState("");

  useEffect(() => {
    async function loadProjects() {
      try {
        setIsLoading(true);
        const rows = await getPublishedProjects();
        setProjects(rows);
      } catch (error) {
        setError("Projects could not be loaded.");
      } finally {
        setIsLoading(false);
      }
    }

    loadProjects();
  }, []);

  if (isLoading) return <p>Loading projects...</p>;
  if (error) return <p>{error}</p>;

  return <ProjectList projects={projects} />;
}
```

Study more: [React Crash Course - Components and Props](https://resources.devweekends.com/courses/react-crash-course/02-components-props)

### `useState` for changing screen data

**Real-life analogy:** think of a whiteboard beside your desk. When something changes, you update the whiteboard and everyone can see the latest status. `useState` is the component's whiteboard: it stores values that can change and tells React to redraw the screen when they do.

**General idea:** use state for data the user can change or data that arrives later, such as selected filters, loading flags, errors, and fetched projects. Do not use normal variables for screen data that should cause the UI to update.

```tsx
const [selectedTag, setSelectedTag] = useState("all");

function handleTagClick(tag: string) {
  setSelectedTag(tag);
}
```

Study more: [React Crash Course - Components and Props](https://resources.devweekends.com/courses/react-crash-course/02-components-props)

### Lists and `key`

**Real-life analogy:** imagine a teacher checking attendance. Names alone may repeat, but each student has a roll number. React needs the same kind of stable identity when rendering many items, so it can tell which card is which after filtering or reordering.

**General idea:** use `.map()` to turn an array into UI. Give each rendered item a stable `key`, usually the database `id` or slug. Do not use the array index when the list can be filtered, reordered, inserted into, or deleted from.

```tsx
function ProjectList({ projects }) {
  return (
    <ul>
      {projects.map((project) => (
        <li key={project.id}>
          <ProjectCard project={project} />
        </li>
      ))}
    </ul>
  );
}
```

Study more: [React Crash Course - Introduction to React and JSX](https://resources.devweekends.com/courses/react-crash-course/01-intro-jsx)

### Events for filters and buttons

**Real-life analogy:** a doorbell does nothing until someone presses it. An event handler is the function React runs when the learner clicks a button, types in a search box, submits a form, or changes a filter.

**General idea:** pass a function to an event prop such as `onClick`, `onChange`, or `onSubmit`. That function usually updates state, starts a request, or validates user input.

```tsx
function ProjectFilters({ selectedTag, onSelectTag }) {
  return (
    <button
      type="button"
      aria-pressed={selectedTag === "react"}
      onClick={() => onSelectTag("react")}
    >
      React
    </button>
  );
}
```

Study more: [React Crash Course - Components and Props](https://resources.devweekends.com/courses/react-crash-course/02-components-props)

## Daily guideline

From `Daily_Software_Development_Guidelines.md`: **separate business logic from UI**. Keep Supabase queries in a project data module and keep `ProjectCard` focused on display. The card should not know how to talk to the database; it should receive a project and render it clearly.

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

Read the React topic explanations above and then study the linked `resources.devweekends.com` pages for any topic that still feels unclear. Required: project cards depend on `useEffect`, state, mapped lists, keys, and filter events.

## Definition of Done

- [ ] Published projects render from Supabase.
- [ ] Draft projects do not appear publicly.
- [ ] Featured projects can appear first.
- [ ] Project detail pages load by slug.
- [ ] Missing, loading, error, and empty states are visible and useful.
- [ ] The project card copy explains outcomes, not only tools.

> **Log it.** In `learning-log/06-projects-from-supabase.md`, explain why drafts must be blocked by the database, not only hidden in React.

## Between chapters

**Quiz:** what should the UI show for each state: loading, Supabase error, no projects, and project slug not found?

**Assignment:** build the projects page first with fake data, then replace only the data source with Supabase. The card UI should not need to know which source was used.

**Reading:** review [React Crash Course - Introduction to React and JSX](https://resources.devweekends.com/courses/react-crash-course/01-intro-jsx), especially lists and `key`.

**React exercise:** render three fake projects first, then add a filter button. Only after the UI works should you replace the fake array with Supabase data.

**Data exercise:** seed one published project and one draft project with the same technology tag. Confirm the filter never reveals the draft.

**Comparison:** state vs props: state belongs to a component and can change over time. Props are values passed into a component by its parent.

**Big word alert:** **side effect** means work React does outside pure rendering, such as fetching from Supabase, setting up a subscription, reading from the browser, or starting a timer.

**Motivation pause:** from `Software_Engineering_Community_Affirmations.md`: "Building teaches lessons that theory cannot." Once this page renders real data, the backend stops being an idea and becomes part of your app.

Next: projects show what you built. Articles show how you think. -> **[Chapter 07 - Articles, comments, search, and pagination](07-articles-comments-search.md)**
