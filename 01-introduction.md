# The Full-Stack Supabase Portfolio Project

> You are building a real, deployed **full-stack software engineer portfolio** with **Vite + React + Supabase + Vercel**. It introduces you clearly, stores real content in Postgres, protects admin tools with Supabase Auth and Row Level Security, handles contact messages through a Supabase Edge Function, sends Brevo email notifications, and ships on a real URL.

This is no longer a static React portfolio. The portfolio is now a small production-shaped system: public pages, database tables, authentication, admin content management, storage, server-side contact handling, email notification, security rules, deployment, and maintenance.

## Introduction - what you'll build and why it matters

A portfolio is usually the first piece of software someone uses to judge your software. A full-stack portfolio raises the bar: the visitor sees your projects and articles, while a reviewer can also inspect how you model data, protect writes, validate input, handle secrets, and deploy a real application.

The product should answer four questions within **30-60 seconds**:

- Who are you?
- What can you build?
- Why should someone trust your work?
- How can they contact you?

The engineering should answer a deeper set of questions:

- How does the frontend get data?
- Which data is public?
- Which data is admin-only?
- Where do secrets live?
- What happens when a request fails?
- How is the site deployed and maintained?

## How to use this course

Work through the chapters in order. Each chapter moves the real project forward, and most chapters follow this rhythm:

1. **Principle** - the idea behind the chapter.
2. **Where we're headed** - the milestone you will have by the end.
3. **Before you build** - required reading, habits, hints, and stuck reminders.
4. **Build steps** - small actions in the order a developer meets them.
5. **What your screen should show** - the visible result to compare against.
6. **Small challenge** - one extension that makes the feature more personal.
7. **Definition of Done** - the gate before moving forward.
8. **Log it** - reflection prompts so you can explain the work later.

Some readings appear inside a build step instead of at the top. That is intentional. Read about RLS when you write policies, Storage when you upload images, Edge Functions when you handle contact messages, and Brevo when you send notifications. Read one useful thing, apply it immediately, then continue.

## The product

The public portfolio includes:

- **Home.** Name, role, summary, featured projects, featured articles, and contact path.
- **About.** Story, strengths, current focus, and goals.
- **Skills.** Skills grouped honestly, without fake percentage bars.
- **Projects.** Published projects loaded from Supabase.
- **Project details.** Case-study pages with problem, solution, contribution, challenge, and result.
- **Articles.** Published blog/article content loaded from Supabase.
- **Article details.** Individual readable articles with tags and publish dates.
- **Contact.** A form that stores messages and triggers a Brevo notification.

The admin area includes:

- **Owner login.** Supabase Auth protects admin screens.
- **Dashboard.** At-a-glance counts and shortcuts.
- **Project management.** Create, edit, publish, unpublish, and delete projects.
- **Article management.** Create drafts, publish articles, edit slugs, tags, and cover images.
- **Contact inbox.** Read, mark, and archive messages.
- **Image uploads.** Store project and article images in Supabase Storage.

## In scope

- Vite + React frontend.
- Supabase project setup.
- Supabase Postgres tables and migrations.
- Row Level Security policies.
- Supabase Auth for one portfolio owner.
- Public reads for published projects and articles.
- Admin CRUD for projects and articles.
- Supabase Storage for project/article images.
- Supabase Edge Function for contact submission.
- Brevo transactional email notification.
- Validation, errors, loading, empty, and success states.
- Vercel deployment.
- Supabase secrets and Vite environment variables.
- Final README, maintenance checklist, and review prep.

## Out of scope

Deliberately not building these:

- Payments.
- Multi-user team accounts.
- Comments.
- Likes.
- Analytics dashboards.
- Complex WYSIWYG editing.
- A separate Express API.
- A mobile app.

Those are future projects. This one is about shipping a focused full-stack portfolio well.

## Course outline

| # | Chapter | Done when... |
|---|---|---|
| 2 | [Project setup with Vite, Supabase, and Git](02-project-setup-vite-supabase-git.md) | The repo, React app, Supabase CLI/project, env files, and Git baseline are ready |
| 3 | [Supabase project and environment](03-supabase-project-and-environment.md) | Local and hosted Supabase settings are understood and secrets are separated |
| 4 | [Data model and migrations](04-data-model-and-migrations.md) | Tables for projects, articles, messages, and settings are designed and migrated |
| 5 | [RLS and security basics](05-rls-and-security-basics.md) | Public reads and owner-only writes are protected by policies |
| 6 | [Public layout and routing](06-public-layout-and-routing.md) | Public pages and routes are scaffolded |
| 7 | [Projects from Supabase](07-projects-from-supabase.md) | Published projects load from Supabase with loading/error/empty states |
| 8 | [Articles from Supabase](08-articles-from-supabase.md) | Published articles load from Supabase and have detail pages |
| 9 | [Owner login with Supabase Auth](09-owner-login-with-supabase-auth.md) | The owner can sign in and sign out |
| 10 | [Protected admin dashboard](10-protected-admin-dashboard.md) | Admin routes are protected and show dashboard summaries |
| 11 | [Admin project CRUD](11-admin-project-crud.md) | The owner can create, edit, publish, and delete projects |
| 12 | [Admin article CRUD](12-admin-article-crud.md) | The owner can draft, edit, publish, and delete articles |
| 13 | [Image uploads with Supabase Storage](13-image-uploads-with-supabase-storage.md) | Project/article images upload safely and render publicly |
| 14 | [Contact Edge Function with Brevo](14-contact-edge-function-brevo.md) | Contact form stores messages and sends a Brevo notification |
| 15 | [Contact inbox](15-contact-inbox.md) | Admin can read and manage contact messages |
| 16 | [Validation, errors, and states](16-validation-errors-and-states.md) | Forms and data screens handle failure clearly |
| 17 | [Spam and abuse protection](17-spam-and-abuse-protection.md) | Contact submission has basic anti-abuse thinking and tests |
| 18 | [Responsive polish and accessibility](18-responsive-polish-and-accessibility.md) | Public and admin screens are usable on mobile and keyboard |
| 19 | [Deploy to Vercel and Supabase](19-deploy-vercel-and-supabase.md) | The app, functions, secrets, policies, and database are deployed |
| 20 | [Final review and maintenance](20-final-review-and-maintenance.md) | README, learning log, and maintenance rhythm are ready |

## Your working rhythm

### Before coding

Ask:

```txt
- What problem am I solving?
- Who will use this?
- Which data is public?
- Which data is private?
- What could break later?
- Can I explain this feature in one sentence?
```

### Habits

- Commit small changes.
- Keep secrets out of Git.
- Read errors before changing code.
- Test happy and unhappy paths.
- Write the learning log.
- Explain security decisions in your own words.
- Prefer boring, maintainable choices over clever ones.

## References used throughout

- Supabase docs: https://supabase.com/docs
- Supabase Row Level Security: https://supabase.com/docs/guides/auth/auth-deep-dive/auth-row-level-security
- Supabase Edge Functions: https://supabase.com/docs/guides/functions
- Supabase function secrets: https://supabase.com/docs/guides/functions/secrets
- Brevo transactional email API: https://developers.brevo.com/docs/send-a-transactional-email
- Vercel docs: https://vercel.com/docs

Ready? Start with **[Chapter 2 - Project setup with Vite, Supabase, and Git](02-project-setup-vite-supabase-git.md)**.
