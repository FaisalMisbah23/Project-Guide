# Chapter 05 - Public layout and routing

The database is protected. Now return to the visitor. A portfolio succeeds when someone can understand it quickly without being taught the interface. Routing is the promise your app makes: each URL should mean something stable.

## Where we're headed

By the end you will have a public layout, navigation, and routes for home, about, projects, project details, articles, article details, contact, and not-found.

## The routing trap

Bad:

```txt
One giant Home component
scroll anchors for everything
project details hidden in modals
no real article URLs
```

Problem: content cannot be linked cleanly, visitors cannot share a project URL, and search/indexing signals are weak.

Better:

```txt
/                 home
/about            owner story and skills
/projects         project list
/projects/:slug   project detail
/articles         article list
/articles/:slug   article detail
/contact          contact form
```

## Build it

Install and configure React Router. Create the public layout with header, main content, footer, and navigation. Keep the layout quiet and work-focused: a software engineer portfolio should be easy to scan, not a maze of decorative sections.

Add placeholder pages first. The goal is to prove the route structure before wiring Supabase data.

Use TailwindCSS for layout and shadcn/ui for repeated interface pieces where they help: buttons, forms, cards, inputs, dialogs, and navigation patterns.

Track page visits later with Supabase, but design the route boundaries now. Do not track admin routes as public visitor behavior.

## Empty routes matter

A missing project slug should not show a blank screen. Create a not-found route and a project/article missing state. Blank pages feel broken.

Good empty copy:

```txt
No project found for this link.
```

Bad empty copy:

```txt
[]
```

## Definition of Done

- [ ] Public layout exists.
- [ ] Routes exist for home, about, projects, project detail, articles, article detail, contact, and not-found.
- [ ] Navigation works on desktop and mobile.
- [ ] Unknown URLs show a not-found page.
- [ ] Admin routes are not mixed into public navigation.

> **Log it.** In `learning-log/05-public-layout-and-routing.md`, explain why project and article detail pages need stable slug URLs.

Next: the routes exist. Now replace placeholder project content with published rows from Supabase. -> **[Chapter 06 - Projects from Supabase](06-projects-from-supabase.md)**
