# Chapter 17 - Responsive Polish And Accessibility

The app works. Now make it usable on phones, tablets, desktops, keyboards, and assistive technology.

## Goal

By the end, the portfolio is responsive, keyboard-friendly, readable, and accessible enough for a serious v1.

## What You Will Build

- Responsive layout pass.
- Mobile navigation.
- Keyboard checks.
- Accessible labels and alt text.
- Focus states.
- Basic contrast and readability review.

## Beginner Concepts

- **Responsive design:** layout adapts to screen size.
- **Breakpoint:** screen width where layout changes.
- **Keyboard navigation:** using Tab, Enter, Escape, and arrows where appropriate.
- **Focus state:** visible indicator of the active element.
- **Semantic HTML:** HTML that communicates meaning, such as `main`, `nav`, `button`, `label`.
- **Contrast:** readability between text and background.

## Step By Step

### Step 1 - Check Real Viewports

Inspect at:

```txt
mobile width around 375px
tablet width around 768px
desktop width around 1280px
```

Check home, projects, article detail, contact, admin dashboard, admin forms, and inbox.

### Step 2 - Fix Navigation On Small Screens

The navbar should not overflow. Add a mobile menu or a compact stacked layout.

Make sure links are large enough to tap.

### Step 3 - Fix Layout Overflow

Look for:

```txt
cards too wide
tables overflowing
long slugs or URLs breaking layout
buttons wrapping badly
forms too cramped
```

Use responsive grids, wrapping, and sensible max widths.

### Step 4 - Check Keyboard Use

Use only the keyboard:

```txt
Tab through nav links
Tab through forms
Submit buttons with Enter
Close menus or dialogs
Reach admin actions
See focus clearly
```

### Step 5 - Add Labels And Alt Text

Every input needs a label. Every meaningful image needs useful alt text. Decorative images should be marked appropriately.

### Step 6 - Check Headings And Page Structure

Each page should have one clear main heading. Sections should use headings in order.

Use:

```txt
header
nav
main
section
footer
```

### Step 7 - Review Color And Text

Check that text is readable. Avoid tiny text, low contrast, and layout where text overlaps.

## Common Mistakes

| Mistake | Why it hurts | Fix |
|---|---|---|
| Designing only on desktop | Mobile breaks | Test narrow screens |
| Removing focus outlines | Keyboard users get lost | Keep visible focus |
| Placeholder alt text | Screen readers get poor info | Write useful alt text |
| Labels replaced by placeholders | Inputs are harder to use | Add real labels |

## Checks Before Moving On

- Public pages work on mobile and desktop.
- Admin pages remain usable.
- Navbar does not overflow.
- Keyboard navigation works.
- Focus is visible.
- Forms have labels.
- Images have alt text.

## Learning Log

In `learning-log/17-responsive-polish-accessibility.md`, answer:

```txt
Which page broke most on mobile?
What keyboard path did you test?
Which images needed better alt text?
What accessibility issue did you fix?
```

## Definition Of Done

- [ ] Mobile, tablet, and desktop layouts are checked.
- [ ] Public and admin navigation are usable.
- [ ] Keyboard navigation is possible.
- [ ] Focus states are visible.
- [ ] Forms have labels.
- [ ] Important images have useful alt text.

Next: deploy the app. -> **[Chapter 18 - Deploy With Vercel And Supabase](18-deploy-vercel-supabase.md)**
