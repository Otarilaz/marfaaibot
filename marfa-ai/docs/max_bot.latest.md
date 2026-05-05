# max_bot — аудит @GPT4Telegrambot

Дата аудита: 2026-03-09 (Europe/Moscow)
Метод: Telegram Web (ручной обход + снимки интерфейса)
Статус: частично полный (основные меню и ключевые inline-кнопки собраны)

---

## 1) Стартовое описание бота (What can this bot do?)

Бот позиционируется как агрегатор ИИ-сервисов:
- Text: ChatGPT, Gemini Pro, Claude, DeepSeek, Perplexity
- Image: Nano Banana Pro, GPT Images, Midjourney, Seedream, Flux 2
- Video: Veo 3.1, Sora 2, Seedance, Kling, Grok Imagine, Hailuo, Pika
- Music: Suno AI, Lyria 3

Также в сообщениях упоминаются бесплатные и премиум-лимиты.

---

## 2) Зафиксированные команды/разделы

В текстах и ответах бота встречаются:
- `/start`
- `/model`
- `/premium`
- `/deletecontext`
- `/s` (поиск с интернет-доступом)
- `/photo`
- `/video`
- `/chirp` (музыка)

---

## 3) /start — приветствие и навигация

Основной смысл стартового текста:
- БЕСПЛАТНО: до 100 запросов в неделю (по части моделей)
- PREMIUM: доступ к продвинутым моделям и доп. функциям
- Инструкции по разделам: текст, поиск, изображения, видео, музыка
- Реферальные/связанные боты: `@MyLook`, `@GPT4AgentsBot`, `@GPT4Tbot`

---

## 4) /model — выбор модели

### Кнопки, которые были доступны в интерфейсе:
- GPT-5.4
- OpenAI o3
- GPT-4.1
- GPT-5 mini
- ✅ GPT-4o mini (выбрана)
- Claude 4.6 Sonnet
- Claude 4.6 Thinking
- DeepSeek-V3.2
- DeepSeek-V3.2 Thinking
- Gemini 3.1 Pro
- Gemini 3.1 Flash
- Кнопка навигации: `← Назад` / `Закрыть` (в разных состояниях)

### Сопровождающий текст (суть):
- GPT-5 mini, Gemini 3.1 Flash, DeepSeek — доступны бесплатно
- Продвинутые модели — в premium
- Для "Thinking" режимов есть повышенный расход генераций
- Работа с документами (docx/pdf/xlsx/xls/csv/pptx/txt) — premium

---

## 5) /premium — подписки и пакеты

### Блок "Статистика использования" (пример состояния):
- Подписка: бесплатная
- Выбрана модель: GPT-4o mini
- Запросов в неделю: 0/100
- Кнопка: `🚀 Подключить Премиум`

### Выбор периода Premium (кнопки):
- `1 месяц – ⭐ 500`
- `3 месяца – ⭐ 1200 (-20%)`
- `6 месяцев – ⭐ 2000 (-35%)`
- `12 месяцев – ⭐ 3000 (-50%)`
- `← Назад`

### Выбор сервиса для покупки (кнопки):
- `Premium`
- `Premium X2`
- `Изображения`
- `Видео`
- `Suno`

### Зафиксированные ценовые блоки (из текста):
- Premium: 100 запросов/день, 500⭐
- Premium X2: 200 запросов/день, 750⭐
- Пакеты изображений: от 250⭐
- Пакеты видео: от 150⭐
- Пакеты Suno: от 250⭐
- Справка по оплате: ссылка на teletype + контакт поддержки

---

## 6) /deletecontext

Ответ бота после команды:
- "Контекст удален. По умолчанию бот в ответе учитывает ваш предыдущий вопрос и свой ответ на него"

---

## 7) Видео-сценарий (Grok Imagine) — отдельный экран

Зафиксирован экран конструктора видео с инструкциями и ограничениями.

### Кнопки/поля:
- `Промпт`
- `Картинка / видео`
- Соотношение сторон: `auto`, `1:1`, `9:16`, `16:9`, `4:3`, `3:4`, `2:3`, `3:2`
- Длительность: `6 сек.`, `9 сек.`, `12 сек.`, `15 сек.`
- Управление: `❌ Отменить`, `Начать генерацию`

### Доп. текстовые ограничения:
- Нельзя 18+, насилие, дипфейки (по правилам провайдера)
- Редактор видео может расходовать 2 генерации

### Покупка видео-пакетов (кнопки):
- `2 генерации – ⭐ 150`
- `10 генераций – ⭐ 500`
- `20 генераций – ⭐ 900`
- `50 генераций – ⭐ 2000`
- `← Назад`

---

## 8) Простые текстовые диалоги (проверка ответа)

Тестовые входы и ответы:
- "Привет" -> "Привет! Как я могу помочь тебе сегодня?"
- "Как дела" -> "У меня все хорошо, спасибо! ..."
- "Не знаю" -> поддерживающий универсальный ответ

Вывод: обычный чатовый режим работает, не только меню-команды.

---

## 9) Что ещё НЕ покрыто полностью

Для формально "полного" аудита остались необойденными некоторые глубокие ветки:
- пошаговые сценарии `/photo` (все подмодели и режимы редактирования)
- `/chirp` (все жанры/шаблоны)
- `/s` (режимы поисковых моделей)
- все состояния после покупки/оплаты (не проходились)
- все ветки каждой модели после переключения

---

## 10) Промежуточный вывод

Собрана большая часть публично доступной функциональности и ключевых кнопок:
- модели,
- premium/тарифы,
- видео-конструктор,
- контекст/сервисные команды,
- базовые диалоговые ответы.

Если нужен 100% exhaustive-map, следующим шагом пройти каждую команду (`/photo`, `/video`, `/chirp`, `/s`) по всем inline-кнопкам до листьев дерева и добавить их в этот файл как таблицу "кнопка -> ответ -> следующая кнопка".


---

## PROGRESS LOG (live)
- 2026-03-09 19:33 MSK: Relay reconnected, exhaustive pass started.
- Scope now: /start, /model, /premium, /photo, /video, /chirp, /s with all reachable inline branches.
- 2026-03-09 19:33:12 MSK: heartbeat — audit in progress.
- 2026-03-09 19:34:13 MSK: heartbeat — audit in progress.
- 2026-03-09 19:35:13 MSK: heartbeat — audit in progress.
- 2026-03-09 19:36:13 MSK: heartbeat — audit in progress.
- 2026-03-09 19:37:13 MSK: heartbeat — audit in progress.
- 2026-03-09 19:38:13 MSK: heartbeat — audit in progress.

- 2026-03-09 19:39 MSK: LIVE UPDATE — подтверждено активное relay-подключение (tab: https://web.telegram.org/a/#8730306931, ws relay 18792).
- 2026-03-09 19:39 MSK: LIVE UPDATE — найден чат `@GPT4Telegrambot` в списке (последний видимый вход: `/start` в 19:22), готов к пошаговому прокликиванию веток.
- 2026-03-09 19:39 MSK: LIVE UPDATE — зафиксирован план обхода: `/start` -> `/model` -> `/premium` -> `/photo` -> `/video` -> `/chirp` -> `/s`; для каждой ветки собираю `кнопка -> ответ -> следующая кнопка`.
# @GPT4Telegrambot — человеческое описание интерфейса и возможностей

Дата: 2026-03-09

Это Telegram-бот-«комбайн» по ИИ, где в одном месте собраны текстовые модели, генерация изображений, видео и музыки.

## Как выглядит и как устроен

После `/start` бот показывает краткую «витрину»:
- что доступно бесплатно,
- что входит в premium,
- куда заходить для текста, картинок, видео и музыки.

Логика навигации простая: команды + inline-кнопки. То есть ты либо пишешь команду (`/model`, `/premium`, `/photo`, `/video`, `/chirp`, `/s`), либо нажимаешь кнопки в сообщениях бота.

## Основные разделы

### 1) Текстовый чат
Бот отвечает как обычный собеседник, умеет держать короткий контекст. Есть команда `/deletecontext` для сброса истории диалога.

### 2) Выбор модели (`/model`)
Есть экран выбора LLM (GPT, Claude, Gemini, DeepSeek и т.д.).
Часть моделей доступна бесплатно, часть — только в premium. Для некоторых «thinking»-режимов повышенный расход лимита.

### 3) Подписка и пакеты (`/premium`)
Раздел с:
- текущим статусом аккаунта,
- лимитами,
- кнопками покупки premium на разные сроки,
- отдельными пакетами под изображения/видео/музыку.

То есть monetization разделён не только по подписке, но и по типам генераций.

### 4) Изображения (`/photo`)
Раздел для генерации картинок и, вероятно, редактирования/вариаций (через подмодели и кнопки сценариев).
По смыслу — это отдельный «конструктор» поверх разных image-моделей.

### 5) Видео (`/video`)
Есть режим видеогенерации с формой:
- поле промпта,
- опциональная картинка/видео как источник,
- выбор aspect ratio,
- выбор длительности,
- кнопки запуска/отмены.

Также присутствуют правила контента и расход генераций в зависимости от действия (обычная генерация vs редактирование).

### 6) Музыка (`/chirp`)
Раздел для музыкальных генераций (Suno/связанные сценарии) с отдельными лимитами/пакетами.

### 7) Поиск (`/s`)
Команда для запросов с интернет-доступом (search-режим), когда нужен ответ не только из модели, но и с опорой на внешние источники.

## Впечатление по UX

Бот сделан как многоуровневое меню:
- сверху — маркетинговое позиционирование,
- ниже — быстрый доступ к функциям,
- внутри каждого направления — свой мини-интерфейс кнопок.

Сильная сторона: «всё в одном» и быстрый старт без сложной настройки.
Слабая сторона: из-за количества веток легко потеряться без полной карты переходов.

## Для разработки: как воспринимать продукт

Это не просто «чат-бот», а продуктовая оболочка над несколькими провайдерами ИИ:
- единый вход,
- единый UX,
- разные тарифные зоны,
- разные unit-экономики по типу контента (text/image/video/music).

Если смотреть как техдок-основание, то архитектурно это:
1) маршрутизация команды/кнопки,
2) выбор провайдера/модели,
3) проверка лимитов/подписки,
4) запуск генерации,
5) возврат результата + следующего шага кнопками.

---

Если нужно, следующим шагом можно сделать вторую версию этого файла в формате:
- «путь пользователя по сценариям» (новичок / power user / premium),
- «болезненные места UX»,
- «что улучшить в конкурентном аналоге». 

---

# Техническая заметка для кодера: UI/UX @GPT4Telegrambot (как это, вероятно, реализовано в коде)

Ниже — инженерная декомпозиция интерфейса и поведения бота, в терминах архитектуры Telegram Bot API (commands + inline keyboards + callback_data + state machine).

## 1) Продуктовая модель интерфейса

UI бота — это **menu-driven conversational app**:
- вход через `/start`;
- дальнейшая навигация через `InlineKeyboardMarkup`;
- каждый экран = сообщение + кнопки + callback-обработчик;
- состояние пользователя хранится в профиле/сессии (выбранная модель, лимиты, подписка, текущий flow генерации).

Фактически это finite-state UX поверх Telegram chat UI.

---

## 2) Предполагаемые сущности (domain model)

### User
- `telegram_user_id`
- `plan` (`free`, `premium`, `premium_x2` ...)
- `weekly_requests_used`
- `daily_requests_used`
- `selected_model`
- `locale`

### Quota / Billing
- `quota_type` (`text`, `image`, `video`, `music`)
- `balance_or_credits`
- `resets_at`
- `pricing_tier`

### GenerationJob
- `job_id`
- `user_id`
- `kind` (`text`, `image`, `video`, `music`, `search`)
- `provider` (`openai`, `gemini`, `claude`, `deepseek`, ...)
- `model`
- `input_payload`
- `status` (`queued`, `running`, `done`, `failed`)
- `cost_units`
- `result_ref`

### ConversationState
- `state` (например `IDLE`, `VIDEO_PROMPT_WAITING`, `VIDEO_ASPECT_WAITING`, ...)
- `context_window` (последние N сообщений)
- `last_screen`

---

## 3) Архитектурный слой UI (Telegram)

### 3.1 Update router
1. `message` handler:
   - команды `/start`, `/model`, `/premium`, `/photo`, `/video`, `/chirp`, `/s`, `/deletecontext`;
   - свободный текст → text pipeline.
2. `callback_query` handler:
   - распарсить `callback_data`;
   - выполнить action;
   - `editMessageText`/`editMessageReplyMarkup` или отправить новое сообщение.

### 3.2 Screen renderer
Каждый экран рендерится как функция:
- `renderStartScreen(user)`
- `renderModelPicker(user)`
- `renderPremiumScreen(user, usage)`
- `renderVideoBuilder(state)`
и т.д.

Возвращает:
- `text`
- `inline_keyboard`
- опционально `parse_mode`, media preview.

### 3.3 Callback schema
`callback_data` обычно короткая и versioned, например:
- `mdl:set:gpt-4o-mini`
- `prem:period:3m`
- `vid:aspect:16x9`
- `vid:dur:12`
- `nav:back:premium`

Важно ограничение Telegram: callback_data до 64 байт.

---

## 4) UX-паттерны, которые уже видны

1. **Hub-and-spokes**: `/start` как хаб, дальше ветки по типу контента.
2. **Progressive disclosure**: сначала high-level кнопки, потом тонкие параметры.
3. **Paywall-aware navigation**: premium-кнопки доступны всем, но фактический запуск gated.
4. **Soft-fail UX**: вместо жёсткой ошибки — подсказка о лимите/подписке.
5. **Back/Close controls**: почти в каждом screen-flow есть навигационные кнопки.

---

## 5) Техреализация ключевых веток

### 5.1 `/model`
Поток:
- показать список моделей + текущую выбранную (`✅`);
- по callback `mdl:set:*` обновить `user.selected_model`;
- перерендерить тот же экран с новым флагом выбора.

Гейтинг:
- если модель premium-only и у пользователя free-план, либо:
  - запретить выбор,
  - либо разрешить выбор, но блокировать генерацию на этапе submit.

### 5.2 `/premium`
Поток:
- показать usage stats + CTA;
- выбор периода (`1m/3m/6m/12m`);
- выбор категории пакета (`premium`, `premium x2`, `image`, `video`, `suno`);
- переход на payment intent/deeplink.

### 5.3 `/video` (конструктор)
Состояние формы:
- `prompt`
- `source_media` (optional)
- `aspect_ratio`
- `duration_sec`

Submit:
- pre-check (план, лимит, policy);
- создать `GenerationJob(kind=video)`;
- async result + polling/webhook completion;
- отправить готовое видео/ссылку и кнопки «повторить/изменить параметры».

### 5.4 `/deletecontext`
- очищает `context_window` (или thread key-value store);
- оставляет сервисные настройки пользователя неизменными.

---

## 6) Оркестрация провайдеров (backend)

Нужен provider abstraction:
- `TextProvider`
- `ImageProvider`
- `VideoProvider`
- `MusicProvider`

С контрактом типа:
- `validate(payload)`
- `estimateCost(payload, userPlan)`
- `submit(payload)`
- `getResult(jobId)`

Маршрутизация:
- по выбранной модели/режиму;
- fallback при ошибке провайдера;
- единый формат ошибок в UX.

---

## 7) Технические риски и что важно кодеру

1. **Idempotency** callback-ов (двойные клики по кнопкам).
2. **Race conditions** (смена модели во время активной генерации).
3. **Rate limiting** Telegram + провайдеров.
4. **Длинные операции** (video/music): очереди, retry, timeout handling.
5. **State drift** при `editMessage*` (сообщение удалено/устарело).
6. **Observability**: логи на уровне `user_id, command, callback, job_id, provider, latency, fail_reason`.

---

## 8) Минимальный каркас модулей (референс)

- `bot/router.ts` — update routing
- `bot/screens/*.ts` — screen renderers
- `bot/callbacks/*.ts` — callback handlers
- `core/state-store.ts` — FSM/user state
- `core/quota-service.ts` — лимиты/план
- `core/billing-service.ts` — платежные intent-ы
- `providers/*` — адаптеры LLM/image/video/music
- `jobs/queue-worker.ts` — async генерации
- `policy/moderation.ts` — контент-ограничения

---

## 9) Что улучшить в UX на уровне кода

1. Унифицировать callback schema (versioned + typed parser).
2. Добавить единый `screen_id` и telemetry переходов (воронка по кнопкам).
3. Ввести "resume flow" после ошибок провайдера (не терять форму).
4. В каждом heavy-flow сделать explicit step indicator (`1/4`, `2/4`...).
5. Нормализовать copy для free/premium-gate (один стиль причин блокировки).

---

Итог для разработчика: текущий UI/UX бота — это классический Telegram FSM-продукт с multi-provider оркестрацией и paywall-логикой. Ключ к стабильности — строгая схема callback-ов, консистентный state-store, и надёжный async-pipeline генераций.


---

# Доп.блок для кодера: интеграция памяти и скрытой маршрутизации (Telegram + MAX)

Источник: входной документ «Интеграция ИИ агрегатора с памятью».

## Цель
Сделать одинаковый продуктовый UX в двух мессенджерах:
- Пользователь видит брендовые режимы (ChatGPT / Claude / Gemini / Midjourney / Suno),
- Под капотом идёт маршрутизация в реальные provider model IDs,
- Контекст диалога сохраняется и используется в text-запросах,
- Команда/действие `deletecontext` гарантированно очищает память.

---

## 1) Каноническая архитектура (общая для TG и MAX)

### 1.1 Unified domain
- `UserProfile`: id, locale, plan, limits, selectedModelKey
- `Conversation`: userId, threadKey, history[], updatedAt
- `QuotaLedger`: userId, metricType, used, resetAt
- `Job`: id, kind(text|image|video|music), provider, modelId, status, cost

### 1.2 Core services
- `ModelRegistry` (user-facing key -> provider/modelId/capabilities)
- `ContextService` (append/read/trim/clear)
- `QuotaService` (check/debit/refund)
- `GenerationService` (provider adapters)
- `ModerationService` (policy gates)
- `TransportAdapters` (`telegram-adapter`, `max-adapter`)

### 1.3 Важный принцип
**Бизнес-логика не должна жить в adapter-слое**. 
Telegram/MAX только:
- принимают событие,
- преобразуют в унифицированный `Intent`,
- отдают в core use-case,
- возвращают `UiResponse`.

---

## 2) Telegram: рекомендации по реализации

Ориентир: Telegram Bot API (commands, messages, callback_query, inline/reply keyboards).

1. Использовать `callback_query` + `callback_data` для меню и выбора моделей.
2. Делать строгую схему callback-data (короткая, versioned), пример:
   - `m:v1:set:claude`
   - `ctx:v1:clear`
   - `nav:v1:back:premium`
3. Команды `/start /model /premium /photo /video /s /deletecontext` — как тонкие контроллеры, без дублирования бизнес-логики.
4. Для контекста: хранить историю по `(chat_id, user_id, thread?)` и обрезать по токен-бюджету, а не только по количеству сообщений.
5. На API-ошибке text-generation:
   - не «ломать» историю,
   - откатывать только последний user-turn при необходимости,
   - логировать correlation-id.
6. Для долгих задач (video/music): очередь + статусные апдейты сообщением (`queued -> running -> done`).

---

## 3) MAX: рекомендации по реализации

Ориентир: `@maxhub/max-bot-api` + события платформы MAX.

1. Ввести тот же intent-layer, что и в Telegram:
   - `MessageIntent`
   - `CommandIntent`
   - `ButtonIntent`
2. Для state и контекста использовать единый storage ключ:
   - `platform=max`
   - `userPlatformId`
   - `dialogKey` (если есть тред/комната — включать в ключ).
3. Reply keyboard и menu-UX синхронизировать с Telegram по сценариям, но не копировать буквально (учитывать ограничения MAX-клиента).
4. Если в MAX нет полного аналога Telegram callback-кнопок — делать fallback через короткие slash/quick команды.
5. Единый telemetry-формат для MAX и TG, чтобы сравнивать воронки:
   - `screen_open`, `model_switch`, `generation_start`, `generation_fail`, `generation_done`, `context_clear`.

---

## 4) Память диалога: production-правила

1. Хранить минимум:
   - `role`, `content`, `createdAt`, `tokenEstimate`, `messageId`.
2. Перед вызовом модели собирать контекст policy-driven:
   - system prompt,
   - сжатое summary long-term,
   - последние релевантные turns по лимиту токенов.
3. Делать авто-суммаризацию длинных диалогов (compaction), чтобы не терять смысл и не раздувать стоимость.
4. `deletecontext` очищает только conversation memory, но не профиль/план/лимиты.
5. Добавить TTL и право удаления данных (privacy compliance).

---

## 5) Model registry (скрытая маршрутизация)

Рекомендовано хранить в отдельном конфиге (yaml/json/db):

- `modelKey` (что видит пользователь): `chatgpt`, `claude`, `gemini`, `midjourney`, `suno`
- `provider`
- `providerModelId`
- `kind`
- `planRequired`
- `costPolicy`
- `enabled`

Плюс feature-flag на hot-swap моделей без деплоя.

---

## 6) Надежность и масштабирование

1. Уйти от in-memory state в персистентное хранилище:
   - SQLite/PostgreSQL для стартового прод,
   - Redis для rate-limit/locks/queues.
2. Idempotency keys для кнопок и retried webhook events.
3. Пер-пользовательный lock на критические операции (смена модели, списание лимита).
4. Dead-letter очередь для упавших генераций.

---

## 7) Безопасность

1. Никогда не отдавать клиенту provider secrets/real routing IDs.
2. Централизованный input sanitation + moderation перед внешними API.
3. Журналировать только нужный минимум (PII-minimization).
4. В логах маскировать токены, user identifiers — хэшировать при аналитике.

---

## 8) Минимальный контракт API между адаптером и ядром

`handleIntent(intent) -> UiResponse[]`

Где:
- `intent` = { platform, userId, chatKey, type, payload, messageId }
- `UiResponse` = { type(text|buttons|media|typing|status), payload }

Это позволит держать один и тот же core для Telegram и MAX, меняя только transport adapter.

---

## 9) Что внедрять первым (прагматичный roadmap)

1. Вынести ModelRegistry + ContextService в отдельные модули.
2. Перенести usersState из RAM в SQLite/Postgres.
3. Унифицировать команды/кнопки в intent map (TG + MAX).
4. Добавить token-budget compaction для истории.
5. Добавить единые метрики и дашборд воронки по платформам.

Итог: документ правильно задаёт направление (скрытая маршрутизация + память). Для production нужно закрепить это архитектурно: shared core, персистентный state, строгие контракты adapters и наблюдаемость на уровне каждого шага UX.


---

# Research-блок: соответствие нейросетей и агрегаторов (OpenRouter / fal.ai / GoAPI)

Дата проверки: 2026-03-09  
Метод: сверка по публичным страницам/эндпоинтам агрегаторов.

## Проверенные источники
- OpenRouter models API: `https://openrouter.ai/api/v1/models`
- GoAPI docs overview + endpoints:
  - `https://goapi.ai/docs/overview`
  - `https://goapi.ai/docs/midjourney-api`
  - `https://goapi.ai/docs/kling-api/create-task`
  - секции `veo3-api`, `veo31-api`, `sora2-api`, `seedance-api`, `song-api`, `gpt-image`, `gemini-api` (обнаружены в карте docs)
- fal.ai model pages:
  - `https://fal.ai/models/fal-ai/flux-pro`
  - `https://fal.ai/models/fal-ai/veo3`
  - `https://fal.ai/models/fal-ai/kling-video/v2.1/master/image-to-video`

> Важно: у агрегаторов названия в UI бота могут быть брендовые, а реальный backend-model-id отличаться.

## Маппинг по моделям из текущего `max_bot.md`

### Текстовые LLM
1. **GPT-5 / GPT-5.4**  
   - **OpenRouter: Да (подтверждено)** — `openai/gpt-5.4`, `openai/gpt-5.4-pro`  
   - fal.ai: нет подтверждения как основного LLM-роутинга  
   - GoAPI: возможно через GPTs/LLM API, но как canonical GPT-5 в docs явно не зафиксировано

2. **GPT-4o**  
   - **OpenRouter: Да (подтверждено)** — `openai/gpt-4o-*`  
   - GoAPI: есть GPTs/LLM API, но привязка к конкретному `gpt-4o` в этой проверке не фиксировалась  
   - fal.ai: не основной канал

3. **GPT-4.1**  
   - **OpenRouter: Да (подтверждено)** — `openai/gpt-4.1`, `gpt-4.1-mini`, `gpt-4.1-nano`

4. **OpenAI o3**  
   - **OpenRouter: Да (подтверждено)** — `openai/o3`, `openai/o3-pro`, `openai/o3-mini*`

5. **Claude 4.6 Sonnet / Thinking**  
   - **OpenRouter: Да (подтверждено)** — `anthropic/claude-sonnet-4.6` (+ другие Claude)

6. **Gemini 3.1 Flash / Pro**  
   - **OpenRouter: Да (подтверждено)** — `google/gemini-3.1-flash-*`, `google/gemini-3.1-pro-*`  
   - **GoAPI: Да (подтверждено как линейка Gemini API в docs)**

7. **DeepSeek-V3.2 / Thinking**  
   - **OpenRouter: Да (подтверждено)** — `deepseek/deepseek-v3.2`, `deepseek/deepseek-v3.2-exp`, etc.

8. **Perplexity**  
   - **OpenRouter: Да (подтверждено)** — `perplexity/sonar*`

### Image / Video / Audio модели
9. **Flux 2**  
   - **fal.ai: Да (подтверждено)** — FLUX endpoint page (`fal-ai/flux-pro`)  
   - **GoAPI: Да (подтверждено)** — `flux-api/*` секция в docs

10. **Midjourney**  
   - **GoAPI: Да (подтверждено)** — отдельная большая секция `midjourney-api`  
   - OpenRouter/fal.ai: не используем как основной canonical-канал Midjourney в текущей схеме

11. **Veo 3.1**  
   - **GoAPI: Да (подтверждено)** — `veo31-api/*`  
   - **fal.ai: Да для линейки Veo (подтверждена страница `fal-ai/veo3`)**

12. **Sora 2**  
   - **GoAPI: Да (подтверждено)** — `sora2-api/*`, `sora2-preview-api/*`, `sora2-pro-api/*`

13. **Seedance**  
   - **GoAPI: Да (подтверждено)** — `seedance-api/*`

14. **Kling**  
   - **GoAPI: Да (подтверждено)** — `kling-api/*`  
   - **fal.ai: Да (подтверждено)** — страница `fal-ai/kling-video/...`

15. **Hailuo**  
   - **GoAPI: Да (подтверждено)** — `hailuo-api/generate-video`  
   - fal.ai/OpenRouter: подтверждения в рамках текущей проверки нет

16. **Pika**  
   - На GoAPI/fal/OpenRouter в явном виде по текущим проверкам не зафиксировано (нужна отдельная точечная сверка)

17. **Suno AI**  
   - **GoAPI: Да (подтверждено косвенно/частично)** — в overview и song-api упоминается Suno (есть также пометка о sunsetting Suno в docs navigation)  
   - Вывод: поддержка может быть исторической/ограниченной — проверить актуальный статус перед прод-роутингом

18. **Lyria 3**  
   - В проверенных источниках OpenRouter/fal/GoAPI явного endpoint-подтверждения не найдено (нужна отдельная проверка по текущему провайдеру музыки)

19. **Nano Banana Pro**  
   - **OpenRouter: Да (подтверждено как Gemini image preview / Nano Banana)** — `google/gemini-3.1-flash-image-preview`  
   - **GoAPI: Да (подтверждено)** — `gemini-api/nano-banana-pro`

20. **GPT Images**  
   - **GoAPI: Да (подтверждено)** — `gpt-image/gpt-image-api`

21. **Grok Imagine**  
   - В OpenRouter подтвержден Grok как LLM-линейка (`x-ai/grok-*`), но именно `Grok Imagine` как image endpoint в текущей проверке не подтверждён.

22. **Seedream**  
   - В текущей сверке OpenRouter/fal/GoAPI явного подтверждения не найдено (нужна отдельная проверка конкретного vendor endpoint).

---

## Практическая рекомендация для кодера

Для прод-конфига держать явный `model_registry.yml` с полями:
- `ui_name`
- `kind` (text/image/video/audio)
- `primary_aggregator` (openrouter|fal|goapi)
- `provider_model_id`
- `fallback_aggregators[]`
- `status` (`active|beta|deprecated|sunsetting`)
- `last_verified_at`
- `evidence_url[]`

И обновлять registry через nightly health-check, чтобы автоматически вылавливать deprecations (особенно для video/music APIs).


---

## 16) Автоматический краулер состояний (добавлено)

Собран минимальный инструмент для автоматического обхода UI бота и фиксации графа экранов:

- Папка: `telegram_bot_crawler/`
- Файлы:
  - `crawler.py`
  - `config.yaml`
  - `requirements.txt`
  - `README.md`

### Назначение

- запуск от аккаунта через Telethon;
- старт от `/start`;
- обход inline-кнопок с ограничениями `max_depth`/`max_steps`;
- защита от циклов через хэш состояния экрана;
- запись результатов в:
  - `out/bot_map.json`
  - `out/bot_report.md`

### Запуск

```bash
cd telegram_bot_crawler
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python crawler.py
```

### Что обновлять в этом документе после проходки

После каждого прогона краулера дополнять этот `max_bot.md`:
1. дату/время проходки;
2. число найденных узлов и переходов;
3. новые экраны/кнопки, которых не было в предыдущем аудите;
4. изменения в тарифах/лимитах/командах;
5. проблемные ветки (циклы, пустые ответы, anti-automation).

## 17) Результат автопроходки краулером (2026-03-10)

Время проходки (UTC): `2026-03-10T10:38:43.991554+00:00`
Целевой бот: `@GPT4Telegrambot`

Итоги текущего прогона:
- Найдено узлов: **1**
- Зафиксировано переходов: **8**

Зафиксированные кнопки 1-го экрана (`/start`):
- 📝 Choose Model
- 🎨 Image Generation
- 🔎 Web Search
- 🎬 Video Generation
- 📄 File Recognition
- 🎸 Music Generation
- 🚀 Premium
- 👤 My Account

Зафиксированные переходы из стартового экрана:
- Choose Model → `970f1fbdeb6f`
- Image Generation → `f3d9cf1dfbee`
- Web Search → `6b701c608665`
- Video Generation → `7363d6bc29f0`
- File Recognition → `1d410fab1fc4`
- Music Generation → `e0465c1f0f80`
- Premium → `fcdc7c7125e1`
- My Account → `abf4e8730242`

Ограничение текущей версии краулера:
- включён безопасный режим `backtrack_to_start_each_branch=true`, из-за чего рекурсивный обход подэкранов не выполнялся (зафиксированы только переходы 1-го уровня).

План улучшения следующей итерации:
1. Добавить полноценную BFS/DFS очередь экранов для обхода уровней >1.
2. Нормализовать сигнатуры состояний (чтобы уменьшить ложные дубли).
3. Добавить обработку `FloodWait`/ретраи и контроль шагов по времени.

## 18) Тех-спека для кодера (Marfa AI UI/UX, Telegram)

### 18.1 `/start` — целевой текст

Требование: приветствие от Марфы AI, без блока «Другие наши боты».

Реализованный шаблон:
- Привет! Я Марфа AI 🤖
- Я помогу с текстом, изображениями, видео и музыкой — всё в одном боте.
- БЕСПЛАТНО: базовые сценарии для быстрого старта.
- PREMIUM: расширенные модели и более мощные режимы генерации.
- Инструкции по режимам:
  - 📝 ТЕКСТ — просто напиши запрос (модель можно выбрать в /model)
  - 🔎 ПОИСК — /s
  - 🖼️ ИЗОБРАЖЕНИЯ — /photo
  - 🎬 ВИДЕО — /video
  - 🎸 МУЗЫКА — /suno
- CTA: «Выбери режим в меню ниже 👇»

### 18.2 Bot Menu (кнопка «Меню» у поля ввода)

Через `setMyCommands` заданы команды:
- `/start` — 👋 Что умеет бот
- `/account` — 👤 Мой профиль
- `/premium` — 🚀 Премиум
- `/deletecontext` — 💬 Удалить контекст
- `/photo` — 🖼️ Создать изображение
- `/video` — 🎬 Создать видео
- `/suno` — 🎸 Создать песню
- `/s` — 🔎 Интернет-поиск
- `/model` — 📝 Выбрать модель
- `/settings` — ⚙️ Настройки бота
- `/help` — 🎱 Основные команды
- `/privacy` — 📄 Соглашение

### 18.3 `/account` — профиль/статистика

Ключевое требование: строка «Выбрана модель» должна быть динамической и зависеть от текущего выбора пользователя.

Реализация:
- Источник: `state.currentModelKey`
- Отображение: `MODELS[state.currentModelKey].uiName`
- Формат строки: `Выбрана модель: <model_name> /model`

Текущий шаблон `/account` включает:
- Подписка (free)
- Выбранная модель (динамически)
- Блок «Статистика использования»
- Пакеты premium/image/video/music
- Контакт поддержки

### 18.4 Файлы, где внесены изменения

- `marfa-ai/src/commands/registerCommands.js`
  - обновлён `/start`
  - добавлен `setMyCommands`
  - добавлены команды `/suno`, `/settings`, `/help`, `/privacy`
- `marfa-ai/src/utils/format.js`
  - обновлён шаблон `/account`
  - добавлена динамическая выбранная модель

### 18.5 Ветка «Создать картинку» (актуализация по референсам)

Обновлено под скриншоты и требования:
- вход в ветку через:
  - нижнюю кнопку `🎨 Создать картинку`
  - команду `/photo`
- показывается inline-меню сервисов:
  - GPT Images
  - Nano Banana 2
  - Midjourney
  - Seedream
  - FLUX 2
  - Замена лиц
  - Увеличение X2/X4
  - Закрыть

Критично:
- пункт **«Набор аватарок» удалён** и не должен отображаться.

Поведение:
- при выборе сервиса редактируется текущее сообщение на карточку сервиса;
- выставляется `currentModelKey` для пользователя;
- есть кнопка `← Назад` для возврата к списку сервисов.

Файлы:
- `marfa-ai/src/config/menu.js`
- `marfa-ai/src/commands/registerCommands.js`
- `marfa-ai/src/index.js`

### 18.6 Детализация под референсы (Image branch)

По присланным скринам добавлена детализация сценариев:

- `FLUX 2`
  - карточка с текстом про выбор модели/ratio;
  - кнопки: `FLUX 2 [Flex]`, `FLUX 2 [Pro]`, `FLUX 2 [Max]`, `✅ FLUX 2`, ratio (`1:1`, `9:16`, `16:9`, `3:4`, `4:3`), `🌱 Добавить seed`, `← Назад`.
  - `Добавить seed` выдаёт отдельную подсказку: «Введите seed для генерации…».

- `Замена лица`
  - текст в формате «Шаг 1/2…», как в референсе;
  - кнопка `← Назад`.

- `Увеличение x2/x4`
  - текст + ограничения по размеру;
  - кнопки `✅ Увеличить X2`, `Увеличить X4`, `← Назад`.

Примечание: `Набор аватарок` по требованию отсутствует.

### 18.7 Галочка выбранного параметра (вся ветка изображений)

Добавлено поведение выбора параметров с визуальной фиксацией `✅`:

- Для GPT Images / Gemini Images / Midjourney / Seedream:
  - ratio кнопки: `1:1`, `2:3`, `3:2`
  - активная кнопка помечается `✅`

- Для FLUX 2:
  - выбор модели: `Flex / Pro / Max` с `✅` у активной
  - выбор ratio: `1:1 / 9:16 / 16:9 / 3:4 / 4:3` с `✅` у активного
  - `🌱 Добавить seed`

- Для Upscale:
  - `Увеличить X2 / Увеличить X4` с `✅` у активного режима

- Для FaceSwap:
  - добавлена карточка с инструкцией и возвратом назад

Технически:
- выбор хранится в `state.imagePrefs[service]`
- callback `photo:set:<service>:<field>:<value>` обновляет state
- сообщение редактируется тем же экраном, где активная кнопка получает `✅`

Файл: `marfa-ai/src/commands/registerCommands.js`

### 18.8 Ветка «Видео» (Veo 3 API-style UX)

Сделано по референсам:

- Экран выбора видео-сервиса (`/video` и кнопка `🎬 Создать видео`) с кнопками:
  - Veo 3.1, Sora Video, Grok Imagine, Hailuo, Kling AI, Seedance 1.5,
    Kling Motion, Pika 2.5, Kling Effects, Pika Effects, Закрыть.

- Для выбранного сервиса открывается экран настройки генерации, как в референсе:
  - Промпт / Кадры / Референсы
  - VEO 3.1 / VEO 3.1 FAST
  - 4K (toggle)
  - 16:9 / 9:16
  - Инструкция / Добавить seed
  - Отменить / Начать генерацию

- Добавлено состояние выбора с `✅` на активных кнопках.

- Логика полей:
  - Промпт → бот просит отправить текстовый сценарий видео;
  - Кадры → бот просит отправить изображение (первый/последний кадр);
  - Референсы → бот просит отправить 1-3 изображения.

Технически:
- `state.videoPrefs[service]` хранит mode/aspect/4k и флаги заполненности;
- callbacks `video:set:*` обновляют state и перерисовывают клавиатуру;
- текущая отправка генерации пока в queued-режиме (заглушка ответа), под финальную интеграцию API провайдера.

---

## UPDATE 2026-03-11 — Добавлен Grok Imagine в раздел генерации изображений

### Что изменено в UX
В `/photo` добавлен новый сервис:
- `🌀 Grok Imagine` (callback: `photo:service:grok_image`)

Обновлён текст раздела изображений:
- теперь явно указано: **Grok Imagine — генерация и редактирование изображений**.

### Логика экрана Grok Imagine (Image)
При выборе `photo:service:grok_image` бот:
1. Переключает текущую модель пользователя на `grok_image`.
2. Показывает экран с описанием сценариев **create/edit**.
3. Отображает inline-кнопки:
   - `📝 Промпт`
   - `🖼️ Картинка`
   - ratio: `1:1`, `9:16`, `16:9`, `4:3`, `3:4`, `2:3`, `3:2`
   - `📌 Инструкция`
   - `← Назад`
4. Сохраняет выбранный ratio через `photo:set:grok_image:ratio:*`.

### Правила/копирайт для пользователя
Текст для Grok Image в боте:
- можно создавать и редактировать изображения;
- edit-режим: загрузить исходную картинку + описать изменения;
- ограничения по контенту: 18+, насилие, дипфейки запрещены;
- в edit-режиме может расходоваться 2 генерации.

### Изменения в коде (для кодера)
#### 1) `src/config/menu.js`
Добавлена кнопка сервиса:
```js
{ text: '🌀 Grok Imagine', callback_data: 'photo:service:grok_image' }
```

#### 2) `src/config/models.js`
Добавлена модель:
```js
grok_image: {
  uiName: 'Grok Imagine (Image)',
  kind: 'image',
  aggregator: 'goapi',
  providerModelId: 'grok-imagine-image'
}
```

#### 3) `src/commands/registerCommands.js`
Добавлено:
- новый сервис `grok_image` в `content` map (оба обработчика: `photo:service:*` и `photo:set:*`);
- инструкция `tips.grok_image`;
- отдельная клавиатура `serviceKeyboard('grok_image', prefs)` с ratio-кнопками и CTA `Промпт/Картинка`.

Ключевые callback для этой ветки:
- `photo:service:grok_image`
- `photo:set:grok_image:ratio:1_1|9_16|16_9|4_3|3_4|2_3|3_2`
- `photo:instruction:grok_image`

#### 4) `src/core/router.js`
Маршрутизация image-goapi переведена на provider-aware вызов:
```js
generateMidjourneyImage(imagePrompt, model.providerModelId)
```

#### 5) `src/providers/goapi.js`
`generateMidjourneyImage(prompt, providerModelId)`:
- если `providerModelId === 'midjourney-v7'` — работает текущий endpoint `mj/v2/imagine`;
- для остальных image provider id (в т.ч. `grok-imagine-image`) возвращает `queued`-stub с `note`, пока не подключён конкретный endpoint.

### Что осталось для полного прод-роутинга Grok Image
1. Подключить конкретный GoAPI endpoint для Grok Image (вместо stub).
2. Передавать в запросе provider-specific параметры (ratio, input image, edit mode).
3. Привязать списание генераций к mode (create/edit).
4. Добавить e2e тест ветки:
   - `/photo` -> `Grok Imagine` -> `ratio` -> prompt -> generation request.

## UPDATE 2026-03-11 — /photo приведён к референсу по карточкам сервисов

Ветка изображений переработана по референс-скринам с раздельной логикой по каждому сервису.

### Главное
- Убрана image-ветка Grok из `/photo`.
- Для каждого image-сервиса теперь свои кнопки параметров и свой UX-текст.

### Карточки и кнопки (как в референсе)
1) **GPT Images**
- Текст: «Создавайте и редактируйте… Отправьте от 1 до 3 изображений…»
- Кнопки: `1:1`, `2:3`, `3:2`, `📌 Инструкция`, `← Назад`.

2) **Gemini Images (Nano Banana)**
- Текст: 2 модели (Nano Banana 2 / Nano Banana Pro), сценарий edit/create.
- Кнопки:
  - модель: `Nano Banana 2`, `Nano Banana Pro`
  - качество: `1k`, `2k`
  - `🍿 Топ-50 промптов`
  - `← Назад`

3) **Midjourney**
- Текст: «Напишите в чат… поддерживаются основные параметры…»
- Кнопки: `📌 Инструкция`, `← Назад`.

4) **Seedream**
- Текст: 2 модели Seedream 4.5 / Seedream 5 + edit/create.
- Кнопки:
  - версия: `Seedream 4.5`, `Seedream 5`
  - качество: `2k`, `3k`
  - ratio: `1:1`, `9:16`, `16:9`, `3:4`, `4:3`
  - `← Назад`

5) **FLUX 2**
- Кнопки сохранены в целевом формате:
  - `FLUX 2 [Flex]`, `FLUX 2 [Pro]`, `FLUX 2 [Max]`
  - ratio: `1:1`, `9:16`, `16:9`, `3:4`, `4:3`
  - `🌱 Добавить seed`, `📌 Инструкция`, `← Назад`

### Техническая реализация (код)
Файл: `marfa-ai/src/commands/registerCommands.js`

- В `ensureImagePrefs` добавлены persistent-поля:
  - `nanoModel`, `nanoResolution`
  - `seedreamModel`, `seedreamResolution`

- В `serviceKeyboard(service, prefs)` добавлены отдельные ветки:
  - `service === 'nano2'`
  - `service === 'seedream'`

- В обработчике `photo:set:*` добавлено сохранение новых параметров:
  - `nanoModel`, `nanoResolution`, `seedreamModel`, `seedreamResolution`.

- В `tips` добавлены инструкции для Nano/Seedream и `nano2_prompts`.

### Callback-схема (новые ключи)
- `photo:set:nano2:nanoModel:nano2|nanopro`
- `photo:set:nano2:nanoResolution:1k|2k`
- `photo:instruction:nano2_prompts`
- `photo:set:seedream:seedreamModel:seedream45|seedream5`
- `photo:set:seedream:seedreamResolution:2k|3k`
- `photo:set:seedream:ratio:1_1|9_16|16_9|3_4|4_3`

### Примечание для кодера
Пока это UI/FSM-уровень (кнопки + состояние + тексты). Для полной прод-связки осталось:
- пробросить новые prefs в реальные provider payloads;
- добавить e2e автопроверку `/photo` по всем 5 карточкам.

### PATCH 2026-03-11 14:20 — FLUX 2 layout sync с референсом

Синхронизирован экран FLUX 2 под мобильный референс:
- в строке моделей добавлен отдельный тумблер `✅ FLUX 2` (рядом с `FLUX 2 [Max]`);
- нижний ряд кнопок приведён к виду: `← Назад` + `🌱 Добавить seed`;
- промежуточная кнопка `📌 Инструкция` для FLUX-экрана убрана из карточки (осталась в других сервисах).

Кодовые изменения:
- `ensureImagePrefs`: добавлено поле `fluxEnabled: true`.
- `serviceKeyboard('flux2')`: обновлён layout (Max + FLUX2 toggle, нижний ряд Back/Seed).
- `photo:set:*`: добавлено поле `fluxEnabled`.

## PATCH 2026-03-11 18:19 — Hailuo video card synced to reference UI

Обновлена ветка `/video -> Hailuo` под референсный экран.

### Новый UX Hailuo
Текст карточки:
- «Вы создаете видео с помощью сервиса Hailuo. Задайте параметры…»
- шаги: промпт -> (опц.) изображение -> модель/длительность/разрешение -> опция «Улучшить промпт».
- статусные строки:
  - `📝 Текущий промпт: не указан`
  - `🖼️ Изображение: не добавлено`

### Кнопки Hailuo
- верхний ряд: `Промпт`, `Изображение`
- модель: `Hailuo 2.3 Fast`, `Hailuo 2.3`, `Hailuo 02`
- параметры: `5 сек.`, `10 сек.`, `768P`, `1080P`
- опция: `Улучшить промпт` (toggle)
- действия: `← Назад`, `🎬 Начать генерацию`

### Callback schema
- `video:set:hailuo:hasPrompt:1`
- `video:set:hailuo:hasFrames:1`
- `video:set:hailuo:hailuoModel:hailuo23_fast|hailuo23|hailuo02`
- `video:set:hailuo:duration:5|10`
- `video:set:hailuo:hailuoResolution:768p|1080p`
- `video:set:hailuo:hailuoEnhancePrompt:1` (toggle)
- `video:start:hailuo`

### Изменения в коде
Файл: `marfa-ai/src/commands/registerCommands.js`
- `ensureVideoPrefs`: добавлены `hailuoModel`, `hailuoResolution`, `hailuoEnhancePrompt`.
- `videoConfigKeyboard`: отдельная ветка `service === 'hailuo'` с кастомным layout.
- `video:service:*`: для `hailuo` отдельный текст карточки.
- `video:set:*`: добавлена обработка полей `hailuoModel`, `hailuoResolution`, `hailuoEnhancePrompt`.

## PATCH 2026-03-11 18:22 — Kling card synced to reference UI

Синхронизирована ветка `/video -> Kling` под референс-экран.

### UX/текст
Карточка Kling теперь содержит шаги:
1) Промпт
2) (Опц.) изображение как основа
3) Длительность 5/10 сек + формат 1:1 / 16:9 / 9:16

Статусы:
- `📝 Текущий промпт: не указан`
- `🖼️ Изображение: не добавлено`

### Кнопки Kling
- `Промпт`, `Изображение`
- `Со звуком` (toggle)
- `5 сек.`, `10 сек.`
- Версия: `3.0 🆕`, `2.6`, `01`, `2.5 Turbo`
- Формат: `1:1`, `16:9`, `9:16`
- `← Назад`, `🎬 Начать генерацию`

### Callback schema
- `video:set:kling:hasPrompt:1`
- `video:set:kling:hasFrames:1`
- `video:set:kling:klingWithSound:1` (toggle)
- `video:set:kling:klingDuration:5|10`
- `video:set:kling:klingVersion:3.0|2.6|01|2.5-turbo`
- `video:set:kling:klingAspect:1:1|16:9|9:16`
- `video:start:kling`

### Кодовые изменения
Файл: `marfa-ai/src/commands/registerCommands.js`
- `ensureVideoPrefs`: добавлены `klingWithSound`, `klingDuration`, `klingVersion`, `klingAspect`.
- `videoConfigKeyboard`: добавлена отдельная ветка `service === 'kling'`.
- `video:service:*`: отдельный текст карточки для Kling.
- `video:set:*`: добавлена обработка `kling*` полей.

## PATCH 2026-03-11 18:26 — Pika 2.5 + Seedance 1.5 Pro synced to reference UI

### 1) /video -> Pika 2.5
Карточка и кнопки синхронизированы:
- текст сценария (промпт + 1-2 изображения + выбор длительности/разрешения/формата);
- статусы: `Текущий промпт: не указан`, `Изображение: не добавлено`.

Кнопки:
- `Промпт`, `Изображение`
- `5 секунд`, `10 секунд`
- `720p`, `1080p`
- `1:1`, `16:9`, `9:16`
- `← Назад`, `🎬 Начать генерацию`

Callbacks:
- `video:set:pika:hasPrompt:1`
- `video:set:pika:hasFrames:1`
- `video:set:pika:pikaDuration:5|10`
- `video:set:pika:pikaResolution:720p|1080p`
- `video:set:pika:pikaAspect:1:1|16:9|9:16`
- `video:start:pika`

### 2) /video -> Seedance 1.5 Pro
Карточка и кнопки синхронизированы:
- текст с 4 шагами + пояснение про фиксированную камеру;
- статусы: `Текущий промпт: не задан`, `Изображение: не добавлено`.

Кнопки:
- `Промпт`, `Изображения`
- aspect: `a`, `1:1`, `9:16`, `16:9`, `4:3`, `3:4`, `21:9`
- `720p`, `1080p`
- `4 сек.`, `8 сек.`, `12 сек.`
- toggles: `Фикс. камера`, `Аудио`
- `← Назад`, `🎬 Начать генерацию`

Callbacks:
- `video:set:seedance:hasPrompt:1`
- `video:set:seedance:hasFrames:1`
- `video:set:seedance:seedanceAspect:auto|1:1|9:16|16:9|4:3|3:4|21:9`
- `video:set:seedance:seedanceResolution:720p|1080p`
- `video:set:seedance:seedanceDuration:4|8|12`
- `video:set:seedance:seedanceFixedCamera:1` (toggle)
- `video:set:seedance:seedanceAudio:1` (toggle)
- `video:start:seedance`

### Код (главное)
Файл: `marfa-ai/src/commands/registerCommands.js`
- `ensureVideoPrefs`: добавлены pika/seedance поля состояния.
- `videoConfigKeyboard`: добавлены ветки `service === 'pika'` и `service === 'seedance'`.
- `video:service:*`: обновлены тексты карточек Pika/Seedance.
- `video:set:*`: добавлена обработка `pika*` и `seedance*` полей.

## PATCH 2026-03-11 18:28 — Интернет-поиск (/s) synced to reference UI

Синхронизирована ветка `/s` (поиск с интернетом) под референсный экран.

### UX
Текст экрана поиска:
- `Выберите модель поиска или оставьте выбранную модель по умолчанию`
- `Чтобы начать поиск, отправьте в чат ваш запрос 👇`

Inline-кнопки:
- `Gemini 3.1 Flash`
- `Gemini 3.1 Pro`
- `Perplexity`
- `Закрыть`

У выбранной модели показывается `✅`.

### Логика
- В состоянии пользователя хранится `searchModelKey`.
- `/s` открывает экран выбора и автоматически применяет выбранную search-модель в `currentModelKey`.
- При нажатии на модель:
  - обновляется `searchModelKey`;
  - обновляется `currentModelKey`;
  - экран перерисовывается с новым `✅`.
- `Закрыть` закрывает экран поиска.

### Callback schema
- `search:set:gemini`
- `search:set:gemini_pro`
- `search:set:perplexity`
- `search:close`

### Изменения в коде
1) `marfa-ai/src/config/models.js`
- Добавлена модель:
  - `gemini_pro` -> `google/gemini-3.1-pro`
- Переименован label `gemini` в `Gemini 3.1 Flash`.

2) `marfa-ai/src/commands/registerCommands.js`
- Добавлен helper `searchKeyboard(state)`.
- Команда `/s` переведена на экран выбора поисковой модели (вместо жёсткого `perplexity`).
- Добавлены обработчики:
  - `bot.action('search:close', ...)`
  - `bot.action(/search:set:(.+)/, ...)`

3) `marfa-ai/src/index.js`
- Кнопка reply-keyboard `🔎 Интернет-поиск` теперь вызывает `/s` (а не мгновенно форсит Perplexity).

## PATCH 2026-03-11 18:31 — /settings: «Выбор модели» ведёт на расширенный экран моделей

Сделано по референсу: в `/settings` пункт **«Выбор модели»** теперь открывает список доступных моделей в стиле экрана `/model`.

### 1) Экран `/settings`
Добавлен полноценный settings-экран с кнопками:
- `Выбор модели`
- `Описание роли`
- `✅/⬜️ Поддержка контекста` (toggle)
- `Голосовые ответы`
- `Язык интерфейса`
- `Закрыть`

Текст блока соответствует референсной структуре (5 пунктов настроек).

### 2) Экран выбора модели (из `/settings` и `/model`)
Список моделей приведён к референсу:
- GPT-5.4
- OpenAI o3
- GPT-4.1
- GPT-5 mini
- GPT-4o mini
- Claude 4.6 Sonnet
- Claude 4.6 Thinking
- DeepSeek-V3.2
- DeepSeek-V3.2 Thinking
- Gemini 3.1 Pro
- Gemini 3.1 Flash

Плюс кнопка `← Назад` (возврат в settings).

У выбранной модели показывается `✅` в inline-кнопке.

### 3) Callback / state
Новые callbacks settings:
- `settings:model`
- `settings:context`
- `settings:role`
- `settings:voice`
- `settings:lang`
- `settings:back`
- `settings:close`

Модели:
- `model:set:gpt54|o3|gpt41|gpt5mini|gpt4omini|claude46sonnet|claude46thinking|deepseekv32|deepseekv32thinking|gemini31pro|gemini31flash`

Логика:
- выбор модели меняет `state.currentModelKey`;
- клавиатура перерисовывается, чтобы показывать актуальный `✅`.

### 4) Кодовые изменения
1. `marfa-ai/src/commands/registerCommands.js`
- добавлены helper-функции:
  - `settingsKeyboard(state)`
  - `modelPickerKeyboard(state)`
  - `modelPickerText`
- `/settings` теперь открывает полноценный экран настроек;
- `/model` показывает расширенный экран моделей;
- добавлены action-обработчики для settings;
- обновлён `model:set:*`: теперь обновляет выбор прямо в inline-клавиатуре.

2. `marfa-ai/src/config/models.js`
- добавлены ключи моделей для расширенного picker-экрана:
  - `gpt54`, `o3`, `gpt41`, `gpt5mini`, `gpt4omini`,
  - `claude46sonnet`, `claude46thinking`,
  - `deepseekv32`, `deepseekv32thinking`,
  - `gemini31pro`, `gemini31flash`.
- сохранены alias-модели для совместимости с существующими флоу.

3. `marfa-ai/src/storage/memoryStore.js`
- default `currentModelKey` изменён на `gpt4omini`.

## PATCH 2026-03-11 18:36 — /settings: экран «Роль» + включение/выключение поддержки роли

Реализована роль exactly по референсу:

### UX
При нажатии `Описание роли` (в settings) открывается отдельный экран:
- текст: возможность задать роль/инструкцию;
- строка: `Текущая роль: ...` (`не установлена`, если пусто);
- кнопки:
  - `Задать роль`
  - `✅/❌ Поддержка роли` (toggle)
  - `← Назад`

### Логика
1. `Задать роль`
- бот просит прислать текст роли (пример: «отвечай только на русском»);
- следующий текст пользователя сохраняется в `state.roleInstruction`.

2. `Поддержка роли`
- переключает `state.roleEnabled`;
- при включении кнопка показывает `✅ Поддержка роли`;
- при выключении — `❌ Поддержка роли`.

3. Применение роли к ответам
- в текстовом роутере при `roleEnabled=true` и непустой роли добавляется `system`-сообщение перед историей диалога.

### Callback schema
- `settings:role`
- `settings:role:set`
- `settings:role:toggle`
- `settings:back`

### Изменения в коде
1) `marfa-ai/src/commands/registerCommands.js`
- добавлены:
  - `roleSettingsKeyboard(state)`
  - `roleScreenText(state)`
- добавлены action handlers:
  - `settings:role`
  - `settings:role:set`
  - `settings:role:toggle`

2) `marfa-ai/src/storage/memoryStore.js`
- новые поля state:
  - `roleInstruction`
  - `roleEnabled`
  - `awaitingRoleInput`

3) `marfa-ai/src/index.js`
- в `bot.on('text')` добавлен режим ввода роли:
  - если `awaitingRoleInput=true`, текст сохраняется как роль и НЕ уходит в генерацию.

4) `marfa-ai/src/core/router.js`
- для текстовых моделей добавляется `system`-инструкция из роли (если роль включена).

## PATCH 2026-03-11 18:47 — /deletecontext copy synced to reference

Обновлён текст ответа на `/deletecontext` под референс:
- было: `🧹 Контекст очищен.`
- стало: `Контекст удален. По умолчанию бот в ответе учитывает ваш предыдущий вопрос и свой ответ на него`

Файл: `marfa-ai/src/commands/registerCommands.js`

## PATCH 2026-03-11 18:49 — reply-кнопки выполняют действия сразу (без «Открой /...») 

По запросу UX изменён: нажатие на нижние reply-кнопки сразу выполняет логику, без промежуточного ответа вида «Открой /model».

### Изменено
1) `🪄 Выбрать модель`
- раньше: бот писал «Открой /model»;
- теперь: сразу открывает экран выбора модели (тот же расширенный picker).

2) `🔎 Интернет-поиск`
- раньше: отправлялся текст `/s`;
- теперь: сразу открывается search-экран с выбором модели поиска.

3) `🧹 Очистить контекст`
- раньше: отправлялся текст `/deletecontext`;
- теперь: контекст очищается сразу и выводится итоговый текст подтверждения.

### Технически
Файл: `marfa-ai/src/index.js`
- добавлены helper-функции в runtime:
  - `mark(...)`
  - `modelPickerKeyboard(state)`
  - `searchKeyboard(state)`
- `bot.hears(...)` для соответствующих reply-кнопок переведены на прямую реализацию логики.
- импортирован `clearContext` из `storage/memoryStore`.

## PATCH 2026-03-11 18:50 — авто-удаление «⏳ Марфа AI думает...» после ответа

Изменено поведение typing/progress-сообщения:
- после получения результата бот удаляет служебное сообщение `⏳ Марфа AI думает...`;
- при ошибке также пытается удалить это сообщение, чтобы не оставлять «висящий» индикатор.

### Технически
Файл: `marfa-ai/src/index.js`
- `thinkingMsg = await ctx.reply('⏳ Марфа AI думает...')`
- перед отправкой результата: `ctx.telegram.deleteMessage(ctx.chat.id, thinkingMsg.message_id)` (в safe try/catch)
- в `catch` добавлен такой же safe delete.

## PATCH 2026-03-11 18:57 — Персистентный контекст пользователей (20 сообщений)

По запросу внедрено сохранение контекста пользователей между перезапусками бота.

### Что реализовано
1. Персистентное хранилище состояния пользователей на диске:
- файл: `marfa-ai/data/user-state.json`
- формат: `version`, `updatedAt`, `users{ userId -> state }`

2. Контекст ограничен 20 сообщениями (turns):
- при добавлении нового сообщения старые автоматически обрезаются до последних 20;
- при загрузке с диска также выполняется нормализация до 20.

3. История в генерации берётся до 20 сообщений:
- в пайплайне ответа заменено `getRecentHistory(..., 10)` -> `getRecentHistory(..., 20)`.

4. `/deletecontext` очищает историю и сохраняет это на диск.

### Технические детали
Файл: `marfa-ai/src/storage/memoryStore.js`
- добавлено file-based хранилище (`fs`) с атомарной записью (`.tmp` + `rename`);
- `loadStore()` вызывается при старте модуля;
- `pushTurn()` и `clearContext()` сохраняют state в файл;
- `getRecentHistory()` ограничивает выборку максимум 20.

Файл: `marfa-ai/src/index.js`
- для генерации используется `getRecentHistory(userId, 20)`.

### Важно
Это user-level persistence: после рестартов бота контекст не теряется, пока существует `data/user-state.json`.

## PATCH 2026-03-11 19:15 — Variant A foundation (1000 users, scalable)

Внедрён практичный «small-but-scalable» фундамент без ломки текущего UX.

### Что добавлено

1) **SQLite persistence layer (Postgres-ready domain model)**
Файл: `src/infra/db.js`
- инициализация `data/marfa.db`;
- таблицы:
  - `users(user_id, state_json, updated_at)`
  - `messages(id, user_id, role, content, ts)`
  - `conversations(user_id, summary, updated_at)`
  - `jobs(id, user_id, kind, status, payload_json, result_json, created_at, updated_at)`
  - `usage_ledger(id, user_id, metric_type, amount, meta_json, created_at)`
- включен WAL mode для устойчивости/параллелизма.

2) **Персистентный memory store на БД**
Файл: `src/storage/memoryStore.js`
- user state читается/пишется в `users`;
- история диалога хранится в `messages`;
- контекст ограничен до **20** сообщений (hard cap);
- `clearContext` очищает `messages` пользователя;
- добавлен периодический flush in-memory state в БД (каждые 5с + on exit/signals).

3) **Rate limiting слой (готов к замене на Redis)**
Файл: `src/infra/rateLimit.js`
- базовый limiter для ~1000 пользователей (25 msg / 60 sec на user);
- интегрирован в `src/index.js` перед запуском генерации.

4) **Model router + fallback policy**
Файл: `src/core/modelRouter.js`
- `resolveModel(modelKey)`
- `resolveFallback(modelKey)` (MVP fallback rules)

Интеграция: `src/core/router.js`
- текстовый pipeline использует router;
- при ошибке primary модели пытается fallback модель.

5) **Очередь задач (скелет)**
Файл: `src/jobs/queue.js`
- добавлен `enqueueJob(...)` с записью в таблицу `jobs`.
- это базовая точка для вынесения media-generation в async workers.

6) **Контекст в ответе увеличен до 20**
Файл: `src/index.js`
- `getRecentHistory(userId, 20)`

### Что это даёт уже сейчас
- контекст и user-state сохраняются между рестартами;
- архитектура больше не привязана к RAM-only хранению;
- есть фундамент для горизонтального роста;
- минимальный anti-flood на user-level.

### Что добавить при росте >1000 (без больших переписываний)
- заменить SQLite на Postgres (с теми же таблицами/контрактами);
- заменить in-process limiter на Redis-based;
- вынести `jobs` в отдельный worker-процесс с retry/DLQ;
- добавить summary compaction в `conversations`.

## PATCH 2026-03-11 19:20 — Контекст в settings: ✅ по умолчанию, ❌ при отключении + применение в логике

Сделано по запросу:

1) В `/settings` кнопка контекста теперь отображает:
- `✅ Поддержка контекста` — когда включено (по умолчанию)
- `❌ Поддержка контекста` — когда отключено

2) Контекст применяется на уровне логики выбранной модели:
- при `contextEnabled=true` в text-пайплайн передаются последние 20 сообщений;
- при `contextEnabled=false` в text-пайплайн передаётся пустая история (`[]`), т.е. модель отвечает без учета предыдущего диалога.

### Код
- `src/commands/registerCommands.js`
  - обновлен вид кнопки `settings:context` (`✅/❌`).
- `src/index.js`
  - история для генерации теперь зависит от `state.contextEnabled`:
    - ON -> `getRecentHistory(userId, 20)`
    - OFF -> `[]`

### Поведение по умолчанию
- значение по умолчанию: `contextEnabled = true`.

## PATCH 2026-03-11 19:32 — Профиль: лимит 50/неделя + живое обновление счетчика

Исправлен блок статистики в `/account`:
- раньше было хардкодом `.../100`;
- теперь используется `FREE_WEEKLY_LIMIT` (по умолчанию 50) и корректный расчет использованных запросов.

### Логика
`used = weeklyLimit - requestsLeft` (с clamp в диапазоне `0..weeklyLimit`).

Отображение:
- `Запросов в неделе: {used}/{weeklyLimit}`

### Файл
- `marfa-ai/src/utils/format.js`

Примечание: счетчик уже обновляется при каждом запросе (`state.requestsLeft -= 1`), теперь корректно показывается и в профиле.

## RESEARCH 2026-03-12 — соответствие Marfa функциям агрегаторов (OpenRouter / FAL / GoAPI)

Провёл ресерч по доступности моделей и сопоставил с текущей логикой Marfa.

### Источники (проверено сейчас)
- OpenRouter: `https://openrouter.ai/api/v1/models` (живой список id)
- GoAPI docs:
  - `https://goapi.ai/docs/overview`
  - `https://goapi.ai/docs/midjourney-api`
  - `https://goapi.ai/docs/kling-api/create-task`
- FAL model pages:
  - `https://fal.ai/models/fal-ai/flux/dev`
  - `https://fal.ai/models/fal-ai/flux/schnell`
  - `https://fal.ai/models/fal-ai/veo3`

---

### Таблица соответствия функций Marfa к агрегаторам

| Функция Marfa | UI/команда | Выбранная модель/сервис | Агрегатор | Статус доступности | Статус в коде Marfa |
|---|---|---|---|---|---|
| Текстовые ответы | обычный текст, /model | GPT/Claude/Gemini/DeepSeek/Perplexity семейства | **OpenRouter** | ✅ подтверждено через `/api/v1/models` для id: `openai/gpt-5.4`, `openai/o3`, `openai/gpt-4.1`, `openai/gpt-5-mini`, `openai/gpt-4o-mini`, `anthropic/claude-sonnet-4.6`, `google/gemini-3.1-flash-lite-preview`, `deepseek/deepseek-v3.2`, `perplexity/sonar` | ✅ используется в `providers/openrouter.js` |
| Текстовые ответы (Gemini Pro) | /model, /s | `google/gemini-3.1-pro` | **OpenRouter** | ⚠️ в live-каталоге обнаружен как `google/gemini-3.1-pro-preview` / `...-customtools`, а не точный `google/gemini-3.1-pro` | ⚠️ нужен id-sync в `config/models.js` |
| Интернет-поиск | /s | Gemini Flash / Gemini Pro / Perplexity | **OpenRouter** | ✅ модели есть (с оговоркой по Gemini Pro id) | ✅ работает через current text model |
| Midjourney изображения | /photo -> Midjourney | `midjourney-v7` | **GoAPI** | ✅ docs есть (`/docs/midjourney-api`, endpoint `mj/v2/imagine`) | ✅ реализовано в `providers/goapi.js` |
| Seedream изображения | /photo -> Seedream | (через goapi image-task) | **GoAPI** | ⚠️ прямой endpoint не зафиксирован в проверенных ссылках; вероятно через `/api/v1/task` | ⚠️ UI/FSM есть, backend пока routed как Midjourney path |
| GPT Image / Nano Banana (image UI) | /photo -> GPT Images / Nano Banana | (OpenAI/Google image backends) | **GoAPI / OpenRouter / отдельный** | ⚠️ в текущем ресерче подтверждены только общие task-flow GoAPI и text в OpenRouter | ⚠️ в коде пока привязано к `flux` (fallback-реализация), требуется отдельная прод-интеграция |
| FLUX изображения | /photo -> FLUX 2 | `fal-ai/flux/dev` (+варианты schnell/pro при расширении) | **FAL** | ✅ `fal-ai/flux/dev` и `fal-ai/flux/schnell` подтверждены | ✅ базовый Flux pipeline реализован |
| Veo видео | /video -> Veo 3.1 | `veo31` (GoAPI path) | **GoAPI** (текущий код) / **FAL** (есть `fal-ai/veo3`) | ⚠️ GoAPI direct doc path для `veo31` не найден в этой сессии; FAL Veo3 подтвержден | ⚠️ в коде сейчас video-goapi как queued stub |
| Sora видео | /video -> Sora | `sora2` | **GoAPI** | ⚠️ прямой doc endpoint в проверке не найден | ⚠️ в коде queued stub |
| Kling видео | /video -> Kling / Motion / Effects | `kling` task | **GoAPI** | ✅ docs есть (`/docs/kling-api/create-task`, task_type video/effects/lip_sync) | ⚠️ UI/FSM + параметры есть, backend generation пока queued stub |
| Seedance видео | /video -> Seedance | seedance | **GoAPI** | ⚠️ прямой doc path в этой проверке не найден | ⚠️ UI/FSM есть, backend queued stub |
| Hailuo видео | /video -> Hailuo | hailuo | **GoAPI** | ⚠️ прямой doc path в этой проверке не найден | ⚠️ UI/FSM есть, backend queued stub |
| Pika видео | /video -> Pika / Effects | pika | **GoAPI** | ⚠️ прямой doc path в этой проверке не найден | ⚠️ UI/FSM есть, backend queued stub |
| Suno музыка | /suno | suno | **GoAPI** | ⚠️ в overview упоминается Suno, но конкретный endpoint в проверке не зафиксирован | ⚠️ в коде queued stub |

---

### Ключевой вывод
1. **Text stack (OpenRouter) — рабочий и подтверждённый.**
2. **Image stack:** Midjourney и FLUX подтверждены; часть image UI (GPT Image / Nano Banana / Seedream) пока требует backend-уточнения endpoint’ов.
3. **Video/music stack:** UI и state-machine детально готовы, но часть генерации пока намеренно в `queued`-заглушках до фиксирования точных endpoint-ов GoAPI.

### Что нужно сделать дальше (короткий тех-план)
1. Привести id Gemini Pro к актуальному OpenRouter id (`...pro-preview` или актуальный prod id).
2. Для каждого видео/музыка сервиса в `providers/goapi.js` подключить конкретные endpoint'ы и payload.
3. Обновить эту таблицу после каждого подключенного endpoint'а (статус ⚠️ -> ✅).

## PATCH 2026-03-12 11:01 — Gloucestershire-маршруты (plug-and-play) для OpenRouter / FAL / GoAPI

По запросу добавлен единый манифест маршрутов, чтобы оставалось подставить только API-ключи и account-параметры.

### Новый файл
- `marfa-ai/src/config/aggregatorRoutes.js`

### Что внутри
1) **OpenRouter**
- базовый маршрут:
  - `POST /chat/completions`
- маппинг текстовых моделей Marfa -> `providerModelId`.
- зафиксированы заголовки (`HTTP-Referer`, `X-Title`) и auth-паттерн.

2) **FAL**
- маршруты для FLUX:
  - `POST /fal-ai/flux/dev`
  - `POST /fal-ai/flux/schnell`
  - `POST /fal-ai/flux-pro` (опц.)
- заготовка для Veo3 через FAL:
  - `POST /fal-ai/veo3`

3) **GoAPI**
- подтвержденный Midjourney route:
  - `POST /mj/v2/imagine`
- универсальный route:
  - `POST /api/v1/task` (generic task orchestration)
- Kling documented family через task endpoint (`model: kling`, `task_type: video_generation|effects|...`).

4) **Function map (Marfa -> Aggregator route)**
- Для каждой функции Marfa прописан целевой агрегаторный маршрут и базовый `model/task_type`:
  - image: midjourney / seedream / gpt-images / nano-banana / flux
  - video: veo31 / sora2 / seedance / hailuo / pika / kling
  - music: suno

### Практический смысл
- это «маршрутная карта» для кодера: где именно дергать endpointы;
- остается подставить `OPENROUTER_API_KEY`, `FAL_KEY`, `GOAPI_API_KEY` и довести payload-специфику по каждому task_type.

### Нюанс по Gemini 3.1 Pro
- в манифесте зафиксирован id `google/gemini-3.1-pro-preview` как безопасный route-кандидат;
- перед продом проверить актуальный OpenRouter id и синхронизировать с `config/models.js`.

## PATCH 2026-03-12 11:23 — Экономика Marfa (startup preset) внедрена в код

По запросу внедрен рабочий пресет экономики для стадии 0–1000 пользователей: максимум полезности на free и контроль себестоимости.

### 1) Model Router по плану (free/premium)
Файл: `src/core/modelRouter.js`
- добавлен `FREE_ALLOWED` whitelist для free-плана;
- `resolveModelForPlan(modelKey, isPremium)`:
  - если free выбрал дорогую модель -> автопереход на `gpt4omini`;
- `maxOutputTokensForPlan()`:
  - free: `400`
  - premium: `1200`
- расширен fallback policy.

### 2) Ограничение по output tokens
Файлы:
- `src/providers/openrouter.js`
- `src/core/router.js`

Сделано:
- `generateText(...)` теперь принимает `maxTokens` и передает `max_tokens` в OpenRouter.
- В роутере для текста лимит выбирается по плану пользователя.

### 3) Кэш повторяемых текстовых запросов
Файлы:
- `src/infra/db.js` (новая таблица `response_cache`)
- `src/infra/cache.js` (новый модуль)
- `src/core/router.js` (интеграция)

Сделано:
- SHA-256 cache key (нормализованный prompt + model + флаги контекста/роли);
- cache hit для коротких типовых запросов;
- TTL:
  - success: 24h
  - fallback success: 6h
- авто-cleanup expired entries каждые 10 минут.

### 4) Anti-abuse и дневные лимиты
Файл: `src/index.js`
- сохраняется существующий minute rate-limit (`25/min`).
- добавлены дневные лимиты:
  - free (обычный): `120/day`
  - new users (<48h): `20/day`
  - premium: `1000/day`
- счетчик дня (`dayKey/dayCount`) сбрасывается автоматически при смене даты.

### 5) Персистентное состояние для экономики
Файл: `src/storage/memoryStore.js`
- default state дополнен:
  - `isPremium`
  - `createdAt`
  - `dayKey`
  - `dayCount`
- состояние периодически flush в БД и сохраняется при ключевых изменениях.

### 6) Связь с текущей юнит-экономикой Marfa
После патча Marfa уже умеет:
- не пускать free-трафик в дорогие модели автоматически;
- держать короткий бесплатный output (token cap);
- экономить на повторах через cache;
- ограничивать абуз на уровне минуты и дня;
- хранить данные для дальнейшего биллинга/конверсии.

### Что осталось (следующий шаг)
1. Вынести медиа-heavy задачи в async jobs (`jobs` table + worker).
2. Добавить реальный paid flag из billing flow (`isPremium=true` через webhook/админ-операцию).
3. Добавить cost метрики в `usage_ledger` по каждому ответу (ориентировочная стоимость по модели).

## PATCH 2026-03-12 12:49 — FLUX полностью убран + production route matrix locked

По запросу выполнено:
- FLUX полностью удален из пользовательских функций Marfa;
- Midjourney не трогали;
- закреплена каноническая маршрутная матрица;
- убраны дубли/лишние маршруты из route-манифеста.

### 1) FLUX убран полностью из Marfa (UI + модель + роутинг)

Изменения:
- `src/config/menu.js`
  - удалена кнопка `FLUX 2` из `/photo`.
- `src/config/models.js`
  - удалена модель `flux`.
- `src/core/router.js`
  - удален импорт `providers/fal.js` и все ветки вызова Flux;
  - image-пайплайн теперь идет через GoAPI image route (Midjourney path).
- `src/commands/registerCommands.js`
  - удалены `photo:service:flux2`/`photo:set:flux2:*` и соответствующие тексты/инструкции;
  - в текстах `/photo` убрано упоминание FLUX;
  - удален `photo:seed` flow, связанный с FLUX.
- `src/index.js`
  - обновлен текст меню изображений без FLUX.

### 2) Каноническая matrix маршрутов закреплена (point #1)

`src/config/aggregatorRoutes.js` переписан как LOCKED production matrix:
- Text/Search -> **OpenRouter**
- Image/Video/Music -> **GoAPI**

### 3) Убраны дубли и лишние маршруты (point #2)

В route manifest удалено:
- отдельный блок `fal`;
- дублирующая маршрутизация, которая пересекалась с целевой production-схемой.

Оставлены только боевые каналы и functionMap для каждой функции Marfa.

### 4) Документация с финальной матрицей обновлена (point #3)

Этот патч фиксирует final routing state для кодера:
- какую функцию в какой агрегатор отправлять,
- какие endpoint'ы использовать,
- где подставлять только API-ключи.

## PATCH 2026-03-12 13:38 — Недельные лимиты: free 25, premium 50 + авто-сброс по неделям

По запросу изменена лимитная логика:

### Новые недельные лимиты
- Free: **25 запросов / неделя** (по умолчанию)
- Premium: **50 запросов / неделя** (по умолчанию)

(переопределяются env-переменными: `FREE_WEEKLY_LIMIT`, `PREMIUM_WEEKLY_LIMIT`)

### Что происходит при исчерпании free-лимита
Показывается сообщение:
`❌ Бесплатные запросы исчерпаны. Подождите до следующей недели или подключите /premium (до 50 запросов в неделю).`

### Логика недельного отсчёта (в коде)
- Добавлен ISO week key (`YYYY-Www`) в runtime.
- На каждом текстовом запросе:
  1) вычисляется текущая неделя,
  2) определяется актуальный недельный лимит по плану (`isPremium`),
  3) если неделя сменилась (или сменился план) — лимит автоматически сбрасывается.

### Состояние пользователя
В state сохраняются поля:
- `weeklyLimit`
- `weekKey`
- `requestsLeft`

### Обновления в профиле
`/account` теперь показывает расход относительно текущего планового недельного лимита пользователя (free/premium), а не по жесткому хардкоду.

### Файлы
- `src/index.js` — weekly reset + сообщение при исчерпании
- `src/storage/memoryStore.js` — дефолт weekly лимитов (25/50)
- `src/utils/format.js` — корректный вывод статистики для текущего weeklyLimit

## PATCH 2026-03-12 17:50 — функции Marfa подогнаны под OpenRouter Quickstart + GoAPI Overview

Выполнена подгонка логики функций под документированные паттерны:
- OpenRouter: `POST /api/v1/chat/completions`
- GoAPI: `POST /api/v1/task` + `POST /mj/v2/imagine` для Midjourney

### 1) Image-функции: формат/ratio и сервисные маршруты
Файл: `src/providers/goapi.js`
- Добавлен `generateImageGoapi({ service, prompt, prefs })`.
- Добавлена нормализация ratio из UI (`1_1`, `9_16`, `16_9`...) в формат GoAPI (`1:1`, `9:16`, `16:9`).
- Маршрутизация:
  - Midjourney -> `POST /mj/v2/imagine` (aspect_ratio/process_mode)
  - Seedream/Nano/GPT-image/Faceswap/Upscale -> `POST /api/v1/task` с model/task_type и input.

### 2) Video-функции: сервис-специфичные task payloads
Файл: `src/providers/goapi.js`
- `generateVideoGoapi({ service, prompt, prefs })`:
  - Kling, Seedance, Hailuo, Pika, Sora, Veo, Grok-video
  - единый `POST /api/v1/task` с нужными полями (duration/aspect/version/resolution/audio и т.д.)

### 3) Music-функция
Файл: `src/providers/goapi.js`
- `generateMusic(prompt, prefs)` -> `POST /api/v1/task` (`model: suno`, `task_type: song_generation`)

### 4) Router: привязка к активному UI-сервису
Файл: `src/core/router.js`
- image path теперь вызывает `generateImageGoapi(...)` и берет:
  - `state.activeImageService`
  - `state.imagePrefs[service]`
- video path теперь вызывает `generateVideoGoapi(...)` и берет:
  - `state.activeVideoService`
  - `state.videoPrefs[service]`
- music path использует `state.musicPrefs`.

### 5) Команды/UI: сохраняется активный сервис
Файл: `src/commands/registerCommands.js`
- При `/photo` устанавливается дефолт `activeImageService=midjourney`.
- При `/video` устанавливается дефолт `activeVideoService=veo31`.
- В `photo:service:*` и `photo:set:*` сохраняется `activeImageService`.
- В `video:service:*` сохраняется `activeVideoService`.
- В `/suno` инициализируется `musicPrefs`.

### Итог
- Каждая функция Marfa теперь отправляется в соответствующий маршрут OpenRouter/GoAPI с форматом параметров ближе к документации.
- Для image/video выбор формата (ratio/duration/resolution/version) из UI реально пробрасывается в payload.

## PATCH 2026-03-12 17:50 (v2) — доводка функций под OpenRouter Quickstart + GoAPI Overview

Дополнительная доводка после первичной интеграции:

### Router binding by active service
- `src/core/router.js`:
  - image path теперь использует `state.activeImageService` + `state.imagePrefs[service]`;
  - video path теперь использует `state.activeVideoService` + `state.videoPrefs[service]`;
  - music path передает `state.musicPrefs`.

Это устраняет прежнюю проблему, когда все image/video запросы могли уходить в один и тот же generic path независимо от UI-выбора.

### GoAPI provider alignment
- `src/providers/goapi.js`:
  - добавлен `createTask(model, task_type, input, config)` в формате `POST /api/v1/task` (по overview);
  - Midjourney оставлен на `POST /mj/v2/imagine`;
  - добавен маппинг image services (`midjourney`, `seedream`, `gpt-image`, `gemini-image`, `faceswap`, `upscale`);
  - добавен маппинг video services (`veo31`, `sora2`, `kling`, `seedance`, `hailuo`, `pika`, `grok-video`);
  - для music используется `model: suno`, `task_type: song_generation`.

### Image format normalization
- Добавлена нормализация ratio `1_1` -> `1:1` и т.д. для payload в GoAPI.

### UI command defaults
- `src/commands/registerCommands.js`:
  - `/photo` выставляет `activeImageService=midjourney` по умолчанию;
  - `/video` выставляет `activeVideoService=veo31` по умолчанию;
  - `photo:service:*`, `photo:set:*`, `video:service:*` обновляют active service в state.

### Runtime status
- сервис перезапущен: `running`, `last exit code = 0`.

## PATCH 2026-03-12 17:54 — Telegram Stars оплата премиума

Подключена оплата Premium через Telegram Stars (XTR) по документации Telegram Payments.

### Что добавлено

1) Выставление инвойса в Stars
- `src/commands/registerCommands.js`:
  - `/premium` теперь отправляет invoice с `currency: 'XTR'`.
- `src/index.js`:
  - кнопка `🚀 Премиум` из reply-клавиатуры также отправляет invoice.

Параметры инвойса:
- `provider_token: ''` (режим Telegram Stars)
- `currency: 'XTR'`
- `prices: [{ label, amount }]`
- сумма берётся из env: `TG_PREMIUM_STARS` (default `199`)

2) Pre-checkout обработка
- `src/index.js`:
  - `bot.on('pre_checkout_query', ...)` -> `answerPreCheckoutQuery(true)`

3) Подтверждение успешной оплаты
- `src/index.js`:
  - обработчик `bot.on('message', ...)` для `successful_payment`
  - валидация `invoice_payload` префикса `premium_` и `currency === 'XTR'`
  - активация premium в state:
    - `isPremium = true`
    - `weeklyLimit = PREMIUM_WEEKLY_LIMIT` (default 50)
    - `requestsLeft` повышается минимум до premium weekly лимита
  - отправляется подтверждение пользователю.

4) Профиль
- `src/utils/format.js`:
  - строка подписки в `/account` теперь динамическая:
    - `бесплатная ✅` / `Премиум 🚀`

### Env
Добавлен используемый параметр:
- `TG_PREMIUM_STARS` — цена премиума в Stars (integer).

### Статус
- сервис перезапущен, `running`, `last exit code = 0`.

## PATCH 2026-03-12 18:11 — видео-меню сокращено до 5 сервисов + endpoint check

По запросу в `/video` оставлены только сервисы:
- Veo 3.1
- Sora Video
- Hailuo
- Kling AI
- Pika 2.5

Удалены из UI-меню видео:
- Grok Imagine
- Seedance
- Kling Motion
- Kling Effects
- Pika Effects

### Изменения в UI/текстах
Файлы:
- `src/config/menu.js`
- `src/commands/registerCommands.js`
- `src/index.js`

Обновлены:
- inline keyboard `/video`
- текст карточки выбора сервиса в `/video`
- текст возврата `video:back`

### Перепроверка endpoint'ов по документации
Опора на:
- OpenRouter Quickstart: text -> `/api/v1/chat/completions`
- GoAPI Overview: универсальный task endpoint -> `POST /api/v1/task`
- GoAPI Kling docs: `POST /api/v1/task` (model=`kling`, task_type=`video_generation|extend_video|lip_sync|effects`)

#### Текущий route mapping для оставшихся 5 видео-сервисов
- Veo 3.1 -> `POST /api/v1/task` (`model: veo31`, `task_type: video_generation`)
- Sora Video -> `POST /api/v1/task` (`model: sora2`, `task_type: video_generation`)
- Hailuo -> `POST /api/v1/task` (`model: hailuo`, `task_type: video_generation`)
- Kling AI -> `POST /api/v1/task` (`model: kling`, `task_type: video_generation`) — подтверждено отдельной docs-страницей
- Pika 2.5 -> `POST /api/v1/task` (`model: pika`, `task_type: video_generation`)

### Статус
- сервис перезапущен, `running`, `last exit code = 0`.

## PATCH 2026-03-12 18:16 — Premium модели и планы под бизнес-модель Marfa

Сделана адаптация premium-доступа по референсу (с учетом текущей экономики/функций):

### Тарифы
- Premium: 100 запросов/день
- Premium X2: 200 запросов/день
- Оплата через Telegram Stars:
  - `TG_PREMIUM_STARS` (default 500)
  - `TG_PREMIUM_X2_STARS` (default 750)

### Что изменено в коде

1) `src/commands/registerCommands.js`
- `/premium` теперь показывает 2 тарифа и inline-кнопки оплаты:
  - `premium:buy:premium`
  - `premium:buy:premium_x2`
- `model:set:*`:
  - premium-only модели недоступны free-пользователям (alert)
  - premium модели: `gpt54`, `gpt41`, `o3`, `claude46sonnet`, `claude46thinking`, `gemini31pro`
- `search:set:gemini_pro` также ограничен Premium.

2) `src/index.js`
- кнопка `🚀 Премиум` из reply-клавиатуры показывает 2 тарифа.
- `successful_payment`:
  - распознает `premium_...` и `premium_x2_...` payload,
  - устанавливает `state.isPremium=true`,
  - устанавливает `state.premiumTier` (`premium`/`premium_x2`),
  - подтверждает пользователю активированный план.
- дневной лимит теперь:
  - free: прежняя логика,
  - premium: 100,
  - premium_x2: 200.

3) `src/storage/memoryStore.js`
- добавлено поле `premiumTier` в state (default `free`).

4) `src/utils/format.js`
- профиль показывает текущий tier (`бесплатная / Премиум / Премиум X2`),
- дневной лимит и premium-описание обновлены под новую бизнес-модель.

### Статус
- сервис перезапущен, `running`, `last exit code = 0`.

## PATCH 2026-03-12 19:51 — admin allowlist: премиум по дефолту

По запросу добавлен admin allowlist с автопремиумом.

### Что реализовано
Файл: `src/storage/memoryStore.js`

- Добавлен `ADMIN_IDS`:
  - фиксированно включен `95027564`
  - + расширение через env: `MARFA_ADMIN_IDS` (comma-separated)

- Добавлен `applyAdminDefaults(userId, state)`:
  - для админов автоматически:
    - `isPremium = true`
    - `premiumTier = 'premium_x2'` (если ранее был free)
    - `weeklyLimit = PREMIUM_WEEKLY_LIMIT`
    - `requestsLeft` повышается минимум до weekly premium лимита

- `getUserState(...)` и `persistUser(...)` теперь применяют admin defaults.

### Результат
Для админов из allowlist premium активен по умолчанию и сохраняется автоматически.

## PATCH 2026-03-12 18:16 (v2) — video: 5 сервисов + endpoint capability handling

Дополнение после проверки запросов к GoAPI на текущем ключе:

- Из 5 оставленных сервисов (`veo31`, `sora`, `hailuo`, `kling`, `pika`) на текущем ключе явно принимаются:
  - `kling` + `task_type=video_generation`
  - `hailuo` + `task_type=video_generation`
- Для некоторых сервисов GoAPI возвращает `invalid model` или `invalid task type` (зависит от enabled API service / naming в аккаунте).

### Что сделано в коде

Файл: `src/providers/goapi.js`
- `createTask(...)` теперь не роняет весь пайплайн при 400:
  - `invalid model` / `invalid task type` -> возвращается JSON `status: unavailable` + сообщение провайдера
  - прочие ошибки -> JSON `status: error`
- Midjourney обернут в safe обработку `status:error`.

Файл: `src/index.js`
- Добавлена user-friendly обработка provider-статусов:
  - `status=unavailable` -> понятное сообщение, что сервис недоступен на текущем ключе/плане
  - `status=error` -> показывается текст ошибки провайдера

### Результат
Вместо общего `❌ Ошибка генерации` пользователь получает точную причину (недоступность сервиса или конкретная ошибка API), что упрощает поддержку и настройку GoAPI billing/service permissions.

## HOTFIX 2026-03-12 20:00 — KPI fix: verified GoAPI payloads for video

Проведена реальная валидация запросов against current GoAPI key (через live API), затем код приведен к рабочим payloads.

### Проверено live (успешно, code=200)
1) **Hailuo**
- `model: hailuo`
- `task_type: video_generation`
- `input.model: v2.3 | v2.3-fast`
- `input.duration: 6 | 10`
- `input.resolution: 768 | 1080`
- `config.service_mode: public`

2) **Veo 3.1**
- `model: veo3.1`
- `task_type: veo3.1-video-fast` (или `veo3.1-video`)
- `input.duration: 4s | 6s | 8s`
- `input.aspect_ratio: 16:9 | 9:16`
- `input.resolution: 720p | 1080p`

3) **Kling**
- `model: kling`
- `task_type: video_generation`
- `input.version`, `mode`, `duration`, `aspect_ratio`

4) **Sora2**
- `model: sora2`
- `task_type: sora2-video`
- `input.duration` + `input.aspect_ratio`

### Не проходит на текущем ключе/доках
- **Pika**: `invalid model: pika`

Поэтому Pika оставлен в меню, но в коде возвращает `status=unavailable` с понятным сообщением (вместо падения).

### Кодовые правки
- `src/providers/goapi.js`
  - пересобраны payloads для `veo31`, `sora`, `hailuo`, `kling` по docs;
  - добавлен `service_mode: public` для Hailuo;
  - Pika -> controlled unavailable response;
  - нормальная классификация ошибок (`unavailable` vs `error`).
- `src/commands/registerCommands.js`
  - Hailuo UI приведен к допустимым параметрам docs (6/10 сек, модели v2.3/v2.3-fast).
- `src/index.js`
  - пользовательские сообщения по статусам провайдера (точная причина).

### Итог
- Видеофункции, которые должны работать по KPI сейчас: **Veo 3.1, Sora2, Hailuo, Kling**.
- **Pika** на текущем GoAPI ключе недоступна (ограничение model availability).

## HOTFIX 2026-03-12 20:26 — ETA + авто-доставка результата в Telegram

По запросу добавлено поведение для long-running задач (особенно видео):

1) При создании задачи бот пишет:
- Task ID
- текущий статус
- примерное ETA по сервису (Veo/Sora/Kling/Hailuo/Pika)

2) После этого запускается фоновый polling GoAPI (`GET /api/v1/task/{task_id}`):
- при `completed` -> бот автоматически отправляет результат в Telegram (прямая ссылка)
- при `failed` -> бот отправляет причину ошибки
- при долгой обработке -> уведомление, что задача всё ещё в работе

### Код
- `src/providers/goapi.js`
  - добавлен `getGoApiTask(taskId)`
- `src/index.js`
  - добавлены `etaByService(...)`, `extractOutputUrl(...)`, `pollAndSendResult(...)`
  - в обработке json task response добавлены ETA + фоновые проверки + автодоставка

## HOTFIX 2026-03-13 19:15 — Hailuo v2.3 via PIAPI endpoint

По запросу внедрена схема Hailuo строго по присланной документации PIAPI:

### Request route
- `POST https://api.piapi.ai/api/v1/task`
- payload:
  - `model: hailuo`
  - `task_type: video_generation`
  - `input.model: v2.3 | v2.3-fast`
  - `input.expand_prompt: true|false`
  - `input.duration: 6|10`
  - `input.resolution: 768|1080`
  - `config.service_mode: public`
  - `config.webhook_config` (optional)

### Get task route
- `GET https://api.piapi.ai/api/v1/task/{task_id}`

### Code updates
- `src/providers/goapi.js`
  - добавлен `piapiBaseURL` (`PIAPI_BASE_URL`, default `https://api.piapi.ai`)
  - Hailuo отправляется на PIAPI route c payload v2.3-совместимым
  - `getGoApiTask` теперь проверяет task на PIAPI, затем fallback на GoAPI
- `src/index.js`
  - извлечение результата дополнили `output.video` (как в PIAPI примере)
- `src/commands/registerCommands.js`
  - default duration для Hailuo -> `6`

### Env (optional)
- `PIAPI_BASE_URL=https://api.piapi.ai`
- `PIAPI_WEBHOOK_ENDPOINT=`
- `PIAPI_WEBHOOK_SECRET=`

Сервис перезапущен, статус `running`.
