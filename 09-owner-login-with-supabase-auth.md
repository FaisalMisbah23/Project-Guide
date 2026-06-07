# Chapter 9 - Owner login with Supabase Auth

The public site can read published content. Now the owner needs a protected way to manage drafts, messages, and images.

> **Principle.** Admin power starts with proving who is using it.

## Where we're headed

By the end, the owner can sign in and sign out with Supabase Auth, and the app knows the current session.

## Before you build

> **Mandatory read.** Read Supabase Auth docs: https://supabase.com/docs/guides/auth. Focus on sessions and the current user.

> **Apply this habit.** Read "Validate Input Everywhere" in [Daily_Software_Development_Guidelines.md](../Daily_Software_Development_Guidelines.md), then define what login errors should say.

## Step 1 - Create the owner account

Create one owner account in Supabase Auth. This account is the only person who should manage the portfolio.

Do not add open public registration. A portfolio admin is not a social app.

## Step 2 - Build login page

Create:

```txt
src/pages/admin/
  Login.jsx
```

The form needs:

```txt
email
password
```

Show clear errors without revealing too much.

## Step 3 - Track auth session

Create an auth helper or provider that can answer:

```txt
Is the owner signed in?
Is auth still loading?
Who is the current user?
```

## Step 4 - Add sign out

The admin area needs a visible sign-out action.

## Step 5 - Test bad login

Test:

- wrong password;
- empty email;
- signed-out refresh;
- sign out then back button.

## What your screen should show

The owner can sign in, see an authenticated state, and sign out.

## Small challenge

Write the login error copy so it is helpful but does not reveal whether an email exists.

Suggested commit:

```bash
git commit -m "feat: add owner login"
```

## Definition of Done

- [ ] Owner account exists.
- [ ] Login page exists.
- [ ] Login handles loading and errors.
- [ ] Session is tracked.
- [ ] Sign out works.
- [ ] Public registration is not exposed.

> **Log it.** In `learning-log/09-owner-login-with-supabase-auth.md`: Why does this app need auth? Why is public registration out of scope?

Next: protect the admin area. -> **[Chapter 10 - Protected admin dashboard](10-protected-admin-dashboard.md)**
