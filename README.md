# A1 Lane MCP Server

A1 Lane is a social publishing service with its own queue, scheduler and delivery receipts. It uploads and publishes video and posts through each platform's official API, and marks a destination live only when read-back from the platform confirms it; channels without read-back are marked Delivered (limited). Through this connector an assistant can list the user's connected accounts, check each platform's posting rules and options, bring in media the user supplies, write and schedule drafts or a week of posts at once, send drafts for approval, read receipts and verification status, investigate failures and apply supported recovery actions, take a post down, and read engagement where supported. It does not bypass required approvals or automatically retry uncertain deliveries.

Works today with YouTube, X, Pinterest, Threads, Bluesky, Mastodon, Discord and Telegram, plus Instagram professional accounts, Facebook Pages you manage and LinkedIn personal profiles (limited). TikTok is in review. Also connects DEV (unofficial), Slack (limited), Tumblr and Pixelfed (limited) for posting from AI assistants and the API.

A listing in an assistant's directory isn't any platform's approval. LinkedIn Community Management access (for Company Pages) is a separate permission still in review; personal-profile connections are available today.

This repository is the public home of A1 Lane's MCP registry record (`server.json`), the tool
inventory (`TOOLS.md`), and client packaging: a Claude Code plugin and marketplace, a Gemini CLI
extension, a Cursor plugin manifest and installable workflow skills. The A1 Lane service itself is
hosted and is not distributed here; there is nothing to run locally.

- Endpoint: `https://a1lane.ai/mcp/v1` (Streamable HTTP), contract v1.15, 19 tools
- Sign-in: OAuth 2.1 with PKCE. Your client opens a1lane.ai, you sign in and approve one workspace and its scopes.
- Listed in the official MCP Registry as ai.a1lane/a1lane. A1 Lane is available in Claude's connector directory.

## Install

Exact, current steps for every client live on one page: https://a1lane.ai/mcp. Each section below says
whether we have run that connect ourselves. Whichever client you use: Works today with YouTube, X, Pinterest, Threads, Bluesky, Mastodon, Discord and Telegram, plus Instagram professional accounts, Facebook Pages you manage and LinkedIn personal profiles (limited). TikTok is in review. Also connects DEV (unofficial), Slack (limited), Tumblr and Pixelfed (limited) for posting from AI assistants and the API.

### Claude (claude.ai and Claude Desktop)

1. Open **Customize → Connectors** and choose **Add custom connector**.
2. Name it **A1 Lane** and paste `https://a1lane.ai/mcp/v1` as the server URL.
3. Leave the sign-in settings as Claude detects them: **Sign in now**, with **Use Claude's published identity** (our server supports it; **Register automatically** works too). Choose **Add**.
4. Choose **Connect**, sign in to A1 Lane, pick the workspace and the scopes.
5. In a chat, open **+** → **Connectors** and switch A1 Lane on.

Full steps, including Team and Enterprise: https://a1lane.ai/mcp#claude

Tested by us: 11 Nov 2026: connected in Claude, and list_accounts and get_workspace answered in a new chat. Steps follow [Claude's custom connector guide](https://claude.com/docs/connectors/custom/remote-mcp) as of 2 Nov 2026.

### Claude Code

Add the server:

```shell
claude mcp add --transport http a1lane https://a1lane.ai/mcp/v1
```

Or install the plugin, which bundles the same server plus the workflow skills in this repo, in one line:

```shell
claude plugin marketplace add a1lane/a1lane-mcp && claude plugin install a1-lane@a1lane
```

Inside a session the same two steps are:

```text
/plugin marketplace add a1lane/a1lane-mcp
/plugin install a1-lane@a1lane
```

Then run `/mcp` and sign in to A1 Lane when asked.

Not yet tested end to end with Claude Code. Steps follow [Claude Code's plugin marketplace docs](https://code.claude.com/docs/en/plugin-marketplaces) as of 15 Nov 2026.

### ChatGPT

1. Open **Plugins** (chatgpt.com/plugins), choose **+**, then **Add custom MCP server**.
2. Name it **A1 Lane**. Under **Connection**, enter `https://a1lane.ai/mcp/v1` as the **Server URL**.
3. Set authentication to **OAuth**. Read the risk warning, choose **I understand and want to continue**, then **Create as a plugin**.
4. Install the plugin and sign in to A1 Lane when asked: pick the workspace and the scopes.
5. In a new chat, type **@** and pick A1 Lane.

Full steps: https://a1lane.ai/mcp#chatgpt

Tested by us: 11 Nov 2026: connected in ChatGPT, signing in with OAuth consent. Steps follow [OpenAI's custom MCP server guide](https://developers.openai.com/api/docs/guides/custom-mcp-server) as of 2 Nov 2026.

### Cursor

Install from the link (paste it into your browser; it opens Cursor and asks you to confirm):

```text
cursor://anysphere.cursor-deeplink/mcp/install?name=a1lane&config=eyJ1cmwiOiJodHRwczovL2ExbGFuZS5haS9tY3AvdjEifQ%3D%3D
```

Or add it by hand to `~/.cursor/mcp.json` (every project) or `.cursor/mcp.json` (one project):

```json
{
  "mcpServers": {
    "a1lane": {
      "url": "https://a1lane.ai/mcp/v1"
    }
  }
}
```

This repo also carries a Cursor plugin manifest (`.cursor-plugin/plugin.json`: the server plus the skills). It is not listed in Cursor's marketplace yet.

Not yet tested end to end with Cursor. Steps follow [Cursor's MCP docs](https://cursor.com/docs/mcp) as of 2 Nov 2026.

### VS Code / GitHub Copilot

[Add to VS Code](https://vscode.dev/redirect?url=vscode%3Amcp%2Finstall%3F%257B%2522name%2522%253A%2522a1lane%2522%252C%2522type%2522%253A%2522http%2522%252C%2522url%2522%253A%2522https%253A%252F%252Fa1lane.ai%252Fmcp%252Fv1%2522%257D) opens VS Code and asks you to confirm. From a terminal:

```shell
code --add-mcp '{"name":"a1lane","type":"http","url":"https://a1lane.ai/mcp/v1"}'
```

Or add it to `.vscode/mcp.json` (VS Code's key is `servers`):

```json
{
  "servers": {
    "a1lane": {
      "type": "http",
      "url": "https://a1lane.ai/mcp/v1"
    }
  }
}
```

Not yet tested end to end with VS Code. Steps follow [VS Code's MCP developer guide](https://code.visualstudio.com/api/extension-guides/ai/mcp) as of 9 Nov 2026.

### Gemini CLI

Install the extension from this repo (the server plus a context file):

```shell
gemini extensions install https://github.com/a1lane/a1lane-mcp
```

Restart Gemini CLI, then sign in with `/mcp auth a1lane`. Or add just the server:

```shell
gemini mcp add --transport http a1lane https://a1lane.ai/mcp/v1
```

Google replaced Gemini CLI with Antigravity CLI for unpaid-tier and Google One users on 18 June 2026; Google's migration guide imports installed extensions with `agy plugin import gemini`. We have not run that import.

Not yet tested end to end with Gemini CLI. Steps follow [Gemini CLI's extension release and MCP server docs](https://geminicli.com/docs/extensions/releasing/) as of 15 Nov 2026.

### Grok

Add the endpoint as a remote MCP server where your plan offers it. Use the server URL `https://a1lane.ai/mcp/v1`; the sign-in is found from the server's OAuth metadata. No Grok setup page was checked for these steps.

Not yet tested end to end with Grok. Steps follow [the MCP authorization spec](https://modelcontextprotocol.io/specification/2025-11-25/basic/authorization) as of 2 Nov 2026.

### Windsurf / Devin Desktop

Devin Local, from a terminal:

```shell
devin mcp add a1lane https://a1lane.ai/mcp/v1
devin mcp login a1lane
```

Cascade: open Cascade's MCP menu → **Open MCP config file** and add:

```json
{
  "mcpServers": {
    "a1lane": {
      "serverUrl": "https://a1lane.ai/mcp/v1"
    }
  }
}
```

Not yet tested end to end with Windsurf. Steps follow [Devin's MCP configuration docs](https://docs.devin.ai/cli/extensibility/mcp/configuration) as of 9 Nov 2026.

### Cline

In the Cline panel: **MCP Servers** → **Remote Servers**, name it `a1lane`, paste the server URL and choose **Streamable HTTP**. Or add to `cline_mcp_settings.json` (keep the `type` line; without it Cline uses the older SSE transport, which A1 Lane doesn't serve):

```json
{
  "mcpServers": {
    "a1lane": {
      "type": "streamableHttp",
      "url": "https://a1lane.ai/mcp/v1"
    }
  }
}
```

Not yet tested end to end with Cline. Steps follow [Cline's remote server guide](https://docs.cline.bot/mcp/connecting-to-a-remote-server) as of 9 Nov 2026.

### Skills for any agent

The workflow skills in `skills/` install into Claude Code, Cursor and the other agents the skills CLI supports:

```shell
npx skills add a1lane/a1lane-mcp
```

The skills call the A1 Lane tools, so add the server to your agent as well.

Not yet tested end to end with the skills CLI. Steps follow [the skills CLI's discovery rules](https://github.com/vercel-labs/skills/blob/main/docs/creating-skills.md) as of 15 Nov 2026.

### Any other MCP client

- Server URL: `https://a1lane.ai/mcp/v1`
- Transport: Streamable HTTP (JSON-RPC over POST)
- Sign-in: OAuth 2.1 with PKCE (S256); an unauthenticated request gets a 401 that points to `https://a1lane.ai/.well-known/oauth-protected-resource`
- Client registration: Client ID Metadata Documents or Dynamic Client Registration; nothing to pre-register
- Scopes: `read`, `write`, `publish`, `accounts`
- Server card: `https://a1lane.ai/.well-known/mcp/server-card.json`
- A workspace token (`plt_your_workspace_token`, sent as `Authorization: Bearer`) also works for developer setups; create it in Settings → API & Webhooks. Never paste a token into a chat.

Steps follow [the MCP authorization spec](https://modelcontextprotocol.io/specification/2025-11-25/basic/authorization) as of 2 Nov 2026.

## Delivery receipts

Every post gets a delivery receipt for each destination it was sent to. Where the platform offers a
way to read the post back, A1 Lane checks it on the platform before marking that destination live
(`verified: true`). Where it doesn't, the receipt records the platform's send response and the
destination reads Delivered (limited) (`verified: false`, with the reason in `message`). Read-back is
per platform, not universal. A send whose outcome is unknown is Uncertain and is never retried
automatically.

A sample `get_verification_status` result (a sample, not a real post; the `verified` and
`message` values come from the server's own rules):

```json
{
  "posts": [
    {
      "postId": "post_sample",
      "status": "published",
      "destinations": [
        {
          "id": "dst_sample_youtube",
          "platform": "youtube",
          "status": "published",
          "verified": true,
          "evidence": "readback",
          "url": "https://youtu.be/SAMPLE00000",
          "stage": null,
          "message": null
        },
        {
          "id": "dst_sample_linkedin",
          "platform": "linkedin",
          "status": "published",
          "verified": false,
          "evidence": "send_response",
          "url": null,
          "stage": null,
          "message": "LinkedIn accepted the post and returned its ID. No LinkedIn delivery has been confirmed end to end yet, so this receipt records LinkedIn's response and doesn't claim the live post was checked."
        }
      ],
      "allVerified": false
    }
  ]
}
```

## Try asking your assistant

- "Which social media accounts do I have connected, and does any of them need reconnecting?"
- "Write up a post for my launch and cross-post it to my accounts — set it up but don't send it yet."
- "Did yesterday's post actually go out? Where is it live, and what's its link?"
- "What's wrong with my posts — why did that one fail, and what's waiting on me?"
- "Give me a summary of what was delivered in the last day."

## Tools

19 tools in contract v1.15. 9 are read-only and 8 are
annotated destructive (they send, remove or overwrite something), so clients that honour
MCP tool annotations ask you before those calls. The server's instructions also tell the assistant
to confirm with you before any call that sends or removes. Annotations per tool: [`TOOLS.md`](TOOLS.md).

| Tool | Scope | What it does |
|---|---|---|
| `add_media` | write | **Add a video or image to the media library.** Use when the user wants to post a video or photo from a link (a public https URL) or from a file on their phone or computer, or to upload one. |
| `get_analytics` | read | **Get engagement, best times and delivery recaps.** Use when the user asks how a post or their accounts performed, when to post (the best time or day they should post), or what went out recently. |
| `get_platform_schema` | read | **Get a platform's posting rules.** Use before writing or scheduling a post, or when the user asks what a platform allows: caption length, video and image limits, carousel size, whether threads and first comments work, disclosure flags, and every per-post option with its type and allowed values. |
| `get_receipt` | read | **Get a post's delivery receipt.** Use when the user asks whether a post went out, where it is live, what its link is, what happened to it, or how to finish it in a platform's app. |
| `get_workspace` | read | **Get A1 Lane workspace, plan and limits.** Use when the user asks about their A1 Lane workspace: which one this is, its plan, whether they can create another workspace, how many accounts or queued posts it can still hold, whether posts need approval, its timezone, or why publishing is paused; and before writing a caption, for the brand's rules. |
| `list_accounts` | read | **List connected social accounts.** Use when the user asks which social media accounts are connected to A1 Lane for posting, which account to post to, whether one needs reconnecting, or how to connect a new one. |
| `list_media` | read | **List the media library or check an upload.** Use when the user asks what videos or images are already in their A1 Lane media library, wants to reuse an earlier file, or after add_media with source upload_link to see whether their file has arrived. |
| `list_post_comments` | read | **Read comments on a published post.** Use when the user asks what people said on one of their published posts, or which comments need an answer. |
| `list_posts` | read | **List posts, problems, repeats and batches.** Use when the user asks to see the posts they drafted, scheduled or published through A1 Lane, what needs fixing, which posts repeat, or how a batch is going. |
| `manage_accounts` | publish (disconnect: accounts) | **Pause, resume or disconnect accounts.** Use when the user asks to stop all posting for now, put publishing on hold, start again, or disconnect a social account. |
| `publish_post` | publish (approval: write) | **Publish, schedule or send a draft for approval.** Use when the user asks to post, publish or share a saved draft: right now, at a specific date and time, or in an account's next free posting slot; or, in a workspace that needs approval, to send it to their team, client or manager for sign-off. |
| `remove_post` | publish (delete_record: write) | **Cancel, take down or delete a post.** Use when the user asks to cancel or unschedule a post, take a published post down, or delete a post. |
| `repeat_post` | publish | **Repeat a post on a schedule.** Use when the user asks to repeat, recycle or re-share a post on a schedule (for example every 7 days or 5 times), or to pause, resume or stop a repeating post. |
| `reply_to_comment` | publish | **Reply to a comment on a post.** Use when the user asks to answer or reply to a comment on their own published post. |
| `report_problem` | read | **Report a problem to the A1 Lane team.** Use when one of this server's tools failed, returned something unexpected, lacks a capability the user needed, or its instructions were unclear, after you have followed the error's fix_hint. |
| `resolve_attention` | publish | **Fix a delivery problem.** Use when the user asks to fix, retry or re-send a failed post, or to clear an item from list_posts view attention. |
| `save_draft` | write | **Create, edit or copy a social post draft.** Use when the user asks to write, prepare, cross-post or set up a social media post, video, carousel or thread, to change a draft or a scheduled post before it starts delivering, or to start a new post from an existing one. |
| `search_instagram_audio` | read | **Search Instagram audio for a Reel.** Use when the user wants music, a trending sound or other audio on an Instagram Reel. |
| `submit_batch` | write | **Create many posts at once.** Use when the user wants several different posts set up at once: a week of content, a content calendar or a bulk schedule. |

## Scopes

Your token's scopes decide which tools your client sees. `write` includes `read`; `publish`
includes `write`; `accounts` adds only account disconnection.

| Scope | Tools visible | What it adds |
|---|---|---|
| `read` | 10 | look only: accounts, posts, receipts, media and the plan. Nothing is changed. |
| `write` | 15 | adds drafting: create, edit and copy draft posts, delete post records, ask for approval and add media. Nothing is queued or published. |
| `publish` | 19 | adds publishing: queue, schedule and publish posts, retry deliveries, cancel or take down posts, and pause the workspace. |
| `accounts` | 11 | adds account management: disconnecting the workspace's social accounts. Publishing does not include it. |

All four scopes together: 19 tools.

## Links

Docs https://a1lane.ai/docs/mcp · Privacy https://a1lane.ai/legal/privacy · Terms https://a1lane.ai/legal/terms ·
Status https://a1lane.ai/status · Support support@a1lane.ai

The MIT license in this repository covers its documentation and configuration files. The hosted
A1 Lane service is governed by https://a1lane.ai/legal/terms.

<!-- Generated by tools/public_repo_pack.py in the A1 Lane product repo from postlane/mcp.py; edit there, not here. -->
