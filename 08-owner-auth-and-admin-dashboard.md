# Chapter 08 - Owner auth and admin dashboard

The public site can now read content. The owner needs a private door. This is where beginners often confuse two different protections: a route guard that keeps the UI tidy, and RLS that keeps the database safe.

## The point of this chapter

Supabase Auth login, protected admin routes, logout, owner verification, and an admin dashboard shell that future admin features plug into.

## Step 1 - Pick the simple auth path

Use email/password or magic link. Do not build custom auth from scratch. Supabase Auth already handles sessions; your job is to integrate it clearly.

## Step 2 - Protect routes for user experience

Create `/admin/login`, an admin layout, and a `RequireAuth` style guard. Signed-out visitors should not wander through admin screens.

## Step 3 - Verify owner, not just signed-in

Any signed-in user is not automatically the owner. Connect the session user id to `owner_profile` and let RLS decide owner-only access.

## Step 4 - Build the shell before the features

Add dashboard navigation for projects, articles, images, messages, newsletter, and analytics. Empty sections are fine today; the shell gives later chapters a home.

## Step 5 - Draw the auth flow

Write the flow before wiring components:

```txt
Visitor opens /admin/projects
  -> route checks session loading
  -> no session: redirect to /admin/login
  -> session exists: render admin layout
  -> data query still depends on RLS and owner_profile
```

The route guard improves navigation. RLS protects data. Keep repeating that until it is boring.

## Step 6 - Create the admin route map

```txt
/admin/login
/admin
/admin/projects
/admin/articles
/admin/images
/admin/messages
/admin/newsletter
/admin/analytics
```

Some pages can be placeholders today. The shell is the important artifact: a private workspace where future chapters land.

## Step 7 - Do it on your project

Create:

```txt
src/features/auth/
src/routes/RequireAuth.tsx
src/pages/admin/AdminLayout.tsx
src/pages/admin/AdminDashboardPage.tsx
src/pages/admin/LoginPage.tsx
```

Add logout early. Beginners often build login and forget the way out.

## Prove it before moving on

Test three paths:

```txt
signed out opens /admin/projects -> redirected
owner logs in -> dashboard opens
signed out direct Supabase query for private table -> blocked by RLS
```

If the third path fails, do not continue to CRUD.

> **📖 Mandatory read.** Read [Supabase Auth](https://supabase.com/docs/guides/auth), [React Router](https://reactrouter.com/home), and [Supabase RLS](https://supabase.com/docs/guides/database/postgres/row-level-security). Required: this chapter makes the difference between identity, route protection, and database permission concrete.

> **💡 Hint.** After route protection works, still test a direct Supabase query as a signed-out user. The database should reject private data even if the UI is bypassed.

## Definition of Done

- [ ] Owner can log in and log out.
- [ ] Signed-out users are redirected away from admin routes.
- [ ] Admin layout and navigation exist.
- [ ] The signed-in owner matches `owner_profile`.
- [ ] RLS still blocks unauthorized database access if the route is bypassed.
- [ ] Session loading has a visible state instead of a blank screen.

> **✍️ Log it (mandatory).** In `learning-log/08-owner-auth-and-admin-dashboard.md`: explain route protection vs RLS protection. Give one example where route protection helps UX but does not secure data.

All boxes ticked? Then continue. The next chapter builds on this gate, not around it.

---

Next: the owner can enter; now give them control over projects. -> **[Chapter 09 - Admin project CRUD](09-admin-project-crud.md)**
