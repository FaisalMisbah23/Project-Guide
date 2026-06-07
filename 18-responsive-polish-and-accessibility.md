# Chapter 18 - Responsive polish and accessibility

The app works. Now it has to feel usable for visitors and for the owner managing content.

> **Principle.** Polish is respect for the person trying to use what you built.

## Where we're headed

By the end, public and admin screens work on mobile, keyboard navigation is sensible, forms have labels, contrast is readable, and content is specific.

## Before you build

> **Mandatory read.** Read relevant sections in the DevWeekends frontend interview guide: https://resources.devweekends.com/resources/frontend-interview-qs. Focus on accessibility, performance, HTML, and images.

> **Apply this habit.** Read "Avoid Premature Optimization" in [Daily_Software_Development_Guidelines.md](../Daily_Software_Development_Guidelines.md), then choose fixes based on real issues you found.

## Step 1 - Audit public pages

Check:

```txt
/
/about
/projects
/projects/:slug
/articles
/articles/:slug
/contact
```

Look for overflow, unclear links, weak contrast, and vague content.

## Step 2 - Audit admin pages

Admin screens should be usable, not fancy. Check table overflow, form labels, save states, and destructive actions.

## Step 3 - Check accessibility basics

Confirm:

- labels for inputs;
- visible focus states;
- useful alt text;
- semantic headings;
- clear button text;
- keyboard access.

## Step 4 - Check images

Uploaded images should not destroy performance. Use reasonable dimensions and compression.

## Step 5 - Replace default metadata

Update browser title and description. Do not ship default Vite metadata.

## What your screen should show

The app feels intentional on mobile and desktop. Admin tools are plain but usable.

## Small challenge

Open the deployed-looking app on your phone and fix the smallest thing that makes it feel more trustworthy.

Suggested commit:

```bash
git commit -m "style: polish responsive full-stack portfolio"
```

## Definition of Done

- [ ] Public pages work on mobile.
- [ ] Admin pages work on mobile or have acceptable responsive behavior.
- [ ] Forms have labels.
- [ ] Focus states are visible.
- [ ] Images have alt text.
- [ ] Default metadata is replaced.
- [ ] Content is specific and recruiter-readable.

> **Log it.** In `learning-log/18-responsive-polish-and-accessibility.md`: What issue did you find only after using the app like a real visitor?

Next: deploy the app. -> **[Chapter 19 - Deploy to Vercel and Supabase](19-deploy-vercel-and-supabase.md)**
