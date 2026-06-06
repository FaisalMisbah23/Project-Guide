# Chapter 12 - Deploy and final review

The portfolio is not finished until someone else can open it on the internet.

This chapter takes the local React app, builds it for production, deploys it, documents it, and prepares you to explain every important decision.

## Where we're headed

By the end, the site is deployed on Netlify or Vercel, the README explains the project, all links are checked, and your learning log is ready for review.

## Before you build

> **Mandatory read.** Revisit DevWeekends Git Fundamentals for repository hygiene, then read the DevWeekends Job Prep & Branding guide before polishing your README and portfolio copy: https://resources.devweekends.com/courses/devops-tools/git-fundamentals and https://resources.devweekends.com/resources/job-prep-branding

Before running the final build, write a short release checklist in `learning-log/12-deploy-and-final-review.md`: what you will test, what links must work, and what the README must explain.

## Step 1 - Run a production build

Run:

```bash
npm run build
```

Vite creates a `dist/` folder. This is the production output. It should stay out of Git because it can be regenerated from the source.

Then preview the build locally:

```bash
npm run preview
```

Click through the site in preview mode. Sometimes a development server hides issues that the production build exposes.

## Step 2 - Choose a deployment platform

Use Netlify or Vercel. Both can deploy a Vite React app.

Typical settings:

```txt
Build command: npm run build
Publish directory: dist
```

If client-side routes break after refresh, configure the platform to serve `index.html` for unknown routes. React Router handles the route after the app loads.

## Step 3 - Check the deployed site

Open the live URL and test:

```txt
Home
About
Skills
Projects
Project details
Learning notes
GitHub/API
Contact
Unknown route
Mobile layout
External links
```

Do not only test locally. Deployment can reveal path, routing, asset, and API issues.

## Step 4 - Write the README

Create or update:

```txt
README.md
```

Include:

- project name;
- short description;
- tech stack;
- features;
- how to run locally;
- live URL;
- screenshots if useful;
- what you learned;
- future improvements.

The README should help a reviewer understand the project before opening the site.

For your portfolio repo and your major linked project repos, the same standard applies: clear overview, screenshots, installation steps, usage notes, tech stack, and future improvements. Empty GitHub repositories and unclear READMEs weaken the portfolio even if the website looks good.

## Step 5 - Prepare the final explanation

You should be able to explain:

- why you used Vite;
- how the `src/` folder is organized;
- what components you reused;
- where props are used;
- where state is used;
- how list rendering works for projects, skills, and notes;
- how routing and dynamic project pages work;
- how form validation works;
- how the API page handles loading, success, error, and empty states;
- what you checked before deployment.

If you cannot explain one of those, revisit the chapter and update your learning log.

## Step 6 - Create a maintenance habit

A portfolio goes stale quietly. Add a short maintenance checklist to your README or learning log:

```txt
Monthly:
  - verify links
  - update resume
  - add recent projects or notes
  - check contact information

Quarterly:
  - refresh screenshots
  - improve case studies
  - rerun Lighthouse
  - review skills and remove anything you cannot defend
```

## Step 7 - Self-review before sharing

Do a final self-review like a small pull request:

```txt
Before sharing:
  - run the build
  - remove debugging code
  - check every route
  - verify edge cases
  - update README
  - check links and resume
  - note what changed and why
```

If you make a final change, commit it with a message that explains the purpose. "final" is not a purpose.

Before sharing the link, return to the reason you wrote in Chapter 1. A portfolio is not only a React exercise; it is evidence that you can keep a promise to yourself, work through confusion, and turn learning into something visible. That is worth noticing before you rush to the next project.

> **Review read.** Skim the DevWeekends React interview deep dive and practice explaining only the parts you used in this project: JSX, components, props, state, events, lists/keys, forms, `useEffect`, and routing. https://resources.devweekends.com/resources/interview-questions/react

> **Interesting to read.** Pick one career or engineering culture article from your article list. A portfolio is not only code; it is how you communicate your engineering identity.

> **Hint - final fixes.** Do not start a redesign on deployment day. Fix broken links, broken layouts, unclear content, and failed builds. Save big redesign ideas for a future version.

## Definition of Done

- [ ] `npm run build` passes.
- [ ] `npm run preview` works locally.
- [ ] The site is deployed on a public URL.
- [ ] Refreshing routed pages works on the deployed site.
- [ ] All internal navigation works.
- [ ] External project, GitHub, resume, and social links work.
- [ ] Resume, LinkedIn, GitHub, and portfolio content are consistent.
- [ ] Contact form validation works on the deployed site.
- [ ] The GitHub/API page handles success and failure.
- [ ] README includes project description, stack, features, local setup, and live URL.
- [ ] README includes screenshots or a clear visual preview if available.
- [ ] A maintenance checklist exists for future updates.
- [ ] A final self-review was completed before sharing the link.
- [ ] No debugging code, temporary notes, or console noise remains.
- [ ] Learning-log files exist for every chapter.
- [ ] Final Git commit is made.

> **Log it.** In `learning-log/12-deploy-and-final-review.md`: (1) Where did you deploy, and what settings did you use? (2) What broke only after deployment or preview? (3) Which React concept do you understand best now? (4) Which concept needs more practice? (5) What would you add in version two?

All boxes ticked? Your portfolio is shipped. Now keep it alive: add real projects, rewrite weak descriptions, and update it as your engineering skill grows.
