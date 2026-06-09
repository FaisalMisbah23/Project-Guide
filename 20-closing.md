# Chapter 20 - Closing

You built more than a portfolio. You built a small system with public reading, owner writing, protected data, server-side workflows, storage, analytics, deployment, and a story behind every important decision.

## The point of this chapter

Turn the finished project into a final case study, a confident demo, and a habit of continued improvement.

## Before you touch code

- Final smoke test has passed or failures are documented.
- Learning log is complete enough to review.
- You have one real project/article to add after the course.
- You can explain the main system boundaries out loud.

## Vocabulary for this chapter

- **Defend.** Explain decisions and tradeoffs under questioning.
- **Tradeoff.** A choice with both benefit and cost.
- **Living portfolio.** A portfolio that keeps receiving real updates.
- **Next improvement.** A specific future change, not vague ambition.

## Guided snippet or contract

This is a shape to aim for, not a finished solution to paste blindly:

```txt
Final defense contract
  demo the public site
  demo owner workflow
  explain RLS and secrets
  explain contact failure behavior
  explain deployment split
  name one residual risk
  name one next improvement
```

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

## If it breaks

| Symptom | Likely cause | Smallest next test |
|---|---|---|
| I cannot explain RLS | You memorized steps without the model | Return to Chapter 04 and redraw allowed/blocked rows. |
| The demo feels like clicking pages | No story path | Narrate visitor trust and owner maintenance. |
| A feature still fails | The course is not actually complete | Document or fix it before claiming final done. |
| Next improvement is vague | No concrete action chosen | Pick one project writeup, article, or security review task. |

## What you should be able to explain

- Why the portfolio demonstrates engineering judgment.
- Which failure behavior you are proudest of.
- What you will improve in the next 30 days.

## The slower beginner path

If this chapter feels too large, split the final defense into one sitting per checkpoint. The goal is not to finish fast; the goal is to finish with proof.

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
