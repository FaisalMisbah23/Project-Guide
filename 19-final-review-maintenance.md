# Chapter 19 - Final Review And Maintenance

The app is deployed. Now turn it into evidence you can explain and maintain.

## Goal

By the end, the project has a strong README, demo script, security review, maintenance checklist, and future improvement plan.

## What You Will Build

- Project README.
- Demo script.
- Case-study notes.
- Security review checklist.
- Maintenance rhythm.
- Backlog of improvements.

## Beginner Concepts

- **README:** first document a reviewer sees.
- **Demo script:** planned path through the app.
- **Case study:** explanation of problem, decisions, tradeoffs, and result.
- **Maintenance:** recurring work that keeps the app healthy.
- **Backlog:** future improvements not required for v1.

## Step By Step

### Step 1 - Write The Project README

Include:

```txt
project purpose
live URL
tech stack
features
setup instructions
environment variables
security notes
screenshots, optional
```

Write for a recruiter and an engineer. Both should understand what matters.

### Step 2 - Create A Demo Script

Write a short flow:

```txt
open homepage
show experience/projects/articles
submit contact form
log in as owner
show dashboard
edit project
show inbox
show analytics
explain deployment
```

Practice the demo before sharing the project.

### Step 3 - Write A Case Study

Use this structure:

```txt
Problem:
Audience:
Key features:
Important technical decisions:
Security decisions:
Tradeoffs:
What I would improve next:
```

### Step 4 - Run Security Review

Check:

```txt
no private keys in repo
no private keys in browser
RLS blocks drafts
RLS blocks messages
admin routes require auth
contact uses Edge Function
Brevo key is server-side
storage uploads are owner-only
```

### Step 5 - Make A Maintenance Checklist

Schedule a monthly review:

```txt
check contact messages
check broken links
update recent work
review dependencies
check logs
test contact form
backup or export important data
```

### Step 6 - Create A Backlog

Examples:

```txt
better article editor
experience admin CRUD
project image gallery
RSS feed
more analytics summaries
theme toggle
automated tests
```

Do not add everything now. A finished v1 beats a forever-unfinished v2.

## Common Mistakes

| Mistake | Why it hurts | Fix |
|---|---|---|
| README only says tech stack | Reviewer misses decisions | Explain features and tradeoffs |
| No demo script | Live demo becomes scattered | Practice a path |
| No maintenance plan | Portfolio goes stale | Schedule review |
| Forgetting security review | Hidden risk remains | Run checklist |

## Checks Before Moving On

- README explains the project clearly.
- Demo script exists.
- Security checklist passes.
- Maintenance schedule exists.
- Backlog is separated from v1.

## Learning Log

In `learning-log/19-final-review-maintenance.md`, answer:

```txt
What is the strongest technical decision in this project?
What tradeoff did you make?
What will you maintain monthly?
What would you improve next?
```

## Definition Of Done

- [ ] README exists.
- [ ] Demo script exists.
- [ ] Case-study notes exist.
- [ ] Security review is complete.
- [ ] Maintenance checklist exists.
- [ ] Backlog exists.

Next: close the course and prepare to explain it. -> **[Chapter 20 - Closing](20-closing.md)**
