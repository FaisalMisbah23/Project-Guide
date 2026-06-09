# Chapter 17 - Responsive polish and accessibility

The app works; now it has to feel trustworthy on real screens and with real input methods. Polish is not decoration. It is whether a visitor can read, navigate, submit, and understand the portfolio without fighting it.

## The point of this chapter

Responsive layout, semantic HTML, keyboard navigation, labels, focus states, alt text, and a final public/admin usability pass.

## Before you touch code

- Core visitor and owner flows work.
- You can open the app at multiple viewport widths.
- You are ready to use keyboard-only navigation.
- You have real-ish long text examples to test overflow.

## Vocabulary for this chapter

- **Responsive.** Layout adapts to screen size.
- **Semantic HTML.** HTML that describes meaning, not only appearance.
- **Focus indicator.** Visible mark showing current keyboard position.
- **Accessible name.** Name assistive tech uses for a control.
- **Alt text.** Text replacement for meaningful images.

## Guided snippet or contract

This is a shape to aim for, not a finished solution to paste blindly:

```txt
Polish contract
  mobile: readable, no horizontal scroll from layout bugs
  desktop: content uses space without becoming stretched
  keyboard: every action reachable and visible
  forms: label + error + focus behavior
  images: stable size + useful alt text
  admin: dense, scannable, not cramped
```

## Step 1 - Test more than your laptop

Check mobile, tablet, desktop, and a narrow awkward width. Layout bugs love the viewport you forgot.

## Step 2 - Use semantic structure

Headers, nav, main, sections, articles, forms, labels, and buttons give the page meaning before CSS improves it.

## Step 3 - Navigate by keyboard

Every link, button, input, menu, and admin action should be reachable and visibly focused without a mouse.

## Step 4 - Treat text overflow as a bug

Buttons, cards, sidebars, and dashboards should not overlap or clip important text. Fix layout, not the user's screen.

## Step 5 - Review images and forms

Meaningful images need useful alt text. Inputs need labels. Errors need to appear near the field they explain.

## Step 6 - Make a viewport checklist

Test at least:

```txt
360px mobile
768px tablet
1024px laptop
1440px desktop
one awkward narrow height
```

Do not only drag the browser until it looks okay. Use named checkpoints so you can repeat the test later.

## Step 7 - Make a keyboard checklist

Keyboard-test these flows:

```txt
open navigation
move through project cards
submit contact form
log in to admin
open admin project actions
edit and save a form
archive a message
```

The visible focus indicator should tell you where you are at every step.

## Step 8 - Do it on your project

Create a polish pass for:

```txt
public typography and spacing
project/article card grids
article body readability
forms and field errors
admin sidebar/header behavior
modal or confirmation actions
image aspect ratios
button text wrapping
```

## Prove it before moving on

Use only the keyboard for one visitor flow and one owner flow. Then inspect a long title, long email, long URL, and empty image. If text overlaps or controls move unpredictably, keep polishing.

## If it breaks

| Symptom | Likely cause | Smallest next test |
|---|---|---|
| Horizontal scroll on mobile | Fixed width or long unbroken content | Inspect the widest element at 360px. |
| Keyboard focus disappears | Focus outline removed or custom control not focusable | Tab through and inspect active element. |
| Button text overlaps | Container too narrow or text cannot wrap | Test longest realistic label and adjust layout. |
| Screen reader label missing | Input uses placeholder only | Add real label or accessible name. |

## What you should be able to explain

- Why polish is part of trust.
- Why keyboard testing finds real bugs.
- Why placeholder text is not a label.
- How you fixed one overflow or focus issue.

## The slower beginner path

If this chapter feels too large, split the responsive and accessibility pass into one sitting per checkpoint. The goal is not to finish fast; the goal is to finish with proof.

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

> **📖 Mandatory read.** Read [MDN accessibility](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Accessibility), [MDN responsive design](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/CSS_layout/Responsive_Design), and [WebAIM keyboard accessibility](https://webaim.org/techniques/keyboard/). Required: visual polish and accessibility are both part of frontend quality.

> **💡 Hint.** Complete the contact form and at least one admin flow using only the keyboard. That test reveals more than staring at the page.

## Definition of Done

- [ ] Public pages work at mobile and desktop widths.
- [ ] Admin screens remain dense but readable.
- [ ] Keyboard navigation reaches all core controls.
- [ ] Visible focus states exist.
- [ ] Forms have labels and useful errors.
- [ ] Meaningful images have useful alt text.
- [ ] Text does not overlap or escape its containers.

> **✍️ Log it (mandatory).** In `learning-log/17-responsive-polish-accessibility.md`: document one responsive or accessibility issue you found and how you fixed it.

All boxes ticked? Then continue. The next chapter builds on this gate, not around it.

---

Next: the app is polished locally; now ship it with the right environment boundaries. -> **[Chapter 18 - Deploy with Vercel and Supabase](18-deploy-vercel-supabase.md)**
