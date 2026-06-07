# Chapter 13 - Contact inbox and Realtime

The contact form now stores messages and sends Brevo notifications. That email is useful, but it should not be the only place messages live. The owner needs an inbox inside the admin dashboard.

## Where we're headed

By the end, the admin dashboard has a contact inbox where the owner can read messages, mark them read, archive them, and see new messages arrive through Supabase Realtime.

## The inbox trap

Bad:

```txt
delete message after reading
```

Problem: the owner loses context, cannot track follow-up, and has no fallback if email was missed.

Better:

```txt
unread -> read -> archived
```

Status gives the owner workflow without destroying useful history.

## Build it

Create `/admin/messages`. Load existing messages first, ordered by newest. Render a list and detail panel. Show sender, subject, date, status, and message body.

Add actions:

```txt
mark as read
archive
restore from archive if you support archived view
```

Then add Realtime. Subscribe to inserts on `contact_messages` so new messages update the inbox or unread count without refresh. Always clean up the subscription when the component unmounts.

## Realtime expectations

Realtime is convenience, not the source of truth. If the socket disconnects, the owner should still see messages on refresh. Show a subtle disconnected state if needed.

## Definition of Done

- [ ] Admin inbox lists contact messages.
- [ ] Message detail view exists.
- [ ] Owner can mark messages read.
- [ ] Owner can archive messages.
- [ ] Realtime updates unread count or message list.
- [ ] Subscription cleanup exists.
- [ ] Signed-out users cannot read contact messages.

> **Log it.** In `learning-log/13-contact-inbox-realtime.md`, explain why the app loads existing messages before subscribing to new ones.

Next: contact is handled. Now let visitors subscribe and send scheduled updates thoughtfully. -> **[Chapter 14 - Newsletter and Cron](14-newsletter-and-cron.md)**
