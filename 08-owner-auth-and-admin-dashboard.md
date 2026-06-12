# Chapter 08 - Add owner auth and dashboard

> Owner auth is where the portfolio stops being a public brochure and becomes a managed product. The lesson from the marketplace guide is the same here: authentication says who you are; authorization says what you may touch.

## 08.01 - Set The Scene

The project now needs **owner auth and admin dashboard**. This chapter adds admin workspace while keeping the portfolio understandable for a beginner and reviewable by a mentor.

The story of this chapter is simple: the owner needs a smooth private workspace, but the database must still protect the content if the browser is bypassed. You will build the professional version from the start, but you will still understand why the tempting shortcut fails.

By the end, `learning-log/08-owner-auth-and-admin-dashboard.md` will explain what you built and why it matters.

---

## 08.02 - Why Owner Auth Matters

This step continues owner auth and admin dashboard from the previous sub-chapter. Keep the step small enough that you can verify it before moving on.

Touch the relevant file or route from this chapter:

```txt
src/features/auth/
src/routes/RequireAuth.tsx
src/pages/admin/
learning-log/08-owner-auth-and-admin-dashboard.md
```

✅ Do make one concrete change and verify it. ❌ Don't merge several untested ideas into one large edit.

**Hint.** If you cannot name what changed after this step, the step is too broad.

---

## 08.03 - What You Will Build

In this chapter you will produce admin workspace.

The visible surface is: admin login. The protected or owner-facing surface is: protected admin shell.

Expected project touchpoints:

```txt
src/features/auth/
src/routes/RequireAuth.tsx
src/pages/admin/
learning-log/08-owner-auth-and-admin-dashboard.md
```

Routes or screens involved:

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

Database areas involved:

```txt
profiles or owner allowlist
projects
articles
contact_messages
```

---

## 08.04 - Authentication Vs Authorization

Authentication proves who the owner is. Authorization decides what that signed-in person is allowed to do.

The weak approach is to treat "signed in" as the whole security story. The professional approach is to sign the owner in, then still ask what that identity may access.

For this portfolio, Supabase Auth answers identity. RLS and owner checks answer permission.


> **Hint.** Ask whether this rule would still hold if someone typed the URL manually or called Supabase outside your UI.

---

## 08.05 - Route Guards Vs Rls

A route guard is React logic that decides whether to render an admin page. RLS is database logic that decides whether rows can be read or changed.

The route guard is useful for experience: signed-out visitors are redirected instead of seeing a broken admin page. It is not enough for security because browser code can be inspected and changed.

✅ Do use both. ❌ Don't replace RLS with a private-looking route.


> **Hint.** Ask whether this rule would still hold if someone typed the URL manually or called Supabase outside your UI.

---

## 08.06 - Sessions In Supabase

Connect the chapter to Supabase only after the local shape works. The client should request exactly the data the UI needs and no private extras.

For `owner auth and admin dashboard`, the query or function should respect:

```txt
public data only for visitors
owner-only data only after auth and policy checks
clear error when Supabase refuses the request
```

✅ Do filter at the query and enforce with RLS. ❌ Don't fetch broad rows and hide fields in React.

Verify with one successful request and one request that should be blocked.

---

## 08.07 - Reading Before You Build

Before building, read or search these topics. The chapter explains the idea first; these readings deepen it.

**Mandatory reads**

- **Supabase Auth with React** - read this because it supports `owner auth and admin dashboard`.
- **Authentication vs authorization** - read this because it supports `owner auth and admin dashboard`.
- **Client-side route guards and why they are not security** - read this because it supports `owner auth and admin dashboard`.

After reading, write two sentences in `learning-log/08-owner-auth-and-admin-dashboard.md`: one idea you understood, and one question you still have.

---

## 08.08 - Where The Project Is Now

Chapter 07 left you with article system. Now this chapter adds admin workspace.

Before touching code, run the smallest check that proves the previous chapter still works. For UI chapters, open the relevant route. For database chapters, inspect the table or policy. For deployment chapters, run the local build first.

✅ Do start from a working baseline. ❌ Don't stack new work on top of a broken previous chapter.

---

## 08.09 - Scaffold Auth Files

Create the folders and files for this chapter before writing feature logic. The scaffold is the map your future self follows.

```txt
src/features/auth/
src/routes/RequireAuth.tsx
src/pages/admin/
learning-log/08-owner-auth-and-admin-dashboard.md
```

Each file should have a clear job. If a file starts doing two unrelated jobs, split it before it becomes hard to test.

✅ Do create empty files or small placeholders with names that match the course. ❌ Don't paste final feature logic yet; first make the shape visible.

Verify with `find` or your editor file tree that every named file exists.

---

## 08.10 - Define The Admin Route Map

The admin route map is the private workspace spine.

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

✅ Do keep admin routes under `/admin`. ❌ Don't mix admin-only links into the public navbar.


> **Hint.** Ask whether this rule would still hold if someone typed the URL manually or called Supabase outside your UI.

---

## 08.11 - Create Auth Api Contract

Define the contract before the implementation. A contract says what must go in, what must come out, and what failure looks like.

```txt
Feature: owner auth and admin dashboard
Input: the smallest data needed for this step
Success: the user sees or receives the expected state
Failure: invalid, missing, private, or not-found data is handled clearly
```

✅ Do write the contract in comments, docs, or types before logic. ❌ Don't let the first implementation secretly decide the rules.

**Hint.** If you cannot describe the failure response, you are not ready to write the happy path.

---

## 08.12 - Create Use Session Contract

Define the contract before the implementation. A contract says what must go in, what must come out, and what failure looks like.

```txt
Feature: owner auth and admin dashboard
Input: the smallest data needed for this step
Success: the user sees or receives the expected state
Failure: invalid, missing, private, or not-found data is handled clearly
```

✅ Do write the contract in comments, docs, or types before logic. ❌ Don't let the first implementation secretly decide the rules.

**Hint.** If you cannot describe the failure response, you are not ready to write the happy path.

---

## 08.13 - Build Login Page Shell

Create `src/pages/admin/LoginPage.tsx`.

The shell needs an email field, password field, submit action, loading state, and error space. It should redirect to `/admin` only after sign-in succeeds.

✅ Do label both fields. ❌ Don't use placeholders as the only labels.


> **Hint.** Ask whether this rule would still hold if someone typed the URL manually or called Supabase outside your UI.

---

## 08.14 - Handle Login States

The login page needs four states: idle, submitting, success redirect, and error.

The weak version leaves the button clickable during submit, causing duplicate requests. The professional version disables the submit action while the request is in flight and shows a calm error when sign-in fails.


> **Hint.** Ask whether this rule would still hold if someone typed the URL manually or called Supabase outside your UI.

---

## 08.15 - Build Require Auth

Create `src/routes/RequireAuth.tsx`.

Behavior contract:

```txt
session loading -> show loading state
no session -> redirect to /admin/login
session exists -> render the admin page
```

✅ Do preserve the destination when useful. ❌ Don't render private children while loading is unresolved.


> **Hint.** Ask whether this rule would still hold if someone typed the URL manually or called Supabase outside your UI.

---

## 08.16 - Wire Admin Routes

Now connect the new piece to the app. Wiring means the route, component, helper, or function is reachable from the place a user or owner naturally expects.

For this chapter, check these entry points:

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

✅ Do wire one path and test it before adding another. ❌ Don't leave orphaned files that exist but cannot be reached.

---

## 08.17 - Build Admin Layout

Create the shared admin layout.

It should include private navigation, a clear page area, and a sign-out action. Admin screens should feel like a workbench, not a marketing page.

✅ Do keep admin navigation separate from public navigation. ❌ Don't show owner tools to public visitors.


> **Hint.** Ask whether this rule would still hold if someone typed the URL manually or called Supabase outside your UI.

---

## 08.18 - Create Dashboard Placeholders

Create placeholders for the admin sections future chapters will fill.

Each placeholder should say what the owner will manage there and should link from the admin layout.

Do not build CRUD yet. This chapter proves the shell; later chapters fill the tools.


> **Hint.** Ask whether this rule would still hold if someone typed the URL manually or called Supabase outside your UI.

---

## 08.19 - Separate Public And Admin Navigation

Check the navigation boundary.

Public navigation should guide visitors to portfolio content. Admin navigation should guide the owner to management tasks.

✅ Do make `/admin/login` reachable in a deliberate way. ❌ Don't add a loud "Admin" button to the visitor-facing hero.


> **Hint.** Ask whether this rule would still hold if someone typed the URL manually or called Supabase outside your UI.

---

## 08.20 - Test Signed Out Redirect

Test while signed out.

Open:

```txt
/admin
/admin/projects
/admin/messages
```

Each should redirect to `/admin/login` or show the signed-out admin flow. Record the result in the learning log.


> **Hint.** Ask whether this rule would still hold if someone typed the URL manually or called Supabase outside your UI.

---

## 08.21 - Test Owner Login

Test the owner login.

Use the owner account created in Supabase Auth. A successful login should reach `/admin`, show the admin layout, and preserve the session after refresh.

✅ Do test refresh. ❌ Don't count a single redirect as proof that session state works.


> **Hint.** Ask whether this rule would still hold if someone typed the URL manually or called Supabase outside your UI.

---

## 08.22 - Prove Rls Still Protects Data

Protect the private side of owner auth and admin dashboard. Browser checks improve experience, but the database or server boundary must enforce the rule.

Run the privacy check as a signed-out user or anon client. The expected result is not hidden UI; the expected result is no private data.

✅ Do test the boundary directly. ❌ Don't trust that a missing link means the feature is secure.

**Hint.** Security checks should still pass if someone types the URL manually.

---

## 08.23 - Write The Learning Log

Create or update `learning-log/08-owner-auth-and-admin-dashboard.md`.

Answer these in your own words:

```txt
What did Chapter 08 add to the project?
What shortcut did you avoid, and why was it risky?
Which file, route, table, or screen proves the work is real?
What failure or privacy check did you run?
```

The learning log is part of the gate. If you cannot explain the chapter, the feature is not finished yet.

✅ Do write short, specific answers tied to your repo. ❌ Don't copy the chapter text back as a summary.

---

## 08.24 - Recap And Next Chapter

You added admin workspace and proved it with visible checks. The important lesson is not only that the feature works; it is that you can explain why this shape is safer than the shortcut.

Next, Chapter 09 builds project management screens.

Before moving on, commit the work with a message that names the chapter outcome.

---

## 08.25 - Definition Of Done

This checklist is the gate for Chapter 08. Do not move on until every item is true in your own project.

- [ ] Admin workspace exists in the repo.
- [ ] The main route, screen, table, or function for `owner auth and admin dashboard` can be opened or inspected.
- [ ] The happy path has been tested.
- [ ] A failure, empty, or validation state has been tested.
- [ ] A privacy or secret-safety check has been tested where relevant.
- [ ] `learning-log/08-owner-auth-and-admin-dashboard.md` explains the decision and the proof.

All boxes ticked? Then continue to the next chapter. If not, that is where today's work is.
