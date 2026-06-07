# Chapter 04 - RLS and security basics

You now have tables. That is only half the database story. The other half is deciding who can see or change each row. Supabase makes this central through **Row Level Security**, usually shortened to RLS. RLS means the database checks access rules per row, not just per API route.

## Where we're headed

By the end, public users can read only published projects and articles, only approved comments are visible publicly, only the owner can manage content, contact messages are not publicly readable, and service-role access is treated as server-only power.

## Authentication vs authorization

Authentication answers: *Who are you?*

Authorization answers: *What are you allowed to do?*

Email/password, OAuth, and magic link are login methods. They prove identity. RLS policies decide what that identity can access.

Bad:

```txt
If the React app hides the admin button, the admin data is safe.
```

Problem: UI hiding is not security. A user can call Supabase directly from the browser.

Better:

```txt
The database rejects unauthorized reads and writes even if the UI is bypassed.
```

## The policy map

Write the policy map before writing policies:

```txt
projects
  public: read where status = 'published'
  owner: insert/update/delete

articles
  public: read where status = 'published'
  owner: insert/update/delete

article_comments
  public: read where status = 'approved'
  public: insert pending comment if allowed
  owner: moderate

contact_messages
  public: no direct reads
  insert: through Edge Function
  owner: read/update/archive

newsletter_subscribers
  public: insert through Edge Function
  owner: read/update

page_visits
  public: insert limited visit metadata
  owner: read aggregate insight
```

For this portfolio, "owner" means the single authenticated portfolio owner. You can store the owner user id in a settings table, compare against `auth.uid()`, or use a small helper function. The important rule is that ownership is enforced in the database, not only in React.

## Build it

Enable RLS on every table. Add policies one table at a time. After each table, test the public case and the owner case before moving on.

Use draft seed data from Chapter 03. Try to read draft projects as a signed-out user. The correct result is no rows. Then sign in as the owner and confirm owner workflows can see or update the rows they should.

## Service-role warning

The Supabase service-role key bypasses RLS. That is useful inside Edge Functions for controlled server work. It is dangerous in the frontend. Never expose it through Vite variables, browser code, screenshots, or logs.

## Mandatory read

Read Supabase's official RLS documentation. Also read a short explanation of authentication vs authorization. Required: admin CRUD, contact inbox, and article moderation all depend on this distinction.

## Definition of Done

- [ ] RLS is enabled on every application table.
- [ ] Public users can read published projects/articles only.
- [ ] Draft content is hidden from public reads.
- [ ] Owner-only writes are blocked for signed-out users.
- [ ] Contact messages are not publicly readable.
- [ ] You can explain why service-role keys never go in frontend code.

> **Log it.** In `learning-log/04-rls-and-security.md`, write the policy map in your own words. Include one blocked case you tested.

Next: the backend is guarded. Now give visitors a public route structure they can actually navigate. -> **[Chapter 05 - Public layout and routing](05-public-layout-and-routing.md)**
