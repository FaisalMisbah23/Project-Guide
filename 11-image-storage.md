# Chapter 11 - Image storage

Projects and articles need images, but images are not normal row data. A screenshot can be large; a database row should store facts and references, not a pile of bytes.

## The point of this chapter

Supabase Storage bucket, owner-only upload policies, database image paths, public rendering, and meaningful alt text.

## Before you touch code

- Supabase project has storage available.
- Owner auth works.
- Project/article forms have image fields planned.
- You know whether portfolio images should be public read.

## Vocabulary for this chapter

- **Bucket.** A named storage container.
- **Object path.** The file key inside a bucket.
- **Public URL.** A browser-accessible link to a stored object.
- **Alt text.** Text equivalent for meaningful images.
- **Storage policy.** Permission rule for files, separate from table RLS.

## Guided snippet or contract

This is a shape to aim for, not a finished solution to paste blindly:

```txt
Image storage contract
  upload: owner only
  read: public for portfolio images
  database: stores image_path and image_alt
  replace: uploads new object and updates row
  archive: keeps object unless deliberately cleaned
```

## Step 1 - Separate file bytes from row metadata

Store the file in object storage. Store the path, alt text, and related metadata in the database. That split keeps rows light and files manageable.

## Step 2 - Decide public read, owner write

Portfolio images are usually public to read. Upload, replace, and delete should be owner-only. Storage policies are separate from table RLS, so configure both.

## Step 3 - Connect uploads to admin forms

The admin form uploads an image, receives or stores the path, and saves that path on the project or article record. Public pages render from the saved path.

## Step 4 - Treat alt text as content

A meaningful screenshot needs meaningful alt text. Decorative images can be empty, but portfolio evidence is rarely decorative.

## Step 5 - Write the storage contract

Your database should not store image bytes. It should store a reference:

```txt
image_path: projects/my-project/cover.webp
image_alt: Screenshot of the dashboard showing project cards
```

The storage bucket holds the file. The database row explains which file belongs to which project or article.

## Step 6 - Plan ownership and cleanup

Images create lifecycle questions:

```txt
upload new image -> save path on row
replace image -> upload new file, update path, decide what happens to old file
archive project -> keep image for history
hard delete draft -> optionally delete unused image
```

You do not need perfect cleanup on day one, but you need to know the tradeoff.

## Step 7 - Do it on your project

Create:

```txt
Supabase storage bucket for portfolio images
owner-only upload/update/delete policy
public read policy if images are public
image fields in project/article forms
helper to build public image URLs from paths
```

## Prove it before moving on

Try three actions:

```txt
signed-in owner uploads image -> succeeds
signed-out visitor views public image -> succeeds
signed-out visitor uploads image -> fails
```

If the third action succeeds, stop and fix storage policies.

## If it breaks

| Symptom | Likely cause | Smallest next test |
|---|---|---|
| Upload fails for owner | Storage policy or bucket name mismatch | Try a tiny file and inspect storage error. |
| Signed-out upload succeeds | Policy is too open | Fix storage write policy before continuing. |
| Image URL works locally not deployed | Bucket public/read settings differ | Generate URL from path in production project. |
| Screen reader gets useless image info | Alt text is missing or generic | Rewrite alt text to describe evidence in the image. |

## What you should be able to explain

- Why image bytes do not belong in normal rows.
- Why storage policies are separate from RLS.
- Why alt text is part of content quality.

## The slower beginner path

If this chapter feels too large, split the image storage feature into one sitting per checkpoint. The goal is not to finish fast; the goal is to finish with proof.

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

> **📖 Mandatory read.** Read [Supabase Storage](https://supabase.com/docs/guides/storage), [Supabase Storage access control](https://supabase.com/docs/guides/storage/security/access-control), and [MDN accessibility](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Accessibility). Required: storage has its own access rules and images need accessible descriptions.

> **💡 Hint.** Signed-out users should be able to view public images but fail to upload one. Test both cases.

## Definition of Done

- [ ] Storage bucket exists.
- [ ] Owner can upload project/article images.
- [ ] Signed-out users cannot upload or replace images.
- [ ] Database rows store image paths and alt text, not image bytes.
- [ ] Public pages render stored images.
- [ ] Meaningful images have useful alt text.

> **✍️ Log it (mandatory).** In `learning-log/11-image-storage.md`: explain why files belong in object storage and paths belong in database rows.

All boxes ticked? Then continue. The next chapter builds on this gate, not around it.

---

Next: images are handled; now build a contact flow that does not lose messages. -> **[Chapter 12 - Contact Edge Function and Brevo](12-contact-edge-function-brevo.md)**
