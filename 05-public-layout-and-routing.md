# Chapter 05 - Public layout and routing

The database is guarded; now the public site needs a shape. Routing is easy to underestimate because beginners can fake pages with component state. But URLs are part of the product. They let visitors bookmark, refresh, share, and understand where they are.

## The point of this chapter

A public route structure with home, about, projects, project detail, articles, article detail, contact, and not-found pages, all wrapped in a shared layout.

## Before you touch code

- The app starts locally.
- You know the public pages the portfolio needs.
- You are not connecting Supabase data yet.
- You have React Router docs open.

## Vocabulary for this chapter

- **Route.** A URL mapped to a component.
- **Layout.** Shared wrapper around related pages.
- **Slug.** URL-safe identifier such as `portfolio-site`.
- **Not-found page.** The recovery page for unknown URLs.

## Guided snippet or contract

This is a shape to aim for, not a finished solution to paste blindly:

```txt
Route contract
  /                  public home
  /about             public about
  /projects          public project list
  /projects/:slug    public project detail
  /articles          public article list
  /articles/:slug    public article detail
  /contact           public contact
  *                  public not found
```

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

## If it breaks

| Symptom | Likely cause | Smallest next test |
|---|---|---|
| Clicking nav reloads page | Internal links use `<a>` instead of router links | Replace internal anchors with `Link` or `NavLink`. |
| Refresh on nested route fails | SPA fallback is not configured for deployment | Test locally now; note Vercel rewrite for Chapter 18. |
| Slug page shows no slug | Route pattern or param hook is wrong | Log route params on a placeholder detail page. |
| Layout duplicates on pages | Layout is placed inside each page instead of route tree | Move shared structure into `PublicLayout`. |

## What you should be able to explain

- Why URLs matter for a portfolio.
- Why placeholder pages should still be meaningful.
- Why internal navigation should use router links.

## The slower beginner path

If this chapter feels too large, split the public route structure into one sitting per checkpoint. The goal is not to finish fast; the goal is to finish with proof.

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
