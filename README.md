# YOLO Residences — yolozanzibar.com (static, Vercel)

Production-ready static build of the YOLO Residences Zanzibar site, exported from
the WordPress backup in this folder (`Website files/` + `Database/`).

## Layout

- `public/` — the static site (5 pages, all assets, themed 404, brochure PDFs under `/docs/`)
- `vercel.json` — trailing-slash URLs (matches WordPress permalinks), long-lived
  caching for `wp-content`/`wp-includes` assets, security headers, and redirects
  (`/home/` → `/`, `wp-admin`/`wp-login` → `/`)

## Deploy

```sh
npm i -g vercel   # if not installed
cd yolo-vercel
vercel            # preview deploy
vercel --prod     # production deploy
```

Then point the `yolozanzibar.com` domain at Vercel (Project → Settings → Domains).

## What still works on static hosting

- All lead-capture forms — they are external CRM widgets embedded from
  `app.flotonzanzibar.com`, unaffected by the move
- Google Maps (map data is inlined in the page), GTM / GA4 / Hotjar analytics,
  WhatsApp button, brochure PDF downloads

## What does not exist on static hosting

- wp-admin / content editing — edit content by re-running the WordPress site
  locally (Docker) and re-exporting, or keep WordPress on a host as the editor
- Gravity Forms server-side submission (not used on any live page — all visible
  forms are the external Floton widgets)

## Fixes applied during export

- Removed hard-coded staging URLs (`yolo.machetelab.co.za`) that made every page
  load a font + map pins from the agency's dev server — this bug exists on the
  live site today and made pages hang on the dead staging host
- Cleared stale WP Fastest Cache pages baked into the backup
- Rewrote all absolute URLs (including JSON-escaped and base64-encoded lazy-load
  variants used by Revolution Slider) to root-relative paths
- Removed dead WordPress endpoints (`wp-json`, `xmlrpc`, feeds, `?p=` shortlinks)
- Fixed the GA cross-domain linker to `yolozanzibar.com`
