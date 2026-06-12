# Chapter 13 - Build contact inbox and realtime

> Saved contact messages are useful only if the owner can safely read and triage them. Realtime is allowed to make the inbox feel alive, but the database remains the source of truth.

## 13.01 - Set The Scene

The project now needs a **contact inbox**. In Chapter 12, visitors could send messages and the backend could save them before trying the Brevo notification. That was the public side of the workflow. This chapter adds the private owner side: a place where those messages can be read, triaged, and kept as useful history.

The story of this chapter is simple: realtime should make the app feel alive, not make the basic inbox fragile. A live update is exciting, but it is not the source of truth. The source of truth is still the `contact_messages` table protected by Supabase policies. You will load from the database first, then add realtime as an enhancement after the inbox already works.

By the end, the owner can open `/admin/messages`, see saved messages, inspect one message, change its status, and prove that signed-out visitors cannot read private contact data. Your `learning-log/13-contact-inbox-realtime.md` will explain why this shape is safer than a realtime-only shortcut.

---

## 13.02 - Why This Feature Matters

The contact form is only half a feature until the owner can act on the messages. A visitor who writes to you has shared their name, email, subject, and message. That data is useful, but it is also private. The inbox is where the product proves it respects both sides: the visitor gets a reliable way to reach you, and the owner gets a protected workflow for following up.

The tempting version is to treat email as the inbox. If Brevo sends the notification, you might think the app no longer needs an admin screen. That breaks down quickly. Email can fail, messages can be missed, and a demo cannot prove what was saved unless the app can show it. The database inbox gives you a durable record. The email notification becomes a convenience, not the only proof the visitor was heard.

Realtime matters for a different reason. It can make a new message appear while the owner is already looking at the dashboard. That is a nice product feeling, but it should never be required for correctness. A user should be able to refresh `/admin/messages` and still see the same truth from the database.

> **Interesting to read.** Search for "production readiness checklist web app" and notice how many items are about boring reliability: states, secrets, permissions, and recovery.

In this chapter, reliability means four concrete things:

```txt
saved messages survive refreshes
private visitor data stays owner-only
message status can change without deleting history
realtime can fail without breaking the inbox
```

---

## 13.03 - What You Will Build

In this chapter you will build the admin inbox for saved contact messages. This is an owner workflow, not a public page. The public user has already done their job by submitting the form; now the owner needs a calm, private place to review the message and decide what happens next.

The protected surface is:

```txt
/admin/messages
```

The screen should show a list of messages, a selected message detail area, and status actions. It should also show the notification result from Chapter 12 so the owner can see whether the Brevo attempt succeeded, failed, or has not been attempted yet.

Expected project touchpoints:

```txt
src/features/messages/
src/features/messages/messageTypes.ts
src/features/messages/messageApi.ts
src/features/messages/MessageList.tsx
src/features/messages/MessageDetail.tsx
src/pages/admin/AdminMessagesPage.tsx
learning-log/13-contact-inbox-realtime.md
```

Database areas involved:

```txt
contact_messages
```

The minimum message fields the UI needs are:

```txt
id
name
email
subject
message
status
notification_status
created_at
```

Do not add a hard-delete flow in this chapter. The product behavior is archive, not erase. Deletion can be a later maintenance feature with stricter confirmation.

---

## 13.04 - The Beginner Approach And Its Cost

The tempting beginner move is to build the inbox around realtime first. The thought is understandable: "Supabase can push new rows to the browser, so I will subscribe to `contact_messages` and render whatever arrives." It feels fast because a live message popping into the UI is satisfying.

The cost appears as soon as the page refreshes. A realtime subscription hears future changes; it does not automatically give you the past. If the owner opens the inbox after five messages already exist, a realtime-only screen can look empty until the sixth message arrives. That is a broken inbox with a flashy transport layer.

There is also a privacy cost. If the UI subscribes broadly and then hides messages in React, the private data has already crossed into the browser. The rule belongs at the database policy and query boundary. The browser can improve the experience, but it must not be the thing that protects visitor data.

Concrete failure modes to avoid:

```txt
refresh shows an empty inbox even though rows exist
signed-out user can query contact_messages directly
archived messages disappear with no audit trail
notification failure is hidden from the owner
realtime disconnect makes the whole inbox useless
```

You do not need to build the weak version. You only need to understand its failure mode well enough to avoid it.

---

## 13.05 - The Professional Approach

The professional path is to load messages normally first, then add realtime as an enhancement. The first render should come from a normal authenticated Supabase query. That query asks for the exact columns the admin UI needs and relies on RLS to decide whether the caller is allowed to see them.

Only after that works should realtime enter the story. Realtime can add a new row to the list, refresh a badge, or show a "new message received" indicator. If the subscription disconnects, the owner should still be able to refresh the page and get the truth from the database.

| Choice | Why it wins here |
|---|---|
| Load from `contact_messages` first | Existing messages appear after refresh and on first visit |
| Keep owner access in RLS | Privacy survives direct requests and UI bypasses |
| Use statuses instead of hard delete | The owner can triage without losing history |
| Add realtime last | Live updates enhance a working inbox instead of replacing it |

✅ Do treat the database query as the source of truth. ❌ Don't make realtime the only way messages enter the screen.

---

## 13.06 - Key Concepts In Plain English

Use these words precisely in this chapter:

- **Inbox:** a private owner workspace for messages that need attention.
- **Status:** a small label that describes where a message is in the workflow, such as `unread`, `read`, or `archived`.
- **Notification status:** the saved result of the email attempt, such as `sent`, `failed`, or `not_attempted`.
- **Source of truth:** the place the app treats as authoritative. Here, that is the database, not realtime events.
- **Realtime subscription:** a listener that receives future database changes while the page is open.
- **Enhancement:** something that improves the experience but is not required for the feature to work.
- **Privacy boundary:** the line private data must not cross unless the caller is allowed to see it.

The important distinction is source of truth versus enhancement. A normal query answers, "What messages exist right now?" A realtime subscription answers, "What changed after I started listening?" The inbox needs both ideas in that order.

---

## 13.07 - Reading Before You Build

Before building, read enough to recognize the tools you are about to use. The chapter has already made the key product decision: the database load is the foundation and realtime is optional polish. These readings help you understand why that decision fits Supabase.

**Mandatory reads**

- **Supabase Realtime** - focus on what a subscription sends and what it does not send.
- **Supabase Row Level Security policies** - revisit how an owner-only table stays private even when a route exists.
- **Inbox status workflows** - search for simple status systems like unread, read, archived, and notice how they preserve history.

**Interesting to read**

- Search for "realtime as progressive enhancement". The web idea is older than Supabase: make the core workflow work first, then add live behavior when the browser and network allow it.

After reading, write two sentences in `learning-log/13-contact-inbox-realtime.md`: one idea you understood, and one question you still have.

---

## 13.08 - Where The Project Is Now

Chapter 12 left you with a contact backend. The expected shape is:

```txt
contact form submits
Edge Function validates the request
contact_messages receives a row
Brevo notification is attempted
notification_status is stored or inferable
```

Before touching the inbox, prove the previous chapter still works. Submit one test message through the contact form or function, then inspect `contact_messages` in Supabase. You need at least one real saved row because this chapter starts with database loading.

Record the message id or timestamp in `learning-log/13-contact-inbox-realtime.md`. That gives you a known row to look for when the inbox appears.

✅ Do start from a working baseline. ❌ Don't stack new work on top of a broken previous chapter.

---

## 13.09 - Scaffold The Files

Create the inbox files before writing feature logic. The scaffold is the map your future self follows, and it gives the feature a clear home inside the app.

```txt
src/features/messages/
src/features/messages/messageTypes.ts
src/features/messages/messageApi.ts
src/features/messages/MessageList.tsx
src/features/messages/MessageDetail.tsx
src/pages/admin/AdminMessagesPage.tsx
learning-log/13-contact-inbox-realtime.md
```

Give each file one job:

```txt
messageTypes.ts        message shapes and status names
messageApi.ts          Supabase reads and status updates
MessageList.tsx        the inbox list surface
MessageDetail.tsx      the selected message surface
AdminMessagesPage.tsx  page-level state and wiring
```

The point is not to create ceremony. The point is to keep data access out of tiny visual components and keep the admin page readable when realtime is added later.

✅ Do create empty files or small placeholders with names that match the course. ❌ Don't paste final feature logic yet; first make the shape visible.

Verify with `find` or your editor file tree that every named file exists.

---

## 13.10 - Define The Contract

Define the contract before the implementation. A contract says what must go in, what must come out, and what failure looks like.

```txt
Feature: admin contact inbox
Route: /admin/messages
Caller: signed-in owner
Success: newest messages appear with status and notification result
Failure: signed-out or unauthorized caller sees no private data
```

The API contract should support three operations:

```txt
list messages ordered newest first
read one selected message in detail
update status to unread, read, or archived
```

The UI contract should support these states:

```txt
loading messages
empty inbox
message list
selected message detail
status update pending
query or update error
realtime connected, disconnected, or unavailable
```

✅ Do write the contract in comments, docs, or types before logic. ❌ Don't let the first implementation secretly decide the rules.

**Hint.** If you cannot describe the failure response, you are not ready to write the happy path.

---

## 13.11 - Create The Data Or Route Shape

Create the route and data shape this chapter needs. The table should already exist from Chapter 12, so this step is mostly about making the inbox agree with the saved message shape instead of inventing a separate one.

Routes:

```txt
/admin/messages
```

Tables:

```txt
contact_messages
```

Statuses:

```txt
unread
read
archived
```

Notification statuses:

```txt
not_attempted
sent
failed
```

If your table uses different names from Chapter 12, do not silently create a second vocabulary in React. Either align the table or map the database values once in `messageApi.ts` so the rest of the feature stays consistent.

✅ Do name the route and statuses for the owner workflow. ❌ Don't name them after an implementation detail that users never understand.

Verify by opening the route, migration, or Supabase table list.

---

## 13.12 - Write The First Screen Or Helper

Build the first visible inbox shell before fetching real data. The shell should make the owner workflow obvious: a list area for messages and a detail area for the selected message.

Use placeholder data only long enough to prove the layout and component boundaries. The placeholder should have the same shape as the contract from the previous step:

```txt
name
email
subject
message
status
notification_status
created_at
```

The screen does not need to be beautiful yet. It needs to make the workflow testable: "I can see a message, select it, and understand where the status actions will go."

✅ Do separate visual layout from data fetching. ❌ Don't query Supabase from `MessageList` or `MessageDetail`; those components should receive data and callbacks from the page or feature boundary.

Verify by rendering the shell or importing the helper without breaking the build.

---

## 13.13 - Wire The Route Or Module

Now connect the inbox page to the admin route map. Wiring means the feature is reachable from the place the owner naturally expects, not merely that files exist in the repo.

For this chapter, check these entry points:

```txt
/admin/messages
admin navigation link or dashboard card
```

The route should sit behind the same owner protection you built in Chapter 08. A signed-out visitor who types `/admin/messages` manually should meet the auth guard before the inbox page can expose anything.

✅ Do wire one path and test it before adding another. ❌ Don't leave orphaned files that exist but cannot be reached.

Verify with two browser checks:

```txt
signed-in owner can reach /admin/messages
signed-out visitor is redirected or blocked
```

---

## 13.14 - Add Loading And Empty State

Add loading and empty states before real data makes the screen look finished. An admin inbox has long quiet stretches. Some days there are no messages. The empty state should feel like a valid product state, not a broken page.

Minimum states for this step:

```txt
loading messages
empty inbox
list with no selected message
```

The empty state should not tell the owner to configure the course or inspect implementation details. It should simply say, in product language, that no contact messages are waiting.

✅ Do write states that tell the owner what happened. ❌ Don't use the empty state as a substitute for privacy; signed-out users should not see an empty private inbox.

Verify by forcing at least one state instead of waiting for it to happen naturally.

---

## 13.15 - Add Error And Validation State

Add error and validation states for the inbox. The main user input in this chapter is not a text field; it is an action: changing a message status. That action can still fail, and the UI needs to handle it.

Minimum failure states:

```txt
message list query fails
status update fails
selected message no longer exists
realtime connection is unavailable
```

The owner can see more specific errors than a public visitor, but the app still should not dump raw provider output into the UI. Keep the visible message useful, and log or inspect the technical detail during development.

✅ Do keep the previous message status visible if an update fails. ❌ Don't optimistically remove a message from the list before the database confirms the new status.

Verify by forcing at least one state instead of waiting for it to happen naturally.

---

## 13.16 - Connect To Supabase

Connect the inbox to Supabase only after the local shape works. The client should request exactly the data the UI needs and no private extras. For this chapter, "private extras" mostly means avoiding broad row fetches that accidentally pull fields the UI never shows or needs.

The list query should behave like this:

```txt
from contact_messages
select id, name, email, subject, message, status, notification_status, created_at
order created_at newest first
limit to a sensible first page
```

The status update should behave like this:

```txt
input: message id and next status
allowed statuses: unread, read, archived
success: updated message is reflected in the inbox
failure: UI keeps the previous status and explains the failure
```

Realtime comes after the normal query. Subscribe only after the first load works. New rows can appear at the top of the list or trigger a "new message" notice.

✅ Do filter at the query and enforce with RLS. ❌ Don't fetch broad rows and hide fields in React.

Verify with one successful request and one request that should be blocked.

---

## 13.17 - Protect Private Data

Protect the private side of the inbox. Browser checks improve experience, but the database boundary must enforce the rule. The contact message contains visitor identity and a private note to the site owner. It should never be readable by anonymous users.

Run the privacy check as a signed-out user or anon client:

```txt
try to open /admin/messages
try to query contact_messages as anon
try to update a message status as anon
```

The expected result is not merely hidden UI. The expected result is no private data and no unauthorized update.

✅ Do test the boundary directly. ❌ Don't trust that a missing link means the feature is secure.

**Hint.** Security checks should still pass if someone types the URL manually.

---

## 13.18 - Add The Admin Or Public Ui

Finish the admin UI for this chapter. This is not a public marketing surface; it is a working owner tool. It should be efficient, scannable, and hard to misuse.

The inbox should make these things obvious:

```txt
which messages are unread
which message is selected
who sent it
when it arrived
whether the email notification succeeded
which status actions are available
whether realtime is currently active, if you expose that state
```

Avoid adding a hard-delete button. Archive is the safer v1 behavior because it removes the message from the active queue without pretending the contact history never existed.

✅ Do use labels, states, and predictable actions. ❌ Don't hide important actions behind unclear icons or vague button text.

Verify by completing the main workflow once from the UI.

---

## 13.19 - Test The Happy Path

Test the happy path. The goal is to prove that the owner can complete the normal inbox workflow from the UI.

Run this check:

```txt
sign in as owner
open /admin/messages
see the saved test message from Chapter 12
select the message
mark it as read
refresh the page
confirm the read status persisted
```

If realtime is enabled, also submit a new contact message in another browser session and confirm the owner sees either the new row or a clear "new message" notice.

Write the exact check you ran in `learning-log/13-contact-inbox-realtime.md`. Include the route and the message id or timestamp you used.

✅ Do test one thing at a time. ❌ Don't mark the chapter done because the screen "looks right" once.

---

## 13.20 - Test The Failure Path

Test the failure path. The goal is to prove the inbox does something understandable when the database or network path refuses to cooperate.

Choose at least two checks:

```txt
temporarily force the list query to fail and confirm an error state appears
try to update a message to an invalid status and confirm it is rejected
simulate a realtime disconnect and confirm the normal inbox still works
archive a message and confirm it does not vanish before the update succeeds
```

Write the exact check you ran in `learning-log/13-contact-inbox-realtime.md`. If you changed code to force a state, change it back before moving on.

✅ Do test one thing at a time. ❌ Don't mark the chapter done because the screen "looks right" once.

---

## 13.21 - Test The Privacy Boundary

Test the privacy boundary. The goal is to prove that private records are blocked even if the UI is bypassed.

Run these checks:

```txt
signed-out browser opens /admin/messages and cannot see the inbox
anon Supabase client cannot select rows from contact_messages
anon Supabase client cannot update status on a message
owner can still select and update the same message
```

The last check matters. A failed anon request proves the lock exists; a successful owner request proves you did not lock the owner out too.

Write the exact check you ran in `learning-log/13-contact-inbox-realtime.md`. If the check uses the browser, record the route. If it uses Supabase, record the table or function. If it uses the terminal, record the command.

✅ Do test one thing at a time. ❌ Don't mark the chapter done because the screen "looks right" once.

---

## 13.22 - Write The Learning Log

Create or update `learning-log/13-contact-inbox-realtime.md`.

Answer these in your own words:

```txt
What did Chapter 13 add to the project?
Why is database loading the source of truth for the inbox?
Why is realtime an enhancement instead of the foundation?
Which file, route, table, or screen proves the work is real?
What happy path, failure path, and privacy-boundary checks did you run?
What would you improve later: search, filters, bulk archive, or message notes?
```

The learning log is part of the gate. If you cannot explain the chapter, the feature is not finished yet.

✅ Do write short, specific answers tied to your repo. ❌ Don't copy the chapter text back as a summary.

---

## 13.23 - Recap And Whats Next

You added a private contact inbox and proved it with visible checks. The important lesson is not only that the feature works; it is that you can explain why this shape is safer than the shortcut.

The durable part is the database-backed workflow:

```txt
saved messages load after refresh
status changes persist
archived messages keep history
privacy is enforced outside the UI
```

The live part is the enhancement:

```txt
new messages can appear while the owner is watching
the inbox still works if realtime is unavailable
```

Next, Chapter 14 builds the newsletter workflow. The same lesson carries forward: scheduled and live features should add power to a reliable base, not replace it.

Before moving on, commit the work with a message that names the chapter outcome.

---

## 13.24 - Definition Of Done

This checklist is the gate for Chapter 13. Do not move on until every item is true in your own project.

- [ ] `src/features/messages/` contains the message types, API boundary, list, and detail components.
- [ ] `/admin/messages` is wired into the protected admin area.
- [ ] The inbox loads existing rows from `contact_messages` after a refresh.
- [ ] Message detail shows sender, email, subject, message, created time, status, and notification status.
- [ ] Owner can mark a message `read`, `unread`, and `archived`.
- [ ] Realtime, if enabled, is an enhancement; the inbox still works without it.
- [ ] Loading, empty, query error, and status-update failure states have been tested.
- [ ] Signed-out or anon access cannot read or update contact messages.
- [ ] `learning-log/13-contact-inbox-realtime.md` explains the database-first decision and records the happy path, failure path, and privacy checks.

All boxes ticked? Then continue to the next chapter. If not, that is where today's work is.
