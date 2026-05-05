# Marfa Landing / CRM — Next Session Handoff

## Current state
The site and CRM were heavily reworked in this session.

Working now:
- landing page UI updated
- Tailwind 4 working
- hero image + floating QR working
- footer cleaned up
- blog/article styling fixed
- CRM dashboard at `/admin`
- site analytics visible
- bot analytics visible from `marfa.db`
- bot user table visible
- bot request technical metrics visible
- website support form exists
- website support tickets API works
- article generation by topic from CRM works
- article editing from CRM works

## Source paths that matter most
### Landing project
- `/home/clawd/.openclaw/workspace/marfa-landing`
- local working copy: `~/Desktop/marfa-landing`

### Bot project
- `/home/clawd/.openclaw/workspace/marfa-ai`
- bot DB: `/home/clawd/.openclaw/workspace/marfa-ai/data/marfa.db`

## Files to inspect first next session
- `docs/SITE_TECH_DOC.md`
- `app/admin/page.tsx`
- `lib/botStats.ts`
- `app/api/admin/generate-article/route.ts`
- `app/api/support/route.ts`
- `docker-compose.yml`

## Protected dashboard baseline (IMPORTANT)
- Current known-good CRM/dashboard build is frozen by `docs/DASHBOARD_BASELINE_2026-03-19.md`.
- `/admin` is a tabbed single-page dashboard (`Сайт`, `Telegram-бот`, `Тикеты`, `Контент`), not separate routes.
- Future sessions must NOT redesign tabs, replace live widget sources, or rewrite `app/admin/page.tsx` / live admin APIs without explicit user approval.
- Treat current live blocks (`BotSummaryLive`, `BotUsersLive`, `BotModelsWeekLive`, `RequestMetricsTable`, `SiteTicketsLive`) as protected production state.

## Important operational warning
A full `rsync --delete` from Desktop to VPS can overwrite live JSON data:
- `data/tickets.json`
- `data/analytics.json`
- `data/articles.json`

If preserving live server data matters, exclude or back up `data/` before sync.

## Most likely next tasks
1. ticket statuses in CRM (`new/read/closed`)
2. bot user filters + segmentation for broadcasts
3. deeper extraction of provider/cost from bot telemetry if available
4. manual article creation form in CRM
5. delete/archive article action
6. domain + HTTPS finalization

## Verified in this session
### Support ticket API
Confirmed by direct request to `/api/support`.

### Article generation API
Confirmed by direct request to `/api/admin/generate-article` with topic:
- `Как использовать AI-ботов в Telegram для отдела продаж`

### CRM uptime
- `/admin` returned HTTP 200
- containers were up after rebuild

## Reliable deploy flow
```bash
rsync -avz --delete --exclude 'node_modules' --exclude '.next' --exclude '.DS_Store' -e 'ssh -i ~/.ssh/id_ed25519' ~/Desktop/marfa-landing/ clawd@109.71.240.3:/home/clawd/.openclaw/workspace/marfa-landing/
ssh -i ~/.ssh/id_ed25519 clawd@109.71.240.3 'cd /home/clawd/.openclaw/workspace/marfa-landing && docker compose up -d --build'
```

## Sanity checks
```bash
ssh -i ~/.ssh/id_ed25519 clawd@109.71.240.3 'cd /home/clawd/.openclaw/workspace/marfa-landing && docker compose ps'
ssh -i ~/.ssh/id_ed25519 clawd@109.71.240.3 'cd /home/clawd/.openclaw/workspace/marfa-landing && docker compose logs --tail=50 marfa-site'
```
