# Chapter 19 - Final review and maintenance

A portfolio becomes evidence when you can explain it and keep it alive. The last engineering task is not another feature; it is turning the system into something readable, demoable, reviewable, and maintainable.

## The point of this chapter

A project README, case study, demo script, security checklist, production smoke-test checklist, and maintenance rhythm.

## Before you touch code

- Production deployment exists or is close.
- Smoke-test results are available.
- Learning log has entries from earlier chapters.
- You are ready to turn the project into a case study.

## Vocabulary for this chapter

- **Case study.** Story of problem, decisions, tradeoffs, result, and next improvement.
- **Maintenance rhythm.** Repeated checks that keep the app alive.
- **Security checklist.** Documented review of secrets, policies, and private data.
- **Demo script.** Planned walkthrough that proves the system.
- **Residual risk.** Known weakness you accept or plan to fix.

## Guided snippet or contract

This is a shape to aim for, not a finished solution to paste blindly:

```txt
Final documentation contract
  README: setup and architecture
  CASE-STUDY: story and tradeoffs
  SECURITY-CHECKLIST: RLS/secrets/storage/logs
  SMOKE-TEST: production checks
  MAINTENANCE: monthly and quarterly routine
```

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

## If it breaks

| Symptom | Likely cause | Smallest next test |
|---|---|---|
| README cannot set up app | Commands/env vars are incomplete | Pretend you are new and follow README only. |
| Case study reads generic | It lists tools but no tradeoffs | Add one real decision and what it cost. |
| Demo runs too long | It has no story path | Use visitor -> owner -> failure/security -> deployment. |
| Maintenance never happens | Checklist has no cadence | Add monthly/quarterly dates or issue template. |

## What you should be able to explain

- Why documentation is part of the finished product.
- Which security checks you will repeat later.
- How you will keep content current.

## The slower beginner path

If this chapter feels too large, split the final review and maintenance package into one sitting per checkpoint. The goal is not to finish fast; the goal is to finish with proof.

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
