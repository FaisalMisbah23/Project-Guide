# Chapter 5 - About and skills

The home page introduced you quickly. Now you build the parts that give the introduction weight: your story and your skills.

The mistake beginners make is turning the about page into either a life story or a list of buzzwords. A useful about page is narrower. It explains your path, what you are practicing now, what strengths show up in your work, and what kind of role or collaboration you are moving toward.

## Where we're headed

By the end, you have an `About` page, a skills section or page, grouped skill data, and reusable components for skill categories or cards.

## Before you build

> **Mandatory read.** Read the DevWeekends React lists and keys chapter: https://resources.devweekends.com/courses/react-crash-course/05-lists-keys. This is the concept behind rendering grouped skills from data.

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

Your about page should include:

- who you are;
- your learning journey;
- your current focus;
- your strengths;
- your goals.

Keep each section short. The visitor should feel oriented, not trapped in an autobiography.

## Step 3 - Store skills as grouped data

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

## Step 4 - Create skill components

Create:

```txt
src/components/
  SkillCategory.jsx
  SkillBadge.jsx
```

`SkillCategory` should receive a category name and list of skills. `SkillBadge` should render one skill. This keeps the page readable and gives repeated UI a home.

## Step 5 - Connect the story to the skills

Do not let the about page and skills page contradict each other. If your about page says you are focused on frontend engineering, the skills page should make React, JavaScript, CSS, accessibility, and responsive UI easy to find.

This is product thinking. The portfolio should tell one coherent story.

> **Interesting to read.** Skim a clean-code or technical-debt article from your article list. Your skill list is not only about tools; it should also signal maintainability and learning habits.

> **Hint - skill honesty.** Do not add tools you cannot discuss. A smaller honest skill list is stronger than a long list that collapses in an interview.

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
