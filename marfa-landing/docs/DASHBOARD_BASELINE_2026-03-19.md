# Marfa Dashboard Protected Baseline — 2026-03-19 (final tabbed live build)

Status: **CURRENT KNOWN-GOOD ADMIN/CRM BUILD**

This document freezes the currently working Marfa CRM dashboard state after the tabbed live-sync refactor on 2026-03-19.
Future sessions must treat this build as the protected baseline.

## Rule for future sessions
- Do **not** redesign, simplify, replace, or re-source the dashboard without explicit user approval.
- Do **not** switch telemetry/cost sources, data readers, or admin UX flows just because a new source exists.
- Do **not** overwrite `app/admin/page.tsx` or admin live widgets during experiments.
- If a change is requested, first back up the current files and preserve the exact working state.
- If a proposed change risks breaking CRM visibility, stop and ask.
- Prefer additive changes over structural rewrites.
- Preserve the current tab model inside `/admin` unless the user explicitly asks for separate routes.

## Protected files
- `app/admin/page.tsx`
- `app/admin/BotSummaryLive.tsx`
- `app/admin/BotUsersLive.tsx`
- `app/admin/BotModelsWeekLive.tsx`
- `app/admin/RequestMetricsTable.tsx`
- `app/admin/SiteTicketsLive.tsx`
- `app/admin/login/page.tsx`
- `app/api/admin/bot-analytics/route.ts`
- `app/api/admin/bot-users/route.ts`
- `app/api/admin/request-metrics/route.ts`
- `app/api/admin/site-tickets/route.ts`
- `app/api/admin/login/route.ts`
- `app/api/admin/tickets/route.ts`
- `app/api/admin/articles/route.ts`
- `app/api/admin/generate-article/route.ts`
- `lib/botStats.ts`
- `lib/store.ts`
- `middleware.ts`
- `docker-compose.yml`
- `next.config.mjs`
- `package.json`

## Protected checksums
- `9c972732162339e311a76ddc6b233d71322081321ff009b10a7e5608b9ddf4d1  app/admin/page.tsx`
- `00be8078dffddc4a93ebe8008e49f5590b7510d8ce81d205344b0f8b485f8737  app/admin/BotSummaryLive.tsx`
- `80e6a3302d385b60e0822a0c7d09770c0ba94725804b1eb529443fdbdb9702ec  app/admin/BotUsersLive.tsx`
- `cce098b84c6096879149358b150669b761724fd6a7b17b07c2b5061cba28bba0  app/admin/BotModelsWeekLive.tsx`
- `1313ea7816e9b322e71ddc6c0e68259be2637fd611074215b57d4695e0418035  app/admin/RequestMetricsTable.tsx`
- `00e5cfbae24805d1bc841449034aa0b4f56fa9ff24dfdc3f348268ee8e793a64  app/admin/SiteTicketsLive.tsx`
- `328dc9510b2a0b04ac80aa546c4be08ad1db42b315c79f99278ef689b8a02607  app/api/admin/bot-analytics/route.ts`
- `3db35dba1ac2903fb5e289ac35d96bce02148c745fd2f69bc97394083f740e7a  app/api/admin/bot-users/route.ts`
- `e20f49fb1ed2a32d1d7588a4ed3535c2eb1b37fae8f1cbd6b5829168853eb185  app/api/admin/request-metrics/route.ts`
- `4963c1bfeb9a41460f5912a6db3b2a4d0e5c7eb3f394b31134bd9f722bdfbde5  app/api/admin/site-tickets/route.ts`
- `9525aac6712aeb6084aa3169e81d0275d9b529eda4c199e18be855b7c93e14c7  app/api/admin/login/route.ts`
- `9f457eae64802eadbd60d9f3d3154e942f96fee53faee9b16b7db533e2700f49  app/api/admin/tickets/route.ts`
- `504f7faefee99c6c36df86de5d872855200a40330afae7d6f2590257a63b5ddc  app/api/admin/articles/route.ts`
- `645113b1ce1295d56ea69fb542679269001d2d3ed6ffa8e5236c979e10c66830  app/api/admin/generate-article/route.ts`
- `d5991a2c41b9ea3f85a2e5456096f3781204c833c9b0825849178e5b73402997  lib/botStats.ts`
- `a6bf2bf8d69ee0d2f8cc966dbfa3aa1c47f06944d1e5884776e2e5e8b3830887  lib/store.ts`
- `5edc97b2e55ecfc0d6b044e49172f0e3ae0331961a2c94eada9be8e09574433a  middleware.ts`
- `5112abd5f9f603306ac2ac741b7b76d2efc49efd45b5a1046900f23972a6e2dc  docker-compose.yml`
- `10f3416af7a0a92f59c4d283113624e9c286f645c6155e91c5a381d512feb9ee  next.config.mjs`
- `21a7d03729da577110745ebb848ed3289c4f35cae5d754327258ca4a6c70303b  package.json`

## Canonical dashboard behavior
Current `/admin` is a single page with client-side tabs:
- `Сайт`
- `Telegram-бот`
- `Тикеты`
- `Контент`

Active tab is stored in browser localStorage (`marfa-admin-tab`).

### Site tab
Static server-rendered cards from `readAnalytics()` + `readTickets()`:
- unique visitors
- unique bot clicks
- unique QR clicks
- new site tickets
- total pageviews
- total bot button clicks
- total QR clicks
- CTR to bot

### Telegram-bot tab
Live widgets + mixed protected sources:
- `BotSummaryLive`
- `BotModelsWeekLive`
- bot support tickets panel
- `BotUsersLive`
- `RequestMetricsTable`

### Tickets tab
- `SiteTicketsLive`
- source: `data/tickets.json`
- live refresh every 10s
- status transitions via `PATCH /api/admin/tickets`

### Content tab
- article CRUD / generation UI
- source: `data/articles.json`

## Canonical data-source mapping
### Bot summary block
Component: `app/admin/BotSummaryLive.tsx`
API: `GET /api/admin/bot-analytics`
Primary source: `/bot-data/bot-analytics-summary.json`

Displayed from summary JSON:
- users.total
- users.free
- users.paid
- users.active_weekly
- payments.day/week/all
- packs.images
- packs.videos
- updated_at

Additional displayed costs:
- cost day / week / all
Source: `request_metrics.costs` from summary, with fallback reconstruction from `/bot-data/request-metrics.jsonl`

### Bot users block
Component: `app/admin/BotUsersLive.tsx`
API: `GET /api/admin/bot-users`
Source: `readBotUsers(250)` from `lib/botStats.ts`
Refresh: every 10s
Shows:
- user_id
- username / first_name / last_name
- premium tier
- active/inactive
- current_model
- requests_week
- last_seen

### Bot models 7d block
Component: `app/admin/BotModelsWeekLive.tsx`
API: `GET /api/admin/bot-analytics`
Source: top models reconstructed from request metrics (`request-metrics.jsonl`), not from legacy `marfa.db` request_started slice.
Fields:
- model
- requests
- users
Refresh: every 10s

### Tech metrics block
Component: `app/admin/RequestMetricsTable.tsx`
API: `GET /api/admin/request-metrics`
Source: `/bot-data/request-metrics.jsonl`
Refresh: every 10s
Behavior:
- append-only JSONL reader
- sorted by `ts DESC`
- pagination 100/page
- filters by `kind`, `model`, `user_id`
- final rows only in main table (`result_type != started`)
- - provider fallback: `goapi` for image/video when blank

### Site tickets block
Component: `app/admin/SiteTicketsLive.tsx`
API: `GET /api/admin/site-tickets`
Source: `data/tickets.json`
Refresh: every 10s

## Admin API policy
Protected by `middleware.ts`:
- `/admin/:path*`
- `/api/admin/:path*`
Exceptions:
- `/admin/login`
- `/api/admin/login`

Dynamic/no-store routes that must stay uncached:
- `/api/admin/bot-analytics`
- `/api/admin/bot-users`
- `/api/admin/request-metrics`
- `/api/admin/site-tickets`

## Dependency / linkage notes
- `BotSummaryLive`, `BotModelsWeekLive` depend on `/api/admin/bot-analytics`
- `BotUsersLive` depends on `/api/admin/bot-users`
- `RequestMetricsTable` depends on `/api/admin/request-metrics`
- `SiteTicketsLive` depends on `/api/admin/site-tickets`
- `SiteTicketsLive` also updates statuses through `/api/admin/tickets`
- live widgets assume admin login cookie `marfa_admin=1`
- do not remove `no-store` / `force-dynamic` from live admin APIs or the dashboard will silently freeze

## Deployment policy
When touching admin files in future sessions:
1. make backups first
2. compare against these checksums after editing
3. rebuild only after confirming scope
4. if the user says “don’t break dashboard”, treat that as a hard constraint
5. after any live-widget change, verify the corresponding admin API returns fresh non-cached data
