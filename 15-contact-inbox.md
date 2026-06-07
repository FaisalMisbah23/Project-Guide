# Chapter 15 - Contact inbox

Email notification is useful, but the database is the source of truth for contact messages.

> **Principle.** If a user sends something important, give it a durable place to live.

## Where we're headed

By the end, the owner can view contact messages in admin, mark them read, and archive them.

## Before you build

> **Apply this habit.** Read "Think About Real Users" in [Daily_Software_Development_Guidelines.md](../Daily_Software_Development_Guidelines.md), then decide what information the owner needs to reply quickly.

## Step 1 - Create messages page

Create:

```txt
src/pages/admin/
  AdminMessages.jsx
```

Show newest messages first.

## Step 2 - Render message list

Each row should show:

```txt
name
email
subject
created_at
status
```

## Step 3 - Render message detail

The owner should be able to read the full message without leaving the inbox flow.

## Step 4 - Mark read and archive

Support:

```txt
mark as read
archive
```

Do not delete messages by default. Archive is safer.

## Step 5 - Test RLS

Signed-out visitors must not read messages.

## What your screen should show

Admin inbox shows stored messages. Public users cannot access them.

## Small challenge

Add an unread count to the admin dashboard.

Suggested commit:

```bash
git commit -m "feat: add contact inbox"
```

## Definition of Done

- [ ] Admin messages route exists.
- [ ] Messages load for owner.
- [ ] Signed-out users cannot read messages.
- [ ] Owner can mark read.
- [ ] Owner can archive.
- [ ] Dashboard shows unread count.

> **Log it.** In `learning-log/15-contact-inbox.md`: Why is archive safer than delete for contact messages?

Next: make failure states consistent. -> **[Chapter 16 - Validation, errors, and states](16-validation-errors-and-states.md)**
