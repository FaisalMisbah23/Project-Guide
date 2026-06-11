# Chapter 11 - Image Storage

Images should not be stuffed into database rows. The database should store image paths and metadata. Supabase Storage should store the files.

## Goal

By the end, the owner can upload images, store paths in records, and provide useful alt text.

## What You Will Build

- Storage bucket.
- Storage policies.
- Image upload helper.
- Admin image upload UI.
- Image path and alt text fields on content.

## Beginner Concepts

- **Storage bucket:** a container for files.
- **Path:** the file location inside the bucket.
- **Public URL:** a URL visitors can use to view a public file.
- **Alt text:** text that describes an image for accessibility.
- **Metadata:** information about a file, not the file itself.

## Step By Step

### Step 1 - Choose What Images Need Storage

Start with:

```txt
project cover images
article cover images
profile/about image, optional
```

### Step 2 - Create A Bucket

Create a Supabase Storage bucket such as:

```txt
portfolio-images
```

Decide whether images are public. For portfolio project covers, public is usually fine. Upload permission should still be owner-only.

### Step 3 - Add Storage Policies

Policies should allow:

```txt
public read for public images
owner upload
owner update
owner delete, if needed
```

Signed-out visitors should not upload files.

### Step 4 - Store Paths In Tables

Add or use fields such as:

```txt
image_path
image_alt
```

Do this for projects and articles. The database stores where the file is and how to describe it.

### Step 5 - Create Upload Helper

Create:

```txt
src/features/images/
  imageStorageApi.ts
  ImageUploader.tsx
```

The helper should upload a file, return the path, and let the form save that path.

### Step 6 - Add Upload UI To Admin Forms

In project and article forms, add:

```txt
file input
upload button
alt text input
preview of uploaded image
```

Keep the first version simple. The important behavior is owner-only upload plus saved path.

### Step 7 - Test Bad Uploads

Try:

```txt
signed-out upload
file too large
wrong file type
missing alt text
broken image path
```

## Common Mistakes

| Mistake | Why it hurts | Fix |
|---|---|---|
| Saving image bytes in table columns | Database gets heavy and awkward | Store files in Storage |
| No alt text | Accessibility suffers | Require useful alt text |
| Public upload policy | Anyone can upload junk | Owner-only writes |
| Saving URL but not path | Harder to move buckets later | Store path and generate URL when needed |

## Checks Before Moving On

- Bucket exists.
- Public images can be read.
- Signed-out visitors cannot upload.
- Owner can upload.
- Project/article records store image path and alt text.
- UI handles failed upload.

## Learning Log

In `learning-log/11-image-storage.md`, answer:

```txt
Why do files belong in Storage instead of database rows?
What does the database store about an image?
Who can upload?
Why does alt text matter?
```

## Definition Of Done

- [ ] Storage bucket exists.
- [ ] Storage policies are correct.
- [ ] Owner can upload an image.
- [ ] Signed-out upload is blocked.
- [ ] Image path and alt text are saved.
- [ ] Public pages can display saved images.

Next: build the contact backend. -> **[Chapter 12 - Contact Edge Function And Brevo](12-contact-edge-function-brevo.md)**
