# Chapter 01 - Introduction

You're building a real, deployed **full-stack software engineer portfolio**. Not a static page. Not a template with your name dropped into it. A small production-shaped system where the public site shows your work, the owner manages content from an admin dashboard, visitors can contact you, and the backend protects what should not be public.

The stack is deliberately modern but not magical: **Vite + React + TailwindCSS + shadcn/ui** for the frontend, **Supabase** for Postgres, Auth, Row Level Security, Storage, Edge Functions, Realtime, and Cron, **Brevo** for email notifications, and **Vercel** for deployment.

The finished app answers a human question first: *Can someone trust this engineer enough to start a conversation?* Then it answers the engineering questions hiding underneath: *Where does the data live? Who can change it? Where do secrets live? What happens if email fails? What does the owner see that a visitor cannot?*

## Where we're headed

By the end you will have a deployed portfolio with public pages, projects, articles, comments, contact form persistence, Brevo email notifications, newsletter subscriptions, page visit tracking, image uploads, owner login, admin CRUD, a contact inbox, RLS policies, and a production deployment.

## The tempting version, and why it is too small

The tempting version is a static portfolio:

```txt
React pages
Hard-coded project cards
mailto: contact link
manual updates in source code
```

That is fine for a weekend demo, but it avoids the decisions employers actually care about. It does not show how you model data, protect private records, handle failure, store images, deploy secrets, or build owner workflows.

The better version is still small, but it has real system boundaries:

```txt
Public visitor -> React pages -> Supabase public reads
Owner -> Supabase Auth -> protected admin dashboard
Contact form -> Edge Function -> contact_messages + Brevo notification
Images -> Supabase Storage
Deployment -> Vercel + Supabase secrets
```

This course is about that better version.

## The people who use it

- **Visitor.** Wants to quickly understand who you are, what you can build, whether your work is credible, and how to contact you.
- **Portfolio owner.** Wants to add projects, publish articles, review messages, see basic visit signals, and update content without editing code.

## In scope

- Public portfolio pages for home, about, projects, articles, article details, contact, and not-found.
- Supabase Postgres tables for projects, articles, comments, contact messages, newsletter subscribers, page visits, newsletter runs, and profile settings.
- Supabase Auth for one owner account using email/password, OAuth, or magic link.
- Row Level Security so public users only read published content and the owner controls admin data.
- Supabase Storage for project and article images.
- Supabase Edge Functions for contact submission and newsletter/email workflows.
- Brevo transactional email from server-side functions only.
- Vercel deployment with public Vite env vars separated from private Supabase/Brevo secrets.

## Out of scope

- A public multi-user platform. This is owner-managed, not a social network.
- Payment processing.
- Complex analytics that require a third-party tracking platform.
- Giving the learner solution code to copy. The guide names what to build and why; the learner writes the implementation.

## Definition of Done

- [ ] You can describe the finished product in one minute.
- [ ] You can name the public user and the owner user.
- [ ] You can explain why this portfolio needs a backend.
- [ ] You can explain which parts belong in Supabase, Vercel, and Brevo.
- [ ] You have created a `learning-log/` folder in the project you will build.

> **Log it.** In `learning-log/01-introduction.md`, answer: why is a database-backed portfolio stronger than a static one for a software engineer? Which part of the system are you most likely to be asked about in an interview?

Next: the product is clear. Now create the project foundation without leaking secrets or making setup painful. -> **[Chapter 02 - Project setup with Vite, Supabase, and Git](02-project-setup-vite-supabase-git.md)**
