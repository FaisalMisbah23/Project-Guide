# Chapter 16 - Validation, errors, and empty states

A feature is not finished when the happy path works. Real users bring slow networks, invalid emails, empty databases, failed uploads, expired sessions, and accidental double clicks. Blank screens are not neutral; they make the app feel broken.

## The point of this chapter

A whole-app pass over validation, loading, empty, error, unauthorized, not-found, failed upload, failed email, and double-submit behavior.

## Before you touch code

- Major features exist at least in rough form.
- You can intentionally create errors in development.
- You are willing to test unhappy paths, not just click through success.

## Vocabulary for this chapter

- **Validation.** Rejecting bad input before work happens.
- **Error state.** UI for failed work.
- **Empty state.** UI for successful work with no records.
- **Unauthorized.** The user is not allowed or not signed in.
- **Regression.** Something that used to work breaks later.

## Guided snippet or contract

This is a shape to aim for, not a finished solution to paste blindly:

```txt
State contract per screen
  loading: something is in progress
  empty: request worked but no rows exist
  error: request failed
  unauthorized: user cannot access this surface
  not-found: requested public item does not exist or is not visible
  success: expected content/action completed
```

## Step 1 - Audit every surface

List projects, articles, contact, newsletter, login, admin CRUD, image upload, inbox, analytics, and dashboard cards. Each needs states, not just content.

## Step 2 - Separate validation from error handling

Validation stops bad input before work happens. Error handling responds when work still fails. Both matter.

## Step 3 - Preserve the user's work

If a form fails validation, do not erase a thoughtful message or article body. The user already did the work once.

## Step 4 - Test ugly paths deliberately

Force slow loading, missing slugs, empty tables, failed uploads, failed Brevo, duplicate submits, and unauthorized access. Write the expected UI before checking the actual UI.

## Step 5 - Add the first tests where risk is high

Validation helpers, mappers, published-only queries, auth guards, and contact degraded-success behavior are good first tests.

## Step 6 - Create a state matrix

Make a table before changing UI:

```txt
Surface              loading empty error success unauthorized not-found double-submit
projects list        yes     yes   yes   yes     n/a          n/a       n/a
project detail       yes     n/a   yes   yes     n/a          yes       n/a
contact form         yes     n/a   yes   yes     n/a          n/a       yes
admin projects       yes     yes   yes   yes     yes          n/a       yes
```

Fill it for every major screen. Empty cells are how blank screens happen.

## Step 7 - Build reusable UI states carefully

You can create shared components for common states, but do not make every message generic. `No data` is not enough. A useful empty state names the thing and the next action.

```txt
No projects match this filter. Clear filters to see all published work.
Message saved, but email notification failed. Check the admin inbox.
```

## Step 8 - Do it on your project

Audit and update:

```txt
public lists and details
contact and newsletter forms
admin login
project/article CRUD forms
image upload
messages inbox
analytics dashboard
```

Add validation helpers where rules repeat.

## Prove it before moving on

Force failures intentionally: invalid email, duplicate slug, slow network, missing slug, empty table, failed upload, forced Brevo failure, expired session, double submit. The UI should never be silent.

## If it breaks

| Symptom | Likely cause | Smallest next test |
|---|---|---|
| Blank screen | Component returns null on error/loading branch | Add visible state for every branch. |
| Form clears after error | State reset runs before save succeeds | Reset only after confirmed success. |
| Duplicate submit | Button remains active while saving | Disable submit and rely on constraints/idempotency where needed. |
| Every failure says same thing | Technical errors are not mapped | Create user-facing messages per failure type. |

## What you should be able to explain

- Why blank screens damage trust.
- Why client and server validation both matter.
- Which failure state is highest risk in this portfolio.

## The slower beginner path

If this chapter feels too large, split the validation and failure-state pass into one sitting per checkpoint. The goal is not to finish fast; the goal is to finish with proof.

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

> **📖 Mandatory read.** Read [MDN form validation](https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Forms/Form_validation), [React conditional rendering](https://react.dev/learn/conditional-rendering), [Vitest](https://vitest.dev/guide/), and [Playwright](https://playwright.dev/docs/intro). Required: designed failure is part of the product.

> **💡 Hint.** A useful error says what happened and what the user can do next. `Error.` is rarely useful.

## Definition of Done

- [ ] Major screens have loading, empty, error, and success states.
- [ ] Unauthorized and not-found states are distinct.
- [ ] Forms validate on the client and server where needed.
- [ ] Double submits do not create duplicate records.
- [ ] Contact saved-but-email-failed has a clear message.
- [ ] At least the riskiest helpers or workflows have tests or written smoke checks.

> **✍️ Log it (mandatory).** In `learning-log/16-validation-errors-empty-states.md`: describe one failure state you improved and why the new behavior is better for the user.

All boxes ticked? Then continue. The next chapter builds on this gate, not around it.

---

Next: the app behaves correctly; now make it work on real devices and input methods. -> **[Chapter 17 - Responsive polish and accessibility](17-responsive-polish-accessibility.md)**
