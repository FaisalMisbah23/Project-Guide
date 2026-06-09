# Chapter 05 - Public layout and routing

The database is guarded; now the public site needs a shape. Routing is easy to underestimate because beginners can fake pages with component state. But URLs are part of the product. They let visitors bookmark, refresh, share, and understand where they are.

## The point of this chapter

A public route structure with home, about, projects, project detail, articles, article detail, contact, and not-found pages, all wrapped in a shared layout.

## Step 1 - Use routes, not manual page state

The shortcut is one giant component with `currentPage` state. It works until refresh, deep links, analytics, not-found pages, and deployment enter the room. Use React Router so URLs represent real pages.

## Step 2 - Build the shared public layout

Create a header, navigation, main content area, and footer. Keep the layout boring and dependable. Public pages should feel easy to scan before they become fancy.

## Step 3 - Add placeholder pages before data

Build every route with meaningful placeholder content first. Projects and articles will connect to Supabase later; today you are proving navigation, not data loading.

## Step 4 - Test direct refresh

Visit `/projects`, `/projects/example-slug`, `/articles`, `/articles/example-slug`, `/contact`, and a nonsense URL. Refresh each one. If refresh breaks, you have a routing/deployment issue to solve before feature work hides it.

## Step 5 - Write the route contract

Before building components, write the route table:

```txt
/                  HomePage
/about             AboutPage
/projects          ProjectsPage
/projects/:slug    ProjectDetailPage
/articles          ArticlesPage
/articles/:slug    ArticleDetailPage
/contact           ContactPage
*                  NotFoundPage
```

This is your frontend contract. A new reader should know which component owns each URL.

## Step 6 - Create the minimum page content

Each placeholder page should answer one question even before data exists:

```txt
Home: who are you and what should the visitor do next?
About: what is your story and current focus?
Projects: what work will appear here?
Articles: what thinking will appear here?
Contact: how will a visitor start a conversation?
Not found: how does the visitor recover?
```

Do not leave pages as `TODO`. A placeholder should still be meaningful.

## Step 7 - Do it on your project

Create these artifacts:

```txt
src/routes/router.tsx
src/pages/HomePage.tsx
src/pages/AboutPage.tsx
src/pages/ProjectsPage.tsx
src/pages/ProjectDetailPage.tsx
src/pages/ArticlesPage.tsx
src/pages/ArticleDetailPage.tsx
src/pages/ContactPage.tsx
src/pages/NotFoundPage.tsx
src/components/layout/PublicLayout.tsx
```

Names can vary, but the responsibilities should remain separate.

## Prove it before moving on

Open every route manually, then refresh it. Click every nav item. Type a bad URL. If any route gives a blank screen, fix routing before Supabase data enters the picture.

> **📖 Mandatory read.** Read [React Router](https://reactrouter.com/home), [React conditional rendering](https://react.dev/learn/conditional-rendering), and [MDN document structure](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Structuring_content/Structuring_documents). Required: routes, layout, and semantic page regions are the vocabulary of this chapter.

> **💡 Hint.** Use `Link` or `NavLink` for internal navigation. A normal `<a>` is for leaving the app or linking to real documents, not for route changes inside the SPA.

## Definition of Done

- [ ] All public routes render.
- [ ] The shared public layout wraps the pages.
- [ ] Navigation works without full page reloads.
- [ ] Slug routes exist for project and article details.
- [ ] Unknown URLs show a friendly not-found page.
- [ ] Direct refresh works locally and has a deployment plan.

> **✍️ Log it (mandatory).** In `learning-log/05-public-layout-and-routing.md`: explain why real URLs are better than manual page switching with component state. Include one thing that would break with the shortcut.

All boxes ticked? Then continue. The next chapter builds on this gate, not around it.

---

Next: the routes exist; now replace placeholder work with published rows from Supabase. -> **[Chapter 06 - Projects from Supabase](06-projects-from-supabase.md)**
