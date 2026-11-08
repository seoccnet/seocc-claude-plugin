# SEOcc plugin for Claude

Use your own **SEOcc** (SEO Control Center) installation from Claude. SEOcc is a free, open-source (AGPL-3.0), self-hosted SEO platform that runs on ordinary shared hosting and stores your Google Search Console, Bing, GA4, rank-tracking, competitor, backlink, AI-visibility, local and site-audit data. This plugin connects Claude to SEOcc's MCP server and teaches Claude how to use that data honestly for everyday SEO work.

SEOcc itself: <https://github.com/seoccnet/seo-control-center>

## What you get

| Skill | Command in Claude Code | What it does |
|---|---|---|
| SEOcc guide | `/seocc:seocc-guide` | Ground rules, tool map and scopes. Claude loads it automatically. |
| Connect | `/seocc:connect` | Set up or troubleshoot the connection. |
| Fix first | `/seocc:fix-first` | A prioritised, per-URL fix list from the audit, opportunities and team tasks. |
| Search performance | `/seocc:search-performance` | Weekly or monthly reviews and traffic-drop diagnosis. |
| Opportunities | `/seocc:opportunities` | Prioritised findings, team tasks and outcomes. |
| Article ideas | `/seocc:article-ideas` | What to write next, with predicted traffic and difficulty. |
| Site audit | `/seocc:site-audit` | Technical issues turned into exact per-URL fixes. |
| Content brief | `/seocc:content-brief` | Evidence-based writing plans, saved as SEOcc briefs. |
| Change timeline | `/seocc:change-timeline` | Record live changes and judge whether they worked. |

You can also just ask, for example "What should I fix first on my tomato seed shop?" or "Did the new title on /sunflower-seeds work?", and Claude picks the right skill.

## Requirements

- A running SEOcc installation (version 1.0 or later) reachable over **HTTPS**.
- An SEOcc account that is an owner or admin of the workspace, to create a token.

## Setup

1. In SEOcc, open **Integrations → AI access → New token**. Choose the projects, the read scopes (include **Pages and their SEO evidence**), any write scopes you want (all off by default), and an expiry. Copy the token; it starts with `scc_` and is shown once.
2. Install the plugin.
   - **Claude Code:**
     ```bash
     claude plugin marketplace add seoccnet/seocc-claude-plugin
     ```
     ```bash
     claude plugin install seocc@seocc
     ```
     When the plugin is enabled, Claude Code asks for your **SEOcc MCP address** (your installation address plus `/mcp`, such as `https://seo.example.com/mcp`) and your **SEOcc MCP token**. The token is stored in Claude Code's secure storage.
   - **Claude.ai, Claude desktop or Cowork:** install the plugin from the directory (or upload it), then add SEOcc as a custom connector under **Settings → Connectors → Add custom connector** with your `/mcp` address and sign in with OAuth. These surfaces don't prompt for plugin settings, so the connector carries the connection and the plugin's skills work on top of it.
3. Ask Claude: "List my SEOcc projects."

## What the plugin does and doesn't do

- It contains only instructions (skills) and one MCP server entry. There are no hooks, scripts, binaries or bundled code.
- The only network connection is the MCP server **you** configure: your own SEOcc address, with your token in the `Authorization` header. Nothing is sent anywhere else, and there's no telemetry.
- SEOcc's MCP tools read stored data. They never call Google or DataForSEO, never start crawls, and never spend money.
- If your token has write scopes, Claude can create change notes, tasks and content briefs, change finding status, and start or stop page watches. The skills tell Claude to show the exact values and ask for your yes before every write. SEOcc writes never delete anything, and every write is audited in SEOcc with the token's name.
- Claude treats everything stored in SEOcc (page titles, notes, competitor text) as data, not instructions.

## Privacy

See [PRIVACY.md](PRIVACY.md). In short: this plugin collects nothing. Your SEO data stays on your own server and reaches Claude only when you ask a question that needs it.

## Support

Open an issue at <https://github.com/seoccnet/seocc-claude-plugin/issues> or e-mail sales@seocc.net.

## Licence

MIT, see [LICENSE](LICENSE). SEOcc itself is AGPL-3.0.
