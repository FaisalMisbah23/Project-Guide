# Chapter 5 - About and skills

The home page introduced you quickly. Now you build the parts that give the introduction weight: your story and your skills.

> **Principle.** Trust grows when your story and your evidence point in the same direction.

The mistake beginners make is turning the about page into either a life story or a list of buzzwords. A useful about page is narrower. It explains your path, what you are practicing now, what strengths show up in your work, and what kind of role or collaboration you are moving toward.

## Where we're headed

By the end, you have an `About` page, a skills section or page, grouped skill data, and reusable components for skill categories or cards.

## Before you build

> **Mandatory read.** Read the DevWeekends React lists and keys chapter: https://resources.devweekends.com/courses/react-crash-course/05-lists-keys. This is the concept behind rendering grouped skills from data.

> **Optional blog.** Skim a clean-code or technical-debt article from your article list. Your skill list is not only about tools; it should also signal maintainability and learning habits.

> **Hint - skill honesty.** Do not add tools you cannot discuss. A smaller honest skill list is stronger than a long list that collapses in an interview.

Before creating `skills.js`, sketch your skill categories in the learning log. Do not write JSX yet; decide what the data should say first.

## Step 1 - Create the page files

Create:

```txt
src/pages/
  About.jsx
  Skills.jsx
```

You may render one at a time in `App.jsx` until routing arrives. The important thing is that the content is separated by page.

## Step 2 - Write the about content as sections

You now have page files; next, fill the about page with a short story that supports the portfolio's promise.

Your about page should include:

- who you are;
- your learning journey;
- your current focus;
- your strengths;
- your goals.

Keep each section short. The visitor should feel oriented, not trapped in an autobiography.

Example:

```txt
Weak:
I have always loved computers and technology since childhood. I enjoy learning
many things and hope to become successful in software engineering.

Stronger:
I am learning frontend engineering by building small, finished React projects.
My current focus is reusable UI, responsive layouts, and explaining my work
clearly through project notes.
```

## Step 3 - Store skills as grouped data

You now have your story; next, turn your skills into data so they stay easy to update and render.

Create:

```txt
src/data/
  skills.js
```

Shape the data by category:

```txt
category: "Frontend"
items: ["React", "JavaScript", "HTML", "CSS"]
```

Possible categories:

- Frontend;
- Backend basics;
- Databases, if you have actually used them;
- Tools;
- Soft skills;
- Currently learning.

The weak approach is to write every skill directly in JSX. That makes the page harder to update and hides the repeated pattern. The better approach is to store skills as data, then render the categories.

Another weak approach is to rate yourself with fake precision:

```txt
React: 95%
JavaScript: 90%
```

Those numbers are subjective and hard to defend. Prefer grouping, ordering, and honest wording. If you want to show depth, use project evidence: "used React state and routing in the portfolio project" says more than a percentage bar.

Example:

```txt
Weak:
React - 95%
JavaScript - 90%
CSS - 85%

Stronger:
Frontend:
  React - built routed pages, project filtering, forms, and API states
  JavaScript - used arrays, objects, state updates, and async fetch
  CSS - built responsive layouts and accessible focus states
```

## Step 4 - Create skill components

You now have grouped skill data; next, create components that can render each group consistently.

Create:

```txt
src/components/
  SkillCategory.jsx
  SkillBadge.jsx
```

`SkillCategory` should receive a category name and list of skills. `SkillBadge` should render one skill. This keeps the page readable and gives repeated UI a home.

## Step 5 - Connect the story to the skills

You now have story content and skill data; next, make sure they reinforce the same professional signal.

Do not let the about page and skills page contradict each other. If your about page says you are focused on frontend engineering, the skills page should make React, JavaScript, CSS, accessibility, and responsive UI easy to find.

This is product thinking. The portfolio should tell one coherent story.

## What your screen should show

The about page should feel concise and human. The skills page should show grouped skills from data, with no percentage bars and no tools you cannot discuss.

## Small challenge

Remove one sentence or skill that sounds impressive but does not help the visitor trust your actual work.

Suggested commit:

```bash
git commit -m "feat: add about and skills pages"
```

## Definition of Done

- [ ] `src/pages/About.jsx` exists.
- [ ] `src/pages/Skills.jsx` exists.
- [ ] `src/data/skills.js` stores grouped skill data.
- [ ] Skills render from data, not repeated hard-coded markup.
- [ ] Skills are grouped logically and do not use percentage ratings.
- [ ] `SkillCategory` and `SkillBadge` exist or equivalent reusable components exist.
- [ ] The about content is specific and concise.
- [ ] The skills page works on mobile.
- [ ] You made a commit for this chapter.

> **Log it.** In `learning-log/05-about-and-skills.md`: (1) What story does your portfolio tell about you? (2) Why group skills by category? (3) Which skills did you leave out because they would be hard to defend?

---

Next: turn project content into data. -> **[Chapter 6 - Projects from data](06-projects-from-data.md)**
