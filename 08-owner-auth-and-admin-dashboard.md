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

## New ideas before you build

### Protected routes

**Real-life analogy:** a staff-only door checks your badge before opening. A protected route checks the session before showing admin screens.

**General idea:** route protection is for navigation and user experience. RLS is still required because users can bypass React and call Supabase directly.

```tsx
function RequireAuth({ children }) {
  if (isLoadingSession) return <p>Checking session...</p>;
  if (!session) return <Navigate to="/admin/login" />;
  return children;
}
```

Study more: [React Crash Course - Components and Props](https://resources.devweekends.com/courses/react-crash-course/02-components-props)

### Dashboard summaries

**Real-life analogy:** a car dashboard shows speed, fuel, and warning lights. An admin dashboard shows what needs attention.

**General idea:** summary cards should answer practical questions quickly: how many drafts, unread messages, subscribers, and recent visits exist.

```tsx
<StatCard label="Unread messages" value={unreadCount} />
```

Study more: [Frontend Interview Questions - React Fundamentals](https://resources.devweekends.com/resources/frontend-interview-qs)

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

## Between chapters

**Blog links:** read [MDN - Using HTTP cookies](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies), [MDN - Session management](https://developer.mozilla.org/en-US/docs/Web/Security/Authentication/Session_management), and [MDN - Overview of HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Overview). Pay attention to cookies, sessions, and the idea that HTTP is stateless but not sessionless.

**Quick quiz:** if a signed-out visitor manually types `/admin`, what should React do? If the same visitor calls Supabase directly, what should the database do?

**Assignment:** write a one-minute explanation of your login choice: email/password, OAuth, or magic link. Include one tradeoff.

**Auth exercise:** test `/admin` in three states: signed out, signed in as owner, and after signing out in another tab. Record what the UI shows while the session is loading.

**Comparison:** session vs cookie: a cookie is a small value stored by the browser. A session is the user's logged-in state, often represented or refreshed using cookies or tokens.

**Big word alert:** **stateless** means the server does not automatically remember previous requests. Login systems add session mechanisms so the app can still recognize a returning user.

Next: the owner can enter the dashboard. Now give them control over projects. -> **[Chapter 09 - Admin project CRUD](09-admin-project-crud.md)**
