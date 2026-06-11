# Beginner Full-Stack Portfolio Course

You are going to build a real software engineer portfolio from the ground up. This is not only a page with your name on it. It is a small production-style app with public pages, owner-managed content, protected admin screens, saved contact messages, image uploads, email notifications, analytics, and deployment.

This version of the course is folder-based. Each chapter is a folder, and each folder contains small ordered sub-chapters. Work through them in order. The final file in each chapter is a gate: do not move on until the Definition of Done or Key Takeaways are complete.

## Stack

- **Vite + React + TypeScript** for the app.
- **TailwindCSS + shadcn/ui** for styling and UI components.
- **Supabase** for database, auth, RLS, storage, Edge Functions, Realtime, and Cron.
- **Brevo** for email notification.
- **Vercel** for deployment.

## How To Use This Course

1. Start with Chapter 01.
2. Read each sub-chapter in order.
3. Build only the professional path described by the chapter.
4. Use the hints when stuck, but write the implementation yourself.
5. Add the required learning-log entry before moving on.

Create a `learning-log/` folder inside the app project you build. The log is mandatory because this project should become interview evidence, not only a finished screen.

Use this format when you get stuck:

```txt
I expected...
Actually happened...
I checked...
My smallest next test is...
```

## Guide Standard

This course follows the DevWeekends project-guide standard from `guide.md`.

Each feature chapter should do more than name tasks. It should:

- reveal the work one small step at a time;
- explain the tempting shortcut and the concrete cost of taking it;
- guide the professional path without giving away solution code;
- name the real folders, files, routes, tables, and checks the learner must create;
- include do/don't guidance where mistakes are likely;
- end with a gate the learner can prove in their own repo.

When a lesson feels too thin, treat Chapter 13 as the current model for the target shape: it keeps the same folder-based structure, but adds deeper explanation, build continuity, verification, and privacy checks.

## Course Outline

| # | Chapter | Phase | Done when... |
|---|---|---|---|
| 01 | [Plan the portfolio](01-introduction/01.01-what-you-are-building.md) | Mindset and product | You know the audience, sections, content inventory, design direction, and data strategy. |
| 02 | [Create the Vite project](02-project-setup-vite-supabase-git/02.01-set-the-scene.md) | Foundation | The app runs, generated files make sense, env files are safe, and Git has a clean baseline. |
| 03 | [Design the data model](03-data-model-and-migrations/03.01-set-the-scene.md) | Foundation | Tables, constraints, seed data, and migrations are planned and created. |
| 04 | [Protect data with RLS](04-rls-and-security-basics/04.01-set-the-scene.md) | Foundation | Public and owner access are enforced by the database. |
| 05 | [Design layout and routes](05-public-layout-and-routing/05.01-set-the-scene.md) | Public experience | Public pages, navbar, footer, route map, and placeholders work. |
| 06 | [Load projects from Supabase](06-projects-from-supabase/06.01-set-the-scene.md) | Public experience | Published projects load while drafts stay private. |
| 07 | [Build articles, comments, search](07-articles-comments-search/07.01-set-the-scene.md) | Public experience | Published articles, safe comments, search, and pagination work. |
| 08 | [Add owner auth and dashboard](08-owner-auth-and-admin-dashboard/08.01-set-the-scene.md) | Owner workspace | Owner login and protected admin shell work. |
| 09 | [Create project CRUD](09-admin-project-crud/09.01-set-the-scene.md) | Owner workspace | Owner can create, edit, publish, unpublish, and archive projects. |
| 10 | [Create article CRUD](10-admin-article-crud/10.01-set-the-scene.md) | Owner workspace | Owner can manage article drafts, previews, publishing, and comments. |
| 11 | [Add image storage](11-image-storage/11.01-set-the-scene.md) | Media and communication | Images upload safely with paths and alt text. |
| 12 | [Build contact Edge Function](12-contact-edge-function-brevo/12.01-set-the-scene.md) | Media and communication | Contact messages save before Brevo notification is attempted. |
| 13 | [Build contact inbox](13-contact-inbox-realtime/13.01-set-the-scene.md) | Media and communication | Admin can read, update, and optionally receive live messages. |
| 14 | [Add newsletter and Cron](14-newsletter-and-cron/14.01-set-the-scene.md) | Growth and insight | Signup and scheduled-send planning work. |
| 15 | [Add analytics](15-analytics-realtime-insights/15.01-set-the-scene.md) | Growth and insight | Public visits produce useful owner-only summaries. |
| 16 | [Handle validation and states](16-validation-errors-empty-states/16.01-set-the-scene.md) | Polish and production | Loading, empty, error, success, and validation states are designed. |
| 17 | [Polish responsive accessibility](17-responsive-polish-accessibility/17.01-set-the-scene.md) | Polish and production | The app works on real screens and keyboard checks. |
| 18 | [Deploy to Vercel and Supabase](18-deploy-vercel-supabase/18.01-set-the-scene.md) | Polish and production | Frontend, backend pieces, secrets, and smoke tests work in production. |
| 19 | [Review and maintain](19-final-review-maintenance/19.01-set-the-scene.md) | Closing and proof | README, demo script, maintenance checklist, and security review exist. |
| 20 | [Close the project](20-closing/20.01-look-back-at-the-finished-app.md) | Closing and proof | You can demo, explain, and continue improving the portfolio. |

## Legacy Drafts

The original compact single-file chapters are preserved in [`_legacy-single-file-chapters/`](_legacy-single-file-chapters/) for reference. Use the folder-based chapters above as the source of truth.
