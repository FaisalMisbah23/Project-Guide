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

## New ideas before you build

### Responsive design

**Real-life analogy:** the same message should fit on a billboard, a poster, and a note card. Responsive design makes one interface fit different screen sizes.

**General idea:** use layout rules that adapt on mobile, tablet, and desktop. Test actual narrow widths, not only your laptop.

```tsx
<section className="grid gap-6 md:grid-cols-2 lg:grid-cols-3">
  {projects.map((project) => <ProjectCard key={project.id} project={project} />)}
</section>
```

Study more: [Frontend Interview Questions - CSS and Styling](https://resources.devweekends.com/resources/frontend-interview-qs)

### Accessibility

**Real-life analogy:** a building needs ramps, signs, and usable doors. A website needs labels, keyboard access, contrast, and meaningful structure.

**General idea:** accessible UI works for keyboard users, screen readers, low-vision users, and people on different devices.

```tsx
<label htmlFor="email">Email</label>
<input id="email" name="email" type="email" />
```

Study more: [Accessibility Overview](https://resources.devweekends.com/courses/angular-crash-course/20-accessibility)

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

## Between chapters

Optional pause. Pick **one or two**, not all of them. Skip the rest without guilt if your Definition of Done is complete.

**Blog links:** read [web.dev - Metadata](https://web.dev/learn/html/metadata/) for SEO and social previews, and [MDN - Webpage metadata](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Structuring_content/Webpage_metadata). Then check whether project and article detail pages have meaningful titles and descriptions.

**Reading:** study [Accessibility Overview](https://resources.devweekends.com/courses/angular-crash-course/20-accessibility), even if the examples use Angular. The accessibility ideas still apply.

**Assignment:** navigate the public site using only the keyboard. Write down the first three places where focus, labels, or button text feel unclear.

**Responsive exercise:** test the homepage, project detail, article detail, contact form, and admin dashboard at mobile, tablet, and desktop widths. Fix the first overflow before adding any new visuals.

**Accessibility exercise:** run through all forms and confirm every input has a visible label, not only placeholder text.

**Comparison:** responsive design vs accessibility: responsive design adapts to screen size. Accessibility makes the interface usable for people with different abilities, tools, and input methods.

**Big word alert:** **focus state** means the visible indicator showing which button, link, or input is currently selected by keyboard navigation.

Next: the app works locally. Ship it with the right environment boundaries. -> **[Chapter 18 - Deploy with Vercel and Supabase](18-deploy-vercel-supabase.md)**
