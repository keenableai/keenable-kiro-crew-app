# Keenable Web Search for Kiro Crew

A Kiro Crew app that gives your agents keyless web search and page reading.

It adds two things:

- **The Keenable MCP server** (`https://api.keenable.ai/mcp-public`, Streamable
  HTTP) with two read-only tools:
  - `search_web_pages`: ranked web results with title, URL and a page-text
    snippet. Optional filters: `site`, `published_after`, `published_before`.
  - `fetch_page_content`: one public page as clean markdown.
- **The `keenable-web-search` skill**, which tells agents when to search, when
  to read a page, and how to cite what they found.

No account or API key is needed.

## What it does not do

The app has no backend, install script, lifecycle hook, cron job, or dashboard
page, so nothing from it runs on your machine. It only declares a remote MCP
server and ships one skill.

Kiro Crew still registers a third-party app's resources only after you trust
that app. Accept the trust prompt when you install, or trust this app alone in
Settings (`agent.apps_trusted`); there is no need to turn on
`agent.apps_allow_third_party` for every app.

## Install

From the Kiro Crew App Store: Apps, Discover, **Keenable Web Search**, Install,
trust the app when asked, then Enable.

From a local clone:

```bash
git clone https://github.com/keenableai/keenable-kiro-crew-app
kirocrew app install "$PWD/keenable-kiro-crew-app"
# trust the app in Settings (or the dashboard prompt), then:
kirocrew app enable keenable
```

When the app is enabled, Kiro Crew registers the server as `keenable:keenable`
in the agent configuration and the skill is available to agents. Disabling or
uninstalling the app removes both.

Ask an agent something that needs the web, for example "What changed in the
latest Python release? Cite your sources."

## Data and limits

- Search queries and fetched URLs are sent to Keenable at `api.keenable.ai`. The
  request carries the header `X-Keenable-Title: kiro-crew` so usage from Kiro Crew
  can be counted. Do not put passwords, tokens, private URLs, or personal data in
  a query.
- The keyless endpoint allows 10 requests per second and 1000 requests per hour
  per IP address.
- Both tools are marked `readOnlyHint: true`. Whether a call needs your approval
  follows your Kiro Crew approval mode, like any other MCP tool.

## Files

```
app.json                          manifest: MCP server, skill, store listing
skills/keenable-web-search/       the agent skill
assets/                           icon, hero images, screenshot
```

## Links

- Keenable MCP server docs: https://docs.keenable.ai/mcp-server
- Kiro Crew App Kit: https://github.com/kirodotdev/KiroCrew/tree/main/docs/app-kit

## License

MIT
