# Chapter 16 - Validation, Errors, And Empty States

A feature is not finished when the happy path works once. Real visitors see slow networks, empty data, invalid input, expired sessions, duplicate clicks, and failed services.

## Goal

By the end, the major screens have designed loading, empty, error, success, and validation states.

## What You Will Build

- Form validation messages.
- Loading states.
- Empty states.
- Error states.
- Success states.
- Basic regression checks.

## Beginner Concepts

- **Validation:** checking user input before saving.
- **Loading state:** UI shown while waiting.
- **Empty state:** UI shown when a request succeeds but returns nothing.
- **Error state:** UI shown when something fails.
- **Success state:** UI shown after an action completes.
- **Double submit:** clicking submit more than once before the request finishes.

## Step By Step

### Step 1 - List Risky Screens

Review:

```txt
contact form
newsletter form
admin project form
admin article form
image upload
projects page
articles page
admin inbox
analytics dashboard
login page
```

### Step 2 - Add Form Validation

For each form, check required fields before submit. Show messages near the field.

Examples:

```txt
Email is required.
Project title is required.
Slug can only use lowercase letters, numbers, and hyphens.
Message must be at least 20 characters.
```

### Step 3 - Preserve User Input

If validation or network submit fails, do not erase the form. The user should not have to rewrite a message or article body.

### Step 4 - Add Loading States

Show loading when:

```txt
fetching projects
fetching article details
logging in
submitting contact form
uploading image
saving admin form
```

Disable submit buttons while saving to prevent double submits.

### Step 5 - Add Empty States

Examples:

```txt
No published projects yet.
No articles match this search.
Your inbox is empty.
No analytics have been recorded yet.
```

An empty state should explain what happened and, when useful, what to do next.

### Step 6 - Add Error States

Errors should be human:

```txt
Projects could not load. Try refreshing.
Image upload failed. Check file size and type.
Login failed. Check your email and password.
```

Avoid showing raw database errors directly to visitors.

### Step 7 - Force Failures

Test:

```txt
invalid email
duplicate slug
empty database
missing route slug
failed image upload
disabled network
expired session
double submit
```

## Common Mistakes

| Mistake | Why it hurts | Fix |
|---|---|---|
| Blank loading screen | User thinks app is broken | Show loading UI |
| Raw error messages | Confusing or unsafe | Translate to friendly messages |
| Clearing failed form | User loses work | Preserve values |
| No empty state | Successful empty result looks broken | Add empty copy |

## Checks Before Moving On

- Major forms validate input.
- Submit buttons prevent duplicate saves.
- Major data pages show loading.
- Empty data looks intentional.
- Errors are understandable.
- At least one failure was forced per risky workflow.

## Learning Log

In `learning-log/16-validation-errors-empty-states.md`, answer:

```txt
Which screens needed loading states?
Which forms needed validation?
What failure did you force?
How did the UI preserve the user's work?
```

## Definition Of Done

- [ ] Validation exists on major forms.
- [ ] Loading states exist on async screens.
- [ ] Empty states exist.
- [ ] Error states exist.
- [ ] Success states exist where actions complete.
- [ ] Failure checks are written or tested.

Next: polish for real devices and accessibility. -> **[Chapter 17 - Responsive Polish And Accessibility](17-responsive-polish-accessibility.md)**
