# ayo-plugins-searxng

A SearXNG web search tool plugin for [ayo](https://github.com/alexcabrera/ayo).

## Overview

This plugin provides a `searxng` tool that enables web search through your own SearXNG instance. SearXNG is a privacy-respecting, self-hostable metasearch engine.

## Installation

```bash
ayo plugins install https://github.com/alexcabrera/ayo-plugins-searxng
```

During installation, you'll be prompted to set `searxng` as the default `search` tool.

## Prerequisites

1. **SearXNG Instance**: You need access to a SearXNG instance with JSON API enabled
2. **Environment Variable**: Set `SEARXNG_ENDPOINT` to your instance hostname:
   ```bash
   export SEARXNG_ENDPOINT=search.example.com
   ```

## Usage

### As a Tool

Agents with `allowed_tools: ["searxng"]` can search the web:

```json
{
  "allowed_tools": ["searxng", "bash"]
}
```

### Via Tool Alias

When configured as the default `search` tool, agents can use the generic `search` alias:

```json
{
  "allowed_tools": ["search", "bash"]
}
```

This is resolved to `searxng` at runtime, allowing users to swap search providers without modifying agent configs.

## Configuration

After installation, the plugin registers itself as the default search tool:

```json
// ~/.config/ayo/ayo.json
{
  "default_tools": {
    "search": "searxng"
  }
}
```

## Tool Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `query` | string | Yes | Search query (use + for spaces) |
| `categories` | string | No | Category: general, news, images, videos, science, it, files, social+media, music, map |
| `time_range` | string | No | Time filter: day, week, month, year |
| `language` | string | No | Language code (e.g., 'en', 'de', 'fr') |

## Response Format

Returns JSON from SearXNG:

```json
{
  "query": "your search query",
  "number_of_results": 12345,
  "results": [
    {
      "url": "https://example.com/page",
      "title": "Page Title",
      "content": "Snippet or description text",
      "engine": "google"
    }
  ],
  "suggestions": ["related", "search", "queries"],
  "infoboxes": [...]
}
```

## Self-Hosting SearXNG

If you don't have a SearXNG instance, you can self-host one:

- [SearXNG Documentation](https://docs.searxng.org/)
- [Docker Installation](https://docs.searxng.org/admin/installation-docker.html)

Make sure to enable JSON output in your instance's settings.

## License

MIT
