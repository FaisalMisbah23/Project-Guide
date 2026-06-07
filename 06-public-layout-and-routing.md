# Chapter 6 - Public layout and routing

The database is protected. Now the visitor needs a clean public experience: pages, navigation, and routes.

> **Principle.** A route is a promise that a URL will show the right thing.

## Where we're headed

By the end, the React app has public routes for home, about, projects, project details, articles, article details, and contact.

```txt
/                  -> Home
/about             -> About
/projects          -> Projects
/projects/:slug    -> ProjectDetails
/articles          -> Articles
/articles/:slug    -> ArticleDetails
/contact           -> Contact
*                  -> NotFound
```

## Before you build

> **Mandatory read.** Read DevWeekends React Router: https://resources.devweekends.com/courses/react-crash-course/09-react-router.

> **Apply this habit.** Read "Name Things Clearly" in [Daily_Software_Development_Guidelines.md](../Daily_Software_Development_Guidelines.md), then name routes after what visitors understand.

## Step 1 - Install routing

Install React Router if it is not installed:

```bash
npm install react-router-dom
```

## Step 2 - Create public pages

Create page files for the public routes:

```txt
src/pages/
  Home.jsx
  About.jsx
  Projects.jsx
  ProjectDetails.jsx
  Articles.jsx
  ArticleDetails.jsx
  Contact.jsx
  NotFound.jsx
```

Some pages can show placeholders until their data chapters arrive.

## Step 3 - Create layout components

Create:

```txt
Navbar
Footer
Layout
SectionTitle
ButtonLink
```

Keep them product-shaped. `ProjectCard` is better than `BoxWithShadow`.

## Step 4 - Wire routes

Create:

```txt
src/routes/
  AppRoutes.jsx
```

Use URL-friendly slugs for projects and articles. Slugs are part of the product.

## Step 5 - Add empty placeholders

Each route should show a clear placeholder:

```txt
Projects from Supabase will appear here.
Articles from Supabase will appear here.
Contact form will submit through an Edge Function.
```

## What your screen should show

Navigation works without full page reloads. Each public route shows the right page.

## Small challenge

Copy a project detail URL shape into your learning log and explain why a slug is better than a database ID in a public URL.

Suggested commit:

```bash
git commit -m "feat: add public routes"
```

## Definition of Done

- [ ] Public routes exist.
- [ ] Navigation links work.
- [ ] Unknown route shows `NotFound`.
- [ ] Slug routes are planned for projects and articles.
- [ ] Placeholders mention Supabase where data will arrive.

> **Log it.** In `learning-log/06-public-layout-and-routing.md`: What public routes exist, and which ones need Supabase data?

Next: load projects from Supabase. -> **[Chapter 7 - Projects from Supabase](07-projects-from-supabase.md)**
