# Chapter 20 - Closing

You built more than a portfolio. You built a small system with public reading, owner writing, protected data, server-side workflows, storage, analytics, deployment, and a story behind every important decision.

## The point of this chapter

Turn the finished project into a final case study, a confident demo, and a habit of continued improvement.

## Section 1 - What you can now defend

You should be able to explain why the app needed a database, what RLS protects, why the anon key can be public, why service-role cannot, why contact stores before email, how images are stored, and how deployment splits between Vercel and Supabase.

## Section 2 - Write the final story

The story is not `I used React and Supabase`. The story is: problem, decision, tradeoff, result, next improvement. That is how engineering work becomes understandable.

## Section 3 - Keep the portfolio alive

Add one real project writeup. Publish one article about a tradeoff. Improve one UI detail. Review one security rule. A living portfolio gets stronger over time.

## Section 4 - Rehearse without notes

Open the production app and demo it as if a senior engineer is watching. Trace one request. Explain one failure. Show one blocked access case.

## Section 5 - The final defense checklist

Before calling the course complete, answer these without reading notes:

```txt
Why did this portfolio need a database?
Which data is public and which is owner-only?
How does RLS protect rows?
Why is the anon key allowed in browser code?
Why is service-role forbidden in React?
What happens when Brevo fails?
How are images stored?
What does deployment split between Vercel and Supabase?
What would you improve next?
```

If one answer is weak, revisit that chapter. The point is not perfection. The point is being honest about what you understand.

## Section 6 - Do one real improvement

Before sharing widely, make one improvement that uses the system you built:

```txt
add one real project writeup
publish one article about a tradeoff
replace placeholder screenshots
improve one empty state
review one RLS policy
run the production smoke test again
```

This turns the portfolio from a course artifact into a living tool.

## Prove it after the course

Schedule a 30-day review. A maintained portfolio beats a frozen one. Check contact messages, broken links, dependencies, production logs, and whether your newest work is represented.

> **📖 Mandatory read.** Read [GitHub profile docs](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-github-profile/customizing-your-profile/about-your-profile), [Vercel domains](https://vercel.com/docs/domains), and [Supabase platform overview](https://supabase.com/docs/guides/platform). Required: the project now connects to your public developer identity.

> **💡 Hint.** If you cannot explain a feature without reading notes, that is not failure. It is the next learning target.

## Definition of Done

- [ ] Production URL works.
- [ ] Admin login works.
- [ ] Public content is polished.
- [ ] Contact flow works and failure behavior is understood.
- [ ] No private secret appears in frontend code.
- [ ] Learning log is complete.
- [ ] Final case study exists.
- [ ] You can demo and defend the system without reading notes.

> **✍️ Log it (mandatory).** In `learning-log/20-closing.md`: write what you built, what you understand now that you did not understand before, and what you will improve next.

All boxes ticked? Then continue. The next chapter builds on this gate, not around it.
