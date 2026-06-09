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
