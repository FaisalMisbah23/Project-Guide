# Chapter 11 - Image storage

Projects and articles need images, but images are not normal row data. A screenshot can be large; a database row should store facts and references, not a pile of bytes.

## The point of this chapter

Supabase Storage bucket, owner-only upload policies, database image paths, public rendering, and meaningful alt text.

## Step 1 - Separate file bytes from row metadata

Store the file in object storage. Store the path, alt text, and related metadata in the database. That split keeps rows light and files manageable.

## Step 2 - Decide public read, owner write

Portfolio images are usually public to read. Upload, replace, and delete should be owner-only. Storage policies are separate from table RLS, so configure both.

## Step 3 - Connect uploads to admin forms

The admin form uploads an image, receives or stores the path, and saves that path on the project or article record. Public pages render from the saved path.

## Step 4 - Treat alt text as content

A meaningful screenshot needs meaningful alt text. Decorative images can be empty, but portfolio evidence is rarely decorative.

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
