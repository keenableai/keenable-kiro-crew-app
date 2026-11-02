---
name: keenable-web-search
description: >-
  Search the public web and read web pages with the Keenable MCP tools
  (search_web_pages, fetch_page_content). Load when a task needs facts from the
  web: current documentation, releases, versions, prices, news, people,
  companies, error messages, or anything that may have changed after the
  model's training data, and when the user pastes a URL to read. Triggers
  include "search the web", "look up", "find sources", "latest", "current
  version", "what changed", "read this page", "summarize this URL".
---

# Keenable web search

The Keenable app adds one MCP server with two read-only tools. Both are keyless:
they need no account or API key.

| Tool | Use it for |
|---|---|
| `search_web_pages` | Finding pages. Returns ranked results with title, URL and a snippet of page text. |
| `fetch_page_content` | Reading one page. Returns the page as clean markdown. |

## How to search

1. Start with `search_web_pages`. The snippets usually answer the question; do
   not fetch pages you do not need.
2. For a broad question, run several focused searches instead of one long
   query. Each search is fast, so breadth is cheap.
3. Narrow with the tool's own filters when they fit: `site` for one domain,
   `published_after` / `published_before` (YYYY-MM-DD) for a date window.
   `published_after` is how to ask for recent pages.
4. Use `fetch_page_content` only when the snippets fall short, the user gave you
   a URL, or you need the exact wording of a passage.

## How to answer

- Cite the URL of every page a claim comes from. Do not cite a page you did not
  get from a tool result.
- A snippet is discovery text. Before you rely on a precise number, date, or
  quote, read the page with `fetch_page_content`.
- Say when results disagree or look stale, and give the dates you saw.
- If a tool call fails or returns nothing, say so. Do not fill the gap from
  memory as if it came from the web.

## Limits

- The keyless endpoint allows 10 requests per second and 1000 requests per hour
  per IP address. If a call is rate limited, wait and retry once, then report it.
- Search queries and fetched URLs are sent to Keenable (`api.keenable.ai`). Do not
  put passwords, tokens, private URLs, or personal data in a query.
