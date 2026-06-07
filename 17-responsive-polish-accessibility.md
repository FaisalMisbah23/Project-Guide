# Chapter 17 - Responsive polish and accessibility

Polish is not decoration. It is respect for the person using the site. A visitor may open your portfolio on a phone between meetings. The owner may manage content on a laptop. Keyboard and screen-reader users should not be treated as an afterthought.

## Where we're headed

By the end, public and admin pages are responsive, readable, keyboard-accessible, labeled, and visually consistent.

## The polish trap

Bad:

```txt
desktop looks fine
mobile cards overflow
buttons have unclear labels
forms depend on placeholder text
```

Problem: the app demos well on your machine and fails in normal use.

Better:

```txt
test mobile early
labels are explicit
focus states are visible
layout handles long text
images have alt text
```

## Build it

Audit every public page at mobile, tablet, and desktop widths. Then audit admin pages. Admin does not need to be flashy; it needs to be efficient and clear.

Check:

```txt
navigation
project cards
article cards
forms
dialogs
tables/lists
image previews
dashboard cards
contact inbox
```

Use Tailwind responsive utilities deliberately. Use shadcn/ui components consistently, but do not let a component library make design decisions for you.

## Accessibility basics

Every input needs a label. Every meaningful image needs alt text. Buttons should say what they do. Destructive actions need confirmation. Keyboard focus should be visible. Heading order should make sense.

## Definition of Done

- [ ] Public pages work on mobile and desktop.
- [ ] Admin pages work on mobile enough to be usable.
- [ ] Forms have labels.
- [ ] Keyboard navigation works.
- [ ] Focus states are visible.
- [ ] Images have useful alt text or are decorative.
- [ ] Destructive actions are confirmed.

> **Log it.** In `learning-log/17-responsive-polish-accessibility.md`, describe one accessibility fix you made and who it helps.

Next: the app works locally. Ship it with the right environment boundaries. -> **[Chapter 18 - Deploy with Vercel and Supabase](18-deploy-vercel-supabase.md)**
