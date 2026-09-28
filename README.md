# Pratika Creation — Netlify-ready website

## Current setup
- Static luxury jewellery showcase.
- 25 jewellery images + 2 videos bundled in `assets/`.
- No prices are shown.
- Enquire buttons open WhatsApp: +91 73857 15603.
- Instagram: @pratika_creation_
- Email: pratikacreation24@gmail.com
- Add/Edit/Delete products and Add Category UI are included.
- Existing bundled media is visible to every website visitor after deployment.
- **Important:** admin changes made in the current version are stored in the current browser's localStorage only. They do not sync to other devices yet.

## Deploy on Netlify
1. Extract this ZIP.
2. Open Netlify and create a new site from the `pratika_site` folder (drag-and-drop deploy also works for a static site).
3. The publish directory is the folder containing `index.html`.
4. No build command is required.

## Future Supabase migration
The HTML contains an `APP_CONFIG` section and a `StorageAdapter` boundary.
Current value:
`storageMode: 'local'`

Later, switch to a Supabase-backed adapter and connect:
- Supabase Database: products + categories
- Supabase Storage bucket: `product-media`
- Supabase Auth: admin login
- RLS: public read for published catalogue; admin-only writes

Use only the Supabase **publishable key** in browser code. Never expose a Supabase secret/service-role key in frontend code.

Recommended product fields:
- id
- name
- category
- kind (`image` / `video`)
- media URL
- poster URL (video)
- storage_path
- description
- featured
- created_at / updated_at

This architecture intentionally keeps storage replaceable, so Supabase Storage can later be replaced by another S3-compatible paid provider without redesigning the public website.
