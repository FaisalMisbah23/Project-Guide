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
