# Chapter 7 - Routing and project details

Until now, your pages exist as files, but the app does not truly navigate between them. This chapter adds React Router so the portfolio behaves like a small application.

Routing is the difference between "I have components" and "I have pages visitors can move through." You will also build project detail pages, where each project can tell a deeper story than a card allows.

## Where we're headed

By the end, your app has routes for every main page, navigation links that do not reload the browser, a dynamic route for project details, and a not-found page.

## Before you build

> **Mandatory read.** Read the DevWeekends React Router chapter: https://resources.devweekends.com/courses/react-crash-course/09-react-router.

Before installing React Router, write your route map in `learning-log/07-routing-and-project-details.md`. A route should exist because a visitor needs that page, not because the outline has a checkbox.

## Step 1 - Install React Router

Install:

```bash
npm install react-router-dom
```

The weak alternative is to fake navigation by conditionally rendering pages with local state. That hides the URL from the visitor, breaks sharing, and does not teach how React apps normally handle pages. Use routing.

## Step 2 - Create the route file

Create:

```txt
src/routes/
  AppRoutes.jsx
```

Your route plan:

```txt
/                 -> Home
/about            -> About
/skills           -> Skills
/projects         -> Projects
/projects/:id     -> ProjectDetails
/notes            -> LearningNotes
/github           -> GitHub
/contact          -> Contact
*                 -> NotFound
```

Some pages may be placeholders until later chapters. That is fine. Create enough structure that navigation has a complete map.

## Step 3 - Use router links in navigation

Update `Navbar` to use React Router navigation links instead of plain reload-style page changes.

Plain anchors are still correct for external links. Router links are for internal pages. Use each for the right job.

## Step 4 - Create the project details page

Create:

```txt
src/pages/
  ProjectDetails.jsx
  NotFound.jsx
```

The dynamic route `/projects/:id` should read the project id from the URL, find the matching project from `projects.js`, and show a deeper project view.

Add more fields to your project data if needed:

```txt
problem
solution
features
lessons
screenshots
```

If the id does not match a project, show a useful fallback. Do not let the page crash.

That fallback is not optional polish; it is designing for failure. Users paste old links, mistype URLs, and click stale bookmarks. Your app should handle that calmly.

## Step 5 - Test route behavior

Test:

```txt
/
/about
/skills
/projects
/projects/a-real-id
/projects/not-real
/anything-random
```

Navigation should work without a full page refresh. Unknown routes should show `NotFound`.

> **Interesting to read.** Read the routing docs for React Router's current version. Use official docs when library behavior matters.

> **Hint - project IDs.** Use URL-friendly IDs such as `react-portfolio` or `todo-app`, not display titles with spaces. URLs are part of the product.

## Definition of Done

- [ ] `react-router-dom` is installed.
- [ ] `src/routes/AppRoutes.jsx` exists.
- [ ] Main routes work for home, about, skills, projects, notes, GitHub, and contact.
- [ ] `Navbar` uses router links for internal navigation.
- [ ] `/projects/:id` shows the matching project detail page.
- [ ] Unknown project IDs show a fallback instead of crashing.
- [ ] Unknown routes show `NotFound`.
- [ ] Refreshing or directly opening a route is considered in your deployment notes for Chapter 12.
- [ ] Navigation does not full-refresh the page.
- [ ] You made a commit for this chapter.

> **Log it.** In `learning-log/07-routing-and-project-details.md`: (1) What problem does React Router solve? (2) Why is URL state useful for project details? (3) How does your app handle a project ID that does not exist?

---

Next: add learning notes with search. -> **[Chapter 8 - Learning notes search](08-learning-notes-search.md)**
