# Chapter 10 - Protected admin dashboard

Login proves identity. The dashboard gives the owner a place to act.

> **Principle.** A protected route is not protected because it looks hidden; it is protected because access is checked.

## Where we're headed

By the end, `/admin` is protected, signed-out visitors are redirected to login, and the owner sees dashboard summaries.

## Before you build

> **Mandatory read.** Review React Router protected route patterns from the React Router docs: https://reactrouter.com. Focus on route guards and redirects.

> **Apply this habit.** Read "Design for Failure" in [Daily_Software_Development_Guidelines.md](../Daily_Software_Development_Guidelines.md), then decide what appears while auth is loading.

## Step 1 - Create admin routes

Create:

```txt
/admin
/admin/projects
/admin/articles
/admin/messages
```

## Step 2 - Build `RequireAuth`

Create a wrapper that:

- waits while auth loads;
- allows signed-in owner;
- redirects signed-out users to login.

Do not rely on hiding nav links. A user can type a URL.

## Step 3 - Build dashboard cards

Show simple counts:

```txt
published projects
draft projects
published articles
draft articles
unread messages
```

## Step 4 - Add admin navigation

Admin navigation should be separate from public navigation.

## Step 5 - Test direct URLs

Open `/admin/projects` while signed out. It should not show admin data.

## What your screen should show

Signed-in owner sees dashboard summaries. Signed-out visitors see login or redirect.

## Small challenge

Add one dashboard card that reminds the owner to update the portfolio monthly.

Suggested commit:

```bash
git commit -m "feat: protect admin dashboard"
```

## Definition of Done

- [ ] Admin routes exist.
- [ ] Signed-out users cannot access admin pages.
- [ ] Auth loading state exists.
- [ ] Admin dashboard shows useful counts.
- [ ] Admin navigation exists.
- [ ] Direct URL access is tested.

> **Log it.** In `learning-log/10-protected-admin-dashboard.md`: What protects the admin area in the UI? What still depends on RLS?

Next: manage projects. -> **[Chapter 11 - Admin project CRUD](11-admin-project-crud.md)**
