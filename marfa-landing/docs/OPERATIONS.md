# marfa-landing operations

## CRM
- Admin URL: `/admin`
- Login/password from env: `ADMIN_LOGIN`, `ADMIN_PASSWORD`
- Metrics tracked:
  - unique visitors
  - page views
  - bot click
  - QR click

## Auto articles (RU)
Endpoint:
`POST /api/cron/publish`
Header:
`x-cron-secret: $CRON_SECRET`

Recommended schedule (2-3/week):
- Tue 09:00
- Thu 09:00
- Sat 09:00

Example cron on VPS:
```bash
0 9 * * 2,4,6 curl -X POST https://YOUR_DOMAIN/api/cron/publish -H "x-cron-secret: YOUR_SECRET"
```

## Current admin UX notes (2026-03-18)
- `/admin` is one dynamic page with client-side tabs: Site / Telegram bot / Tickets / Content
- Telegram bot metrics are read from mounted bot DB path `/bot-data/marfa.db`
- request cost in CRM is expected to come from bot event JSON metadata (`generation_result.meta_json`) rather than from a separate site-side pricing table
- when changing admin UI, verify live HTML after login (`/api/admin/login` + `/admin`) because browser/server cache confusion caused false negatives during iteration

## Protected admin/dashboard baseline
- Current `/admin` implementation is the protected known-good build.
- The dashboard is tabbed inside a single route and uses multiple live widgets backed by protected admin APIs.
- Before changing dashboard code, back up `app/admin/page.tsx` and all live widget/admin API files.
- Do not migrate metrics/cost sources, simplify admin UX, or remove dynamic/no-store behavior without explicit user approval.
- Reference: `docs/DASHBOARD_BASELINE_2026-03-19.md`.
