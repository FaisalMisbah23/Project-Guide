# Chapter 08 - Owner Auth And Admin Dashboard

The public site can read content. Now the owner needs a private workspace. This chapter adds login, protected admin routes, and the admin dashboard shell.

## Goal

By the end, the owner can sign in and view a protected admin dashboard while signed-out users are kept out of admin screens.

## What You Will Build

- Login page.
- Auth helper functions.
- Protected route wrapper.
- Admin layout.
- Dashboard navigation.
- Placeholder admin pages.

## Beginner Concepts

- **Authentication:** proving who a user is.
- **Session:** saved login state.
- **Route guard:** React logic that redirects signed-out users.
- **Admin shell:** shared layout for private pages.
- **RLS:** database protection that still matters even with route guards.

## Step By Step

### Step 1 - Create Auth Feature Files

Create:

```txt
src/features/auth/
  authApi.ts
  useSession.ts
```

`authApi.ts` should wrap Supabase login/logout calls. `useSession.ts` should help React know whether the owner is signed in.

### Step 2 - Add Admin Routes

Add these routes:

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

### Step 3 - Build The Login Page

Create:

```txt
src/pages/admin/LoginPage.tsx
```

The form should ask for email and password. On success, send the owner to `/admin`.

### Step 4 - Build `RequireAuth`

Create:

```txt
src/routes/RequireAuth.tsx
```

Behavior:

```txt
session loading -> show loading state
no session -> redirect to /admin/login
session exists -> render admin page
```

### Step 5 - Build The Admin Layout

Create:

```txt
src/pages/admin/AdminLayout.tsx
src/pages/admin/AdminDashboardPage.tsx
```

The layout should include private navigation for dashboard, projects, articles, images, messages, newsletter, and analytics.

### Step 6 - Confirm RLS Still Protects Data

Route guards improve user experience. They do not replace RLS. Test a signed-out database query for private rows and confirm it is blocked.

## Common Mistakes

| Mistake | Why it hurts | Fix |
|---|---|---|
| Treating route guard as security | Browser code can be bypassed | Keep RLS policies |
| Letting any signed-in user edit | Wrong user can become admin | Check owner identity in RLS |
| No loading state | Auth check flashes wrong page | Show loading while session loads |
| Admin links mixed with public nav | Visitors see irrelevant links | Keep admin layout separate |

## Checks Before Moving On

- Owner can log in.
- Signed-out visitor is redirected from `/admin`.
- Admin layout appears after login.
- Dashboard navigation exists.
- RLS still blocks private rows when signed out.

## Learning Log

In `learning-log/08-owner-auth-and-admin-dashboard.md`, answer:

```txt
What does authentication prove?
What does the route guard do?
What does RLS do that the route guard cannot?
Which admin sections will future chapters fill in?
```

## Definition Of Done

- [ ] Login page exists.
- [ ] Session state is handled.
- [ ] Protected admin routes exist.
- [ ] Admin layout and navigation exist.
- [ ] Signed-out users cannot browse admin pages.
- [ ] RLS still blocks private data directly.

Next: add project management. -> **[Chapter 09 - Admin Project CRUD](09-admin-project-crud.md)**
