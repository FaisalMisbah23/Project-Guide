# Chapter 13 - Contact inbox and Realtime

Now that messages are stored, the owner needs a place to read them. Email is useful, but the app's inbox is the durable workflow. Realtime can make it feel alive, but it is not the source of truth.

## The point of this chapter

Owner-only contact inbox with list, detail, read/archive workflow, notification-status visibility, and optional Realtime updates for new messages.

## Before you touch code

- Contact form stores messages.
- Owner auth works.
- RLS blocks signed-out reads of contact_messages.
- At least one message row exists.

## Vocabulary for this chapter

- **Inbox.** Admin workflow for stored contact messages.
- **Unread/read.** Workflow status for owner attention.
- **Archive.** Hide from active view without deleting.
- **Realtime channel.** Subscription that receives future database changes.
- **Cleanup.** Stopping a subscription when a component unmounts.

## Guided snippet or contract

This is a shape to aim for, not a finished solution to paste blindly:

```txt
Inbox contract
  initial load: newest messages from database
  detail: selected message body and metadata
  actions: mark read, archive, optional restore
  Realtime: new inserts update count/list
  fallback: refresh always reloads truth
```

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

## If it breaks

| Symptom | Likely cause | Smallest next test |
|---|---|---|
| New messages duplicate | Realtime subscription created multiple times | Navigate away/back and inspect cleanup. |
| Inbox empty after disconnect | UI depends only on Realtime | Reload from database first, subscribe second. |
| Signed-out user can read messages | RLS policy too broad | Test anon select and fix policy. |
| Owner misses email failure | Notification status is hidden | Show `notification_status` in list or detail. |

## What you should be able to explain

- Why Realtime is convenience, not source of truth.
- Why messages use statuses instead of immediate deletion.
- How cleanup prevents duplicate events.

## The slower beginner path

If this chapter feels too large, split the contact inbox and Realtime workflow into one sitting per checkpoint. The goal is not to finish fast; the goal is to finish with proof.

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
