# 🚨 КУДА ВСТАВЛЯТЬ API-КЛЮЧИ ДЛЯ МАРФЫ

Заполняй **только** файл:

`/Users/clawdbot/.openclaw/workspace/marfa-ai/.env`

## Обязательные ключи

```env
# 1) Telegram BotFather token (сам бот)
TELEGRAM_BOT_TOKEN=PASTE_TELEGRAM_BOT_TOKEN_HERE

# 2) OpenRouter API key (текстовые модели / поиск)
OPENROUTER_API_KEY=PASTE_OPENROUTER_API_KEY_HERE

# 3) GoAPI key (изображения/видео/музыка)
GOAPI_API_KEY=PASTE_GOAPI_API_KEY_HERE
```

## Опционально

```env
# FAL сейчас в production-матрице выключен
FAL_KEY=

OPENROUTER_REFERER=https://example.com
OPENROUTER_TITLE=Marfa AI
DEFAULT_MODEL_KEY=gpt4omini
FREE_WEEKLY_LIMIT=25
PREMIUM_WEEKLY_LIMIT=50
```

## После вставки ключей

1. Сохранить `.env`
2. Перезапустить сервис Марфы
3. Проверить `/start`, `/s`, `/photo`, `/video`, `/suno`

---

⚠️ Не храни ключи в `max_bot.md`, `*.md` документах или в коде `src/*`.
Только в `.env`.
