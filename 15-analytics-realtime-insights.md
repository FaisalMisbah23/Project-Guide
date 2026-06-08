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

## New ideas before you build

### Analytics events

**Real-life analogy:** a museum counts which rooms people visit so it can improve signs and exhibits. It does not need to record private conversations.

**General idea:** track only what helps improve the portfolio. Avoid sensitive form content, precise personal data, and admin activity.

```ts
await supabase.from("page_visits").insert({
  path: window.location.pathname,
  referrer: document.referrer || null,
});
```

Study more: [Frontend Interview Questions - Performance and Best Practices](https://resources.devweekends.com/resources/frontend-interview-qs)

### Aggregates

**Real-life analogy:** a shop owner wants totals, not every receipt one by one.

**General idea:** dashboards should summarize raw visit rows into useful counts and trends.

```sql
select path, count(*) as visits
from page_visits
group by path
order by visits desc;
```

Study more: [Database Engineering - Case Studies](https://resources.devweekends.com/courses/database-engineering/case-studies)

## Daily guideline

From `Daily_Software_Development_Guidelines.md`: **think in systems**. Analytics changes affect users, privacy, database size, dashboard behavior, and production monitoring. Track the smallest useful data, then explain what you deliberately chose not to collect.

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

## Between chapters

Optional pause. Pick **one or two**, not all of them. Skip the rest without guilt if your Definition of Done is complete.

**Ethics prompt:** write a short note titled `Analytics I refuse to collect`. Include at least three examples and the reason each one would reduce visitor trust.

**Quiz:** which is more useful for this portfolio: raw visit rows or top-page summaries? When would you need the raw rows?

**Performance exercise:** insert sample visit rows for several paths, then compare showing raw rows vs grouped counts. The dashboard should prefer summaries for scanning.

**Privacy exercise:** review every analytics field and mark it as useful, risky, or unnecessary. Remove at least one field you cannot defend.

**Comparison:** raw data vs aggregate data: raw data is every individual visit row. Aggregate data is a summary, such as total visits per page.

**Big word alert:** **referrer** means the page or site a visitor came from before landing on your page, when the browser provides it.

**Diagram:**

```txt
Public route loads
  -> record page_visits row
  -> dashboard query groups visits
  -> insight cards show totals, top pages, referrers
```

Next: the features exist. Now make every failure state understandable. -> **[Chapter 16 - Validation, errors, and empty states](16-validation-errors-empty-states.md)**
