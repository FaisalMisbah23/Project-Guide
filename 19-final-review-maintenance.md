# Chapter 19 - Final review and maintenance

Shipping is not the end of the course. The final test is whether you can explain the system you built: the data model, security rules, frontend routes, admin flows, email path, deployment boundary, and tradeoffs.

## Where we're headed

By the end, the portfolio has a final README, a maintenance rhythm, a demo script, and a self-review that proves understanding.

## The final-review trap

Bad:

```txt
Here is my link.
```

Problem: a link shows the result, not the thinking.

Better:

```txt
Here is my link.
Here is the architecture.
Here is what is public/private.
Here is how contact works.
Here is what I would improve next.
```

## Build it

Write the project README. Include:

```txt
product summary
tech stack
features
architecture overview
database tables
security/RLS summary
environment variable guide
deployment notes
known tradeoffs
future improvements
```

Prepare a demo path:

```txt
public homepage
projects
articles
contact submission
admin login
message inbox
project/article edit
image upload
deployment/secrets explanation
```

Create a maintenance rhythm. Monthly: check messages, update articles/projects, review broken links. Quarterly: review dependencies, secrets, RLS policies, and analytics.

## Human rhythm

When stuck, think on paper. Write what you expected, what happened, what changed recently, and what you tried. Rubber duck debugging means explaining the problem out loud to something or someone that does not solve it for you. The explanation often reveals the missing assumption.

Remember why you started: this portfolio is not only a site. It is evidence of your judgment.

## Definition of Done

- [ ] README explains the full-stack system.
- [ ] Demo script exists.
- [ ] Maintenance rhythm exists.
- [ ] Learner can explain Supabase Auth, RLS, Storage, Edge Functions, Brevo, and Vercel env vars.
- [ ] Learning log is complete.
- [ ] Final production smoke test passes.

> **Log it.** In `learning-log/19-final-review-maintenance.md`, write your final architecture explanation as if answering an interview question.

Next: close the course by turning the shipped project into a professional habit. -> **[Chapter 20 - Closing](20-closing.md)**
