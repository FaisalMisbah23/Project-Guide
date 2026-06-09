# Chapter 15 - Analytics and Realtime insights

A portfolio owner benefits from knowing what people read. But analytics is a trust decision. You are not building an ad-tech platform, and browser-submitted analytics should never be treated as exact truth.

## The point of this chapter

Minimal page visit tracking, admin route exclusion, database-side summaries, and optional Realtime recent activity, all with browser analytics marked as untrusted/noisy.

## Before you touch code

- Public routes exist.
- Admin dashboard shell exists.
- page_visits table exists or is planned.
- You have written a privacy refusal list before choosing fields.

## Vocabulary for this chapter

- **Analytics event.** A stored record that something happened.
- **Aggregate.** A summary such as count by page.
- **Referrer.** The previous page/site reported by the browser, when available.
- **Untrusted browser data.** Data the visitor can spoof or spam.
- **Privacy budget.** The smallest amount of data needed for the feature.

## Guided snippet or contract

This is a shape to aim for, not a finished solution to paste blindly:

```sql
-- minimal analytics shape
page_visits(
  path text not null,
  referrer text null,
  created_at timestamptz not null default now()
)

-- summary contract
get_top_pages(days) -> path, visits
get_recent_visits(limit) -> path, referrer, created_at
```

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

## If it breaks

| Symptom | Likely cause | Smallest next test |
|---|---|---|
| Admin visits counted | Tracker does not exclude `/admin` | Visit admin route then inspect recent rows. |
| Counts look inflated | Browser inserts are spoofed/noisy or double-tracked | Log one route transition and inspect insert count. |
| Dashboard is slow | React loads raw rows instead of summaries | Replace raw load with grouped query/RPC. |
| Sensitive data appears in logs | Tracker captures too much | Remove field and document refusal. |

## What you should be able to explain

- Why analytics should be minimal.
- Why browser inserts are untrusted/noisy.
- Why summaries belong near the database.
- Which fields you refuse to collect and why.

## The slower beginner path

If this chapter feels too large, split the analytics feature into one sitting per checkpoint. The goal is not to finish fast; the goal is to finish with proof.

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
