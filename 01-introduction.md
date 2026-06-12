# Chapter 01 - Plan the portfolio

> You are building a real, deployed software engineer portfolio, not a decorative landing page. The finished app has public pages, owner-managed content, protected admin screens, saved contact messages, image uploads, email notifications, analytics, and a production deployment.

This chapter gives the project its product shape before tools enter the room. Like the old marketplace guide, it starts with the audience, the scope, the working rhythm, and the proof you will collect as you build.

## 01.01 - What You Are Building

You are building a full-stack software engineer portfolio, not a decorative landing page. By the end, the site has public pages, owner-managed content, protected admin screens, saved contact messages, image uploads, notifications, analytics, and a production deployment.

The weak version is to start with colors and animations, then hope the content catches up. The professional version starts with the audience and the proof: who must trust this portfolio, what evidence they need, and which parts of the app must stay editable after launch.

> **Interesting to read.** Search for strong engineering portfolio case studies and notice how often the best ones explain trade-offs, failures, and constraints instead of only showing screenshots.

---

## 01.02 - How To Use This Course

Work through this course in order. Each chapter is a gate: read the concept, build the named project step, verify it, and write the learning-log entry before moving on.

Create `learning-log/` inside the app repo. Each chapter tells you the exact file to write. The log is mandatory because the final review tests whether you understand the work, not whether the screens merely exist.

When you are stuck, write this before asking for help:

```txt
I expected...
Actually happened...
I checked...
My smallest next test is...
```

✅ Do make the problem smaller before asking. ❌ Don't paste an error without saying what you already checked.

---

## 01.03 - The Product And Its Audience

This planning step turns the portfolio from a vague idea into a product-shaped project. The weak approach is to decide later; the professional approach is to name the decision now, keep it small, and let later chapters build from it.

For this step, update your planning notes with the answer to the question in the title. Keep it concrete: one audience, one design direction, one content inventory, and one data strategy.

✅ Do write choices that affect files, screens, or data. ❌ Don't write inspirational phrases that cannot guide implementation.

Verify it by opening `learning-log/01-plan-the-portfolio.md` and checking that this decision is written in your own words.

---

## 01.04 - In Scope And Out Of Scope

This planning step turns the portfolio from a vague idea into a product-shaped project. The weak approach is to decide later; the professional approach is to name the decision now, keep it small, and let later chapters build from it.

For this step, update your planning notes with the answer to the question in the title. Keep it concrete: one audience, one design direction, one content inventory, and one data strategy.

✅ Do write choices that affect files, screens, or data. ❌ Don't write inspirational phrases that cannot guide implementation.

Verify it by opening `learning-log/01-plan-the-portfolio.md` and checking that this decision is written in your own words.

---

## 01.05 - Prerequisites

This is a beginner full-stack course, but it still assumes a small floor.

| You should be comfortable with | Why you need it |
|---|---|
| Basic HTML, CSS, and JavaScript | React pages build on those ideas |
| Running terminal commands | Vite, Supabase, and deploy steps use the terminal |
| Everyday Git | You will commit safe checkpoints |
| Basic React components and props | The course teaches architecture around them |

Helpful but taught as you go: Supabase, RLS, Edge Functions, deployment, and production smoke tests.

---

## 01.06 - Course Outline

The course climbs from planning to production. Every chapter leaves a visible artifact in your repo.

| # | Chapter | Done when... |
|---|---|---|
| 01 | [Plan the portfolio](../01-introduction/01.01-what-you-are-building.md) | You know the audience, sections, content inventory, design direction, and data strategy. |
| 02 | [Create the Vite project](../02-project-setup-vite-supabase-git/02.01-set-the-scene.md) | The app runs, generated files make sense, env files are safe, and Git has a clean baseline. |
| 03 | [Design the data model](../03-data-model-and-migrations/03.01-set-the-scene.md) | Tables, constraints, seed data, and migrations are planned and created. |
| 04 | [Protect data with RLS](../04-rls-and-security-basics/04.01-set-the-scene.md) | Public and owner access are enforced by the database. |
| 05 | [Design layout and routes](../05-public-layout-and-routing/05.01-set-the-scene.md) | Public pages, navbar, footer, route map, and placeholders work. |
| 06 | [Load projects from Supabase](../06-projects-from-supabase/06.01-set-the-scene.md) | Published projects load while drafts stay private. |
| 07 | [Build articles, comments, search](../07-articles-comments-search/07.01-set-the-scene.md) | Published articles, safe comments, search, and pagination work. |
| 08 | [Add owner auth and dashboard](../08-owner-auth-and-admin-dashboard/08.01-set-the-scene.md) | Owner login and protected admin shell work. |
| 09 | [Create project CRUD](../09-admin-project-crud/09.01-set-the-scene.md) | Owner can create, edit, publish, unpublish, and archive projects. |
| 10 | [Create article CRUD](../10-admin-article-crud/10.01-set-the-scene.md) | Owner can manage article drafts, previews, publishing, and comments. |
| 11 | [Add image storage](../11-image-storage/11.01-set-the-scene.md) | Images upload safely with paths and alt text. |
| 12 | [Build contact Edge Function](../12-contact-edge-function-brevo/12.01-set-the-scene.md) | Contact messages save before Brevo notification is attempted. |
| 13 | [Build contact inbox](../13-contact-inbox-realtime/13.01-set-the-scene.md) | Admin can read, update, and optionally receive live messages. |
| 14 | [Add newsletter and Cron](../14-newsletter-and-cron/14.01-set-the-scene.md) | Signup and scheduled-send planning work. |
| 15 | [Add analytics](../15-analytics-realtime-insights/15.01-set-the-scene.md) | Public visits produce useful owner-only summaries. |
| 16 | [Handle validation and states](../16-validation-errors-empty-states/16.01-set-the-scene.md) | Loading, empty, error, success, and validation states are designed. |
| 17 | [Polish responsive accessibility](../17-responsive-polish-accessibility/17.01-set-the-scene.md) | The app works on real screens and keyboard checks. |
| 18 | [Deploy to Vercel and Supabase](../18-deploy-vercel-supabase/18.01-set-the-scene.md) | Frontend, backend pieces, secrets, and smoke tests work in production. |
| 19 | [Review and maintain](../19-final-review-maintenance/19.01-set-the-scene.md) | README, demo script, maintenance checklist, and security review exist. |
| 20 | [Close the project](../20-closing/20.01-look-back-at-the-finished-app.md) | You can demo, explain, and continue improving the portfolio. |

---

## 01.07 - Your Working Rhythm

This planning step turns the portfolio from a vague idea into a product-shaped project. The weak approach is to decide later; the professional approach is to name the decision now, keep it small, and let later chapters build from it.

For this step, update your planning notes with the answer to the question in the title. Keep it concrete: one audience, one design direction, one content inventory, and one data strategy.

✅ Do write choices that affect files, screens, or data. ❌ Don't write inspirational phrases that cannot guide implementation.

Verify it by opening `learning-log/01-plan-the-portfolio.md` and checking that this decision is written in your own words.

---

## 01.08 - Content Inventory

This planning step turns the portfolio from a vague idea into a product-shaped project. The weak approach is to decide later; the professional approach is to name the decision now, keep it small, and let later chapters build from it.

For this step, update your planning notes with the answer to the question in the title. Keep it concrete: one audience, one design direction, one content inventory, and one data strategy.

✅ Do write choices that affect files, screens, or data. ❌ Don't write inspirational phrases that cannot guide implementation.

Verify it by opening `learning-log/01-plan-the-portfolio.md` and checking that this decision is written in your own words.

---

## 01.09 - Design Direction

This planning step turns the portfolio from a vague idea into a product-shaped project. The weak approach is to decide later; the professional approach is to name the decision now, keep it small, and let later chapters build from it.

For this step, update your planning notes with the answer to the question in the title. Keep it concrete: one audience, one design direction, one content inventory, and one data strategy.

✅ Do write choices that affect files, screens, or data. ❌ Don't write inspirational phrases that cannot guide implementation.

Verify it by opening `learning-log/01-plan-the-portfolio.md` and checking that this decision is written in your own words.

---

## 01.10 - Data Strategy

This planning step turns the portfolio from a vague idea into a product-shaped project. The weak approach is to decide later; the professional approach is to name the decision now, keep it small, and let later chapters build from it.

For this step, update your planning notes with the answer to the question in the title. Keep it concrete: one audience, one design direction, one content inventory, and one data strategy.

✅ Do write choices that affect files, screens, or data. ❌ Don't write inspirational phrases that cannot guide implementation.

Verify it by opening `learning-log/01-plan-the-portfolio.md` and checking that this decision is written in your own words.

---

## 01.11 - Learning Log Gate

This planning step turns the portfolio from a vague idea into a product-shaped project. The weak approach is to decide later; the professional approach is to name the decision now, keep it small, and let later chapters build from it.

For this step, update your planning notes with the answer to the question in the title. Keep it concrete: one audience, one design direction, one content inventory, and one data strategy.

✅ Do write choices that affect files, screens, or data. ❌ Don't write inspirational phrases that cannot guide implementation.

Verify it by opening `learning-log/01-plan-the-portfolio.md` and checking that this decision is written in your own words.

---

## 01.12 - Definition Of Done

This checklist is the gate for Chapter 01. Do not move on until every item is true in your own project.

- [ ] Portfolio plan exists in the repo.
- [ ] The main route, screen, table, or function for `portfolio plan` can be opened or inspected.
- [ ] The happy path has been tested.
- [ ] A failure, empty, or validation state has been tested.
- [ ] A privacy or secret-safety check has been tested where relevant.
- [ ] `docs/content-inventory.md` explains the decision and the proof.

All boxes ticked? Then continue to the next chapter. If not, that is where today's work is.
