# Chapter 16 - Validation, errors, and empty states

Features are not finished when the happy path works. Real users arrive with slow connections, empty databases, invalid emails, missing slugs, broken uploads, and accidental double clicks. This chapter turns those cases into designed behavior.

## Where we're headed

By the end, forms validate input, errors are understandable, loading states are visible, empty states are helpful, and edge cases have been tested.

## The failure trap

Bad:

```txt
console.error(error)
return null
```

Problem: the developer sees something in the console, but the user sees a broken or blank screen.

Better:

```txt
show a human message
preserve useful user input
offer next action
log enough for debugging
```

## Build it

Audit every major surface:

```txt
projects list
project detail
articles list
article detail
contact form
newsletter form
admin login
CRUD forms
image upload
contact inbox
dashboard cards
```

For each, test loading, empty, error, success, and blocked cases.

## Empty state examples

Bad:

```txt
No data.
```

Better:

```txt
No projects match this category yet. Clear filters to see all projects.
```

Bad:

```txt
Error.
```

Better:

```txt
Message saved, but the email notification failed. Check the admin inbox.
```

## Daily guideline

Read the "Think About Real Users" and "Test Edge Cases" sections in `Daily_Software_Development_Guidelines.md` if that file is part of your cohort resources. Use them right here: decide what the visitor or owner needs to know at the moment of failure.

## Definition of Done

- [ ] Required forms validate before submission and on the server where needed.
- [ ] Loading states exist.
- [ ] Empty states explain what happened.
- [ ] Error states offer a next step.
- [ ] Success states confirm what changed.
- [ ] Edge cases were tested and logged.

> **Log it.** In `learning-log/16-validation-errors-empty-states.md`, list three edge cases you tested and how the UI responded.

Next: the app behaves correctly. Now make it feel good on real devices and assistive technology. -> **[Chapter 17 - Responsive polish and accessibility](17-responsive-polish-accessibility.md)**
