# Chapter 15 - Analytics And Realtime Insights

Analytics help the owner understand which public pages visitors use. Keep analytics minimal, privacy-aware, and owner-only.

## Goal

By the end, public page visits can be recorded and summarized for the owner dashboard.

## What You Will Build

- Page visit tracker.
- `page_visits` insert path.
- Admin analytics dashboard.
- Summary queries.
- Optional Realtime recent activity.

## Beginner Concepts

- **Analytics:** measured activity, such as page visits.
- **Untrusted data:** browser-sent data that may be incomplete or fake.
- **Summary:** grouped result such as visits per path.
- **Admin exclusion:** not counting owner dashboard visits.
- **Privacy:** collecting only what you actually need.

## Step By Step

### Step 1 - Decide What To Track

Track only simple public data:

```txt
path
referrer, optional
created_at
```

Do not collect private messages, passwords, or unnecessary personal data.

### Step 2 - Create Analytics Feature Files

Create:

```txt
src/features/analytics/
  trackPageVisit.ts
  analyticsApi.ts
  AnalyticsDashboard.tsx
```

### Step 3 - Track Public Routes

When a public route loads, insert a page visit. Skip:

```txt
/admin
/admin/*
/admin/login
```

Admin activity should not pollute public portfolio analytics.

### Step 4 - Treat Browser Analytics As Noisy

The browser can lie, fail, block requests, or send duplicates. Analytics should be useful hints, not perfect truth.

### Step 5 - Build Dashboard Summaries

In `/admin/analytics`, show:

```txt
top pages
recent visits
visits over time, optional
```

Prefer database-side summary queries or RPC functions instead of loading every visit into React.

### Step 6 - Add Optional Realtime

After normal summaries work, add a Realtime feed for recent public visits if desired. The dashboard should still work from normal queries.

## Common Mistakes

| Mistake | Why it hurts | Fix |
|---|---|---|
| Counting admin visits | Dashboard becomes misleading | Exclude admin paths |
| Loading all visits into React | Slow and wasteful | Summarize near database |
| Treating analytics as exact | Browser data is noisy | Present as directional |
| Public analytics dashboard | Visitor behavior leaks | Owner-only RLS |

## Checks Before Moving On

- Public visits are recorded.
- Admin visits are excluded.
- Owner can see summaries.
- Signed-out users cannot read analytics.
- Dashboard still works without Realtime.

## Learning Log

In `learning-log/15-analytics-realtime-insights.md`, answer:

```txt
Why is browser analytics untrusted?
Why exclude admin paths?
Why should summaries happen near the database?
Which analytics data did you intentionally avoid collecting?
```

## Definition Of Done

- [ ] Page visit tracking exists.
- [ ] Admin routes are excluded.
- [ ] Owner analytics dashboard exists.
- [ ] Summaries use database-side logic or narrow queries.
- [ ] Analytics rows are private.
- [ ] Realtime, if used, is optional.

Next: design validation and UI states. -> **[Chapter 16 - Validation, Errors, And Empty States](16-validation-errors-empty-states.md)**
