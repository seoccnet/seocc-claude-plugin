---
name: connect
description: Connect Claude to the user's own SEOcc (SEO Control Center) installation, or fix a connection that doesn't work. Use when SEOcc tools such as projects_list are missing or fail, when an expected SEOcc tool isn't listed, or when the user asks how to set up SEOcc in Claude.
---

# Connect SEOcc

Check first: call `projects_list`. If it answers, SEOcc is connected. Say which projects it sees and stop.

The plugin doesn't contain a server address, because every SEOcc installation has its own. The user connects their installation once, as an MCP server, and signs in with OAuth. Never ask the user to paste a password or token into the chat.

The server address is the installation address plus `/mcp`, for example `https://seo.example.com/mcp`. It must use HTTPS.

## Claude Code

1. The user runs this in a terminal, with their own address:

   ```bash
   claude mcp add --transport http seocc https://seo.example.com/mcp
   ```

   Add `--scope user` to use it in every project, not only the current folder.
2. In Claude Code, run `/mcp`, select `seocc` and choose **Authenticate**. A browser opens on SEOcc.
3. On SEOcc's consent page the user signs in, picks the workspace and the scopes, and clicks **Allow**. Only workspace owners and admins can approve. The access covers every project in that workspace the user can see; to limit Claude to some projects, use a token instead (see the fallback below).

## Claude.ai, the Claude desktop chat, or Cowork

1. **Settings → Connectors → Add custom connector**.
2. URL: the installation address plus `/mcp`.
3. Connect, then sign in and approve on SEOcc's consent page as above.

## Which scopes to approve

- **Read**: Projects, Search Console performance, Keywords and metrics, Rankings, Competitors, Opportunities, Pages and their SEO evidence. Most skills need **Pages** (`pages:read`) for URL-level work.
- **Write** (optional, unticked by default): change notes, team tasks, content briefs, opportunity status, page watches, keyword relevance, topic owners, investigations. Leave them off for read-only use.

To change scopes later, the user revokes the access in SEOcc under **Integrations → AI access** and connects again.

## With a token (fallback)

Where OAuth sign-in isn't possible, or to limit access to some projects, an owner or admin can create a token in SEOcc under **Integrations → AI access → New token** (choose projects, scopes and expiry; it starts with `scc_` and is shown once) and add it themselves:

```bash
claude mcp add --transport http seocc https://seo.example.com/mcp --header "Authorization: Bearer YOUR_TOKEN"
```

The user types this in their own terminal. Don't run it with a real token for them, and don't repeat the token.

## Troubleshooting

| Symptom | Likely cause and fix |
|---|---|
| Sign-in page doesn't open or fails | Check that `https://<address>/.well-known/oauth-authorization-server` loads. If not, the SEOcc address or its HTTPS setup is wrong. |
| 401 or "invalid token" | Access expired or was revoked. Authenticate again in `/mcp` (or create a new token). |
| Connects but a tool is missing | The access lacks that scope. Revoke it in SEOcc and connect again with the scope ticked. |
| "Project not found" | The access doesn't include that project, or the user lost access to it. |
| Empty, garbled or HTML response | Hosting strips the `Authorization` header, or security software or a web filter rewrites `/mcp` responses. Test from another network, and see the *Troubleshooting* chapter (`guide_search "troubleshooting"` once connected, or the SEOcc docs). |
| "Too many requests" | 60 calls a minute per connection. Wait a minute; don't retry in a loop. |
