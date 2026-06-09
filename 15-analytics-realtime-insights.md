# Chapter 15 - Analytics and Realtime insights

A portfolio owner benefits from knowing what people read. But analytics is a trust decision. You are not building an ad-tech platform, and browser-submitted analytics should never be treated as exact truth.

## The point of this chapter

Minimal page visit tracking, admin route exclusion, database-side summaries, and optional Realtime recent activity, all with browser analytics marked as untrusted/noisy.

## Step 1 - Decide what you refuse to collect

Start with the smallest useful event: path, referrer if available, and timestamp. Do not store form content, secrets, precise personal data, or admin activity.

## Step 2 - Treat browser inserts as untrusted

A visitor controls the browser. They can spoof or spam analytics requests. If you insert from the browser, keep the policy narrow and the fields minimal. Consider an Edge Function or rate limiting if abuse matters.

## Step 3 - Summarize in the database

The dashboard should ask for totals, top pages, top referrers, and recent visits. It should not load every row and count in React.

## Step 4 - Use Realtime only where it helps

Live recent activity can be nice. It is not a replacement for stored events and summary queries.

## Step 5 - Write the analytics contract

Start with a deliberately small event:

```txt
page_visits
  path text
  referrer text nullable
  created_at timestamptz
```

Anything beyond this needs a reason. Country, city, user-agent family, and session-like identifiers can become privacy decisions quickly.

## Step 6 - Choose browser insert or function insert

| Approach | Benefit | Risk |
|---|---|---|
| Browser insert | simple and fast to build | spoofable, noisy, needs narrow RLS |
| Edge Function | more control and rate-limit options | more server code |

For a beginner portfolio, browser insert can be acceptable if you document that it is untrusted and collect only minimal fields. Do not call it exact analytics.

## Step 7 - Define dashboard summaries

The dashboard should ask for summaries:

```txt
total visits this week
top pages in last 30 days
top referrers
recent visits limited to 20
```

Use grouped database queries or RPC functions. Do not load every row into React and count there.

## Step 8 - Do it on your project

Create:

```txt
src/features/analytics/trackPageVisit.ts
src/features/analytics/analyticsApi.ts
src/features/analytics/AnalyticsDashboard.tsx
page_visits insert path or Edge Function
summary query/RPC shapes
optional recent-visit Realtime subscription
```

The tracker should immediately return for `/admin` paths.

## Prove it before moving on

Visit public pages, then admin pages. Public visits should count; admin visits should not. Try inserting extra fields from the browser if using direct insert. The database or API should ignore/block fields you did not choose.

> **📖 Mandatory read.** Read [Supabase JavaScript client](https://supabase.com/docs/reference/javascript/introduction), [Supabase Realtime](https://supabase.com/docs/guides/realtime), [Supabase RLS](https://supabase.com/docs/guides/database/postgres/row-level-security), and [PostgreSQL aggregate functions](https://www.postgresql.org/docs/current/functions-aggregate.html). Required: analytics is a database, privacy, and trust-boundary feature.

> **💡 Hint.** Write `Analytics I refuse to collect` before coding. If you cannot defend a field, remove it.

## Definition of Done

- [ ] Public page visits are recorded minimally.
- [ ] Admin routes are excluded.
- [ ] Visit logs contain no sensitive form content or private data.
- [ ] Browser analytics is documented as untrusted and noisy.
- [ ] Dashboard uses database-side summaries.
- [ ] Realtime, if used, is cleaned up and non-essential.

> **✍️ Log it (mandatory).** In `learning-log/15-analytics-realtime-insights.md`: list at least three analytics fields you refuse to collect and explain why.

All boxes ticked? Then continue. The next chapter builds on this gate, not around it.

---

Next: the features exist; now make failure states understandable. -> **[Chapter 16 - Validation, errors, and empty states](16-validation-errors-empty-states.md)**
