# Как использовать систему скрапинга Reddit

## Быстрый старт:

1. **Скрапинг** (через MCP или Apify API)
2. **Обработка** (перевод, удаление модераторов)  
3. **Пуш в GitHub** для Pages

## Параметры MCP Apify запросов:

```json
{
  "subreddits": ["ChatGPT"],
  "sort": "top",
  "time": "week",
  "maxItems": 5,        // постов на сабреддит
  "maxComments": 3,     // комментариев на пост
  "maxCommentDepth": 1, // уровень вложенности
  "includeNSFW": false,
  "searchPosts": true,
  "skipComments": false
}
```

**54 сабреддита** - см. `apify_mcp_queries.json`

## Скрипты:

- `get_reddit_posts.py <subreddit>` - выводит запрос для MCP
- `scrape_and_process.py` - обрабатывает JSON (перевод, удаление модераторов, саммери)
- `apify_mcp_queries.json` - список всех сабреддитов для запросов

## Структура JSON:

```json
{
  "posts": [
    {
      "id": "1xxxxxx",
      "title_ru": "Русский заголовок",
      "content_ru": "Русский текст",
      "ai_summary_ru": "Краткое содержание",
      "score": 123
    }
  ]
}
```

## Путь загрузки данных:

- **viewer.html** загружает: `data/{redditId}/{subredditId}/index.json` или `data/{redditId}.json`
- **index.html** читает: `data/categories.json` для навигации

## Автоматизация:

Для cron нужен **Apify API** (MCP не работает в неинтерактивном режиме). См. `AUTOMATION_README.md`.