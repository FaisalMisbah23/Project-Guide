# Beginner Full-Stack Portfolio Course

You are going to build a real software engineer portfolio from the ground up. This is not only a page with your name on it. It is a small production-style app with public pages, owner-managed content, protected admin screens, saved contact messages, image uploads, email notifications, analytics, and deployment.

The course is written for beginners. Every chapter explains what you are building, why it matters, which files are involved, what command to run, what you should see, and how to prove the work is complete.

## What You Will Build

The public portfolio includes:

- Home page with a clear hero section.
- About page with your story and current focus.
- Work experience section.
- Projects list and project detail pages.
- Skills/tools section.
- Articles or blog pages.
- Contact form.
- Resume and social links.
- Optional newsletter signup.

The owner/admin side includes:

- Login.
- Admin dashboard.
- Project management.
- Article management.
- Image uploads.
- Contact inbox.
- Newsletter workflow.
- Basic analytics.

The stack is:

- **Vite + React + TypeScript** for the app.
- **TailwindCSS + shadcn/ui** for styling and UI components.
- **Supabase** for database, auth, RLS, storage, Edge Functions, Realtime, and Cron.
- **Brevo** for email notification.
- **Vercel** for deployment.

## How To Use This Course

Work through the chapters in order. Each chapter has the same rhythm:

1. Understand the goal.
2. Learn the beginner concepts.
3. Build one small piece at a time.
4. Run the checks.
5. Write a short learning-log explanation.

Create a `learning-log/` folder inside the app project you build. The log is mandatory because this project should become interview evidence, not only a finished screen.

Use this format when you get stuck:

```txt
I expected...
Actually happened...
I checked...
My smallest next test is...
```

## Content Strategy

The course uses three content levels:

- **Hardcoded JSX** for one tiny static sentence or label.
- **Local arrays/objects** for beginner-friendly repeated content such as skills, starter projects, and work experience.
- **Supabase tables** for content that should be editable, protected, filtered, or managed from the admin dashboard.

Recommended path: build the UI first with local arrays, then replace the data source with Supabase after the page shape is clear.

## Course Outline

| # | Chapter | Done when... |
|---|---------|--------------|
| 01 | [Plan the portfolio](01-introduction.md) | You know the audience, required sections, content inventory, layout idea, and data strategy |
| 02 | [Create the Vite project](02-project-setup-vite-supabase-git.md) | The app runs, generated files make sense, env files are safe, and Git has a clean baseline |
| 03 | [Design the data model](03-data-model-and-migrations.md) | Tables, constraints, seed data, and migrations are planned and created |
| 04 | [Protect data with RLS](04-rls-and-security-basics.md) | Public and owner access are enforced by the database |
| 05 | [Design layout and routes](05-public-layout-and-routing.md) | Public pages, navbar, footer, route map, and placeholders work |
| 06 | [Load projects from Supabase](06-projects-from-supabase.md) | Published projects load while drafts stay private |
| 07 | [Build articles, comments, search](07-articles-comments-search.md) | Published articles, safe comments, search, and pagination work |
| 08 | [Add owner auth and dashboard](08-owner-auth-and-admin-dashboard.md) | Owner login and protected admin shell work |
| 09 | [Create project CRUD](09-admin-project-crud.md) | Owner can create, edit, publish, unpublish, and archive projects |
| 10 | [Create article CRUD](10-admin-article-crud.md) | Owner can manage article drafts, previews, publishing, and comments |
| 11 | [Add image storage](11-image-storage.md) | Images upload safely with paths and alt text |
| 12 | [Build contact Edge Function](12-contact-edge-function-brevo.md) | Contact messages save before Brevo notification is attempted |
| 13 | [Build contact inbox](13-contact-inbox-realtime.md) | Admin can read, update, and optionally receive live messages |
| 14 | [Add newsletter and Cron](14-newsletter-and-cron.md) | Signup and scheduled-send planning work |
| 15 | [Add analytics](15-analytics-realtime-insights.md) | Public visits produce useful owner-only summaries |
| 16 | [Handle validation and states](16-validation-errors-empty-states.md) | Loading, empty, error, success, and validation states are designed |
| 17 | [Polish responsive accessibility](17-responsive-polish-accessibility.md) | The app works on real screens and keyboard checks |
| 18 | [Deploy to Vercel and Supabase](18-deploy-vercel-supabase.md) | Frontend, backend pieces, secrets, and smoke tests work in production |
| 19 | [Review and maintain](19-final-review-maintenance.md) | README, demo script, maintenance checklist, and security review exist |
| 20 | [Close the project](20-closing.md) | You can demo, explain, and continue improving the portfolio |

## Minimum Proof Per Chapter

Every chapter should end with:

- One visible artifact: route, table, policy, form, function, dashboard, checklist, or deployed URL.
- One proof command or browser check.
- One failure or privacy check.
- One learning-log explanation.

Start with Chapter 01. Plan the portfolio before touching tools.
