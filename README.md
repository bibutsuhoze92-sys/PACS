# PACS

The app entry point is `PACS/index.html`. It loads `PACS/manifest.json` and `PACS/icon.svg`, and registers `PACS/sw.js` when served over HTTP or HTTPS.

GitHub Pages deployment is configured through `.github/workflows/pages.yml`. Push to `main`, then enable **Settings > Pages > GitHub Actions** in the repository settings.

## Supabase setup

The page is configured for the current Supabase project. For another project, override these globals before the page script loads:

```js
window.PACS_SUPABASE_URL = 'https://your-project.supabase.co';
window.PACS_SUPABASE_ANON_KEY = 'your-anon-key';
```

The page uses the Supabase JavaScript client and expects these core tables:

- `captures`: `label`, `detail`, `created_at`
- `study_sessions`: `title`, `topic`, `goal`, `duration_minutes`, `status`, `created_at`
- `countdowns`: `title`, `event_type`, `target_at`, `notes`, `created_at`
- `curriculum_topics`: `name`, `unit`, `subtopic`, `status`, `confidence`, `created_at`
- `past_papers`: `title`, `subject_id`, `year`, `examination`, `duration_minutes`, `total_marks`, `created_at`
- `error_bank`: `mistake`, `topic`, `cause`, `correct_method`, `severity`, `status`, `created_at`
- `research_resources`: `title`, `author`, `source`, `url`, `topic`, `type`, `created_at`

The app also reads optional helper tables for analytics and profile features: `assessments`, `paper_attempts`, `profiles`, and `activity_log`.

Older single-word table names such as `study`, `curriculum`, `papers`, `errors`, and `research` are still accepted as legacy fallbacks when a project was created with the earlier schema. Configure Supabase Row Level Security policies for the signed-in users or service role that should read and write this data. The page uses the public anon key and does not contain a service-role key.