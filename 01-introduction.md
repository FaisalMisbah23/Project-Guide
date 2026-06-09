# Chapter 01 - Plan The Portfolio

This chapter does not start with code. A beginner mistake is opening React before knowing what the portfolio needs to say. First you will plan the audience, required sections, content, layout, and data strategy.

## Goal

By the end, you will have a clear portfolio plan in `learning-log/01-introduction.md`.

## What You Will Build

A planning document with:

- Target audience.
- Required portfolio sections.
- Content inventory.
- Rough layout sketch.
- First data strategy.
- Notes about what will become database-backed later.

## Beginner Concepts

- **Audience:** the people who will visit the site, such as recruiters, hiring managers, clients, or collaborators.
- **Section:** a major area of the portfolio, such as Projects or Work Experience.
- **Content inventory:** the text, links, images, dates, and labels you need before coding.
- **Data strategy:** where content lives: JSX, a local array, or Supabase.

## Step By Step

### Step 1 - Define The Audience

Create `learning-log/01-introduction.md` when the app project exists later. For now, write the same answers in a notebook or plain text note:

```txt
Who should trust me after visiting this portfolio?
What role or opportunity am I aiming for?
What proof would convince that audience?
```

This matters because a portfolio for frontend roles should highlight UI polish, while a full-stack portfolio should also show data, auth, deployment, and security decisions.

### Step 2 - Choose Mandatory Sections

Use these required sections:

```txt
Home / Hero
About
Work Experience
Projects
Skills / Tools
Articles / Blog
Contact
Resume and social links
```

The newsletter is optional. Admin pages are private and will be built later.

### Step 3 - Make A Content Inventory

Write the first draft of your content:

```txt
Name:
Short role title:
One-sentence introduction:
Three skills I want to prove:
Work experience items:
Project ideas:
Article ideas:
Contact email:
Resume link:
GitHub / LinkedIn links:
```

Do not wait for perfect writing. Beginner projects move faster when placeholder content has a real shape.

### Step 4 - Pick A Simple Design Direction

Choose one direction:

```txt
Calm professional
Developer dashboard
Editorial / writing focused
Creative portfolio
```

Write down your choice and why it fits the audience.

### Step 5 - Sketch The First Layout

Draw or write this layout:

```txt
Top navigation:
  logo/name, About, Experience, Projects, Articles, Contact

Home page:
  hero, featured projects, experience preview, skills, contact call-to-action

Footer:
  resume, GitHub, LinkedIn, email
```

This is only a plan. Chapter 05 turns it into routes and layout components.

### Step 6 - Choose The Starting Data Strategy

Use this beginner path:

```txt
Hardcoded JSX: one-off headings and labels
Local arrays: skills, work experience, starter projects
Supabase: projects, articles, contact messages, newsletter, analytics, admin-managed content
```

Work experience starts as a local array so you can practice rendering repeated content. Later you may move it to Supabase if you want admin editing.

## Common Mistakes

| Mistake | Why it hurts | Fix |
|---|---|---|
| Starting with colors before content | The layout has nothing real to organize | Write the content inventory first |
| Skipping work experience | The portfolio looks like only project cards | Add jobs, internships, freelance work, volunteer work, or learning milestones |
| Putting every idea in v1 | The project becomes too large | Keep the required sections, mark extras as later |

## Checks Before Moving On

- You can name the audience.
- You selected all mandatory sections.
- You wrote a rough content inventory.
- You selected a design direction.
- You understand JSX vs local arrays vs Supabase.

## Learning Log

In `learning-log/01-introduction.md`, answer:

```txt
Who is this portfolio for?
Which sections are mandatory?
Which content starts in local arrays?
Which content should eventually live in Supabase?
Why is this stronger than a static portfolio?
```

## Definition Of Done

- [ ] Audience is defined.
- [ ] Mandatory sections are listed.
- [ ] Content inventory exists.
- [ ] Layout sketch exists.
- [ ] Data strategy is written.
- [ ] You can explain why the portfolio needs both public pages and owner workflows.

Next: create the project foundation. -> **[Chapter 02 - Create The Vite Project](02-project-setup-vite-supabase-git.md)**
