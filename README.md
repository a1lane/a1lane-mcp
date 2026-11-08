# A1 Lane MCP Server

A1 Lane is a social publishing service with its own queue, scheduler and delivery
receipts. Through this connector an assistant can list the user's connected accounts,
check each platform's posting rules and options, bring in media the user supplies,
write and schedule drafts or a week of posts at once, send drafts for approval, read
receipts and verification status, fix what failed, take a post down, and read
engagement. It never publishes past an approval state or an uncertain outcome.

Draft-first tools for YouTube, X, Bluesky, Mastodon, Discord and Telegram, plus LinkedIn personal profiles; Facebook Pages, Instagram, Threads, TikTok and Pinterest remain unavailable to new accounts until their platform approvals are granted and A1 Lane enables them.

Listing in this directory is not an approval by any social platform. LinkedIn
Community Management access (for Company Pages) is a separate permission still in
review; personal-profile connections are available today.

This repository is the public home of the registry record (`server.json`), the tool
inventory (`TOOLS.md`) and client packaging. The A1 Lane service itself is hosted and
is not distributed here.

## Delivery receipts

Every post gets a delivery receipt for each destination it was sent to. Where the
platform offers a way to read the post back, A1 Lane checks it on the platform before
marking that destination live. Where it doesn't (Telegram, for example), the receipt
records the platform's send response instead and the destination is marked
Delivered (limited). Read-back is per platform, not universal.

YouTube is fully available, including public uploads. Taking a YouTube video down is a
hand-off by design: A1 Lane points you to the video so you delete it in YouTube
yourself; it does not delete YouTube videos from inside the product.

## Connect

- Endpoint: `https://a1lane.ai/mcp/v1` (Streamable HTTP)
- Sign-in: OAuth 2.1 with PKCE (S256). Your client opens a1lane.ai, you sign in and
  approve one workspace and its scopes, and you're back in your client. A workspace
  token (`plt_…`) also works for developer setups.
- Official MCP Registry: `ai.a1lane/a1lane`

Exact, current steps per client (kept on one page so they can't drift here):

- Claude: https://a1lane.ai/mcp#claude
- ChatGPT: https://a1lane.ai/mcp#chatgpt
- Cursor: https://a1lane.ai/mcp#cursor
- Any other MCP client: https://a1lane.ai/mcp#any-client

## Tools

26 tools in contract v1.8; your token's scope decides which you see (read 14,
read + write 21, read + write + publish 26). Full list with annotations:
[`TOOLS.md`](TOOLS.md) and https://a1lane.ai/docs/mcp.

| Area | Tools |
|---|---|
| Accounts and platform rules | `list_accounts`, `get_platform_schema` |
| Media | `upload_media`, `create_upload_link`, `get_upload_status` |
| Drafts and scheduling | `create_draft`, `update_draft_settings`, `schedule_draft`, `cancel_scheduled`, `delete_draft`, `submit_batch`, `get_batch_status`, `request_approval` |
| Receipts and delivery | `get_receipt`, `get_verification_status`, `list_posts`, `get_delivery_digest` |
| Fixing and control | `list_attention_items`, `resolve_attention`, `get_handoff_pack`, `pause_workspace`, `unpublish_post` |
| Engagement | `get_post_engagement`, `get_engagement_rollup`, `get_best_times`, `get_engagement_coverage` |

Tools that send or remove something are annotated as destructive, so clients that
honour MCP tool annotations ask you to confirm first.

## Try asking your assistant

- "What accounts do I have connected in A1 Lane?"
- "Draft a post for my Bluesky and Mastodon accounts: …"
- "Schedule that for tomorrow at 9am."
- "Did yesterday's posts go out? Show me the receipts."
- "What needs my attention in A1 Lane?"
- "How did my posts do this week?"

## Links

Docs https://a1lane.ai/docs/mcp · Privacy https://a1lane.ai/legal/privacy ·
Terms https://a1lane.ai/legal/terms · Status https://a1lane.ai/status ·
Support support@a1lane.ai

The MIT license in this repository covers its documentation and configuration files.
The hosted A1 Lane service is governed by https://a1lane.ai/legal/terms.
