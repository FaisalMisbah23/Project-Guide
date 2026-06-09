# Chapter 02 - Project setup with Vite, Supabase, and Git

Last chapter gave the product a shape. Now you create the workspace where it will live. Setup is not glamorous, but it is one of the first places beginners accidentally create future pain: secrets in the wrong file, no reproducible commands, no folder plan, no clean commit to return to.

This chapter builds the skeleton slowly and deliberately. Nothing useful is on screen yet, and that's fine. A clean foundation is a feature.

## The point of this chapter

A Vite React app runs locally, builds for production, has a clear folder layout, reads only browser-safe Supabase variables, ignores real secrets, commits a safe `.env.example`, and has a baseline Git commit.

## Step 1 - Create the React app

Use Vite because it gives React beginners fast feedback and a simple production build:

```bash
npm create vite@latest portfolio-app -- --template react-ts
cd portfolio-app
npm install
npm run dev
```

What each piece means:

- **Vite** runs the local development server and builds the final browser assets.
- **React** renders the UI from components.
- **TypeScript** helps catch wrong-shaped data before runtime.

Do not add Supabase yet. First prove the app itself starts.

## Step 2 - Install the UI tools

This course uses TailwindCSS and shadcn/ui because the app has both public marketing-style pages and dense admin screens. Follow the official Vite instructions for both tools. Do not paste random setup from an old blog post; frontend tooling changes.

## Step 7 - Make the setup reproducible

A future learner, teammate, or future-you should be able to open the repo and know what to do. Add these scripts if they are not already present:

```jsonc
{
  "scripts": {
    "dev": "vite",
    "build": "tsc -b && vite build",
    "preview": "vite preview"
  }
}
```

The exact scripts may differ if Vite generated something newer, but the intent should not: one command for development, one command for production build, one command to preview the built app.

## Step 8 - Write the first setup contract

Add a short `README` note in the app project later, or at least a learning-log section now, that names the setup contract:

```txt
To run locally:
  install dependencies
  create .env from .env.example
  provide VITE_SUPABASE_URL and VITE_SUPABASE_ANON_KEY
  run npm run dev

Never commit:
  .env
  service-role keys
  Brevo keys
  database passwords
```

This is not busywork. Reproducibility is how setup becomes professional.

## Step 9 - Verify the secret boundary manually

Run these checks before committing:

```bash
git status
npm run build
```

Then inspect the source tree for suspicious names:

```txt
BREVO_API_KEY
SUPABASE_SERVICE_ROLE_KEY
DATABASE_URL
password
secret
```

Finding those words is not automatically wrong, because docs and examples mention them. Finding real values is wrong. If a real private value touched Git, rotate it.

## Do it on your project

Create these artifacts:

```txt
.env                 real local values, ignored
.env.example         safe names only, committed
src/lib/supabaseClient.ts
src/components/
src/features/
src/pages/
src/routes/
src/styles/
learning-log/02-project-setup.md
```

Commit only after the build succeeds and the secret boundary is clear.

## Prove it before moving on

A clean proof looks like this:

```txt
npm run dev      -> app opens locally
npm run build    -> production build succeeds
git status       -> .env is not staged; .env.example is visible
code search      -> no real private secret exists in frontend files
```

If any line fails, fix setup now. Setup problems become harder to untangle after Supabase, routing, and admin features arrive.

> **📖 Mandatory read.** Read [Vite's guide](https://vite.dev/guide/), [React's project guide](https://react.dev/learn/start-a-new-react-project), [Tailwind's Vite installation](https://tailwindcss.com/docs/installation/using-vite), [shadcn/ui's Vite installation](https://ui.shadcn.com/docs/installation/vite), and [Vite environment variables](https://vite.dev/guide/env-and-mode). Required: the rest of the course assumes you know what the dev server, build command, and `VITE_` prefix do.

## Step 3 - Choose the folder shape

A flat `src/` feels easy for one page. It becomes confusing once you have projects, articles, auth, admin CRUD, contact, newsletter, analytics, and storage.

Use this feature-friendly shape:

```txt
src/
  components/   shared UI pieces
  features/     project, article, admin, contact, analytics logic
  lib/          clients and shared helpers
  pages/        route-level pages
  routes/       router setup
  styles/       global styles
```

The rule is simple: code that changes together should be easy to find together.

## Step 4 - Set up environment files safely

Create `.env` for real local values and `.env.example` for safe placeholders.

```txt
# .env.example
VITE_SUPABASE_URL=
VITE_SUPABASE_ANON_KEY=
```

Only `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY` belong in frontend env files. The anon key is browser-safe only because RLS will protect the database later. Brevo keys, service-role keys, database passwords, and provider tokens do not belong in React.

Add `.env`, `node_modules/`, build output, logs, and local clutter to `.gitignore`.

## Step 5 - Add the Supabase client helper

Create `src/lib/supabaseClient.ts`. It should read only `import.meta.env.VITE_SUPABASE_URL` and `import.meta.env.VITE_SUPABASE_ANON_KEY`.

Do not make the client work by adding a service-role key. That would bypass the security model before you even build it.

## Step 6 - Build, check, commit

Run:

```bash
npm run dev
npm run build
git status
```

Confirm `.env` is ignored and `.env.example` is visible. Then make the baseline commit.

> **💡 Hint.** If an env variable is `undefined`, restart the dev server after editing `.env`. Vite reads env files when the server starts.

## Definition of Done

- [ ] Vite React app starts locally.
- [ ] TailwindCSS and shadcn/ui are installed from official docs.
- [ ] The project has the agreed `src/` folder shape.
- [ ] Supabase client helper reads only `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY`.
- [ ] `.env` is ignored; `.env.example` is committed and contains no real values.
- [ ] `npm run build` succeeds.
- [ ] A baseline Git commit exists.
- [ ] No Brevo key, service-role key, database password, or private token appears in frontend code.

> **✍️ Log it (mandatory).** In `learning-log/02-project-setup.md`: explain why `VITE_SUPABASE_ANON_KEY` may appear in browser code but `SUPABASE_SERVICE_ROLE_KEY` must not. Also explain why `.env.example` is committed but `.env` is not.

All boxes ticked? Then the app exists. Now give it durable truth.

---

Next: the app exists; now give it durable truth. -> **[Chapter 03 - Data model and migrations](03-data-model-and-migrations.md)**
