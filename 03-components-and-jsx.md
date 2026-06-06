# Chapter 3 - Components and JSX

Your app exists. Now it needs a shape. React's first real idea is that a screen is not one giant file; it is a set of small UI pieces that can be named, reused, and understood.

This chapter turns the blank Vite app into a portfolio shell: layout, navigation, footer, buttons, and section titles. Nothing fancy yet. The goal is to learn how JSX and components work before you build the home page.

## Where we're headed

By the end, your app has a reusable layout and the first shared components in `src/components/`. The browser should show a simple portfolio frame: navigation at the top, a main content area, and a footer.

## Step 1 - Understand JSX

JSX is JavaScript syntax that describes UI. It looks like HTML, but it is not exactly HTML. It lives inside JavaScript, can use variables, and must follow JavaScript rules.

The tempting mistake is to treat JSX as pasted HTML. That quickly causes confusion: `class` becomes `className`, inline styles become objects, and every component must return one parent value. The better approach is to remember this sentence:

```txt
JSX is UI written as JavaScript expressions.
```

That is why this is valid as a data shape:

```txt
name: "Your Name"
role: "Software Engineer"
primaryAction: "View Projects"
```

And your JSX can use those values instead of repeating text everywhere.

## Step 2 - Create your layout components

Create these files:

```txt
src/components/
  Navbar.jsx
  Footer.jsx
  Button.jsx
  SectionTitle.jsx
```

Each component should have one clear job:

- `Navbar` shows the portfolio name and main navigation links.
- `Footer` shows a short copyright line and useful links.
- `Button` gives repeated action links one consistent style.
- `SectionTitle` gives major sections a consistent heading pattern.

Do not build page-specific content inside shared components. A `Button` should not know about the projects page. A `Navbar` should not contain the whole home page. Keep components focused.

This is the daily guideline "one component = one responsibility" in React form. If a component is hard to name, it probably has too many jobs or no clear job yet.

## Step 3 - Wire the shell into `App.jsx`

Use `App.jsx` as the temporary app shell:

```txt
App
  Navbar
  main
    placeholder content
  Footer
```

This is not the final routing setup. React Router arrives in Chapter 7. For now, `App.jsx` should prove that components can be imported, rendered, and composed.

## Step 4 - Add basic global styles

Set a calm base in your CSS:

- readable body font;
- sensible line height;
- no default body margin;
- consistent link styling;
- max-width container utility if you want one;
- spacing for `main`;
- simple button styles.

Do not start polishing every pixel. The home page will give the design real content in Chapter 4. This chapter only needs enough styling to make the shell readable.

## Step 5 - Use props in small places

Props are values passed into a component. They let a component stay reusable instead of hard-coded.

For example, your `Button` should be able to represent different actions:

```txt
Button receives:
  label
  href
  variant
```

Your `SectionTitle` might receive:

```txt
SectionTitle receives:
  eyebrow
  title
  description
```

Do not overdo it. If a component is only used once and has no repeated pattern yet, it may not need props. Props are for real variation.

Avoid over-abstraction here. Not every repeated line deserves a new component. Create an abstraction when it improves clarity, removes meaningful duplication, or gives a repeated UI pattern one clear home.

> **Mandatory read.** Read the DevWeekends React crash course chapters on JSX and components/props: https://resources.devweekends.com/courses/react-crash-course/01-intro-jsx and https://resources.devweekends.com/courses/react-crash-course/02-components-props.

> **Interesting to read.** Read the "Keep components focused and reusable" notes in `react_learning_package.md`. Keep the extra reading light here; the project matters more than collecting theory.

> **Hint - naming components.** Name components after what they are in the product, not after CSS tricks. `ProjectCard` is clearer than `BoxWithShadow`; `SectionTitle` is clearer than `BigText`.

## Definition of Done

- [ ] `src/components/Navbar.jsx` exists and renders the portfolio name plus navigation labels.
- [ ] `src/components/Footer.jsx` exists and renders footer content.
- [ ] `src/components/Button.jsx` exists and can be reused for different actions.
- [ ] `src/components/SectionTitle.jsx` exists and can be reused for different sections.
- [ ] `App.jsx` imports and renders these components.
- [ ] The browser shows a portfolio shell, not a blank page.
- [ ] Basic CSS makes the shell readable on desktop and mobile.
- [ ] Component names describe product/UI roles clearly.
- [ ] No component is doing several unrelated jobs.
- [ ] You made a commit for this chapter.

> **Log it.** In `learning-log/03-components-and-jsx.md`: (1) What is JSX? (2) How is a component different from a normal JavaScript function? (3) What are props? (4) Which components did you create, and why does each deserve to exist?

---

Next: build the first real page. -> **[Chapter 4 - The home page](04-home-page.md)**
