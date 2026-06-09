# Chapter 17 - Responsive polish and accessibility

The app works; now it has to feel trustworthy on real screens and with real input methods. Polish is not decoration. It is whether a visitor can read, navigate, submit, and understand the portfolio without fighting it.

## The point of this chapter

Responsive layout, semantic HTML, keyboard navigation, labels, focus states, alt text, and a final public/admin usability pass.

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
