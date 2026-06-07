# Chapter 13 - Image uploads with Supabase Storage

Projects and articles often need images. Images do not belong as giant database fields; they belong in object storage.

> **Principle.** Store files as files, and store references in the database.

## Where we're headed

By the end, the owner can upload cover images to Supabase Storage and save image paths on projects or articles.

## Before you build

> **Mandatory read.** Read Supabase Storage docs: https://supabase.com/docs/guides/storage. Focus on buckets, paths, public URLs, and access control.

> **Apply this habit.** Read "Think About Real Users" in [Daily_Software_Development_Guidelines.md](../Daily_Software_Development_Guidelines.md), then decide what image size and alt text a visitor needs.

## Step 1 - Create buckets

Create buckets:

```txt
project-images
article-images
```

Choose public or private deliberately. For a portfolio, public cover images are acceptable if they contain no private data.

## Step 2 - Add storage policies

Public visitors can read public cover images. Only the owner can upload, update, or delete.

## Step 3 - Build upload control

Add upload controls to project and article forms.

Show:

- selected file name;
- upload loading;
- upload error;
- preview after upload.

## Step 4 - Save image path

Save the storage path in:

```txt
projects.cover_image_path
articles.cover_image_path
```

Do not store large base64 strings in the database.

## Step 5 - Render images publicly

Public pages should render images with useful `alt` text.

## What your screen should show

Admin can upload an image. Public project/article pages show it.

## Small challenge

Add a default fallback visual when an item has no cover image.

Suggested commit:

```bash
git commit -m "feat: add supabase image uploads"
```

## Definition of Done

- [ ] Storage buckets exist.
- [ ] Storage policies are deliberate.
- [ ] Owner can upload images.
- [ ] Public pages render uploaded images.
- [ ] Image paths are stored in database rows.
- [ ] Images have useful alt text.

> **Log it.** In `learning-log/13-image-uploads-with-supabase-storage.md`: Why store paths instead of image blobs in Postgres?

Next: make contact real. -> **[Chapter 14 - Contact Edge Function with Brevo](14-contact-edge-function-brevo.md)**
