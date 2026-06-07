# Chapter 20 - Final review and maintenance

The portfolio is live. Now make it reviewable, explainable, and maintainable.

> **Principle.** Shipping is not the end of ownership; it is the start of maintenance.

## Where we're headed

By the end, the README, learning log, admin content, security notes, and maintenance checklist are ready for review.

## Before you build

> **Mandatory read.** Read DevWeekends job prep and branding: https://resources.devweekends.com/resources/job-prep-branding. Focus on making your work easy for a reviewer to understand quickly.

> **Review read.** Skim the DevWeekends React interview deep dive: https://resources.devweekends.com/resources/interview-questions/react. Practice only the concepts you used.

## Step 1 - Write the README

Include:

- project name;
- live URL;
- stack;
- features;
- Supabase services used;
- setup instructions;
- environment variables;
- security notes;
- screenshots;
- future improvements.

## Step 2 - Explain the architecture

Add a short architecture section:

```txt
React/Vite -> Supabase client -> Postgres/RLS/Auth/Storage
Contact form -> Edge Function -> contact_messages + Brevo
Admin routes -> Supabase Auth -> RLS-protected writes
```

## Step 3 - Prepare final explanation

You should be able to explain:

- why Supabase fits this portfolio;
- how RLS protects data;
- why Brevo runs from an Edge Function;
- which values are frontend-safe;
- how drafts differ from published content;
- how deployment works.

## Step 4 - Complete final self-review

Before sharing:

- [ ] Tested local build.
- [ ] Tested deployed site.
- [ ] Checked public routes.
- [ ] Checked admin routes.
- [ ] Checked RLS blocked cases.
- [ ] Checked contact and Brevo.
- [ ] Removed console noise.
- [ ] Updated README.
- [ ] Updated screenshots.
- [ ] Wrote final learning log.

## Step 5 - Create maintenance rhythm

Monthly:

```txt
- verify links
- review contact messages
- update projects
- publish or revise one article
- check Brevo logs
- check Supabase usage
```

Quarterly:

```txt
- rotate secrets if needed
- review RLS policies
- rerun accessibility/performance checks
- refresh screenshots
- remove weak or outdated claims
```

## What your screen should show

The public site is polished, admin content is accurate, contact works, and the README helps a reviewer understand the system before opening the code.

## Small challenge

Write a one-minute explanation of the project as if a senior engineer asked, "What makes this full-stack?"

Suggested commit:

```bash
git commit -m "docs: finalize full-stack portfolio guide"
```

## Definition of Done

- [ ] README is complete.
- [ ] Live URL works.
- [ ] Public pages are accurate.
- [ ] Admin dashboard works.
- [ ] Projects and articles are manageable.
- [ ] Contact messages store and notify.
- [ ] RLS behavior is tested.
- [ ] Secrets are not exposed.
- [ ] Maintenance checklist exists.
- [ ] Learning logs exist for all chapters.

> **Log it.** In `learning-log/20-final-review-and-maintenance.md`: What can you now build and explain that you could not at the start?

All boxes ticked? You have a full-stack portfolio: public product, protected admin, real database, server-side contact handling, Brevo notification, deployment, and a story you can defend.
