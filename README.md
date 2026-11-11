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

31 tools in contract v1.9; your token's scope decides which you see (read 17,
read + write 25, read + write + publish + accounts 31). Each tool's one-line purpose below is
its title followed by the opening line of the description the server itself serves in
`tools/list`. Full list with annotations: [`TOOLS.md`](TOOLS.md) and
https://a1lane.ai/docs/mcp.

| Tool | What it does |
|---|---|
| `cancel_scheduled` | **Cancel a scheduled post** Use when the user asks to cancel, stop or unschedule a queued or scheduled post. |
| `create_draft` | **Create a draft post** Use when the user asks to write, prepare, cross-post or set up a social media post, video, carousel or thread, including one post going to several accounts: that is one draft with one destination per account. |
| `create_upload_link` | **Create a file upload link** Use when the user wants to post a video or photo from their phone or computer that has no public link. |
| `delete_post_record` | **Delete a post record** Use only to delete A1 Lane's own record of a post: this does NOT remove anything from any social platform, and a live post stays live. |
| `disconnect_account` | **Disconnect a social account** Use only when the user explicitly asks to disconnect, remove or unlink a social media account from this workspace, for example to free a connection slot for a different account. |
| `duplicate_post` | **Copy a post into a new draft** Use when the user asks to post something again, reuse an earlier post, repost it, or start a new post from an existing one. |
| `get_batch_status` | **Check a batch's delivery** Use when the user asks how a batch of posts or a bulk schedule is going. |
| `get_best_times` | **Get best times to post** Use when the user asks when to post or what time to schedule on one account. |
| `get_brand_instructions` | **Get the workspace's brand instructions** Use before writing or rewriting a caption for this workspace, or when the user asks what the brand allows. |
| `get_connect_link` | **Get the link to connect an account** Use when the user asks to connect, add, link or reconnect a social media account, or asks what they need before connecting one. |
| `get_delivery_digest` | **Summarize recent deliveries** Use when the user asks what went out, how their posting went today or this week, or for a recap or status update. |
| `get_engagement_rollup` | **Get engagement totals** Use when the user asks how their accounts or posts did over a period, for engagement totals, or for a performance report. |
| `get_handoff_pack` | **Get steps to finish a post in-app** Use when the user asks how to finish a post in the platform's own app, or what a needs-attention post is waiting on. |
| `get_platform_schema` | **Get a platform's posting rules** Use before writing or scheduling a post, or when the user asks what a platform allows: caption length, video and image limits, how many images a carousel takes, whether threads and first comments work there, disclosure flags, and every per-post option with its type and allowed values (for example YouTube title, privacy, tags, category and made-for-kids designation, Pinterest board, Mastodon content warning). |
| `get_post_engagement` | **Get a post's engagement** Use when the user asks how a post performed: its views, likes, comments, shares or stats. |
| `get_receipt` | **Get a post's delivery receipt** Use when the user asks whether a specific post went out, where it is live, what its link is, or what happened to it. |
| `get_upload_status` | **Check an upload link** Use after create_upload_link to see whether the user's file has arrived. |
| `get_verification_status` | **Check if posts are verified live** Use when the user asks whether their posts actually went live, or wants a post they just published double-checked. |
| `get_workspace` | **Get workspace, plan and limits** Use when the user asks which workspace this is, what plan it is on, how many social accounts or queued posts it can still hold, whether posts need approval before they send, which timezone schedule times are read in, or why publishing is paused. |
| `import_media` | **Import media from a link** Use when the user gives a public https link to a video or image file they want to post. |
| `list_accounts` | **List connected social accounts** Use when the user asks which social media accounts are connected, which account to post to, whether an account needs reconnecting, or how to connect a new one. |
| `list_attention_items` | **List posts that need attention** Use when the user asks what needs fixing, why a post failed, what went wrong, or what is waiting on them. |
| `list_media` | **List media in the library** Use when the user asks what videos or images are already in their media library, or wants to reuse a file they uploaded earlier instead of uploading it again. |
| `list_posts` | **List and filter posts** Use when the user asks to see their posts: drafts, what is scheduled or queued, what was published, or what failed. |
| `pause_workspace` | **Pause or resume publishing** Use when the user asks to stop all posting for now, put publishing on hold, or start again. |
| `publish_post` | **Publish or schedule a draft** Use when the user asks to post, publish or share a saved draft: right now, at a specific date and time, or in an account's next free posting slot. |
| `request_approval` | **Send a draft for approval** Use when the user asks to send a draft to their team, client or manager for review or sign-off before it is posted. |
| `resolve_attention` | **Fix a delivery problem** Use when the user asks to fix, retry or re-send a failed post, or to clear an item from list_attention_items. |
| `submit_batch` | **Create many posts at once** Use when the user wants several different posts set up at once: a week of content, a content calendar or a bulk schedule. |
| `unpublish_post` | **Delete a live post from platforms** Use when the user asks to take a published post down or delete it from a platform. |
| `update_draft_settings` | **Edit a draft or scheduled post** Use when the user asks to change a draft or a scheduled post before it starts delivering: its caption, media, accounts, per-platform options (for example YouTube privacy or tags), scheduled time, thread parts, first comment or UTM tags. |

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
