# Chapter 02 - Project setup with Vite, Supabase, and Git

Last chapter gave the product a shape. Now you create the workspace where it will live. Setup is not glamorous, but it is one of the first places beginners accidentally create future pain: secrets in the wrong file, no reproducible commands, no folder plan, no clean commit to return to.

This chapter builds the skeleton slowly and deliberately. Nothing useful is on screen yet, and that's fine. A clean foundation is a feature.

## The point of this chapter

A Vite React app runs locally, builds for production, has a clear folder layout, reads only browser-safe Supabase variables, ignores real secrets, commits a safe `.env.example`, and has a baseline Git commit.

## Before you touch code

- Confirm Node and npm are installed.
- Make sure you are inside the folder where you want the app project to live.
- Have a Supabase project URL and anon key only if you are ready to connect Supabase; setup can start without them.
- Decide the project folder name before running create commands.

## Vocabulary for this chapter

- **Dev server.** The local server Vite runs while you build.
- **Production build.** The optimized files Vercel will serve.
- **Environment variable.** A config value read by the app at runtime or build time.
- **Secret.** A value that gives private power and must not be visible in browser code.
- **Baseline commit.** The first known-good checkpoint after setup works.

## Guided snippet or contract

This is a shape to aim for, not a finished solution to paste blindly:

```txt
Setup contract, not final code
  commands: npm install, npm run dev, npm run build
  frontend env: VITE_SUPABASE_URL, VITE_SUPABASE_ANON_KEY
  ignored: .env, node_modules, dist, logs
  committed: .env.example, package files, source files, learning-log notes
```

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

## If it breaks

| Symptom | Likely cause | Smallest next test |
|---|---|---|
| `npm run dev` fails | Dependencies are missing or the project folder is wrong | Run `npm install`, then check `package.json` scripts. |
| Env values are undefined | Vite server started before `.env` existed or names lack `VITE_` | Restart dev server and inspect variable names. |
| `.env` appears in Git status | `.gitignore` is missing or added too late | Stop, untrack `.env` if needed, and rotate any leaked value. |
| Build fails after setup | Tooling config is incomplete | Fix the first build error before adding features. |

## What you should be able to explain

- Why `VITE_` variables are browser-visible.
- Why `.env.example` is safe but `.env` is not.
- Why a baseline commit matters before feature work.

## The slower beginner path

If this chapter feels too large, split the project setup into one sitting per checkpoint. The goal is not to finish fast; the goal is to finish with proof.

### Sitting 1 - Read and translate

- Read the mandatory docs with this chapter open beside you.
- Write five plain-language notes in the learning log.
- Circle any word you cannot define yet.
- Rewrite the point of the chapter in your own words.
- Stop before coding if you cannot explain what you are about to change.

### Sitting 2 - Create the smallest artifact

- Create only the first file, table, route, policy, function, checklist, or note this chapter requires.
- Add placeholder content or a tiny shape before trying to make it complete.
- Run the smallest possible check.
- If it fails, debug that one artifact before adding the next one.

### Sitting 3 - Connect the artifact

- Connect the artifact to the previous chapter's work.
- Keep the connection narrow: one query, one route, one form submit, one policy, or one checklist item.
- Add a visible loading, empty, blocked, or failure state if this chapter touches UI or data.
- Write down what changed in the request flow.

### Sitting 4 - Break it safely

- Try the shortcut this chapter warned you about in a harmless way.
- Try the most likely beginner mistake from the troubleshooting table.
- Confirm the app fails safely, or fix it until it does.
- Record the before/after in the learning log.

## Checkpoints during the work

Use this mini-review after each sitting:

```txt
What did I create or change?
What command, route, query, or click proves it exists?
What private data or failure case did I protect?
What is the next smallest test?
```

If you cannot answer the second question, you do not have proof yet. If you cannot answer the third question, you may have built only the happy path.

## Suggested commit rhythm

Make small commits when code changes. A good commit for this chapter should complete one idea, not the whole universe:

```txt
setup: add safe Supabase client shape
schema: add project and article tables
security: add public published-project policy
ui: add project loading and empty states
admin: add project archive action
ops: add production smoke-test checklist
```

Use the style that fits your repo, but keep the habit: one clear change, one clear reason, one checkpoint you can return to.

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
