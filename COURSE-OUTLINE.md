# Software Engineer Portfolio - Next.js Project Guide

**Course outline & chapter breakdown**

| | |
|---|---|
| **Stack** | Next.js App Router · React · TypeScript · Tailwind CSS · Prisma · PostgreSQL · Vercel |
| **Domain** | Personal software-engineer portfolio with a database-backed writing/admin workflow |
| **Difficulty** | Medium - assumes React basics and teaches Next.js, Prisma, security boundaries, and deployment |
| **Duration** | 4 weeks; progress by chapters finished, not clock |
| **Design** | Clean technical editorial style - readable, restrained, and proof-focused |
| **Product line** | *You're building a software-engineer portfolio that proves your work, publishes your thinking, and can be safely maintained after deployment.* |

## Phase demo targets

| Phase | Done when the mentee can demo... |
|---|---|
| Week 1 - Foundation | A Next.js app runs with shared shell, home/story pages, responsive navigation, and clean lint/build checks |
| Week 2 - Portfolio proof + data | Project case studies render with media/diagrams; Prisma/Postgres stores article data with seed fallback |
| Week 3 - Publishing workflow | Public articles work; admin can log in, see dashboard stats, and create/edit/publish/delete articles |
| Week 4 - Hardening + ship | Revision history, contact/security, SEO/analytics/headers, and live Vercel deployment all work on HTTPS |

## Course folder layout

```text
software-engineer-portfolio/
  COURSE-OUTLINE.md
  01-introduction/
  02-project-skeleton/
  ...
  16-deploy-and-ship/
  17-closing/
```

Chapters are numbered folders at the course root. Week groupings are labels in this outline, not directory names.

## Mentee-facing rules

- Build in order; every checklist is a gate.
- The guide gives contracts, paths, commands, and verification steps, not finished solution bodies.
- Public pages, admin pages, API routes, and database helpers must keep their boundaries clear.
- Every phase ends with something demoable in the browser.

## Prerequisites

| Skill | Expected level |
|---|---|
| React | Can build components, props, lists, and forms |
| TypeScript | Can read and write basic types and interfaces |
| Git | Can commit small changes and read `git status` before committing |
| Terminal | Can run npm scripts and inspect errors |
| Databases | Understands tables, rows, unique fields, and migrations at a basic level |
| Web basics | Understands routes, forms, JSON, cookies, and environment variables at a basic level |

## Chapter index

| # | Chapter folder | Phase | Done when... |
|---|---|---|---|
| 01 | `01-introduction/` | Orientation | Mentee understands the finished product, workflow, scope, and prerequisites. |
| 02 | `02-project-skeleton/` | Week 1 - Foundation | A Next.js app runs locally with the first route, folders, lint script, and README. |
| 03 | `03-design-system-and-shell/` | Week 1 - Foundation | The site has global styling, header, footer, navigation, and responsive shell behavior. |
| 04 | `04-home-and-story-pages/` | Week 1 - Foundation | The public portfolio has a credible home page, story page, about sections, and skills presentation. |
| 05 | `05-project-catalogue/` | Week 2 - Portfolio proof | Projects render from typed data with cards, detail routes, galleries, and architecture summaries. |
| 06 | `06-project-media-and-diagrams/` | Week 2 - Portfolio proof | Project screenshots and Mermaid diagrams render safely and help explain architecture, data, and flows. |
| 07 | `07-database-and-prisma/` | Week 2 - Publishing foundation | PostgreSQL and Prisma are configured with safe env files, migrations, and a reusable Prisma client. |
| 08 | `08-article-domain-model/` | Week 2 - Publishing foundation | Articles have statuses, reading time, repository functions, seed fallback, and safe public/admin shapes. |
| 09 | `09-public-articles/` | Week 3 - Publishing workflow | Readers can list and open published articles while drafts stay private. |
| 10 | `10-admin-auth/` | Week 3 - Publishing workflow | Admin login, logout, session cookie, CSRF token, and protected redirects work without exposing secrets. |
| 11 | `11-admin-dashboard/` | Week 3 - Publishing workflow | Authenticated admins can view stats, navigation shortcuts, data-source mode, and protected article management pages. |
| 12 | `12-article-editor/` | Week 3 - Publishing workflow | Admins can create, edit, delete, publish, archive, and validate articles with predictable API behavior. |
| 13 | `13-revision-history/` | Week 4 - Hardening | Article edits create revision snapshots that admins can inspect without exposing them publicly. |
| 14 | `14-contact-and-security/` | Week 4 - Hardening | The contact form validates input, optional email delivery is safe, and shared security helpers protect admin mutations. |
| 15 | `15-seo-observability-and-policies/` | Week 4 - Ship shape | The site publishes metadata, sitemap, robots, analytics, speed insights, security headers, and project policy docs. |
| 16 | `16-deploy-and-ship/` | Week 4 - Ship shape | The portfolio is deployed with production env vars, smoke tests, build checks, and a final case study. |
| 17 | `17-closing/` | Closing | Mentee has a final demo script, documentation, and bar-raiser list for future improvements. |

# Chapter breakdowns

## 01 - Introduction (`01-introduction/`)
**Gate:** Mentee understands the finished product, workflow, scope, and prerequisites.
| File | Cluster | What it covers |
|---|---|---|
| `01.01-what-youre-building.md` | Open | Orient yourself around a professional portfolio that is also a small publishing system. |
| `01.02-how-to-use-this-course.md` | Open | Work chapter by chapter, finish every checklist, and keep commits small. |
| `01.03-the-product-and-its-audience.md` | Open | Name the visitors: recruiters, collaborators, readers, and the site owner. |
| `01.04-scope.md` | Open | Separate the portfolio, publishing workflow, contact channel, and deployment from nice-to-have extras. |
| `01.05-prerequisites.md` | Open | Confirm the React, TypeScript, command line, Git, and database basics assumed by this guide. |
| `01.06-course-outline.md` | Open | Preview the phases and demo targets before writing code. |
| `01.07-working-rhythm.md` | Wrap | Use commits, notes, environment hygiene, and browser verification as part of the build. |
| `01.08-checklist.md` | Checklist | Gate the introduction before the first scaffold chapter. |

## 02 - Project skeleton (`02-project-skeleton/`)
**Gate:** A Next.js app runs locally with the first route, folders, lint script, and README.
| File | Cluster | What it covers |
|---|---|---|
| `02.01-set-the-scene.md` | Open | Turn an empty folder into a running application shell. |
| `02.02-why-structure-matters.md` | Learn | Compare route-first chaos with a small feature-oriented structure. |
| `02.03-what-youll-build.md` | Open | Preview the root files, app folder, component folders, lib folders, docs, and public assets. |
| `02.04-choose-the-stack.md` | Learn | Use Next.js App Router, TypeScript, Tailwind CSS, Prisma, and PostgreSQL for this course. |
| `02.05-create-the-app.md` | Build | Create the Next app in your own product folder and install dependencies. |
| `02.06-root-gitignore-and-readme.md` | Build | Create ignore rules, a minimal README, and a learning-log folder. |
| `02.07-folder-conventions.md` | Build | Create app route groups, components, lib, docs, prisma, and public/projects placeholders. |
| `02.08-first-layout.md` | Build | Define the root layout, metadata defaults, and shared body classes. |
| `02.09-first-home-route.md` | Build | Create the first home page with temporary product copy. |
| `02.10-lint-and-typecheck.md` | Build | Run lint and keep TypeScript strict enough to catch route mistakes early. |
| `02.11-verify-in-browser.md` | Build | Open the local app and confirm the first screen renders from Next, not static HTML. |
| `02.12-recap-and-whats-next.md` | Wrap | Lock the skeleton before styling and navigation arrive. |
| `02.13-checklist.md` | Checklist | Gate the skeleton before design work. |

## 03 - Design system and shell (`03-design-system-and-shell/`)
**Gate:** The site has global styling, header, footer, navigation, and responsive shell behavior.
| File | Cluster | What it covers |
|---|---|---|
| `03.01-set-the-scene.md` | Open | Give the portfolio a reusable frame before filling pages. |
| `03.02-why-shells-matter.md` | Learn | Explain why navigation, spacing, and typography belong in shared primitives. |
| `03.03-what-youll-build.md` | Open | Build global CSS, header, footer, back-to-top, and page containers. |
| `03.04-tailwind-and-global-css.md` | Build | Set typography, colors, focus states, and base backgrounds in app/globals.css. |
| `03.05-layout-component-map.md` | Learn | Decide what belongs in app/layout.tsx versus components/layout/. |
| `03.06-header-navigation.md` | Build | Create components/layout/Header.tsx with stable links to home, story, projects, articles, contact. |
| `03.07-footer.md` | Build | Create components/layout/Footer.tsx with contact links and compact site metadata. |
| `03.08-back-to-top-button.md` | Build | Create a small client component for returning to the top after long pages. |
| `03.09-responsive-containers.md` | Build | Use consistent max-widths and spacing so every page scans well on mobile and desktop. |
| `03.10-accessibility-pass.md` | Build | Check landmarks, keyboard focus, link names, and color contrast. |
| `03.11-visual-smoke-test.md` | Build | Resize the browser and verify the shell does not overlap or reflow awkwardly. |
| `03.12-recap-and-whats-next.md` | Wrap | Prepare to fill the shell with the portfolio story. |
| `03.13-checklist.md` | Checklist | Gate shared shell work. |

## 04 - Home and story pages (`04-home-and-story-pages/`)
**Gate:** The public portfolio has a credible home page, story page, about sections, and skills presentation.
| File | Cluster | What it covers |
|---|---|---|
| `04.01-set-the-scene.md` | Open | A portfolio succeeds when visitors quickly understand the person and proof of work. |
| `04.02-why-narrative-matters.md` | Learn | Contrast generic claims with a story tied to visible projects and skills. |
| `04.03-what-youll-build.md` | Open | Build the hero, story teaser, skills sections, story page, and about navigation. |
| `04.04-write-the-positioning.md` | Build | Draft the one-sentence professional positioning that drives the home page. |
| `04.05-home-hero.md` | Build | Update app/page.tsx with hero copy and primary links to story, projects, and contact. |
| `04.06-skills-data.md` | Build | Model skills as typed arrays with labels and icons instead of repeated markup. |
| `04.07-skills-section.md` | Build | Render grouped skills using reusable chips and readable color categories. |
| `04.08-story-teaser.md` | Build | Add a short narrative preview that links to the full story page. |
| `04.09-story-route.md` | Build | Create app/story/page.tsx with a longer learning-to-building narrative. |
| `04.10-story-section-navigation.md` | Build | Create components/story/AboutSectionNav.tsx for long-story navigation. |
| `04.11-bookshelf-or-influences.md` | Build | Add a section that shows learning influences without turning the page into a resume dump. |
| `04.12-about-route.md` | Build | Create app/about/page.tsx as a concise alternate entry for visitors who expect About. |
| `04.13-copy-edit-pass.md` | Build | Remove vague claims and make every claim point toward evidence elsewhere in the site. |
| `04.14-recap-and-whats-next.md` | Wrap | The person is now legible; next prove it with projects. |
| `04.15-checklist.md` | Checklist | Gate home and story pages. |

## 05 - Project catalogue (`05-project-catalogue/`)
**Gate:** Projects render from typed data with cards, detail routes, galleries, and architecture summaries.
| File | Cluster | What it covers |
|---|---|---|
| `05.01-set-the-scene.md` | Open | Projects are the proof layer of a portfolio. |
| `05.02-case-study-vs-gallery.md` | Learn | Explain why project pages need problem, solution, results, and flow, not only screenshots. |
| `05.03-what-youll-build.md` | Open | Build typed project data, project cards, list page, and project detail pages. |
| `05.04-project-data-shape.md` | Learn | Define the fields a project case study must carry before any component renders it. |
| `05.05-create-project-data-file.md` | Build | Create lib/projects/data.ts with typed project objects and slugs. |
| `05.06-project-card.md` | Build | Create components/projects/ProjectCard.tsx for list and featured sections. |
| `05.07-featured-projects-on-home.md` | Build | Render selected projects on the home page from the shared data source. |
| `05.08-projects-index-route.md` | Build | Create app/projects/page.tsx with all project cards. |
| `05.09-dynamic-project-route.md` | Build | Create a slug-based project detail route and not-found behavior. |
| `05.10-case-study-sections.md` | Build | Add challenge, solution, results, features, and technology sections to the detail page. |
| `05.11-external-links.md` | Build | Add live and GitHub links with clear missing-link handling. |
| `05.12-empty-and-invalid-states.md` | Build | Verify the site behaves cleanly when a project slug does not exist. |
| `05.13-recap-and-whats-next.md` | Wrap | Project content exists; next make media and diagrams useful. |
| `05.14-checklist.md` | Checklist | Gate project catalogue. |

## 06 - Project media and diagrams (`06-project-media-and-diagrams/`)
**Gate:** Project screenshots and Mermaid diagrams render safely and help explain architecture, data, and flows.
| File | Cluster | What it covers |
|---|---|---|
| `06.01-set-the-scene.md` | Open | Screenshots show the product; diagrams show the thinking behind it. |
| `06.02-why-diagrams-help.md` | Learn | Contrast vague architecture claims with diagrams that show boundaries and flow. |
| `06.03-what-youll-build.md` | Open | Add public project assets, galleries, architecture summaries, and Mermaid rendering. |
| `06.04-asset-folder.md` | Build | Create public/projects and name images by project and screen purpose. |
| `06.05-image-fields.md` | Build | Connect image and gallery fields in lib/projects/data.ts. |
| `06.06-project-gallery.md` | Build | Create components/projects/ProjectGallery.tsx with stable image sizes and captions. |
| `06.07-architecture-summary.md` | Build | Add architecture, data, user-flow, and background-flow summaries to project detail pages. |
| `06.08-mermaid-basics.md` | Learn | Teach Mermaid as text-to-diagram syntax and where it is useful. |
| `06.09-mermaid-component.md` | Build | Create components/projects/MermaidDiagram.tsx as a client component with strict security mode. |
| `06.10-diagram-data.md` | Build | Add Mermaid strings to project data without mixing them into layout components. |
| `06.11-render-diagrams.md` | Build | Render architecture, database, user flow, and background flow diagrams on project pages. |
| `06.12-fallbacks.md` | Build | Show useful fallback text if a diagram is missing or fails to render. |
| `06.13-visual-verification.md` | Build | Check galleries and diagrams on mobile and desktop. |
| `06.14-recap-and-whats-next.md` | Wrap | The portfolio can explain work; next it needs persistent writing. |
| `06.15-checklist.md` | Checklist | Gate media and diagrams. |

## 07 - Database and Prisma (`07-database-and-prisma/`)
**Gate:** PostgreSQL and Prisma are configured with safe env files, migrations, and a reusable Prisma client.
| File | Cluster | What it covers |
|---|---|---|
| `07.01-set-the-scene.md` | Open | Articles need persistence, not hardcoded arrays. |
| `07.02-why-postgres-here.md` | Learn | Explain why relational data fits authors, articles, statuses, and revisions. |
| `07.03-what-youll-build.md` | Open | Add env files, Prisma schema, migrations, and a shared client. |
| `07.04-env-discipline.md` | Learn | Separate .env from .env.example and keep secrets out of Git. |
| `07.05-install-prisma.md` | Build | Install prisma and @prisma/client and add generate/migrate scripts. |
| `07.06-create-env-example.md` | Build | Document DATABASE_URL, DIRECT_URL, admin, site, and optional contact variables. |
| `07.07-prisma-schema-start.md` | Build | Create prisma/schema.prisma with PostgreSQL datasource and client generator. |
| `07.08-user-model.md` | Build | Add User with id, email, name, role, timestamps, and article relation. |
| `07.09-article-model.md` | Build | Add Article with slug uniqueness, status, tags, reading time, author, and timestamps. |
| `07.10-first-migration.md` | Build | Run the first migration locally and inspect the generated SQL. |
| `07.11-prisma-client-helper.md` | Build | Create lib/db/prisma.ts with a reusable client that behaves in development hot reload. |
| `07.12-db-connection-check.md` | Build | Confirm prisma generate, migration, and a simple read path all work. |
| `07.13-recap-and-whats-next.md` | Wrap | The database exists; next shape the article domain around it. |
| `07.14-checklist.md` | Checklist | Gate database setup. |

## 08 - Article domain model (`08-article-domain-model/`)
**Gate:** Articles have statuses, reading time, repository functions, seed fallback, and safe public/admin shapes.
| File | Cluster | What it covers |
|---|---|---|
| `08.01-set-the-scene.md` | Open | Writing is a product feature when it has states, metadata, and ownership. |
| `08.02-draft-vs-published.md` | Learn | Explain why public readers and the admin need different article views. |
| `08.03-what-youll-build.md` | Open | Build article repository functions, seed data, and reading-time helpers. |
| `08.04-domain-shapes.md` | Learn | Define public cards, admin rows, and editor form values as separate shapes. |
| `08.05-reading-time-helper.md` | Build | Create lib/articles/reading-time.ts and specify its word-count behavior. |
| `08.06-seed-articles.md` | Build | Create lib/articles/seed.ts for fallback published content when the database is unavailable. |
| `08.07-repository-boundary.md` | Learn | Keep database access in lib/articles/repository.ts instead of page components. |
| `08.08-published-card-query.md` | Build | Add a repository read for published article cards sorted by publish date. |
| `08.09-featured-article-query.md` | Build | Add a limited read for the home page featured articles. |
| `08.10-admin-row-query.md` | Build | Add a repository read for admin article table rows. |
| `08.11-form-value-query.md` | Build | Add a repository read for editor initial values with seed fallback awareness. |
| `08.12-slug-rules.md` | Build | Specify slug uniqueness, lowercase format, and duplicate-check behavior. |
| `08.13-fallback-behavior.md` | Build | Verify the site still shows seed public content if DB env is missing. |
| `08.14-recap-and-whats-next.md` | Wrap | Article data is shaped; next expose it to readers. |
| `08.15-checklist.md` | Checklist | Gate article domain model. |

## 09 - Public articles (`09-public-articles/`)
**Gate:** Readers can list and open published articles while drafts stay private.
| File | Cluster | What it covers |
|---|---|---|
| `09.01-set-the-scene.md` | Open | Public writing turns a portfolio from a brochure into evidence of thinking. |
| `09.02-why-filter-status.md` | Learn | Explain why drafts must never leak through public routes. |
| `09.03-what-youll-build.md` | Open | Build public article list, article cards, article pages, and metadata. |
| `09.04-article-card.md` | Build | Create components/articles/ArticleCard.tsx for title, excerpt, tags, date, and reading time. |
| `09.05-articles-index-route.md` | Build | Create app/articles/page.tsx that calls the published-card repository function. |
| `09.06-article-detail-route.md` | Build | Create a slug route for published article content with not-found handling. |
| `09.07-markdown-rendering.md` | Build | Render article Markdown with react-markdown and remark-gfm while keeping unsafe HTML out. |
| `09.08-metadata-per-article.md` | Build | Generate page title and description from article fields. |
| `09.09-featured-articles-home.md` | Build | Show two featured published articles on the home page. |
| `09.10-empty-state.md` | Build | Design a quiet empty state when no published articles exist. |
| `09.11-draft-leak-test.md` | Build | Create a draft and confirm it appears in admin reads but not public reads. |
| `09.12-recap-and-whats-next.md` | Wrap | Readers can see articles; next the owner needs an admin door. |
| `09.13-checklist.md` | Checklist | Gate public articles. |

## 10 - Admin auth (`10-admin-auth/`)
**Gate:** Admin login, logout, session cookie, CSRF token, and protected redirects work without exposing secrets.
| File | Cluster | What it covers |
|---|---|---|
| `10.01-set-the-scene.md` | Open | Publishing needs a locked room, not hidden links. |
| `10.02-password-gate-tradeoff.md` | Learn | Explain why a single-owner portfolio can use a shared admin password with strong env discipline. |
| `10.03-what-youll-build.md` | Open | Build admin login, session validation, CSRF token, logout, and redirects. |
| `10.04-session-cookie-shape.md` | Learn | Teach httpOnly, sameSite, secure, maxAge, and why the browser should not read the token. |
| `10.05-admin-env-vars.md` | Build | Add ADMIN_PASSWORD, ADMIN_SESSION_TOKEN, ADMIN_USER_ID, and ADMIN_EMAIL to the env contract. |
| `10.06-admin-session-helper.md` | Build | Create lib/auth/admin-session.ts with constants and validation behavior. |
| `10.07-login-page.md` | Build | Create app/admin/login/page.tsx with a password form posting to the login route. |
| `10.08-login-route.md` | Build | Create app/api/admin/login/route.ts to compare the password and set session/CSRF cookies. |
| `10.09-admin-index-redirect.md` | Build | Create app/admin/page.tsx to redirect valid sessions to dashboard and invalid sessions to login. |
| `10.10-logout-route.md` | Build | Create app/api/admin/logout/route.ts that requires CSRF and clears cookies. |
| `10.11-same-origin-check.md` | Build | Add server-side same-origin validation for admin mutations. |
| `10.12-manual-auth-test.md` | Build | Verify wrong password, correct password, refresh, and logout behavior in the browser. |
| `10.13-recap-and-whats-next.md` | Wrap | The admin door exists; next put useful work behind it. |
| `10.14-checklist.md` | Checklist | Gate admin auth. |

## 11 - Admin dashboard (`11-admin-dashboard/`)
**Gate:** Authenticated admins can view stats, navigation shortcuts, data-source mode, and protected article management pages.
| File | Cluster | What it covers |
|---|---|---|
| `11.01-set-the-scene.md` | Open | A dashboard should reduce publishing friction, not become another brochure page. |
| `11.02-dashboard-information.md` | Learn | Choose stats that help the owner act: total, published, draft, and data source. |
| `11.03-what-youll-build.md` | Open | Build protected dashboard, stats query, quick actions, and article manager route. |
| `11.04-stats-repository.md` | Build | Add getArticleStats in the repository with database and seed fallback modes. |
| `11.05-dashboard-route.md` | Build | Create app/admin/dashboard/page.tsx and redirect unauthenticated requests. |
| `11.06-stats-cards.md` | Build | Render article counts and data-source mode as dashboard cards. |
| `11.07-quick-actions.md` | Build | Add links for article manager, new article, public articles, and website home. |
| `11.08-logout-form.md` | Build | Place a logout form with the CSRF token from cookies. |
| `11.09-article-manager-route.md` | Build | Create app/admin/articles/page.tsx with protected admin article rows. |
| `11.10-row-actions-component.md` | Build | Create components/admin/ArticleRowActions.tsx for edit/delete actions. |
| `11.11-protected-route-review.md` | Build | Check every admin page redirects when the session cookie is absent or invalid. |
| `11.12-recap-and-whats-next.md` | Wrap | The dashboard can see content; next it needs to edit it. |
| `11.13-checklist.md` | Checklist | Gate admin dashboard. |

## 12 - Article editor (`12-article-editor/`)
**Gate:** Admins can create, edit, delete, publish, archive, and validate articles with predictable API behavior.
| File | Cluster | What it covers |
|---|---|---|
| `12.01-set-the-scene.md` | Open | A publishing tool is mostly state management plus trust boundaries. |
| `12.02-form-state-vs-server-truth.md` | Learn | Explain why the client form is convenient but the route handler owns validation. |
| `12.03-what-youll-build.md` | Open | Build editor form, create/edit pages, article APIs, slug check, and delete action. |
| `12.04-article-api-contract.md` | Learn | Define required fields, optional fields, statuses, and error responses for article mutations. |
| `12.05-new-article-route.md` | Build | Create app/admin/articles/new/page.tsx with the admin article form in create mode. |
| `12.06-edit-article-route.md` | Build | Create app/admin/articles/[id]/page.tsx with initial values and not-found behavior. |
| `12.07-admin-article-form.md` | Build | Create components/admin/AdminArticleForm.tsx with controlled fields and status selection. |
| `12.08-create-api-route.md` | Build | Create POST /api/articles for authenticated create behavior. |
| `12.09-update-api-route.md` | Build | Create PATCH /api/articles/[id] for authenticated update behavior. |
| `12.10-delete-api-route.md` | Build | Create DELETE /api/articles/[id] with same-origin and CSRF checks. |
| `12.11-slug-check-route.md` | Build | Create /api/articles/check-slug so the editor can warn about duplicates. |
| `12.12-status-transitions.md` | Build | Implement draft, published, and archived behavior with publishedAt rules. |
| `12.13-error-mapping.md` | Build | Map validation, duplicate slug, missing article, and unauthorized errors to clear UI messages. |
| `12.14-manual-editor-test.md` | Build | Create, publish, edit, archive, and delete one article while watching public visibility. |
| `12.15-recap-and-whats-next.md` | Wrap | The editor works; next preserve history. |
| `12.16-checklist.md` | Checklist | Gate article editor. |

## 13 - Revision history (`13-revision-history/`)
**Gate:** Article edits create revision snapshots that admins can inspect without exposing them publicly.
| File | Cluster | What it covers |
|---|---|---|
| `13.01-set-the-scene.md` | Open | Publishing systems need memory because edits are part of the work. |
| `13.02-snapshot-vs-diff.md` | Learn | Compare full revision snapshots with text diffs and choose snapshots for this project. |
| `13.03-what-youll-build.md` | Open | Add ArticleRevision, migration, snapshot creation, and revision history UI. |
| `13.04-revision-model.md` | Build | Add ArticleRevision with article relation, revisionNumber, content fields, and indexes. |
| `13.05-revision-migration.md` | Build | Run a migration and inspect cascade delete plus unique revision numbering. |
| `13.06-snapshot-on-create.md` | Build | Create revision 1 when an article is first created. |
| `13.07-snapshot-on-update.md` | Build | Create the next revision when meaningful article fields change. |
| `13.08-revision-query.md` | Build | Add a repository/API read for revisions belonging to one article. |
| `13.09-revision-api-route.md` | Build | Create app/api/articles/[id]/revisions/route.ts protected by admin session. |
| `13.10-revision-history-component.md` | Build | Create components/admin/ArticleRevisionHistory.tsx with revision number, date, status, and title. |
| `13.11-embed-history-in-editor.md` | Build | Show revision history on the edit page without blocking the form. |
| `13.12-privacy-check.md` | Build | Confirm revisions are not reachable from public article pages or unauthenticated API calls. |
| `13.13-recap-and-whats-next.md` | Wrap | Publishing is safer; next protect forms and contact routes. |
| `13.14-checklist.md` | Checklist | Gate revision history. |

## 14 - Contact and security (`14-contact-and-security/`)
**Gate:** The contact form validates input, optional email delivery is safe, and shared security helpers protect admin mutations.
| File | Cluster | What it covers |
|---|---|---|
| `14.01-set-the-scene.md` | Open | A contact form is an invitation from the internet into your server. |
| `14.02-threat-model.md` | Learn | Name spam, HTML injection, forged admin requests, and leaked secrets before building. |
| `14.03-what-youll-build.md` | Open | Build contact page, contact API, escaping, optional Resend integration, and security helpers. |
| `14.04-contact-page.md` | Build | Create app/contact/page.tsx with contact methods and the form component. |
| `14.05-contact-form-component.md` | Build | Create components/contact/ContactForm.tsx with client-side states and accessible messages. |
| `14.06-contact-api-contract.md` | Learn | Define name, email, message, validation limits, and success/error shapes. |
| `14.07-contact-route.md` | Build | Create app/api/contact/route.ts with server-side validation and clear responses. |
| `14.08-html-escape-helper.md` | Build | Create a server helper that escapes user-provided contact content before email HTML. |
| `14.09-optional-email-provider.md` | Build | Use RESEND_API_KEY, CONTACT_TO_EMAIL, and CONTACT_FROM_EMAIL only when configured. |
| `14.10-client-security-helper.md` | Build | Create client helper behavior for CSRF token reads or same-origin request ergonomics. |
| `14.11-server-security-helper.md` | Build | Centralize same-origin and CSRF validation in lib/security/server.ts. |
| `14.12-negative-tests.md` | Build | Send missing fields, long messages, invalid email, and cross-origin-like requests. |
| `14.13-recap-and-whats-next.md` | Wrap | The site accepts messages safely; next make it discoverable and observable. |
| `14.14-checklist.md` | Checklist | Gate contact and security. |

## 15 - SEO, observability, and policies (`15-seo-observability-and-policies/`)
**Gate:** The site publishes metadata, sitemap, robots, analytics, speed insights, security headers, and project policy docs.
| File | Cluster | What it covers |
|---|---|---|
| `15.01-set-the-scene.md` | Open | Shipping a portfolio includes how machines and browsers read it. |
| `15.02-seo-without-theater.md` | Learn | Focus on titles, descriptions, crawl paths, and stable URLs instead of keyword stuffing. |
| `15.03-what-youll-build.md` | Open | Add metadata, sitemap, robots, analytics, speed insights, headers, and docs. |
| `15.04-root-metadata.md` | Build | Set app/layout.tsx metadata defaults using NEXT_PUBLIC_SITE_URL where needed. |
| `15.05-route-metadata.md` | Build | Add focused metadata to projects, articles, story, and contact routes. |
| `15.06-sitemap-route.md` | Build | Create app/sitemap.ts with static routes plus project/article URLs. |
| `15.07-robots-route.md` | Build | Create app/robots.ts that points crawlers to the sitemap. |
| `15.08-analytics-and-speed.md` | Build | Add Vercel Analytics and Speed Insights in the app shell. |
| `15.09-security-headers.md` | Build | Configure next.config.ts headers including CSP, HSTS, frame, referrer, and permissions policies. |
| `15.10-project-policies-doc.md` | Build | Create docs/project-policies.md for security, env, publishing, and deployment rules. |
| `15.11-audit-pass.md` | Build | Run lint, audit, and build; record failures before fixing them. |
| `15.12-recap-and-whats-next.md` | Wrap | The site is production-shaped; next deploy and prove it. |
| `15.13-checklist.md` | Checklist | Gate SEO and policies. |

## 16 - Deploy and ship (`16-deploy-and-ship/`)
**Gate:** The portfolio is deployed with production env vars, smoke tests, build checks, and a final case study.
| File | Cluster | What it covers |
|---|---|---|
| `16.01-set-the-scene.md` | Open | A portfolio is not finished until someone else can visit it. |
| `16.02-local-vs-production.md` | Learn | Explain how env vars, database URLs, cookies, and HTTPS change in production. |
| `16.03-what-youll-build.md` | Open | Prepare env, deploy to Vercel, run smoke tests, and write final docs. |
| `16.04-production-env-checklist.md` | Build | List DATABASE_URL, DIRECT_URL, NEXT_PUBLIC_SITE_URL, admin, and contact variables for Vercel. |
| `16.05-database-production.md` | Build | Create or connect the production PostgreSQL database and run migrations intentionally. |
| `16.06-vercel-project.md` | Build | Import the repo into Vercel and confirm build settings match Next.js. |
| `16.07-first-deploy.md` | Build | Deploy, read logs, and fix only verified issues. |
| `16.08-smoke-test-public.md` | Build | Check home, story, projects, diagrams, articles, contact, sitemap, and robots on HTTPS. |
| `16.09-smoke-test-admin.md` | Build | Check login, dashboard, create/edit/publish/delete, revision history, and logout on HTTPS. |
| `16.10-security-smoke-test.md` | Build | Confirm drafts stay private, admin rejects missing session, and headers are present. |
| `16.11-performance-check.md` | Build | Use build output and browser checks to catch large images or slow pages. |
| `16.12-readme-final.md` | Build | Update README with setup, env, scripts, verification, and deployment notes. |
| `16.13-case-study.md` | Build | Write a short case study explaining the product, architecture, tradeoffs, and security choices. |
| `16.14-recap-and-whats-next.md` | Wrap | The app is live; closing work turns it into a portfolio artifact. |
| `16.15-checklist.md` | Checklist | Gate shipping. |

## 17 - Closing (`17-closing/`)
**Gate:** Mentee has a final demo script, documentation, and bar-raiser list for future improvements.
| File | Cluster | What it covers |
|---|---|---|
| `17.01-ship-it.md` | Wrap | Record the final live URL, repo URL, screenshots, and demo path. |
| `17.02-document-it.md` | Wrap | Make the README and case study clear enough for another developer to run and review. |
| `17.03-bar-raiser.md` | Wrap | Choose future improvements without hiding unfinished required work. |
| `17.04-final-checklist.md` | Checklist | Close the course only when the portfolio can be demoed end to end. |


