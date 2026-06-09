# Chapter 02 - Create The Vite Project

Now you create the React app from absolute zero. Move slowly. Setup is where beginners often lose track of which folder they are in, what files were generated, and which values are safe to commit.

## Goal

By the end, the app runs locally, builds for production, has a safe folder structure, has safe environment files, and has a clean Git baseline.

## What You Will Build

- A Vite React TypeScript app.
- A beginner-friendly `src/` folder structure.
- Safe `.env` and `.env.example` files.
- A Supabase client helper.
- A baseline Git commit.

## Beginner Concepts

- **Vite:** tool that starts the local dev server and builds production files.
- **React:** library for building UI from components.
- **TypeScript:** JavaScript with type checking.
- **Package:** installed code from npm.
- **Environment variable:** configuration value read by the app.
- **Secret:** private value that must not be exposed in browser code.

## Step By Step

### Step 1 - Create The App

Open a terminal in the folder where you want the app to live. Run:

```bash
npm create vite@latest portfolio-app -- --template react-ts
cd portfolio-app
npm install
npm run dev
```

You should see a local URL such as `http://localhost:5173`. Open it. The starter Vite page should appear.

### Step 2 - Understand What Vite Generated

Look at the generated files:

```txt
portfolio-app/
  public/             static files copied as-is
  src/                React source code
  src/main.tsx        React starts here
  src/App.tsx         starter app component
  index.html          HTML shell where React is mounted
  package.json        scripts and dependencies
  vite.config.ts      Vite configuration
  tsconfig*.json      TypeScript configuration
```

Important: most work happens in `src/`. Do not put private secrets in `public/` because public files can be downloaded by visitors.

### Step 3 - Check The Scripts

Open `package.json`. You should see scripts like:

```json
{
  "dev": "vite",
  "build": "tsc -b && vite build",
  "preview": "vite preview"
}
```

Run:

```bash
npm run build
```

This proves the starter app can compile.

### Step 4 - Install Styling And Routing Tools

Install the tools the course will use:

```bash
npm install react-router-dom @supabase/supabase-js
```

Set up TailwindCSS and shadcn/ui next. Use the official docs for the exact current commands, but do not treat the step as complete until these artifacts exist:

```txt
Tailwind is installed
global CSS imports Tailwind
Vite build still succeeds
shadcn/ui is initialized
at least one shadcn/ui component can be added
```

Reference docs:

- Tailwind Vite install: <https://tailwindcss.com/docs/installation/using-vite>
- shadcn/ui Vite install: <https://ui.shadcn.com/docs/installation/vite>

After installing, run:

```bash
npm run dev
npm run build
```

### Step 5 - Create A Clear `src/` Shape

Create these folders:

```txt
src/
  components/     shared UI such as layout, buttons, cards
  data/           local arrays used before database fetching
  features/       feature-specific logic
  lib/            Supabase client and shared helpers
  pages/          route-level pages
  routes/         router setup
  styles/         global styles if needed
```

Why this matters: a beginner can find code faster when files are grouped by purpose.

### Step 6 - Add Environment Files

Create `.env` for real local values:

```txt
VITE_SUPABASE_URL=
VITE_SUPABASE_ANON_KEY=
```

Create `.env.example` with the same names but no real values:

```txt
VITE_SUPABASE_URL=
VITE_SUPABASE_ANON_KEY=
```

Add `.env` to `.gitignore`.

Only `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY` belong in React. Brevo keys, service-role keys, database passwords, and private tokens do not belong in the frontend.

### Step 7 - Add The Supabase Client Helper

Create `src/lib/supabaseClient.ts`. It should read:

```ts
import { createClient } from '@supabase/supabase-js';

const supabaseUrl = import.meta.env.VITE_SUPABASE_URL;
const supabaseAnonKey = import.meta.env.VITE_SUPABASE_ANON_KEY;

export const supabase = createClient(supabaseUrl, supabaseAnonKey);
```

This helper gives the browser a public Supabase client. RLS will protect what the anon key can access.

### Step 8 - Verify Before Committing

Run:

```bash
npm run dev
npm run build
git status
```

Check:

```txt
.env is ignored
.env.example can be committed
node_modules is ignored
dist is ignored
no real secrets appear in source files
```

Then make a baseline commit.

## Common Mistakes

| Mistake | Why it hurts | Fix |
|---|---|---|
| Running commands in the wrong folder | npm cannot find `package.json` | Run `pwd` or check the terminal path |
| Forgetting `npm install` | scripts fail because packages are missing | Run `npm install` inside the app folder |
| Putting a service-role key in React | It gives the browser private database power | Remove it and rotate the key |
| Editing `.env` while dev server runs | Vite may not reload env values | Restart `npm run dev` |

## Checks Before Moving On

- Starter app opens in the browser.
- `npm run build` succeeds.
- You can explain the generated folders.
- `.env` is ignored.
- `.env.example` exists.
- Supabase client helper exists.

## Learning Log

In `learning-log/02-project-setup.md`, answer:

```txt
What command created the app?
What does `src/` contain?
Why is `.env.example` safe but `.env` is not?
Why are `VITE_` variables visible to browser code?
What did the baseline commit prove?
```

## Definition Of Done

- [ ] Vite React TypeScript app runs locally.
- [ ] Production build succeeds.
- [ ] Generated files and folders are understood.
- [ ] Course folder structure exists.
- [ ] `.env` is ignored and `.env.example` is committed.
- [ ] Supabase client helper uses only browser-safe env variables.

Next: design the database shape. -> **[Chapter 03 - Data Model And Migrations](03-data-model-and-migrations.md)**
