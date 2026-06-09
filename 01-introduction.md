# Chapter 01 - Introduction

You're going to build a portfolio that behaves like a small production system. That sentence matters. A static portfolio can show taste, but this one also shows judgment: where data lives, who can change it, how private rows stay private, what happens when email fails, and how the finished app ships without leaking secrets.

This first chapter does not ask you to code yet. It asks you to understand the shape of the thing you are about to build, because beginners often get pushed straight into tools before they know what problem those tools are solving.

## The point of this chapter

By the end, you can describe the product, the two people who use it, the major system pieces, and why a database-backed portfolio is stronger evidence than a static page.

## Section 1 - The product, in plain language

The public site helps a visitor answer: *should I talk to this engineer?* It needs a strong home page, credible projects, thoughtful articles, and a contact path that does not silently lose messages.

The admin side helps the owner answer: *can I keep this portfolio alive without editing source code every time?* It needs login, content management, messages, image uploads, newsletter workflows, and basic insight into what people read.

That gives you the real shape:

```txt
Visitor -> React public pages -> Supabase public reads
Owner -> Supabase Auth -> protected admin routes -> RLS-backed writes
Contact form -> Edge Function -> database first -> Brevo second
Images -> Supabase Storage
Deployment -> Vercel frontend + Supabase backend pieces
```

## Section 2 - Why not a static portfolio?

A static version is tempting:

```txt
hard-coded project cards
hard-coded articles
mailto link
manual updates in source files
```

That can be fine for a weekend. It is not enough for this course. The moment you want drafts, contact persistence, admin editing, image management, newsletter subscribers, or security rules, static content stops being the right model.

The better version is still small, but it has boundaries you can defend. Published content is public. Drafts are private. The owner can write. Visitors cannot. Email is a notification, not the only record. Secrets live server-side.

## Section 3 - The people who use it

There are only two actors, which keeps the project focused:

- **Visitor.** Reads your work, decides whether you are credible, and contacts you.
- **Owner.** Logs in, manages content, reads messages, uploads images, and reviews simple analytics.

There is no public multi-user platform here. No payments. No social network. No complex admin hierarchy. That restraint is intentional.

## Section 4 - How to work through the course

Create `learning-log/` in the app project when Chapter 02 starts. Every chapter asks for a written explanation. Write it before the memory fades.

Move through the chapters in order. Do not skip RLS because the UI seems to hide things. Do not skip deployment checks because the homepage loads. Do not skip failure states because the happy path works once.

## Section 5 - Draw the system before tools

Create a one-page sketch in your learning log before writing any code. It should show the request paths, not just product features:

```txt
Public visitor opens /projects
  -> React route renders ProjectsPage
  -> Supabase query asks for published projects
  -> RLS blocks drafts even if the query is changed

Visitor submits contact form
  -> React calls Edge Function
  -> Function validates input
  -> Function inserts contact_messages row
  -> Function calls Brevo notification
  -> Admin inbox still has the message if Brevo fails
```

This drawing is deliberately plain. Beginners often hide confusion behind tool names. A simple request path proves you understand what talks to what.

## Section 6 - Define the chapter gates now

For this course, a chapter is finished only when you can do three things:

1. **Show it** - a route, table, policy, form, function, deployment, or checklist exists.
2. **Break it safely** - you tried the obvious failure or bypass case.
3. **Explain it** - your learning log says why this approach was chosen.

That means `it works on my machine once` is not enough. You need proof.

## Section 7 - Do it on your project

Before Chapter 02, create a planning note with these headings:

```txt
Product promise:
Public visitor needs:
Owner needs:
Data that is public:
Data that is private:
Secrets that must never reach the browser:
One failure I expect:
```

Fill it in with your own words. Do not write generic textbook definitions. Use this portfolio.

## Prove it before moving on

Explain the whole system to yourself without naming React first. If your explanation starts with tools, restart with people: visitor, owner, message, content, trust. Tools come second.

> **📖 Mandatory read.** Read [MDN's overview of HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Overview), [React's start guide](https://react.dev/learn/start-a-new-react-project), [Supabase's database overview](https://supabase.com/docs/guides/database/overview), and [Vercel's Vite deployment docs](https://vercel.com/docs/frameworks/vite). Required: you need the words browser, server, database, and deployment to mean something before you build.

> **💡 Hint.** If the app feels huge, split it into four stories: public reading, owner writing, server-side workflows, and deployment. You never have to understand the whole thing at once.

## Definition of Done

- [ ] You can describe the finished product in one minute.
- [ ] You can name the visitor workflow and the owner workflow.
- [ ] You can explain why this portfolio needs a backend.
- [ ] You can name which parts belong to React, Supabase, Brevo, and Vercel.
- [ ] You have committed to keeping a `learning-log/` folder when the app project begins.

> **✍️ Log it (mandatory).** In `learning-log/01-introduction.md`, answer: why is a database-backed portfolio stronger than a static one for a software engineer? Which part of the system do you most want to be able to explain in an interview?

All boxes ticked? Good. You know what you are building. Now make the project real without making a mess on day one.

---

Next: the product is clear; now create the project foundation without leaking secrets. -> **[Chapter 02 - Project setup with Vite, Supabase, and Git](02-project-setup-vite-supabase-git.md)**
