# Marfa Landing — Technical Documentation

Last updated: 2026-03-18 (America/Los_Angeles)

## 1) Purpose
Marfa Landing is the public promo site for Marfa AI.

It currently includes:
- marketing landing page
- model catalog section
- Telegram CTA flow
- QR-based launch entry
- blog index and article pages
- CRM dashboard
- lightweight site analytics
- Telegram bot analytics from bot database
- support ticket intake form on the website
- article generation + article editing inside CRM

Primary URL:
- `http://109.71.240.3/`

Primary CTA target:
- `https://t.me/SuperMarfaAiBot`

Support contact:
- `https://t.me/FangedTwin`

Other product linked from footer:
- `https://content-pilot.io`

Stack:
- Next.js 14 App Router
- React 18
- Tailwind CSS 4
- Docker Compose
- Nginx reverse proxy
- Node `sqlite` reader for bot DB integration

---

## 2) Runtime architecture

### Services
- `marfa-site` — Next.js application, internal port `3000`
- `marfa-site-nginx` — reverse proxy, public port `80`

### Important files
- Compose: `docker-compose.yml`
- Docker image build: `Dockerfile`
- Nginx config: `nginx/default.conf`

### Persistent storage
Mounted volume:
- `./data:/app/data`

Stored inside `data/`:
- `articles.json`
- `analytics.json`
- `tickets.json`

### Bot DB mount
The website container mounts the Marfa bot database directory read-only:
- Host path: `/home/clawd/.openclaw/workspace/marfa-ai/data`
- Container path: `/bot-data`
- Expected DB file inside container: `/bot-data/marfa.db`

Environment variable:
- `BOT_DB_PATH=/bot-data/marfa.db`

---

## 3) Current site structure

### Home page (`app/page.tsx`)
Current sections:
- sticky header
- hero with large Marfa PNG visual
- floating QR card over hero image
- catalog
- pricing
- blog preview
- footer

### Hero block
Current implementation details:
- large transparent PNG visual: `public/marfa-hero.png`
- QR card is overlaid in the lower-right area of the image
- QR card has a soft floating animation
- hero CTA opens Telegram bot

### Catalog block
Current model groups shown on the site:

#### Text and code
- GPT-5.4 and GPT-4o mini
- Claude 4.6 Sonnet and 3.5 Haiku
- Gemini 3.1 Pro and Flash

#### Images
- Midjourney
- NanaBanana 2 and NanaBanana Pro

#### Video
- Sora & Veo
- Kling
- Hailuo

### Footer
Current footer structure:
- Navigation
- Help → Support only (`https://t.me/FangedTwin`)
- Inline text support form
- Other products → Content Pilot (`https://content-pilot.io`)
- copyright line: `© 2026 Марфа Ai. Все права защищены.`

Removed from footer:
- FAQ
- API
- Privacy link
- Offer link
- old “Community” block

---

## 4) Blog system

### Pages
- Blog index: `app/blog/page.tsx`
- Article page: `app/article/[slug]/page.tsx`

### Data source
- `data/articles.json`

### Current rendering behavior
The article page normalizes markdown-like content into styled HTML blocks:
- headings
- paragraphs
- numbered lists
- cleaned inline markdown

The blog and article pages were rewritten to use Tailwind classes directly instead of legacy custom layout classes.

---

## 5) Site analytics / tracking

### Tracking API
- `app/api/track/route.ts`

### Events tracked
- `pageview`
- `bot_click`
- `qr_click`

### Feed API
- `app/api/articles/route.ts`

Home page refreshes blog feed every 30 seconds from `/api/articles`.

Data file:
- `data/analytics.json`

---

## 6) Support tickets from website

### Website support form
A text support form is embedded into the footer “Помощь” section on the landing page.

Fields submitted:
- contact
- message
- page
- visitor id (`vid`)

### API
- `app/api/support/route.ts`

### Storage
- `data/tickets.json`

### Ticket structure
Current stored fields:
- `id`
- `vid`
- `message`
- `contact`
- `page`
- `status`
- `ts`
- `ua`

### Verified behavior
Confirmed during this session:
- support ticket POST works
- ticket persists to `tickets.json`
- ticket appears in CRM when file is populated

Important note:
- Local Desktop copy currently has `data/tickets.json` reset to `[]` in the synced project snapshot. If tickets were created directly on VPS before a later full sync, they may have been overwritten by the Desktop copy. The API itself works; the operational risk is sync direction, not route logic.

---

## 7) CRM dashboard

### Admin pages
- Dashboard: `app/admin/page.tsx`
- Login: `app/admin/login/page.tsx`
- Login API: `app/api/admin/login/route.ts`
- Guard: `middleware.ts`

### Admin tab layout
Current `/admin` layout is tabbed inside one page (not separate routes):
- `Сайт`
- `Telegram-бот`
- `Тикеты`
- `Контент`

Notes:
- tabs switch client-side without full page reload
- active tab is persisted in browser localStorage
- `Контент` tab contains article CRUD + generation UI

### CRM sections currently implemented

#### A. Site section
Shows:
- unique visitors
- unique bot clicks
- unique QR clicks
- new site tickets
- total pageviews
- total bot button clicks
- total QR clicks
- CTR to bot

#### B. Telegram bot section
Read directly from `marfa.db` using `lib/botStats.ts`.

Current dashboard UX:
- Telegram bot area is on its own admin tab
- ticket summary cards were removed from the Telegram bot KPI grid
- legacy Premium tier summary cards were removed from the Telegram bot KPI grid

Shows:
- total users
- paid users
- free users
- active weekly users
- payments day / week / all
- activity day / week
- token usage day / week
- cost day / week / all
- image packs stats
- video packs stats

#### C. Bot users table
Shows:
- `user_id`
- Telegram username
- Telegram first/last name
- premium/free status
- active/inactive status
- current model
- starts count
- requests over last 7 days
- last seen timestamp

Data source details:
- usernames/names are read from `users.state_json` (`telegramUsername`, `telegramFirstName`, `telegramLastName`)
- fallback for older rows comes from latest `start` event metadata

#### D. Request technical metrics table
Shows (without prompt text):
- timestamp
- `user_id`
- model
- tokens in / out / total
- source
- cost

Current extraction logic:
- rows are anchored on `bot_events.event_type='request_started'`
- request cost is read directly from the nearest `generation_result.meta_json`
- cost priority order:
  1. `raw_usage.cost`
  2. `cost`
  3. `upstream_inference_cost`
- token priority order:
  1. `raw_usage.prompt_tokens` / `raw_usage.completion_tokens` / `raw_usage.total_tokens`
  2. `tokens_in` / `tokens_out` from `generation_result.meta_json`
- dashboard no longer shows Provider/Origin columns in the request table
- request table intentionally avoids deriving price from a pricing table; it uses stored JSON metadata from bot events
- token counts are correlated from `usage_ledger`
- provider/cost are read from `meta_json` only if present

#### E. Website support tickets section
Shows site tickets stored in `data/tickets.json`.

#### F. Article management section
Supports:
- generate article by topic
- open blog
- edit existing article title/excerpt/tags/content
- save article via API

---

## 8) Bot analytics integration

### Source of truth
Main logic in bot project:
- `/home/clawd/.openclaw/workspace/marfa-ai/src/infra/analytics.js`
- `/home/clawd/.openclaw/workspace/marfa-ai/src/index.js`

### DB path
- `/home/clawd/.openclaw/workspace/marfa-ai/data/marfa.db`

### Relevant bot tables confirmed during this session
- `bot_events`
- `bot_payments`
- `support_tickets`
- `usage_ledger`
- `users`

### Files in landing project
- `lib/botStats.ts` — bot DB reader for CRM

### Current assumptions in CRM layer
- premium status is derived from `users.state_json.isPremium`
- active status is approximated by recent activity / last seen
- request rows are based on `request_started` events
- token usage is paired from `usage_ledger`

### Verified DB observations during this session
Observed in real data:
- `bot_events.meta_json` contains at least `model` and `source`
- `usage_ledger.meta_json` contains at least `model`
- current sampled rows did **not** show provider/cost in the inspected examples

This means:
- model + token metrics are already grounded in DB
- provider/cost may require deeper source instrumentation or a different event payload path if they are expected but not visible in current rows

---

## 9) Article generation and editing

### Auto-blog pipeline (scheduled)
- `POST /api/cron/publish`
- file: `app/api/cron/publish/route.ts`

### CRM generation endpoint
- `POST /api/admin/generate-article`
- file: `app/api/admin/generate-article/route.ts`

### CRM generation behavior
Current behavior:
- accepts optional `topic`
- fetches current trend signals from Google News RSS
- builds prompt for OpenRouter
- generates article JSON
- saves to `data/articles.json`

### Manual article edit API
- `app/api/admin/articles/route.ts`

Supports:
- `POST` — create article manually
- `PUT` — update existing article by slug

### Verified behavior
Confirmed during this session:
- generation by topic works
- article save path works
- generated article is persisted into `articles.json`

---

## 10) Styling system

Current styling system:
- Tailwind CSS 4
- global styles in `app/globals.css`

Important notes:
- project was migrated to Tailwind 4 syntax
- theme variables are defined in `@theme`
- custom utility `text-balance` is defined in `app/globals.css`
- hero QR floating animation is defined in `app/globals.css`

---

## 11) Deployment / operations

### Workdir on VPS
- `/home/clawd/.openclaw/workspace/marfa-landing`

### Deploy current version
```bash
docker compose up -d --build
```

### Reliable sync from Desktop to VPS
```bash
rsync -avz --delete --exclude 'node_modules' --exclude '.next' --exclude '.DS_Store' -e 'ssh -i ~/.ssh/id_ed25519' ~/Desktop/marfa-landing/ clawd@109.71.240.3:/home/clawd/.openclaw/workspace/marfa-landing/
ssh -i ~/.ssh/id_ed25519 clawd@109.71.240.3 'cd /home/clawd/.openclaw/workspace/marfa-landing && docker compose up -d --build'
```

### Check status
```bash
docker compose ps
```

### Tail app logs
```bash
docker compose logs -f marfa-site
```

### Tail nginx logs
```bash
docker compose logs -f nginx
```

### Manual article publish (scheduled flow)
```bash
./scripts_run_autoblog.sh
```

### Notes from this session
- old `owner-*` CRM remnants on VPS had to be removed via full `rsync --delete`
- stale files on server can break clean rebuilds even if local tree is already fixed
- full sync with delete is the safest way to restore project consistency

---

## 12) Code map

- Home page: `app/page.tsx`
- Global styles: `app/globals.css`
- Blog index: `app/blog/page.tsx`
- Article page: `app/article/[slug]/page.tsx`
- Admin login: `app/admin/login/page.tsx`
- Admin dashboard: `app/admin/page.tsx`
- Track API: `app/api/track/route.ts`
- Site support API: `app/api/support/route.ts`
- Articles feed API: `app/api/articles/route.ts`
- Manual article admin API: `app/api/admin/articles/route.ts`
- CRM article generation API: `app/api/admin/generate-article/route.ts`
- Scheduled publish API: `app/api/cron/publish/route.ts`
- Generic store helpers: `lib/store.ts`
- Bot DB readers: `lib/botStats.ts`
- Middleware: `middleware.ts`
- Hero asset: `public/marfa-hero.png`
- Docker compose: `docker-compose.yml`
- Dockerfile: `Dockerfile`
- Nginx config: `nginx/default.conf`

---

## 13) Next-session handoff / priorities

### Already verified working
- landing is up on VPS
- `/admin` responds with HTTP 200
- support ticket API works
- topic-based article generation works
- bot DB is mounted into landing container
- bot overview/user/request data are readable from `marfa.db`

### Highest-priority next improvements
1. Add ticket status controls in CRM (`new / read / closed`).
2. Add filters/search for bot users (premium, active, inactive).
3. Investigate deeper bot payloads for `provider` and `cost` if these are expected but missing in current CRM request table.
4. Add manual article creation form directly in CRM UI (not only API support).
5. Add article delete/archive action.
6. Add better ticket persistence discipline when syncing from Desktop to VPS (avoid overwriting live `tickets.json` accidentally).
7. Improve domain/HTTPS configuration once final domain is chosen.

### Important caution for next session
When syncing project from Desktop to VPS using `rsync --delete`, local `data/*.json` files can overwrite newer live data on server. This is especially relevant for:
- `data/tickets.json`
- `data/analytics.json`
- `data/articles.json`

Before a destructive sync, decide whether live server data should be preserved and exclude/sync data files accordingly.

### Good first checks next session
```bash
ssh -i ~/.ssh/id_ed25519 clawd@109.71.240.3 'cd /home/clawd/.openclaw/workspace/marfa-landing && docker compose ps'
ssh -i ~/.ssh/id_ed25519 clawd@109.71.240.3 'python3 - <<"PY"
import json
print(open("/home/clawd/.openclaw/workspace/marfa-landing/data/tickets.json").read()[:1000])
PY'
```

---

## 14) Current known issues / follow-ups

1. Next.js version in project is still `14.2.5`; it should be upgraded to a patched version.
2. `favicon.ico` should be added if browser tab branding matters.
3. Metadata/canonical can be improved further for final production SEO.
4. HTTPS/domain setup should be finalized if the site moves from raw IP to public domain.
5. If traffic grows, JSON storage should eventually move to a database.
6. `provider` / `cost` fields are only shown if present in bot event payloads; current sampled rows did not expose them.

## 8) Telegram bot data mapping used by CRM

### Canonical bot DB
- Host path: `/home/clawd/.openclaw/workspace/marfa-ai/data/marfa.db`

### Key bot tables used by site CRM
- `users`
- `bot_events`
- `bot_payments`
- `usage_ledger`
- `support_tickets`

### Metric logic source files
- Bot-side analytics/event writing: `/home/clawd/.openclaw/workspace/marfa-ai/src/infra/analytics.js`
- Bot-side request handling/event emission: `/home/clawd/.openclaw/workspace/marfa-ai/src/index.js`
- `/start` event registration: `/home/clawd/.openclaw/workspace/marfa-ai/src/commands/registerCommands.js`
- Site-side reader: `/home/clawd/.openclaw/workspace/marfa-landing/lib/botStats.ts`

### Verified counter semantics
- **Total users** = distinct `user_id` with `bot_events.event_type='start'`
- **Paid users** = started users whose `users.state_json.isPremium = 1`
- **Free users** = started users whose `users.state_json.isPremium != 1`
- **Active weekly** = users with `3+` `request_started` events in the last 7 days
- **Payments** = direct aggregates from `bot_payments`
- **Tokens** = direct aggregates from `usage_ledger` (`tokens_in`, `tokens_out`)
- **Cost** = direct aggregate from `generation_result.meta_json` JSON fields, not a site-side pricing formula

### Dashboard implementation notes from 2026-03-18
- `/admin` was switched to dynamic rendering to avoid frozen bot metrics from static builds
- Telegram usernames and names were added to CRM user table
- request cost handling was corrected to prefer stored provider JSON metadata
- Provider/Origin columns were later removed from UI at user request
- bot ticket count cards and Premium tier summary cards were removed from Telegram bot KPI area at user request


## 8) Dashboard runtime architecture (2026-03-19 stable build)

### Tab structure
`/admin` is a single page with client-side tabs:
- Site
- Telegram bot
- Tickets
- Content

State:
- selected tab persisted in browser `localStorage` as `marfa-admin-tab`

### Live admin widgets
- `BotSummaryLive.tsx` → `/api/admin/bot-analytics`
- `BotUsersLive.tsx` → `/api/admin/bot-users`
- `BotModelsWeekLive.tsx` → `/api/admin/bot-analytics`
- `RequestMetricsTable.tsx` → `/api/admin/request-metrics`
- `SiteTicketsLive.tsx` → `/api/admin/site-tickets`

Refresh model:
- polling every 10s
- manual refresh buttons on live blocks
- admin APIs must remain `force-dynamic` / `revalidate = 0` / `Cache-Control: no-store`

### Canonical sources
- bot summary: `/home/clawd/.openclaw/workspace/marfa-ai/data/bot-analytics-summary.json`
- request metrics: `/home/clawd/.openclaw/workspace/marfa-ai/data/request-metrics.jsonl`
- site tickets: `data/tickets.json`
- site analytics: `data/analytics.json`
- articles: `data/articles.json`

### Important source rules
- `Telegram-бот` summary block uses summary JSON as canonical source.
- `Cost day/week/all` displayed in the bot summary block comes from request metrics (`request_metrics.costs` or fallback reconstruction from JSONL).
- `Модели бота за 7 дней` is sourced from request metrics, not legacy DB-only model slices.
- `Техметрики запросов` always uses `request-metrics.jsonl`.
- `Пользователи бота` are live-fetched from `readBotUsers()` via admin API.
- `Тикеты поддержки сайта` are live-fetched from `data/tickets.json` via admin API.

### Operational warning
Do not refactor live admin widgets back into static server-only blocks unless explicitly requested. Previous sessions showed that cached/static admin APIs can make the dashboard appear broken even when data exists on disk.
