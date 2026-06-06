# Chapter 4 - The home page

Your portfolio has a shell. Now it needs a first impression.

The home page has one job: help a visitor understand who you are, what kind of software work you do, and where to go next. It should not explain your entire life. It should open the door.

> **Principle.** The home page is not a biography; it is a useful first answer.

Use the 30-60 second test from the introduction. A recruiter should be able to land here and quickly answer: who is this, what do they build, and what should I click next?

## Where we're headed

By the end, the home page has a hero section, a short professional summary, a main skills preview, and calls to action for projects and contact.

## Before you build

> **Mandatory read.** Read the DevWeekends React components/props chapter, then skim the lists and keys chapter before rendering skills from an array: https://resources.devweekends.com/courses/react-crash-course/02-components-props and https://resources.devweekends.com/courses/react-crash-course/05-lists-keys.

> **Daily guideline.** Read the "Name Things Clearly" and "Keep Components Focused" sections in `Daily_Software_Development_Guidelines.md`.

> **Hint - hero copy.** Write the summary in plain language first. If it sounds like a slogan from a template, rewrite it with one concrete skill and one concrete outcome.

Before touching `Home.jsx`, write the hero's purpose in one sentence: who you are, what you build, and what the visitor should click next.

## Step 1 - Create the page file

Create:

```txt
src/pages/
  Home.jsx
```

For now, import `Home` into `App.jsx` and render it inside `main`. Routing comes later.

The weak approach is to keep writing every section in `App.jsx`. That file becomes a junk drawer. The better approach is to make `App.jsx` the app frame and put page content inside page files.

## Step 2 - Build the hero section

The hero should answer:

```txt
Who are you?
What do you build?
What should the visitor do next?
```

Include:

- your name;
- role, such as "Software Engineer" or "Frontend-focused Software Engineer";
- a specific two-to-three-line summary;
- a primary action to view projects;
- a secondary action to download your resume, contact you, or read about you.

Avoid vague claims. Do not write "passionate developer who loves technology" unless the rest of the sentence proves it. Prefer concrete language about React, web interfaces, learning notes, problem solving, or project work.

Example:

```txt
Weak:
I am a passionate developer who loves building amazing digital experiences.

Stronger:
I build responsive React interfaces, organize UI into reusable components,
and document what I learn while shipping small web projects.
```

## Step 3 - Add a skills preview

Create a short array of main skills inside the page or in a temporary data file:

```txt
React
JavaScript
HTML
CSS
Git
Responsive UI
```

Render the list using a reusable badge or simple repeated element. The point is to practice list rendering, not to manually copy six badges.

## Step 4 - Add a project preview placeholder

Add a small section that points visitors toward the projects page. Do not build full project cards yet; Chapter 6 handles projects properly from data.

The home page can say what kind of projects will appear and link to the future projects route. If the link does not work yet, that is fine until routing arrives, but the page should still communicate the intended flow.

## Step 5 - Make it responsive early

Check the home page on a narrow screen. The hero text should wrap cleanly, buttons should not overflow, and sections should have enough spacing.

Do not wait until Chapter 11 to care about mobile. Chapter 11 is for final polish; every chapter should avoid obvious layout breakage as it is built.

## What your screen should show

The page should show your name, role, short summary, two clear actions, and a small skills preview. On mobile, nothing should overflow horizontally and both action buttons should be easy to tap.

## Small challenge

Ask: "If someone only reads the hero, what would they remember about me?" Rewrite one sentence until the answer is specific.

Example:

```txt
Weak memory:
They like coding.

Better memory:
They are a frontend-focused engineer who can build and explain React projects.
```

Suggested commit:

```bash
git commit -m "feat: build portfolio home page"
```

## Definition of Done

- [ ] `src/pages/Home.jsx` exists.
- [ ] `App.jsx` renders `Home` inside the app shell.
- [ ] The hero includes your name, role, summary, and two actions.
- [ ] The page answers who you are, what you build, and where to go next within 30-60 seconds.
- [ ] Skills are rendered from an array, not manually copied one by one.
- [ ] The page includes a clear path toward projects and contact.
- [ ] The home page does not overflow on mobile.
- [ ] You made a commit for this chapter.

> **Log it.** In `learning-log/04-home-page.md`: (1) What should a portfolio home page communicate in the first few seconds? (2) Why render skills from an array? (3) What did you change after checking mobile?

---

Next: tell the deeper story. -> **[Chapter 5 - About and skills](05-about-and-skills.md)**
