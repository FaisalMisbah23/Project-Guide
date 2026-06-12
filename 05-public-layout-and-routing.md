# Chapter 05 - Design layout and routes

## 05.01 - Set The Scene

The project now needs **public portfolio navigation**. This chapter adds public app shell while keeping the portfolio understandable for a beginner and reviewable by a mentor.

The story of this chapter is simple: a stable shell keeps database work from hiding layout and routing mistakes. You will build the professional version from the start, but you will still understand why the tempting shortcut fails.

By the end, `learning-log/05-public-layout-and-routing.md` will explain what you built and why it matters.

---

## 05.02 - Why This Feature Matters

Public portfolio navigation matters because it changes how the portfolio behaves for real users. It is not a decorative layer; it affects what visitors can see, what the owner can manage, and what proof the final demo can show.

In a toy build, you could skip this and fake the screen. In a production-style portfolio, the feature must survive refreshes, bad input, empty data, and privacy checks.

> **Interesting to read.** Search for "production readiness checklist web app" and notice how many items are about boring reliability: states, secrets, permissions, and recovery.

---

## 05.03 - What You Will Build

In this chapter you will produce public app shell.

The visible surface is: home, about, projects, articles, contact routes. The protected or owner-facing surface is: none yet.

Expected project touchpoints:

```txt
src/routes/router.tsx
src/pages/
src/components/layout/
learning-log/05-public-layout-and-routing.md
```

Routes or screens involved:

```txt
/
/about
/projects
/projects/:slug
/articles
/articles/:slug
/contact
```

Database areas involved:

```txt
No table change in this step
```

---

## 05.04 - The Beginner Approach And Its Cost

The tempting beginner move is to connect Supabase before the site has a stable visual and route shape. It feels fast because it removes planning, but the cost appears later when the app must handle real data, privacy, or production checks.

Concrete cost: the shortcut usually moves a rule into the weakest possible place. If the browser hides something, the browser can also reveal it. If a person remembers a deployment step, another person can forget it. If a form has no validation path, the first bad input becomes a confusing bug.

You do not need to build the weak version. You only need to understand its failure mode well enough to avoid it.

---

## 05.05 - The Professional Approach

The professional path is to prove the public shell with placeholders and local data before adding remote data. This is the required path for the course because every later chapter assumes the same shape.

| Choice | Why it wins here |
|---|---|
| Keep the rule close to the data or boundary | It still works when the UI changes |
| Name files and contracts before filling logic | The build stays navigable |
| Verify each step immediately | Bugs stay small |

✅ Do follow the course shape even if another structure could work. ❌ Don't fork the architecture casually; later chapters name exact files.

---

## 05.06 - Key Concepts In Plain English

Use these words precisely in this chapter:

- **Contract:** the shape a screen, function, route, or table promises to honor.
- **Boundary:** the place where data crosses from one trust level to another, such as browser to function or public route to admin route.
- **Source of truth:** the place the app treats as authoritative.
- **Verification:** a small check that proves the last step worked before you continue.

For this chapter, the source of truth should be the project artifact, not a memory of what you intended to build.

---

## 05.07 - Reading Before You Build

Before building, read or search these topics. The chapter explains the idea first; these readings deepen it.

**Mandatory reads**

- **React Router layout routes** - read this because it supports `public portfolio navigation`.
- **Semantic HTML landmarks** - read this because it supports `public portfolio navigation`.
- **Navigation IA basics** - read this because it supports `public portfolio navigation`.

After reading, write two sentences in `learning-log/05-public-layout-and-routing.md`: one idea you understood, and one question you still have.

---

## 05.08 - Where The Project Is Now

Chapter 04 left you with RLS policies. Now this chapter adds public app shell.

Before touching code, run the smallest check that proves the previous chapter still works. For UI chapters, open the relevant route. For database chapters, inspect the table or policy. For deployment chapters, run the local build first.

✅ Do start from a working baseline. ❌ Don't stack new work on top of a broken previous chapter.

---

## 05.09 - Scaffold The Files

Create the folders and files for this chapter before writing feature logic. The scaffold is the map your future self follows.

```txt
src/routes/router.tsx
src/pages/
src/components/layout/
learning-log/05-public-layout-and-routing.md
```

Each file should have a clear job. If a file starts doing two unrelated jobs, split it before it becomes hard to test.

✅ Do create empty files or small placeholders with names that match the course. ❌ Don't paste final feature logic yet; first make the shape visible.

Verify with `find` or your editor file tree that every named file exists.

---

## 05.10 - Define The Contract

Define the contract before the implementation. A contract says what must go in, what must come out, and what failure looks like.

```txt
Feature: public portfolio navigation
Input: the smallest data needed for this step
Success: the user sees or receives the expected state
Failure: invalid, missing, private, or not-found data is handled clearly
```

✅ Do write the contract in comments, docs, or types before logic. ❌ Don't let the first implementation secretly decide the rules.

**Hint.** If you cannot describe the failure response, you are not ready to write the happy path.

---

## 05.11 - Create The Data Or Route Shape

Create the route, table, or state shape this chapter needs.

Routes:

```txt
/
/about
/projects
/projects/:slug
/articles
/articles/:slug
/contact
```

Tables:

```txt
No new table; use the existing schema.
```

✅ Do name the route or table for the product behavior. ❌ Don't name it after an implementation detail that users never understand.

Verify by opening the route, migration, or Supabase table list.

---

## 05.12 - Write The First Screen Or Helper

Build the first visible or reusable piece for public portfolio navigation. Keep it intentionally small: one screen shell, one helper contract, or one component boundary.

The piece should show enough structure that another developer can see where data will enter later.

✅ Do separate visual layout from data fetching when the chapter needs both. ❌ Don't query Supabase from a deeply nested card or button unless that component owns the workflow.

Verify by rendering the shell or importing the helper without breaking the build.

---

## 05.13 - Wire The Route Or Module

Now connect the new piece to the app. Wiring means the route, component, helper, or function is reachable from the place a user or owner naturally expects.

For this chapter, check these entry points:

```txt
/
/about
/projects
/projects/:slug
/articles
/articles/:slug
/contact
```

✅ Do wire one path and test it before adding another. ❌ Don't leave orphaned files that exist but cannot be reached.

---

## 05.14 - Add Loading And Empty State

Add loading and empty states for public portfolio navigation. A user should never have to guess whether the app is waiting, empty, broken, or rejecting their input.

Minimum states:

```txt
loading
empty
error
success, where relevant
validation message, where relevant
```

✅ Do write messages that tell the user what happened and what to try next. ❌ Don't show raw database or provider errors to visitors.

Verify by forcing at least one state instead of waiting for it to happen naturally.

---

## 05.15 - Add Error And Validation State

Add error and validation states for public portfolio navigation. A user should never have to guess whether the app is waiting, empty, broken, or rejecting their input.

Minimum states:

```txt
loading
empty
error
success, where relevant
validation message, where relevant
```

✅ Do write messages that tell the user what happened and what to try next. ❌ Don't show raw database or provider errors to visitors.

Verify by forcing at least one state instead of waiting for it to happen naturally.

---

## 05.16 - Connect To Supabase

Connect the chapter to Supabase only after the local shape works. The client should request exactly the data the UI needs and no private extras.

For `public portfolio navigation`, the query or function should respect:

```txt
public data only for visitors
owner-only data only after auth and policy checks
clear error when Supabase refuses the request
```

✅ Do filter at the query and enforce with RLS. ❌ Don't fetch broad rows and hide fields in React.

Verify with one successful request and one request that should be blocked.

---

## 05.17 - Protect Private Data

Protect the private side of public portfolio navigation. Browser checks improve experience, but the database or server boundary must enforce the rule.

Run the privacy check as a signed-out user or anon client. The expected result is not hidden UI; the expected result is no private data.

✅ Do test the boundary directly. ❌ Don't trust that a missing link means the feature is secure.

**Hint.** Security checks should still pass if someone types the URL manually.

---

## 05.18 - Add The Admin Or Public Ui

Finish the user-facing surface for this chapter. Public UI should be calm and readable; admin UI should be efficient, scannable, and hard to misuse.

For this chapter, the UI should make `public app shell` obvious without explaining the course itself on screen.

✅ Do use labels, states, and predictable actions. ❌ Don't hide important actions behind unclear icons or vague button text.

Verify by completing the main workflow once from the UI.

---

## 05.19 - Test The Happy Path

Test the happy path. The goal is to prove that the expected user completes the expected workflow.

Write the exact check you ran in `learning-log/05-public-layout-and-routing.md`. If the check uses the browser, record the route. If it uses Supabase, record the table or function. If it uses the terminal, record the command.

✅ Do test one thing at a time. ❌ Don't mark the chapter done because the screen "looks right" once.

---

## 05.20 - Test The Failure Path

Test the failure path. The goal is to prove that bad input, missing data, or a service failure is handled cleanly.

Write the exact check you ran in `learning-log/05-public-layout-and-routing.md`. If the check uses the browser, record the route. If it uses Supabase, record the table or function. If it uses the terminal, record the command.

✅ Do test one thing at a time. ❌ Don't mark the chapter done because the screen "looks right" once.

---

## 05.21 - Test The Privacy Boundary

Test the privacy boundary. The goal is to prove that private records are blocked even if the UI is bypassed.

Write the exact check you ran in `learning-log/05-public-layout-and-routing.md`. If the check uses the browser, record the route. If it uses Supabase, record the table or function. If it uses the terminal, record the command.

✅ Do test one thing at a time. ❌ Don't mark the chapter done because the screen "looks right" once.

---

## 05.22 - Write The Learning Log

Create or update `learning-log/05-public-layout-and-routing.md`.

Answer these in your own words:

```txt
What did Chapter 05 add to the project?
What shortcut did you avoid, and why was it risky?
Which file, route, table, or screen proves the work is real?
What failure or privacy check did you run?
```

The learning log is part of the gate. If you cannot explain the chapter, the feature is not finished yet.

✅ Do write short, specific answers tied to your repo. ❌ Don't copy the chapter text back as a summary.

---

## 05.23 - Recap And Whats Next

You added public app shell and proved it with visible checks. The important lesson is not only that the feature works; it is that you can explain why this shape is safer than the shortcut.

Next, Chapter 06 builds project list and detail pages.

Before moving on, commit the work with a message that names the chapter outcome.

---

## 05.24 - Definition Of Done

This checklist is the gate for Chapter 05. Do not move on until every item is true in your own project.

- [ ] Public app shell exists in the repo.
- [ ] The main route, screen, table, or function for `public portfolio navigation` can be opened or inspected.
- [ ] The happy path has been tested.
- [ ] A failure, empty, or validation state has been tested.
- [ ] A privacy or secret-safety check has been tested where relevant.
- [ ] `learning-log/05-public-layout-and-routing.md` explains the decision and the proof.

All boxes ticked? Then continue to the next chapter. If not, that is where today's work is.
