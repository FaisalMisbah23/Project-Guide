# Chapter 7 - Routing and project details

Until now, your pages exist as files, but the app does not truly navigate between them. This chapter adds React Router so the portfolio behaves like a small application.

Routing is the difference between "I have components" and "I have pages visitors can move through." You will also build project detail pages, where each project can tell a deeper story than a card allows.

> **Principle.** A URL is a promise: if someone saves it, shares it, or refreshes it, the app should know what to show.

## Where we're headed

By the end, your app has routes for every main page, navigation links that do not reload the browser, a dynamic route for project details, and a not-found page.

```mermaid
flowchart TD
  Root[/] --> Home[Home]
  AboutRoute[/about] --> About[About]
  SkillsRoute[/skills] --> Skills[Skills]
  ProjectsRoute[/projects] --> Projects[Projects]
  ProjectId[/projects/:id] --> ProjectDetails[ProjectDetails]
  NotesRoute[/notes] --> Notes[LearningNotes]
  GithubRoute[/github] --> GitHub[GitHub]
  ContactRoute[/contact] --> Contact[Contact]
  Unknown[*] --> NotFound[NotFound]
```

## Before you build

> **Mandatory read.** Read the DevWeekends React Router chapter: https://resources.devweekends.com/courses/react-crash-course/09-react-router.

> **Optional docs.** Read the routing docs for React Router's current version. Use official docs when library behavior matters.

> **Hint - project IDs.** Use URL-friendly IDs such as `react-portfolio` or `todo-app`, not display titles with spaces. URLs are part of the product.

Before installing React Router, write your route map in `learning-log/07-routing-and-project-details.md`. A route should exist because a visitor needs that page, not because the outline has a checkbox.

## Step 1 - Install React Router

Install:

```bash
npm install react-router-dom
```

The weak alternative is to fake navigation by conditionally rendering pages with local state. That hides the URL from the visitor, breaks sharing, and does not teach how React apps normally handle pages. Use routing.

Example:

```txt
Weak:
User clicks "Projects" -> setCurrentPage("projects")
URL stays "/"

Stronger:
User clicks "Projects" -> route changes to "/projects"
URL can be shared, refreshed, and bookmarked
```

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

Example:

```txt
Weak:
Cannot read properties of undefined.

Stronger:
Project not found.
This project may have moved or been removed. Go back to all projects.
```

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

## What your screen should show

Clicking navigation links should swap pages without a full reload. A project card should open a matching detail page, a fake project id should show a useful fallback, and a nonsense URL should show `NotFound`.

## Small challenge

Copy one project detail URL, paste it into a new tab, and refresh it. Then write down what should happen after deployment if that same URL is opened directly.

Suggested commit:

```bash
git commit -m "feat: add routing and project detail pages"
```

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
