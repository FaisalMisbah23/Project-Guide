# Chapter 19 - Final review and maintenance

A portfolio becomes evidence when you can explain it and keep it alive. The last engineering task is not another feature; it is turning the system into something readable, demoable, reviewable, and maintainable.

## The point of this chapter

A project README, case study, demo script, security checklist, production smoke-test checklist, and maintenance rhythm.

## Step 1 - Write the project README

Explain what the app does, the stack, setup commands, safe env vars, server-only secrets, scripts, deployment, and core architecture. Do not paste real secret values.

## Step 2 - Write the case study

Use: problem, decision, tradeoff, result, next improvement. The portfolio itself is now one of your best projects.

## Step 3 - Rehearse the demo

Public pages, admin login, project publish, article preview, image upload, contact stored-before-email, inbox, analytics, and deployment boundaries.

## Step 4 - Review security

Check RLS, service-role usage, storage policies, public reads, private messages, subscribers, and logs.

## Step 5 - Schedule maintenance

Monthly: content, messages, broken links, smoke test. Quarterly: dependencies, secrets, RLS spot checks, analytics fields, and deployment review.

## Step 6 - Create the final documentation set

Your repo should have enough documentation for someone else to understand it:

```txt
README.md              setup, stack, scripts, env vars, architecture
CASE-STUDY.md          problem, decisions, tradeoffs, result
SECURITY-CHECKLIST.md  RLS, secrets, storage, service-role, logs
SMOKE-TEST.md          production workflow checks
MAINTENANCE.md         monthly and quarterly rhythm
```

The filenames can differ, but the artifacts should exist.

## Step 7 - Write the demo script

A strong demo is a path, not a feature list:

```txt
visitor sees published work
owner logs in
owner creates or edits a project
owner publishes content
visitor submits contact form
owner sees message in inbox
analytics shows public activity
explain where secrets and RLS fit
```

## Step 8 - Do it on your project

Run the demo once while recording notes. Wherever you stumble, improve either the app or the explanation. The final review is allowed to change the project.

## Prove it before moving on

Hand your README and case study to a future reader in your imagination. Can they run the app, understand the boundaries, and know what is intentionally out of scope? If not, documentation is not done.

> **📖 Mandatory read.** Read [GitHub README docs](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-readmes), [Vercel observability](https://vercel.com/docs/observability), [Supabase logs](https://supabase.com/docs/guides/platform/logs), and [GitHub Actions quickstart](https://docs.github.com/en/actions/writing-workflows/quickstart). Required: a deployed app still needs explanation and care.

> **💡 Hint.** If your README only says how to run the app, it is incomplete. It should also explain why the app is shaped the way it is.

## Definition of Done

- [ ] Project README exists and is safe to share.
- [ ] Case study exists.
- [ ] Demo script covers public and owner workflows.
- [ ] Security checklist covers RLS, secrets, service-role, storage, and private data.
- [ ] Production smoke-test checklist exists.
- [ ] Monthly and quarterly maintenance rhythm exists.

> **✍️ Log it (mandatory).** In `learning-log/19-final-review-maintenance.md`: explain how you will keep the portfolio alive after launch and which workflow you will test monthly.

All boxes ticked? Then continue. The next chapter builds on this gate, not around it.

---

Next: the system is documented; now turn it into a story you can defend. -> **[Chapter 20 - Closing](20-closing.md)**
