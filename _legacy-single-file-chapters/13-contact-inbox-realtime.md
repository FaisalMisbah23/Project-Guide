# Chapter 13 - Contact Inbox And Realtime

Messages are saved. Now the owner needs a private inbox to read them. Realtime can make the inbox feel live, but normal database loading remains the source of truth.

## Goal

By the end, the admin dashboard has a contact inbox with list, detail, read/archive actions, notification status, and optional Realtime updates.

## What You Will Build

- Message API functions.
- Admin inbox page.
- Message detail panel.
- Status update actions.
- Optional Realtime subscription.

## Beginner Concepts

- **Inbox:** private owner workflow for messages.
- **Unread/read/archive:** statuses that organize work.
- **Realtime:** live updates from database changes.
- **Initial load:** normal query used when the page opens.
- **Subscription:** ongoing listener for future changes.

## Step By Step

### Step 1 - Create Message Feature Files

Create:

```txt
src/features/messages/
  messageTypes.ts
  messageApi.ts
  MessageList.tsx
  MessageDetail.tsx
```

### Step 2 - Load Messages Normally First

On `/admin/messages`, fetch the newest messages from the database.

Show:

```txt
loading
empty inbox
error
message list
```

### Step 3 - Show Message Details

When the owner selects a message, show:

```txt
name
email
subject
message
created_at
status
notification_status
```

Notification status helps the owner know whether Brevo succeeded.

### Step 4 - Add Status Actions

Add actions:

```txt
mark as read
mark as unread
archive
```

Avoid hard delete in v1. Messages are useful history.

### Step 5 - Add Optional Realtime

After normal loading works, subscribe to new contact messages. New messages can appear in the inbox or show a “new message” indicator.

The page must still work if Realtime is off.

### Step 6 - Test Permissions

Check:

```txt
owner can read messages
signed-out visitor cannot read messages
owner can update status
signed-out visitor cannot update status
```

## Common Mistakes

| Mistake | Why it hurts | Fix |
|---|---|---|
| Depending only on Realtime | Refresh may show nothing | Load from database first |
| Deleting messages immediately | Loses contact history | Archive |
| Hiding notification failure | Owner misses email problems | Show status |
| Public inbox access | Private visitor data leaks | Owner-only RLS |

## Checks Before Moving On

- Admin inbox loads messages.
- Empty state exists.
- Message detail works.
- Read/unread/archive actions work.
- Notification status is visible.
- Signed-out users are blocked.

## Learning Log

In `learning-log/13-contact-inbox-realtime.md`, answer:

```txt
Why is the database inbox more reliable than email?
Why should Realtime be optional?
What statuses does a message need?
How did you prove messages are private?
```

## Definition Of Done

- [ ] Message list loads.
- [ ] Message detail renders.
- [ ] Owner can change message status.
- [ ] Archived messages are handled.
- [ ] Notification status is visible.
- [ ] RLS blocks unauthorized reads and writes.

Next: add newsletter workflow. -> **[Chapter 14 - Newsletter And Cron](14-newsletter-and-cron.md)**
