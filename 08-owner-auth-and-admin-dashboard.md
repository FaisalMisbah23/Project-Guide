# Chapter 08 - Owner auth and admin dashboard

The public site now reads from Supabase. The owner needs a private workspace to manage that content. This is where authentication becomes visible.

## Where we're headed

By the end, the owner can sign in with a chosen login method, protected admin routes reject signed-out users, and the dashboard summarizes projects, articles, contact messages, subscribers, and visit signals.

## Login choices

Supabase supports email/password, OAuth, and magic link login.

Email/password is familiar and simple to demonstrate.

OAuth is convenient if the owner wants GitHub or Google login.

Magic link reduces password handling but depends on email deliverability and can feel slower.

Choose one for the first build. Do not build all three unless the course explicitly needs them.

## The auth trap

Bad:

```txt
if (isAdmin) show dashboard
```

Problem: where did `isAdmin` come from? If it only lives in React state, refreshing or manipulating the app breaks the assumption.

Better:

```txt
Supabase Auth session -> protected route -> RLS-backed queries
```

The UI protects navigation. The database protects data. You need both.

## Build it

Create `/admin/login` and `/admin`. Build a `RequireAuth` wrapper that waits for the Supabase session, shows a loading state while checking, redirects signed-out users, and lets signed-in owners continue.

The dashboard should be useful, not decorative. Add summary cards:

```txt
Published projects
Draft articles
Unread contact messages
Newsletter subscribers
Recent visits
```

Add sign out. Test direct URL access by opening `/admin` in a signed-out browser session.

## Definition of Done

- [ ] Owner login works with the chosen method.
- [ ] Sign out works.
- [ ] Protected admin routes reject signed-out visitors.
- [ ] Auth loading state prevents flicker.
- [ ] Dashboard shows useful summary cards.
- [ ] RLS still blocks unauthorized data if the route is bypassed.

> **Log it.** In `learning-log/08-owner-auth-and-admin-dashboard.md`, explain the difference between route protection and RLS protection.

Next: the owner can enter the dashboard. Now give them control over projects. -> **[Chapter 09 - Admin project CRUD](09-admin-project-crud.md)**
