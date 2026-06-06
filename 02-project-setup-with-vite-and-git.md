# Chapter 2 - Project setup with Vite and Git

You've decided what you're building: a React portfolio for a software engineer. Now you create the application skeleton that everything else will sit inside.

This chapter is not glamorous. A blank Vite app is not something you can show a recruiter. But the decisions here shape the whole project: how the app starts, what files belong in Git, what gets cleaned out, where your source code lives, and how you make the first checkpoint before adding real features.

## The point of this chapter

By the end, you have a Vite + React app that runs locally, a cleaned starter project, a sensible first folder structure, a `learning-log/` folder, a `.gitignore`, and your first commit.

## Before you build

> **Mandatory read - Git habits.** Read DevWeekends Git Fundamentals: https://resources.devweekends.com/courses/devops-tools/git-fundamentals. Focus on repositories, staging, commits, and the basic Git workflow. The goal is simple: small commits, clear messages, no generated files.

> **Hint - if `npm run dev` works but `npm run build` fails.** Development servers can hide some mistakes until the production build runs. Read the build error from the top, find the file it names, and fix that first. Do not edit random files hoping the error disappears.

> **When you're stuck.** Use the rubber duck method before changing more code: explain what Vite is supposed to do, what command you ran, what the terminal printed, and which file you changed last. If the explanation feels messy, write it in `learning-log/02-project-setup-with-vite-and-git.md` first; messy thoughts become debuggable when they become text.

## Step 1 - Create the Vite app

Start in the folder where you want the portfolio project to live. Create the app with Vite's React template:

```bash
npm create vite@latest my-portfolio -- --template react
cd my-portfolio
npm install
npm run dev
```

Vite is a frontend build tool. In plain English: it runs your app during development, refreshes quickly when files change, and builds optimized static files for deployment later. You are using it here because it is simple, fast, and widely used for React projects.

The weak alternative is to start with a random downloaded starter kit. It feels faster, but you inherit choices you cannot explain: folder names, dependencies, styling systems, routing decisions, and half-configured tools. For this course, start small and earn each addition.

Before you run the command, apply the daily guideline: understand the expected outcome. You are not "installing React" vaguely; you are creating a Vite-powered React project with scripts, dependencies, a source folder, and a local dev server.

## Step 2 - Understand the files before changing them

Before deleting anything, inspect the starter:

```txt
my-portfolio/
  index.html
  package.json
  vite.config.js
  src/
    App.jsx
    App.css
    main.jsx
    index.css
    assets/
```

The important pieces:

- **`index.html`** is the HTML shell Vite serves. React mounts inside it.
- **`src/main.jsx`** is the entry point. It tells React where to render your app.
- **`src/App.jsx`** is the starter component.
- **`package.json`** stores dependencies and scripts such as `dev`, `build`, and `preview`.
- **`vite.config.js`** stores Vite configuration.

Do not treat these files as magic. A React app is still HTML, CSS, and JavaScript; Vite gives them a development and build workflow.

## Step 3 - Clean the starter without over-building

Now remove the demo-specific content: logos, counter behavior, and starter copy. Your goal is a small blank app that proves React is rendering.

Keep the app minimal:

```txt
src/
  App.jsx        -> renders a simple portfolio placeholder
  main.jsx       -> mounts <App />
  index.css      -> global base styles
```

You may delete unused logo assets and starter CSS that only supported the demo screen.

Do not build the hero, navbar, routing, or project cards yet. Chapter 3 teaches components properly; Chapter 4 builds the home page. Rushing ahead here usually creates code you will have to reorganize two chapters later.

## Step 4 - Add the first real folders

Create the folders the next chapters will fill:

```txt
src/
  assets/
  components/
  data/
  hooks/
  pages/
  routes/
  styles/
```

This structure is feature-aware without being over-engineered:

- **`components/`** holds reusable UI pieces like `Navbar`, `Button`, `ProjectCard`, and `ContactForm`.
- **`pages/`** holds route-level screens like `Home`, `Projects`, and `Contact`.
- **`data/`** holds arrays for projects, skills, and notes.
- **`hooks/`** holds reusable React hook logic later, such as API fetching if you choose to extract it.
- **`routes/`** holds route wiring once React Router arrives.
- **`styles/`** holds shared CSS if you split beyond `index.css`.
- **`assets/`** holds images and files used by the UI.

The tempting shortcut is to create files only when you need them. That is fine for tiny experiments, but this course already knows the app will have pages, components, data, and routes. Creating the folders now gives every future chapter a predictable home.

## Step 5 - Confirm the scripts

Open `package.json` and understand the scripts Vite created:

```jsonc
{
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "lint": "eslint .",
    "preview": "vite preview"
  }
}
```

The exact scripts may vary slightly with your Vite version, but the model is the same:

- **`dev`** runs the local development server.
- **`build`** creates production-ready files in `dist/`.
- **`preview`** serves the production build locally so you can check it before deploying.
- **`lint`** checks code quality if the template includes ESLint.

Run the build once now:

```bash
npm run build
```

If it passes, the cleaned starter still compiles. If it fails, fix it before continuing. A broken build at setup is cheaper to fix than a broken build after ten chapters.

## Step 6 - Set up Git and `.gitignore`

Initialize Git:

```bash
git init
```

Make sure `.gitignore` excludes generated and private files:

```gitignore
node_modules/
dist/
.env
*.log
```

`node_modules/` is reinstalled from `package.json`; it should never be committed. `dist/` is build output; Vite regenerates it. `.env` is where secrets would live in future projects; even if this portfolio has no secrets, the habit starts here.

Also keep logs and temporary files out of commits. A clean repository is easier to review, deploy, and trust.

Now create the learning log:

```txt
learning-log/
  02-project-setup-with-vite-and-git.md
```

Finally, make the first commit:

```bash
git status
git add -A
git commit -m "chore: set up vite react portfolio"
```

> **Read before the next chapter.** Read the DevWeekends React crash course introduction to JSX: https://resources.devweekends.com/courses/react-crash-course/01-intro-jsx. Focus on what JSX is and why React components return it.

## Definition of Done

Things you can see or run, and the gate to Chapter 3:

- [ ] `npm run dev` starts the portfolio locally.
- [ ] The Vite starter demo content is removed.
- [ ] The browser shows a simple portfolio placeholder, not the default Vite screen.
- [ ] `src/` contains `assets/`, `components/`, `data/`, `hooks/`, `pages/`, `routes/`, and `styles/`.
- [ ] `npm run build` completes successfully.
- [ ] Git is initialized.
- [ ] `.gitignore` excludes `node_modules/`, `dist/`, `.env`, and logs.
- [ ] `learning-log/02-project-setup-with-vite-and-git.md` exists.
- [ ] A first commit is made with a meaningful message.
- [ ] You can explain what files Vite generated before you start adding features.

> **Log it.** In `learning-log/02-project-setup-with-vite-and-git.md`: (1) What does Vite do for your React project? (2) Why should `node_modules/` and `dist/` stay out of Git? (3) What is the difference between `npm run dev`, `npm run build`, and `npm run preview`? (4) What folders did you create under `src/`, and what belongs in each?

All boxes ticked and the log written? Continue. The app exists and has a clean home for the work ahead.

---

Next: turn the blank app into a real React structure. -> **[Chapter 3 - Components and JSX](03-components-and-jsx.md)**
