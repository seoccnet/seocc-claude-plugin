---
name: connect
description: Connect Claude to the user's own SEOcc (SEO Control Center) installation, or fix a connection that doesn't work. Use when SEOcc tools such as projects_list are missing or fail, when an expected SEOcc tool isn't listed, or when the user asks how to set up SEOcc in Claude.
---

# Connect SEOcc

Check first: call `projects_list`. If it answers, SEOcc is connected. Say which projects the token sees and stop.

Never ask the user to paste a token into the chat. It goes only into the plugin's or connector's settings.

## 1. Create a token in SEOcc

The user (a workspace owner or admin) opens SEOcc, goes to **Integrations → AI access → New token**, and chooses:

- **Projects**: only the sites Claude should see.
- **Read scopes**: Projects, Search Console performance, Keywords and metrics, Rankings, Competitors, Opportunities, Pages and their SEO evidence. Most skills need **Pages** (`pages:read`) for URL-level work.
- **Write scopes** (optional, unticked by default): change notes, team tasks, content briefs, opportunity status, page watches, keyword relevance, topic owners, investigations. Leave them off for read-only use.
- **Expiry**.

The token starts with `scc_` and is shown once.

## 2. Add it to Claude

**Claude Code (this plugin):** when the plugin is enabled, Claude Code asks for two settings:

- **SEOcc MCP address**: the installation address plus `/mcp`, such as `https://seo.example.com/mcp`. HTTPS is required.
- **SEOcc MCP token**: the `scc_…` token. It's stored in secure storage, not in `settings.json`.

To change them later, the user opens `/plugin`, selects the `seocc` plugin, and edits its options. Then run `/mcp` to reconnect.

**Claude.ai, the Claude desktop chat, or Cowork:** these don't prompt for plugin settings, so the plugin's built-in server stays off there. Its skills still work once SEOcc is added as a custom connector:

1. **Settings → Connectors → Add custom connector**.
2. URL: the installation address plus `/mcp`.
3. Sign in with **OAuth**: SEOcc opens, the user signs in, picks the workspace, projects and scopes, and clicks **Allow**. Only owners and admins can approve.

**Without the plugin (Claude Code):**

```bash
claude mcp add --transport http seocc https://seo.example.com/mcp --header "Authorization: Bearer YOUR_TOKEN"
```

## 3. Troubleshooting

| Symptom | Likely cause and fix |
|---|---|
| 401 or "invalid token" | Token expired, revoked, or mistyped. Create a new one. |
| Connects but a tool is missing | The token lacks that scope. Create a new token with it; existing tokens never gain scopes. |
| "Project not found" | The token doesn't include that project, or the user lost access to it. |
| Empty, garbled or HTML response | Hosting strips the `Authorization` header, or security software or a web filter rewrites `/mcp` responses. Test from another network, and see the *Troubleshooting* chapter (`guide_search "troubleshooting"` once connected, or the SEOcc docs). |
| "Too many requests" | 60 calls a minute per token. Wait a minute; don't retry in a loop. |
| `http://` address refused | Use HTTPS. Claude won't send a token to a plain-HTTP remote server. |
