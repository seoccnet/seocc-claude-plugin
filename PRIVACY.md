# Privacy

The SEOcc plugin for Claude collects no data.

- **No collection or telemetry.** The plugin is made of text instructions and one MCP server entry. It has no code that runs on your computer, and it never contacts the plugin's authors or any vendor server.
- **One connection, chosen by you.** Claude connects only to the SEOcc address you enter, using the token you create. That server is your own self-hosted installation; its data stays on your hosting.
- **What reaches Claude.** When you ask a question, Claude reads the SEOcc data it needs (search performance, pages, keywords, audit results and similar) through your token's scopes. That data is then part of your Claude conversation and is handled under your agreement with Anthropic.
- **Your token.** In Claude Code the token is kept in Claude Code's secure credential storage, not in plain settings files. In claude.ai the connection uses OAuth, and SEOcc stores only a hash of the access token. You can revoke tokens at any time in SEOcc under **Integrations → AI access**.
- **Writes.** If your token has write scopes, Claude can save change notes, tasks, briefs, finding status and page watches in your SEOcc, only after you approve each one. SEOcc audits every write with the token's name.
- **Retention.** The plugin keeps nothing. Your SEOcc installation keeps your data under your own retention settings.
- **Not for children.** The plugin is a business tool and isn't directed at anyone under 18.

Questions: sales@seocc.net
