# Chapter 16 - Validation, errors, and states

The app has real data now. Real data means real failure: invalid input, blocked policies, slow networks, missing rows, and email provider errors.

> **Principle.** A full-stack app is not complete until failure has a design.

## Where we're headed

By the end, public and admin flows handle validation, loading, success, empty, not-found, and error states consistently.

## Before you build

> **Apply this habit.** Read "Test Edge Cases" in [Daily_Software_Development_Guidelines.md](../Daily_Software_Development_Guidelines.md), then list five edge cases this app must handle.

## Step 1 - Define state patterns

Every data screen should know these states:

```txt
loading
success
empty
error
not found
unauthorized
```

## Step 2 - Standardize form errors

Form errors should appear near fields and be specific.

Bad:

```txt
Invalid.
```

Better:

```txt
Message must be at least 20 characters so I have enough context to reply.
```

## Step 3 - Standardize Supabase errors

Map technical failures to safe user messages.

Do not show raw database errors to public visitors.

## Step 4 - Add retry where useful

Retry is useful for data loading. It is not always useful for destructive actions.

## Step 5 - Test the matrix

Test:

- no projects;
- no articles;
- missing slug;
- signed-out admin;
- failed contact function;
- failed image upload;
- RLS blocked write.

## What your screen should show

The app never shows a blank mystery area. Every important state has clear feedback.

## Small challenge

Create one shared status component for loading/error/empty states if it reduces duplication.

Suggested commit:

```bash
git commit -m "feat: standardize app states"
```

## Definition of Done

- [ ] Public data screens have loading/error/empty states.
- [ ] Admin forms show validation errors.
- [ ] Missing slugs show not found.
- [ ] Signed-out admin access is handled.
- [ ] Contact failure is handled.
- [ ] Image upload failure is handled.

> **Log it.** In `learning-log/16-validation-errors-and-states.md`: Which failure state was easiest to forget? How did you make it visible?

Next: reduce spam and abuse. -> **[Chapter 17 - Spam and abuse protection](17-spam-and-abuse-protection.md)**
