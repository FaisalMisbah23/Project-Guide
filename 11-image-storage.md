# Chapter 11 - Image storage

Projects and articles need images. The tempting path is to paste image URLs or store files as database blobs. The production-shaped path is object storage: the database stores metadata and paths; storage holds the file.

## Where we're headed

By the end, project and article images upload to Supabase Storage, paths are saved in database rows, alt text is stored, and public pages render images with fallbacks.

## Why files do not belong in rows

Bad:

```txt
projects.image_base64 = giant encoded file
```

Problem: rows become huge, queries get heavier, backups bloat, and the database starts doing file storage work badly.

Better:

```txt
Supabase Storage bucket stores the file
projects.image_path stores the path
projects.image_alt stores the human description
```

## Public or private?

Portfolio project/article images are meant to be public. A public bucket is reasonable if only the owner can upload and paths are safe. Private files, such as invoices or personal documents, would need signed URLs. Do not use private complexity where public content is intended.

## Build it

Create buckets for project images and article images, or one organized public content bucket with prefixes:

```txt
projects/<project-id>/<filename>
articles/<article-id>/<filename>
```

Add storage policies so only the authenticated owner can upload/update/delete. Public users can read public images.

Add upload controls in project and article admin forms. Show selected filename, loading state, upload error, preview, and saved path. Store alt text with the content record.

## Real developer mistake

Mistake: save the image URL but no alt text.

Why it is bad: accessibility suffers, and broken images have no meaningful fallback.

Fix: require useful alt text for meaningful images.

## Definition of Done

- [ ] Supabase Storage bucket exists.
- [ ] Owner can upload project images.
- [ ] Owner can upload article images.
- [ ] Public pages render images from saved paths.
- [ ] Upload loading and error states exist.
- [ ] Alt text is stored and rendered.
- [ ] Signed-out users cannot upload.

> **Log it.** In `learning-log/11-image-storage.md`, explain why storage paths belong in the database but file bytes do not.

Next: visitors need to contact the owner. Email alone is not enough; store first, then notify. -> **[Chapter 12 - Contact Edge Function and Brevo](12-contact-edge-function-brevo.md)**
