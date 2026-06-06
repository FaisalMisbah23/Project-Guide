# Chapter 11 - Responsive polish and accessibility

The portfolio now has the main features. This chapter makes it feel finished.

Polish is not decoration. It is the work that lets visitors use the site without friction: mobile layout, readable text, good spacing, keyboard-friendly navigation, clear focus states, color contrast, and content that says something specific.

Your target is not perfection, but you should be aiming for Lighthouse scores around **90+** in Performance, Accessibility, SEO, and Best Practices before sharing the site seriously.

## Where we're headed

By the end, the site works cleanly on mobile and desktop, navigation is usable, forms are accessible, project content is sharper, and the UI feels consistent.

## Before you build

> **Mandatory read.** Read the relevant HTML, accessibility, performance, and image-optimization sections in the DevWeekends frontend interview guide: https://resources.devweekends.com/resources/frontend-interview-qs. Then check whether your portfolio images are too large.

> **Daily guideline.** Read "Avoid Premature Optimization" in `Daily_Software_Development_Guidelines.md`.

> **Hint - visual consistency.** If every section uses different spacing, button styles, and card styles, the site feels assembled from scraps. Reuse patterns deliberately.

Before editing CSS, write the three biggest issues you are trying to improve: mobile layout, accessibility, performance, content clarity, or SEO metadata. Polish should respond to evidence.

## Step 1 - Audit the site on mobile

Check every route on a narrow screen:

```txt
/
/about
/skills
/projects
/projects/:id
/notes
/github
/contact
```

Look for:

- horizontal scrolling;
- buttons that overflow;
- cramped cards;
- unreadably small text;
- navigation that wraps badly;
- form fields that are hard to tap.

Fix the layout problems before visual decoration.

## Step 2 - Improve navigation

If the navigation has too many links for mobile, add a simple mobile menu state.

The menu should:

- open and close;
- close after choosing a link;
- be reachable by keyboard;
- not cover content in a confusing way.

Do not add complex animation here. The goal is usable navigation.

## Step 3 - Check accessibility basics

Accessibility means people with different devices and abilities can use the site. For this project, check:

- every image has useful `alt` text or is marked decorative;
- form inputs have labels;
- buttons have clear text;
- links describe where they go;
- keyboard tab order is sensible;
- focus styles are visible;
- color contrast is readable.

These are not bonus points. They are part of web quality.

## Step 4 - Refine the content

Read every project card and detail page. Replace vague text with specific text.

Weak:

```txt
Made a website using React.
```

Stronger:

```txt
Built a responsive React portfolio with reusable components,
project filtering, dynamic routes, form validation, and deployment.
```

Do the same for the about page and learning notes. The site should sound like a person who understands their work.

## Step 5 - Check performance basics

Keep it simple:

- remove unused assets;
- compress large images;
- prefer WebP or AVIF when practical;
- lazy-load non-critical images;
- limit font families and heavy third-party scripts;
- avoid huge libraries for tiny effects;
- run `npm run build`;
- use the browser dev tools or Lighthouse if available.

Do not chase advanced optimization. Make it work, make it correct, measure, then improve.

This is where "measure before refactoring" matters. If a page feels slow, gather evidence first: image size, bundle size, Lighthouse output, or a visible network delay. Do not add complex optimization patterns because they sound senior.

## Step 6 - Check SEO and sharing basics

Even a simple portfolio should have enough metadata to look intentional when shared.

Check:

- page title;
- meta description;
- Open Graph title, description, and image if you add social sharing polish;
- resume link, if provided;
- no obvious spelling or grammar mistakes;
- no console errors.

If you are using plain Vite without a metadata library, start with the basics in `index.html`. You do not need a complex SEO setup for this project, but you should not ship with default Vite metadata.

## Definition of Done

- [ ] Every route works on mobile and desktop.
- [ ] No page has accidental horizontal scrolling.
- [ ] Navigation is usable on mobile.
- [ ] Form fields have labels.
- [ ] Focus states are visible.
- [ ] Images have appropriate alt text.
- [ ] Project descriptions are specific.
- [ ] Large unused assets are removed or replaced.
- [ ] The default Vite title/metadata has been replaced with portfolio-specific text.
- [ ] Lighthouse or an equivalent manual review has been run, with an aim of 90+ in key categories.
- [ ] Any optimization you made is tied to a visible problem or measurement.
- [ ] `npm run build` passes.
- [ ] You made a commit for this chapter.

> **Log it.** In `learning-log/11-responsive-polish-and-accessibility.md`: (1) What mobile issues did you find and fix? (2) What accessibility checks did you perform? (3) What content did you rewrite to be more specific? (4) What did you choose not to optimize yet, and why?

---

Next: ship it. -> **[Chapter 12 - Deploy and final review](12-deploy-and-final-review.md)**
