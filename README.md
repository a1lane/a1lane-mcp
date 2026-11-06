# A1 Lane — MCP Server

**One queue for every social platform, operable by your AI assistant.**

A1 Lane is a hosted publishing service: connect your social accounts once, then
schedule and publish posts and videos to YouTube, Instagram, TikTok, Facebook,
X, LinkedIn, Pinterest, Threads, Bluesky, Mastodon, Discord and Telegram from
a single queue. This repository is the
public home of A1 Lane's **MCP server** — the connector that lets assistants
like Claude, ChatGPT, Cursor and Grok work with your A1 Lane account directly.

Every post A1 Lane sends is proven, not assumed: a post is marked live only
after A1 Lane reads it back from the platform itself. Each delivery carries a
**receipt** — the platform read-back and the live link — which your assistant
can fetch and show you.

- **Endpoint:** `https://a1lane.ai/mcp/v1` (Streamable HTTP)
- **Auth:** OAuth 2.0 — on first connect you sign in at a1lane.ai and approve
  access. No API key to copy. (A pasted workspace token also works for
  developer setups.)
- **Tool contract:** v1.7 — 26 tools, listed in [TOOLS.md](TOOLS.md) and in
  [`server.json`](server.json) (the official MCP Registry record).
- **Product:** https://a1lane.ai · **MCP page:** https://a1lane.ai/mcp ·
  **Docs:** https://a1lane.ai/docs/mcp

<!-- Glama badge goes here once the listing is claimed and scored. -->

## Connect it

**Claude** — Settings → Connectors → Add custom connector →
`https://a1lane.ai/mcp/v1`, then approve in the browser.

**ChatGPT** — Settings → Connectors → add the same URL and approve. (Domain
verification is served by A1 Lane.)

**Cursor** — one-click: use the "Add to Cursor" deep link on
https://a1lane.ai/mcp, or add the URL as a remote MCP server in
`~/.cursor/mcp.json`:

```json
{ "mcpServers": { "a1lane": { "url": "https://a1lane.ai/mcp/v1" } } }
```

**Grok** — grok.com/connectors → New Connector → Custom → the same URL.

**Any MCP client** — point it at the endpoint; OAuth discovery is automatic
(`/.well-known/oauth-protected-resource`). Tokens are scoped per workspace:
`read` sees 14 tools, `read write` sees 21, `read write publish` sees all 26.

## Try asking your assistant

- "What accounts do I have connected in A1 Lane?"
- "Draft a post for my Bluesky and Mastodon accounts: …"
- "Schedule that for tomorrow at 9am."
- "Did yesterday's posts actually go live? Show me the receipts."
- "What needs my attention in A1 Lane?"
- "How did my posts do this week?"

Draft-first by design: assistants create drafts, and anything destructive or
public (publishing, deleting a live post, force-retrying a delivery) is
annotated so your client asks you to confirm first.

## What this repo is

The visibility and filing repo for the A1 Lane MCP surface: the registry
record, the tool inventory, and client packaging. The A1 Lane service itself
is hosted software and is not distributed from this repository.

Support: https://a1lane.ai/support · Privacy: https://a1lane.ai/legal/privacy ·
Terms: https://a1lane.ai/legal/terms · Status: https://a1lane.ai/status
