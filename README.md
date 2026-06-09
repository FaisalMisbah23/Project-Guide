# The Full-Stack Portfolio Project

> You're building a real, deployed **software engineer portfolio** - not a static resume page, not a template with your name swapped in, and not a weekend demo that forgets everything after refresh. This portfolio has public pages, owner-managed content, protected admin workflows, saved contact messages, email notifications, image storage, lightweight analytics, and a production deployment you can explain.

This course is written for a complete beginner, but it does not treat you like someone who can only copy commands. The point is to learn how software decisions connect: why content belongs in a database, why hiding a button is not security, why an email provider should never be called from React, why deployment is more than a green Vercel checkmark, and why every feature needs a failure story.

## What you're building

The finished app has two worlds.

The **public world** is what visitors see: home, about, projects, articles, article details, comments, contact, newsletter signup, and polished responsive pages. It answers the human question: *Can I trust this engineer enough to start a conversation?*

The **owner world** is what you use: login, dashboard, project CRUD, article CRUD, image uploads, comment moderation, contact inbox, newsletter runs, and analytics. It answers the engineering question: *Can this person build, protect, debug, and ship a small production system?*

The stack is deliberately practical: **Vite + React + TailwindCSS + shadcn/ui** for the frontend, **Supabase** for Postgres, Auth, RLS, Storage, Edge Functions, Realtime, and Cron, **Brevo** for email notifications, and **Vercel** for deployment.

## How to use this course

Read in order. Each chapter is a gate, not a suggestion. A chapter teaches the decision, shows the tempting shortcut and why it fails, gives you the production-shaped approach, then asks you to build and prove it. Do not skip the proof. The proof is where the learning sticks.

You'll see three recurring pieces:

- **📖 Mandatory read** - official docs or primary references you read before moving on. The course explains the path, but the docs are how you learn to stand on your own.
- **💡 Hint** - a nudge for a tricky part. Hints point at the thinking, not the final answer.
- **✅ Definition of Done** - observable checks. You can run them, see them, query them, or explain them. If you cannot tick the box honestly, the chapter is not done.

## The learning log is mandatory

Create `learning-log/` in the project you build. Every chapter asks you to write a short explanation there. That log is not homework decoration. It is your interview rehearsal and your proof that you understand the decisions behind the app.

Write like you are explaining to a skeptical senior engineer. One-line answers do not count.

## How you're judged

You're judged on understanding. A deployed URL matters, but it is not enough. You should be able to trace a contact form request from browser to Edge Function to database to Brevo, explain why RLS still matters when routes are protected, show where secrets live, and describe what happens when a provider fails.

## When you're stuck

Use this four-line reset before asking for help:

```txt
I expected...
Actually happened...
I checked...
My smallest next test is...
```

If you cannot fill in the lines, the problem is still too vague. Make it smaller.


## Expected effort

Treat this as a capstone, not a weekend template. A careful beginner should expect roughly **50-90 hours** across the full build, depending on how much React, SQL, Supabase, and deployment are new. Speed is not the score. The score is whether you can build, test, and explain each decision.

A useful weekly rhythm is:

```txt
Read docs -> write a short note -> build one small piece -> prove it -> commit -> log the decision
```

If you only code, you will finish with gaps you cannot defend. If you only read, you will never meet the bugs. The course works because you do both.

## How to read documentation

Official docs are not novels. Read them with a job:

- Before setup docs, ask: what command changes my project, and what file should I inspect after?
- Before Supabase docs, ask: which code runs in the browser, which runs server-side, and which permission boundary applies?
- Before deployment docs, ask: where does this value live in production, and who can see it?

Keep one note per chapter in `learning-log/`. Copying docs is not useful. Translating them into your project is.

## Module map

### Module 1 - Foundations

Chapters 01-04 establish the product, project setup, database model, and RLS security model. Do not rush this module. Every later feature assumes the database shape and permission rules are correct.

### Module 2 - Public site

Chapters 05-07 build the public reading experience: routes, projects, articles, comments, search, and pagination. The rule is public content only: published rows and approved comments.

### Module 3 - Owner workflows

Chapters 08-14 build the private owner side: login, admin dashboard, project CRUD, article CRUD, image storage, contact inbox, newsletter signup, and scheduled work. This is where the portfolio becomes maintainable.

### Module 4 - Production quality

Chapters 15-18 handle analytics, failure states, responsive/accessibility polish, and deployment. These chapters turn a working app into one you can trust in front of real users.

### Module 5 - Prove and maintain

Chapters 19-20 turn the shipped app into evidence: README, case study, demo script, smoke tests, maintenance rhythm, and the final explanation.


## How to use troubleshooting tables

Every chapter now includes an **If it breaks** table. Use it like a debugging ladder:

1. Find the symptom closest to what you see.
2. Read the likely cause, but do not assume it is correct yet.
3. Run the smallest next test exactly as written or adapt it narrowly.
4. Change one thing at a time.
5. Record the result in your learning log if it taught you something.

The goal is not to memorize fixes. The goal is to learn how to make a vague problem smaller.

## How to know you are stuck productively

You are productively stuck when you can say:

```txt
I know which chapter/feature I am in.
I know what I expected.
I know what actually happened.
I have checked one log, query, console message, or network request.
I have one smallest next test.
```

You are unproductively stuck when the problem is still `it does not work`. In that case, stop coding and write the four-line reset from above.

## Suggested pacing

A beginner-friendly pace is four passes:

```txt
Pass 1: Foundations       Chapters 01-04   setup, schema, RLS
Pass 2: Public site       Chapters 05-07   routes, projects, articles
Pass 3: Owner workflows   Chapters 08-14   admin, storage, contact, newsletter
Pass 4: Production proof  Chapters 15-20   analytics, polish, deploy, maintain
```

If you work part-time, one or two chapters per week is reasonable. If you work intensively, do not measure only by chapter count. Measure by gates cleared honestly.

## Minimum proof per chapter

Before moving on from any chapter, you need at least this much proof:

```txt
1 visible artifact     route, table, policy, form, function, dashboard, checklist, or deployed URL
1 failure test         blocked read, invalid input, missing row, provider failure, bad route, or bad viewport
1 explanation          learning-log answer in your own words
1 commit or checkpoint if code changed
```

This is the course's rhythm: build, break safely, explain, then continue.

## Course outline

| # | Chapter | Done when... |
|---|---------|--------------|
| 01 | [Introduction](01-introduction.md) | You can explain the product, users, and why this is more than a static portfolio |
| 02 | [Project setup with Vite, Supabase, and Git](02-project-setup-vite-supabase-git.md) | The app runs, builds, ignores secrets, and has a clean baseline commit |
| 03 | [Data model and migrations](03-data-model-and-migrations.md) | Tables, constraints, seed data, `owner_profile`, and reliable `updated_at` exist through migrations |
| 04 | [RLS and security basics](04-rls-and-security-basics.md) | Public and owner access are enforced by database policies, not the UI |
| 05 | [Public layout and routing](05-public-layout-and-routing.md) | Public routes, layout, navigation, and not-found handling work |
| 06 | [Projects from Supabase](06-projects-from-supabase.md) | Published projects load from Supabase while drafts stay hidden |
| 07 | [Articles, comments, search, and pagination](07-articles-comments-search.md) | Published articles, safe rendering, pending comments, search, and pagination work |
| 08 | [Owner auth and admin dashboard](08-owner-auth-and-admin-dashboard.md) | Owner login, protected routes, dashboard shell, and RLS-backed access work |
| 09 | [Admin project CRUD](09-admin-project-crud.md) | Owner can create, edit, publish, unpublish, and archive projects safely |
| 10 | [Admin article CRUD](10-admin-article-crud.md) | Owner can manage drafts, publish articles, preview safely, and moderate comments |
| 11 | [Image storage](11-image-storage.md) | Images upload to storage and records store paths plus alt text |
| 12 | [Contact Edge Function and Brevo](12-contact-edge-function-brevo.md) | Contact messages are stored before Brevo notification is attempted |
| 13 | [Contact inbox and Realtime](13-contact-inbox-realtime.md) | Stored messages load in admin and new messages can appear live |
| 14 | [Newsletter and Cron](14-newsletter-and-cron.md) | Signup is server-side, duplicates are controlled, and scheduled sends are logged or planned |
| 15 | [Analytics and Realtime insights](15-analytics-realtime-insights.md) | Minimal, untrusted analytics feed useful dashboard summaries |
| 16 | [Validation, errors, and empty states](16-validation-errors-empty-states.md) | Major screens have designed failure, loading, empty, and success states |
| 17 | [Responsive polish and accessibility](17-responsive-polish-accessibility.md) | The app works on real screens and basic keyboard/accessibility checks pass |
| 18 | [Deploy with Vercel and Supabase](18-deploy-vercel-supabase.md) | Frontend, backend pieces, secrets, and production smoke tests are complete |
| 19 | [Final review and maintenance](19-final-review-maintenance.md) | README, case study, demo script, security review, and maintenance rhythm exist |
| 20 | [Closing](20-closing.md) | You can demo, defend, and keep improving the portfolio |

Work the chapters in order. Every checklist is a gate.
