# Chapter 08 - Owner auth and admin dashboard

The public site can now read content. The owner needs a private door. This is where beginners often confuse two different protections: a route guard that keeps the UI tidy, and RLS that keeps the database safe.

## The point of this chapter

Supabase Auth login, protected admin routes, logout, owner verification, and an admin dashboard shell that future admin features plug into.

## Before you touch code

- RLS owner policies exist for at least one admin table.
- `owner_profile` contains the intended owner user id.
- Public routes still work signed out.
- You know which admin routes will exist.

## Vocabulary for this chapter

- **Session.** Browser-held proof that Supabase Auth knows the user.
- **Protected route.** A UI route that redirects when no session exists.
- **Owner check.** Database-backed check that the signed-in user is the portfolio owner.
- **Admin shell.** Shared private layout for admin pages.

## Guided snippet or contract

This is a shape to aim for, not a finished solution to paste blindly:

```txt
Admin route contract
  /admin/login      public login screen
  /admin            owner dashboard
  /admin/projects   owner project management
  /admin/articles   owner article management
  /admin/messages   owner inbox
  /admin/newsletter owner newsletter runs/subscribers
  /admin/analytics  owner analytics summaries
```

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

## If it breaks

| Symptom | Likely cause | Smallest next test |
|---|---|---|
| Admin page flashes then redirects | Session loading state is treated as signed out | Add an explicit loading branch before redirect. |
| Any signed-in user can access data | Owner identity is not checked by RLS | Test with a second non-owner user. |
| Login works but queries fail | `owner_profile.user_id` does not match session user | Compare auth user id with owner row. |
| Logout does not clear UI | Session state is cached in app state | Subscribe to auth state changes or refetch session after logout. |

## What you should be able to explain

- Why route protection is UX and RLS is security.
- Why any signed-in user is not automatically owner.
- How admin shell helps later chapters.

## The slower beginner path

If this chapter feels too large, split the owner auth and dashboard feature into one sitting per checkpoint. The goal is not to finish fast; the goal is to finish with proof.

### Sitting 1 - Read and translate

- Read the mandatory docs with this chapter open beside you.
- Write five plain-language notes in the learning log.
- Circle any word you cannot define yet.
- Rewrite the point of the chapter in your own words.
- Stop before coding if you cannot explain what you are about to change.

### Sitting 2 - Create the smallest artifact

- Create only the first file, table, route, policy, function, checklist, or note this chapter requires.
- Add placeholder content or a tiny shape before trying to make it complete.
- Run the smallest possible check.
- If it fails, debug that one artifact before adding the next one.

### Sitting 3 - Connect the artifact

- Connect the artifact to the previous chapter's work.
- Keep the connection narrow: one query, one route, one form submit, one policy, or one checklist item.
- Add a visible loading, empty, blocked, or failure state if this chapter touches UI or data.
- Write down what changed in the request flow.

### Sitting 4 - Break it safely

- Try the shortcut this chapter warned you about in a harmless way.
- Try the most likely beginner mistake from the troubleshooting table.
- Confirm the app fails safely, or fix it until it does.
- Record the before/after in the learning log.

## Checkpoints during the work

Use this mini-review after each sitting:

```txt
What did I create or change?
What command, route, query, or click proves it exists?
What private data or failure case did I protect?
What is the next smallest test?
```

If you cannot answer the second question, you do not have proof yet. If you cannot answer the third question, you may have built only the happy path.

## Suggested commit rhythm

Make small commits when code changes. A good commit for this chapter should complete one idea, not the whole universe:

```txt
setup: add safe Supabase client shape
schema: add project and article tables
security: add public published-project policy
ui: add project loading and empty states
admin: add project archive action
ops: add production smoke-test checklist
```

Use the style that fits your repo, but keep the habit: one clear change, one clear reason, one checkpoint you can return to.

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
