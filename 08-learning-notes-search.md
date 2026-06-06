# Chapter 8 - Learning notes search

A strong portfolio does not only show finished projects. It can also show how you think and learn. This chapter adds a small learning notes page: articles, notes, or write-ups rendered from data, with search or tag filtering.

This is also another controlled use of state. The visitor changes a search value or tag, and the UI updates.

## Where we're headed

By the end, your portfolio has a learning notes page with notes rendered from data, searchable by title or filterable by tag, plus an empty state.

## Before you build

> **Mandatory read.** From `Software_Engineering_Community_Affirmations.md`, keep this as the chapter motto: "Learn, build, share, repeat." Then write one real note title you would be willing to publish.

> **Optional blog.** If you want a broader frontend review, skim the DevWeekends frontend interview guide and pick one beginner-friendly section that connects to your note: https://resources.devweekends.com/resources/frontend-interview-qs

> **Hint - derived data.** The filtered list should be calculated from `notes` and the current search/tag. Do not store both the original list and filtered list in state unless you can explain why.

Before creating `notes.js`, write three possible learning-note titles from this project. Choose titles that say what you learned, not just what topic you touched.

## Step 1 - Create the notes page and data

Create:

```txt
src/pages/
  LearningNotes.jsx

src/data/
  notes.js
```

Each note should have:

```txt
id
title
summary
tags
date
link or slug
```

These can be real external links, short local summaries, or placeholders for notes you plan to write. Be honest about what exists.

## Step 2 - Create note components

Create:

```txt
src/components/
  NoteCard.jsx
  SearchBar.jsx
  TagFilter.jsx
```

If your design combines search and tags differently, that is fine. The page still needs clear, reusable pieces.

## Step 3 - Add search state

Use state to store the current search text. Filter notes by title, summary, or tags.

The flow:

```txt
Visitor types
  -> search state changes
  -> filtered notes are recalculated
  -> note list re-renders
```

Do not mutate the original notes array. Filtering should produce a derived list.

## Step 4 - Add tags

Tags help visitors scan your learning areas:

```txt
React
JavaScript
CSS
Git
Accessibility
Deployment
```

You may implement tag filtering instead of search, or both if the page stays simple. If no notes match, show an empty state.

## Step 5 - Make notes useful

A learning note should say something. Avoid titles like "React Notes." Prefer titles like:

```txt
What I learned about props while building reusable project cards
How I debugged my first React Router not-found page
Why I stopped hard-coding repeated project markup
```

Specific notes make the portfolio feel lived-in.

## Definition of Done

- [ ] `src/pages/LearningNotes.jsx` exists.
- [ ] `src/data/notes.js` exists.
- [ ] Notes render from data.
- [ ] Search or tag filtering works.
- [ ] Empty results show a clear message.
- [ ] Note cards have useful titles and summaries.
- [ ] The notes page is linked in the route map and navigation.
- [ ] You made a commit for this chapter.

> **Log it.** In `learning-log/08-learning-notes-search.md`: (1) Why include learning notes in a portfolio? (2) What state did you use for search or filtering? (3) What is derived data? (4) What is one note you could write from this project?

---

Next: build the contact form. -> **[Chapter 9 - The contact form](09-contact-form.md)**
