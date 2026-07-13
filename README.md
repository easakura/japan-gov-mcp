# Japan Open Government Data — MCP Servers

Nine MCP servers that give AI agents live access to Japan's official government data: subsidies, laws, parliament records, company registries, weather alerts, corporate filings, statistics, and real-estate prices.

All data comes from **official government APIs** (no scraping), served as **remote MCP servers** — add a URL to your client and go. Free tier included.

## Why

Japan's government publishes a surprising amount of open data through official APIs — but as of mid-2026, almost none of it was reachable from AI agents. English-speaking ecosystems have 20,000+ MCP servers; Japanese public data was a blank spot. These servers fill that gap.

Example (Claude, with the subsidy server connected):

> **User:** Find manufacturing subsidies open for applications in Tokyo, sorted by deadline.
>
> **Claude:** There are 11 currently open. The nearest deadlines: Business Succession & M&A Subsidy (15th round) — up to ¥10M, closes Jul 24. Monozukuri Manufacturing Subsidy (19th round) — up to ¥40M, closes Sep 28. (Each with the official application URL.)

## The servers

| Server | What it does | Data source | Endpoint |
|---|---|---|---|
| **Japan Subsidy Search** | Search open government subsidies & grants: deadlines, amounts, eligibility | jGrants (Digital Agency) | `https://hojokin-mcp.easakura.workers.dev/mcp` |
| **Japan Law Search** | Full-text search across all ~10,000 current laws, down to exact articles | e-Gov Laws API | `https://horei-mcp.easakura.workers.dev/mcp` |
| **Japan Parliament Search** | Search National Diet records, 1947–present | National Diet Library | `https://kokkai-mcp.easakura.workers.dev/mcp` |
| **Japan Company Leads Finder** | Search 1M+ companies by size, capital, location, subsidy history | gBizINFO (METI) | `https://gbiz-leads-mcp.easakura.workers.dev/mcp` |
| **Japan Weather & Alerts** | Forecasts, warnings, earthquake info | Japan Meteorological Agency | `https://tenki-mcp.easakura.workers.dev/mcp` |
| **Japan Address & Geocoding** | Address normalization, postal codes, coordinates | GSI & official registries | `https://jusho-mcp.easakura.workers.dev/mcp` |
| **Japan Corporate Filings** | Securities reports & disclosure filings | EDINET (FSA) | `https://edinet-mcp.easakura.workers.dev/mcp` |
| **Japan Official Statistics** | Population, economy, labor statistics | e-Stat | `https://estat-mcp.easakura.workers.dev/mcp` |
| **Japan Real Estate Prices** | Actual transaction prices & official land values | MLIT Real Estate Library | `https://fudousan-mcp.easakura.workers.dev/mcp` |

## Quick start

**Claude Code** (one command):

```bash
claude mcp add --transport http japan-subsidy https://hojokin-mcp.easakura.workers.dev/mcp
```

**Claude Desktop**: Settings → Connectors → Add custom connector → paste an endpoint URL.

**Any MCP client**: all servers speak Streamable HTTP at `/mcp` and legacy SSE at `/sse`.

The free endpoints are rate-limited to 10 calls/min per IP. For production or commercial use, metered versions ($0.02/tool-call) are on [Apify Store](https://apify.com/e-asakura).

## Where they're listed

- [Official MCP Registry](https://registry.modelcontextprotocol.io) (`io.github.easakura/*`)
- [Glama](https://glama.ai/mcp/servers/easakura/japan-subsidy-search-mcp) · [mcp.so](https://mcp.so/servers/japan-subsidy-search-mcp) · Apify Store

## Source

Implementation repos (TypeScript, Cloudflare Workers + MCP SDK, MIT):
[japan-subsidy-search-mcp](https://github.com/easakura/japan-subsidy-search-mcp) · [japan-law-search-mcp](https://github.com/easakura/japan-law-search-mcp) · [japan-parliament-search-mcp](https://github.com/easakura/japan-parliament-search-mcp) · [japan-company-leads-mcp](https://github.com/easakura/japan-company-leads-mcp)

## Notes on data

- All sources are official, free, public government APIs. Attribution and terms of each source apply.
- Servers return source URLs so agents can cite the primary record (e.g., the exact Diet transcript page or the official subsidy application page).
- 日本語での紹介記事: [Zenn](https://zenn.dev/easakura/articles/japan-gov-data-9-mcp-servers)

---

Built by [Edward Asakura](https://x.com/namonakiconsul). Requests for other Japanese public datasets welcome — open an issue.
