# PACS

The app entry point is `PACS/index.html`. It loads `PACS/manifest.json` and `PACS/icon.svg`, and registers `PACS/sw.js` when served over HTTP or HTTPS.

GitHub Pages deployment is configured through `.github/workflows/pages.yml`. Push to `main`, then enable **Settings > Pages > GitHub Actions** in the repository settings.

## Supabase setup

The page is configured for the current Supabase project. For another project, override these globals before the page script loads:

```js
window.PACS_SUPABASE_URL = 'https://your-project.supabase.co';
window.PACS_SUPABASE_ANON_KEY = 'your-anon-key';
```

The page uses the Supabase JavaScript client and expects these tables:

- `captures`: `label`, `content`, `detail`, `created_at`
- `study`: `name`, `detail`, `status`, `created_at`
- `curriculum`: `name`, `detail`, `status`, `created_at`
- `papers`: `name`, `detail`, `status`, `created_at`
- `errors`: `name`, `detail`, `status`, `created_at`
- `research`: `name`, `detail`, `status`, `created_at`

Configure Supabase Row Level Security policies for the signed-in users or service role that should read and write this data. The page uses the public anon key and does not contain a service-role key.