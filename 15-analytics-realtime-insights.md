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
