# SEOcc dashboard map

Use the dashboard for what MCP can't do: starting a site audit, paid lookups (rank checks, research, backlinks, AI mentions), Google indexing checks, report schedules, integrations and tokens. Those are the user's actions. Point them to the page; if you have a browser tool and the user asks you to operate it, they sign in themselves and you ask before every save.

Replace `{APP}` with the user's SEOcc address (their MCP address without `/mcp`) and `{project}` with the project's public UUID from `projects_list`.

| Page | Address |
|---|---|
| Overview | `{APP}/projects/{project}` |
| Performance | `{APP}/projects/{project}/performance` |
| Pages | `{APP}/projects/{project}/pages` |
| Keywords | `{APP}/projects/{project}/keywords` |
| Rankings | `{APP}/projects/{project}/rankings` |
| Competitors | `{APP}/projects/{project}/competitors` |
| Article ideas | `{APP}/projects/{project}/article-ideas` |
| Opportunities | `{APP}/projects/{project}/opportunities` |
| Team tasks | `{APP}/projects/{project}/opportunities/tasks` |
| Site audit | `{APP}/projects/{project}/site-audit` |
| Backlinks | `{APP}/projects/{project}/backlinks` |
| Content briefs | `{APP}/projects/{project}/content-briefs` |
| Page monitoring | `{APP}/projects/{project}/page-monitoring` |
| AI visibility | `{APP}/projects/{project}/ai-visibility` |
| Local | `{APP}/projects/{project}/local` |
| Google indexing | `{APP}/projects/{project}/indexing` |
| Reports | `{APP}/projects/{project}/reports` |
| Change timeline | `{APP}/projects/{project}/annotations` |
| AI access (MCP tokens) | `{APP}/integrations/mcp` |

Addresses can change between SEOcc versions. If one is wrong, use the left menu (Traffic, Research, Improve, Visibility, Manage) or `guide_search`.

## Background work

Imports, crawls and lookups run through SEOcc's cron, usually within minutes. Don't loop-wait: tell the user to come back after the next run and read the result over MCP.

## Never in the browser without the user

- Typing passwords, tokens or 2FA codes. The user signs in.
- Starting paid lookups. Show the displayed cost and wait for a yes.
- Changing integrations, tokens, roles, e-mail, updates or backups. Those are the administrator's.
- Deleting anything.
