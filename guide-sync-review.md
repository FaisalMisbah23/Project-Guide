# Guide Sync Review

This review compares `portfolio-website/` with the DevWeekends authoring rules in `guide.md`.

## What Already Matches

- The course is folder-based, with chapters split into small ordered sub-chapters.
- Most feature chapters have 24 sub-chapters, which fits the guide's 20-30 sub-chapter target.
- The course has a clear product arc: setup, data, security, public experience, owner workspace, communication, analytics, polish, deploy, maintenance, close.
- Each chapter ends with a Definition of Done or final gate.
- The stack and course outline are visible from the top-level README.

## Main Gaps

- Many lesson files are structurally correct but too thin. A 10-20 line sub-chapter often names the task but does not teach the decision deeply enough.
- Several chapters use a repeated generic skeleton. The guide allows structure, but asks the prose to feel like a guided story rather than a stamped template.
- The weak approach is often named, but the concrete cost is not always specific to the feature.
- Some build steps say "create the shape" or "wire the module" without enough detail about the exact behavior, checks, and mistakes to avoid.
- Reading blocks often name topics, but they should be woven into the chapter's reasoning so reading extends the lesson rather than replacing it.

## Sync Applied

Chapter 13, `contact inbox and realtime`, has been expanded as the current model chapter.

The synced version now emphasizes:

- database load as the source of truth;
- realtime as an enhancement, not the foundation;
- concrete inbox statuses and message fields;
- exact project touchpoints for files, route, table, and learning log;
- do/don't guidance in build steps;
- happy path, failure path, and privacy-boundary verification;
- a stronger Definition of Done tied to observable repo behavior.

## Recommended Next Pass

Use Chapter 13 as the pattern and update one chapter at a time, starting with chapters that introduce new concepts:

1. Chapter 02: make setup steps more explicit about env safety, Git baseline, and why Vite/Supabase are chosen.
2. Chapter 03: deepen data modeling with concrete table sketches, constraints, and migration verification.
3. Chapter 04: expand RLS with direct anon vs owner checks.
4. Chapter 08: keep the custom structure, but deepen auth concepts and owner workflow.
5. Chapters 14-15: explain scheduled work, analytics privacy, aggregation, and realtime/cron failure modes in more detail.

Avoid regenerating the whole course at once. The guide specifically favors fixing one chapter at a time so the course keeps its product thread.
