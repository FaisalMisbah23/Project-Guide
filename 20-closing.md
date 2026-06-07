# Chapter 20 - Closing

You built a full-stack portfolio: public pages, Supabase data, RLS, owner auth, admin CRUD, articles, comments, image storage, contact persistence, Brevo notifications, newsletter workflow, analytics, Realtime, and deployment.

That is more than a portfolio. It is a small system with boundaries you can explain.

## What you can now defend

You should be able to answer:

```txt
Why did this app need a database?
What data is public?
What data is owner-only?
How does RLS protect rows?
Why is the anon key allowed in the browser?
Why are Brevo keys server-only?
What happens when contact email fails?
How are images stored?
How do admin routes differ from database policies?
How does deployment split between Vercel and Supabase?
```

## The real next step

Do not let the portfolio freeze. Add one good project writeup. Add one article about a tradeoff you actually faced. Improve one UI detail. Review one security rule. The project gets stronger when it stays alive.

## Final Definition of Done

- [ ] Production URL works.
- [ ] Admin login works.
- [ ] Public content is polished.
- [ ] Contact flow works.
- [ ] Brevo notification works.
- [ ] No private secret appears in frontend code.
- [ ] Learning log is complete.
- [ ] You can demo and explain the system without reading notes.

> **Final log.** In `learning-log/20-closing.md`, write the story of what you built, what you understand now that you did not understand before, and what you will improve next.

You now have the kind of portfolio that does not merely say "I am a software engineer." It shows the work.
