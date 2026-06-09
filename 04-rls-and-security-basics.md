# Chapter 04 - RLS and security basics

You now have tables, which means you also have a problem: tables will answer questions unless you teach them who is allowed to ask. A hidden admin button is not security. A route guard is not database security. A public anon key is not dangerous by itself, but an anon key against badly protected tables absolutely is.

This chapter is the security hinge of the whole course.

## The point of this chapter

Public users can read only public rows. The owner can manage owner-only content. Contact messages and subscribers stay private. The service-role key is treated as server-only power. RLS, not React, becomes the guardrail.

## Section 1 - Authentication is not authorization

Authentication answers: *who are you?* Authorization answers: *what are you allowed to do?*

A signed-in user is not automatically the owner. A hidden admin link does not stop someone from calling Supabase directly. RLS policies are where the database decides whether a row may be read or changed.

## Section 2 - Write the policy map first

Before SQL, write the rules:

```txt
projects: public reads published; owner writes
articles: public reads published; owner writes
article_comments: public reads approved; public may insert pending if allowed; owner moderates
contact_messages: no public reads; owner reads and archives
newsletter_subscribers: no public reads; signup through server workflow
page_visits: minimal public insert or server insert; owner reads summaries
owner_profile: private owner identity source
```

That map is the spec. Policies implement it.

## Section 3 - Use one owner helper

Use the owner table from Chapter 03. A teaching-safe helper should schema-qualify objects and fix its search path:

```sql
create or replace function public.is_owner()
returns boolean
language sql
security definer
set search_path = public
as $$
  select exists (
    select 1
    from public.owner_profile
    where owner_profile.user_id = auth.uid()
  );
$$;
```

This helper is for owner-only policies. Do not use it as a shortcut to make public features work. If public reads fail, fix the public policy; do not reach for service-role.

## Section 5 - Write policies one table at a time

Do not enable everything and hope. Work table by table:

```txt
projects
  public select: status = 'published'
  owner insert/update/delete: public.is_owner()

articles
  public select: status = 'published'
  owner insert/update/delete: public.is_owner()

contact_messages
  public select: never
  owner select/update: public.is_owner()
```

After each table, test both an allowed case and a blocked case. Security work done in one giant batch is hard to debug.

## Section 6 - Understand the anon key boundary

The anon key is not a password in the normal sense. It is allowed in the browser because the database is supposed to enforce permissions with RLS. That gives you this rule:

| Key | Browser? | Why |
|---|---:|---|
| Supabase anon key | yes | limited by RLS policies |
| Supabase service-role key | no | bypasses RLS entirely |
| Brevo API key | no | can send email as your account |
| Database password | no | direct database power |

If a feature only works when you move service-role into React, the feature is not fixed. It is unsafe.

## Section 7 - Do it on your project

Create a written `policy-map.md` or learning-log section before writing policies. Then implement policies in this order:

1. Enable RLS on all app tables.
2. Create and test `public.is_owner()`.
3. Add public read policies for published/approved content.
4. Add owner policies for admin-managed tables.
5. Add narrow insert policies only where public insertion is intentional.
6. Leave private tables private by default.

## Section 8 - Prove blocked access directly

Use the public Supabase client, browser console, or a small script. Test:

```txt
public reads published project        -> allowed
public reads draft project            -> blocked or empty
public reads contact_messages         -> blocked or empty
signed-out updates article            -> blocked
owner updates own project             -> allowed
```

Record the exact result in the learning log. Security you did not test is a hope, not a gate.

> **📖 Mandatory read.** Read [Supabase Row Level Security](https://supabase.com/docs/guides/database/postgres/row-level-security), [PostgreSQL row security](https://www.postgresql.org/docs/current/ddl-rowsecurity.html), [Supabase Auth](https://supabase.com/docs/guides/auth), and [Supabase function secrets](https://supabase.com/docs/guides/functions/secrets). Required: admin CRUD, inbox, comments, analytics, and deployment all depend on this distinction.

## Section 4 - Test blocked cases like an attacker

After each policy, test both sides. Public should read published projects but not drafts. Signed-out users should not update articles. Public users should not read contact messages. The owner should still be able to do owner work.

Use the browser console or a tiny script with the anon key. That is the point: prove the database rejects bypass attempts.

> **💡 Hint.** A correct blocked read often returns no rows, not dramatic fireworks. Learn what success looks like for both allowed and blocked cases.

## Definition of Done

- [ ] RLS is enabled on every application table.
- [ ] Public users can read published projects/articles and approved comments only.
- [ ] Draft content is hidden from public reads.
- [ ] Owner-only policies use one consistent `public.is_owner()` helper or equivalent.
- [ ] The owner identity table is not publicly readable or editable.
- [ ] Contact messages and subscribers are not publicly readable.
- [ ] Signed-out write attempts fail.
- [ ] You can explain why the anon key is browser-safe only when RLS is correct.
- [ ] No service-role key appears in frontend code.

> **✍️ Log it (mandatory).** In `learning-log/04-rls-and-security.md`: write your policy map, then describe one blocked read and one blocked write you tested. Explain why service-role must never go in React.

All boxes ticked? Then the backend has its guardrails. Now build pages visitors can actually navigate.

---

Next: the backend has guardrails; now give visitors a route structure they can navigate. -> **[Chapter 05 - Public layout and routing](05-public-layout-and-routing.md)**
