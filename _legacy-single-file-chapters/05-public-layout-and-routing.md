# Chapter 05 - Public Layout And Routing

The database is protected. Now you build the public shape of the portfolio: pages, navigation, layout, and placeholders. Do not connect Supabase yet. First prove the site structure.

## Goal

By the end, the public portfolio has real routes, a navbar, a footer, and meaningful placeholder pages.

## What You Will Build

- Public route map.
- Shared public layout.
- Navbar and footer.
- Placeholder pages for required sections.
- Local arrays for early experience, skills, and project previews.

## Beginner Concepts

- **Route:** a URL mapped to a page component.
- **Layout:** shared wrapper around pages.
- **Navbar:** links used to move through the site.
- **Placeholder:** temporary content that still describes what belongs there.
- **Local array:** repeated content stored in a TypeScript file before database fetching.

## Step By Step

### Step 1 - Confirm The Design Direction

Use the choice from Chapter 01. Write one sentence:

```txt
This portfolio should feel like: calm professional / developer dashboard / editorial / creative.
```

That decision affects spacing, typography, and page density.

### Step 2 - Write The Route Contract

Use this public route map:

```txt
/                  HomePage
/about             AboutPage
/experience        ExperiencePage
/projects          ProjectsPage
/projects/:slug    ProjectDetailPage
/articles          ArticlesPage
/articles/:slug    ArticleDetailPage
/contact           ContactPage
*                  NotFoundPage
```

### Step 3 - Create Starter Local Data

Create local data files:

```txt
src/data/experience.ts
src/data/skills.ts
src/data/starterProjects.ts
```

These files should export arrays. This lets beginners practice rendering lists before Supabase is involved.

### Step 4 - Create Page Components

Create page files in `src/pages/`:

```txt
HomePage.tsx
AboutPage.tsx
ExperiencePage.tsx
ProjectsPage.tsx
ProjectDetailPage.tsx
ArticlesPage.tsx
ArticleDetailPage.tsx
ContactPage.tsx
NotFoundPage.tsx
```

Each page should show a heading and one useful sentence. Avoid empty `TODO` pages.

### Step 5 - Create The Layout

Create:

```txt
src/components/layout/PublicLayout.tsx
```

It should contain:

```txt
header with site name and navbar
main area for the current route
footer with resume, GitHub, LinkedIn, email
```

### Step 6 - Add React Router

Create:

```txt
src/routes/router.tsx
```

Use `createBrowserRouter` or the React Router pattern you choose. Wrap public pages in `PublicLayout`.

### Step 7 - Check Navigation

Run:

```bash
npm run dev
```

Click every navbar link. Refresh these URLs:

```txt
/
/about
/experience
/projects
/projects/example-slug
/articles
/articles/example-slug
/contact
/not-a-real-page
```

## Common Mistakes

| Mistake | Why it hurts | Fix |
|---|---|---|
| Using component state instead of routes | Refresh and sharing links break | Use React Router |
| Using `<a>` for internal links | The app fully reloads | Use `Link` or `NavLink` |
| Empty placeholder pages | You cannot judge layout | Add meaningful starter text |
| Skipping experience route | Required portfolio proof is missing | Add `/experience` |

## Checks Before Moving On

- All public routes render.
- Navbar links work without full reloads.
- Footer appears on public pages.
- Work experience has a page or section.
- Local arrays exist for beginner content practice.
- Bad URLs show a not-found page.

## Learning Log

In `learning-log/05-public-layout-and-routing.md`, answer:

```txt
What routes does the public portfolio need?
Why are real URLs better than page state?
What content is currently in local arrays?
How does the navbar match the portfolio sections?
```

## Definition Of Done

- [ ] Public route map is implemented.
- [ ] Shared layout exists.
- [ ] Navbar and footer exist.
- [ ] Home, About, Experience, Projects, Articles, Contact, and Not Found pages render.
- [ ] Local arrays render at least one repeated section.
- [ ] Direct refresh works locally.

Next: replace starter project cards with Supabase data. -> **[Chapter 06 - Projects From Supabase](06-projects-from-supabase.md)**
