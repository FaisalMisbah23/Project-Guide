# Chapter 15 - Analytics and Realtime insights

A portfolio owner benefits from knowing which pages people visit. But analytics should be useful, minimal, and honest. You are not building an ad-tech platform. You are tracking enough to improve the portfolio.

## Where we're headed

By the end, the app records page visits, referrers, and coarse location metadata if available, and the dashboard shows basic insight cards. Realtime can update recent activity.

## The analytics trap

Bad:

```txt
track everything because we can
store personal data forever
mix admin route traffic with public visitor traffic
```

Problem: the owner gets noisy data, visitors lose trust, and the system stores more than it needs.

Better:

```txt
track path, referrer, timestamp, and coarse source
exclude admin routes
show simple counts and trends
```

## Build it

Create a small tracking function or Supabase insert path for public page visits. Record:

```txt
path
referrer
user_agent family if needed
country/city if reliably available
created_at
```

Do not store sensitive form content in visit logs. Do not track admin routes.

On the dashboard, show:

```txt
total visits this week
top pages
top referrers
recent visits
```

Add Realtime only if it improves the admin experience. Live updates are fun, but they are not a substitute for correct stored data.

## Definition of Done

- [ ] Public page visits are recorded.
- [ ] Admin routes are excluded.
- [ ] Dashboard shows useful visit summaries.
- [ ] Referrers are tracked where available.
- [ ] Location data is coarse or omitted.
- [ ] Realtime is used only where it helps.

> **Log it.** In `learning-log/15-analytics-realtime-insights.md`, explain what you chose not to track and why.

Next: the features exist. Now make every failure state understandable. -> **[Chapter 16 - Validation, errors, and empty states](16-validation-errors-empty-states.md)**
