# Chapter 16 - Validation, errors, and empty states

A feature is not finished when the happy path works. Real users bring slow networks, invalid emails, empty databases, failed uploads, expired sessions, and accidental double clicks. Blank screens are not neutral; they make the app feel broken.

## The point of this chapter

A whole-app pass over validation, loading, empty, error, unauthorized, not-found, failed upload, failed email, and double-submit behavior.

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
