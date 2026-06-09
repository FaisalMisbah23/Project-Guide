# Chapter 13 - Contact inbox and Realtime

Now that messages are stored, the owner needs a place to read them. Email is useful, but the app's inbox is the durable workflow. Realtime can make it feel alive, but it is not the source of truth.

## The point of this chapter

Owner-only contact inbox with list, detail, read/archive workflow, notification-status visibility, and optional Realtime updates for new messages.

## Step 1 - Load stored messages first

The inbox begins with a normal query ordered newest first. If Realtime disconnects, refresh should still show the truth.

## Step 2 - Use statuses instead of deleting

Unread, read, and archived give the owner workflow without destroying history. Delete can exist later, but it should not be the default.

## Step 3 - Add Realtime as convenience

Subscribe to inserts on `contact_messages` to update an unread count or prepend new messages. Then clean up the channel when the component unmounts.

## Step 4 - Surface notification problems

If Brevo failed in Chapter 12, the inbox should show that. The owner needs to know the database has a message even if email did not arrive.

## Step 5 - Define the inbox feature folder

```txt
src/features/messages/
  messageTypes.ts
  messageApi.ts
  useMessagesRealtime.ts
  AdminMessagesPage.tsx
  MessageList.tsx
  MessageDetail.tsx
```

The Realtime hook should be optional. The page should still work from normal queries.

## Step 6 - Write the inbox states

Messages need a lifecycle:

```txt
unread -> read -> archived
archived -> restored, if you support it
notification_status -> sent or failed
```

Status gives workflow without destroying history.

## Step 7 - Do it on your project

Build in this order:

1. Query newest messages.
2. Render list and detail.
3. Mark read.
4. Archive.
5. Show notification failure from Chapter 12.
6. Add Realtime insert subscription.
7. Add cleanup.
8. Add disconnected or refresh fallback if useful.

## Prove it before moving on

Submit the contact form in one browser while the inbox is open in another. The message may appear live, but after refresh it must still appear from stored data. Then navigate away and back repeatedly to check for duplicate subscriptions.

> **📖 Mandatory read.** Read [Supabase Realtime](https://supabase.com/docs/guides/realtime), [Supabase JavaScript client](https://supabase.com/docs/reference/javascript/introduction), and [React effect lifecycle](https://react.dev/learn/lifecycle-of-reactive-effects). Required: subscriptions must be started and cleaned up deliberately.

> **💡 Hint.** Navigate away from the inbox and back several times. If one new message appears three times, you probably forgot cleanup.

## Definition of Done

- [ ] Admin inbox lists stored messages.
- [ ] Owner can open a message detail view.
- [ ] Owner can mark messages read and archive them.
- [ ] Notification success/failure is visible.
- [ ] Realtime updates unread count or list when enabled.
- [ ] Realtime subscription cleanup exists.
- [ ] Signed-out users cannot read contact messages.

> **✍️ Log it (mandatory).** In `learning-log/13-contact-inbox-realtime.md`: explain why the inbox loads existing messages before subscribing to new ones.

All boxes ticked? Then continue. The next chapter builds on this gate, not around it.

---

Next: contact is handled; now let visitors subscribe without leaking provider secrets. -> **[Chapter 14 - Newsletter and Cron](14-newsletter-and-cron.md)**
