# A1 Lane MCP — tool inventory (contract v1.15)

19 tools served at `https://a1lane.ai/mcp/v1`. `tools/list` is filtered by the token's scope: `read` sees 10, `read write` sees 15, `read write publish` sees 19, and all four scopes (adding `accounts`) see all 19. The annotations below are the values the server serves; "destructive" includes public sends that cannot be recalled, so clients that honour annotations ask before those calls.

Generated from `postlane/mcp.py` by `tools/public_repo_pack.py` in the A1 Lane product repo; do not edit by hand.

| # | Tool | Title | Scope | Read-only | Destructive | Open-world | Idempotent |
|---|---|---|---|---|---|---|---|
| 1 | `add_media` | Add a video or image to the media library | write | – | – | ✓ | – |
| 2 | `get_analytics` | Get engagement, best times and delivery recaps | read | ✓ | – | – | ✓ |
| 3 | `get_platform_schema` | Get a platform's posting rules | read | ✓ | – | – | ✓ |
| 4 | `get_receipt` | Get a post's delivery receipt | read | ✓ | – | – | ✓ |
| 5 | `get_workspace` | Get A1 Lane workspace, plan and limits | read | ✓ | – | – | ✓ |
| 6 | `list_accounts` | List connected social accounts | read | ✓ | – | – | ✓ |
| 7 | `list_media` | List the media library or check an upload | read | ✓ | – | – | ✓ |
| 8 | `list_post_comments` | Read comments on a published post | read | ✓ | – | ✓ | ✓ |
| 9 | `list_posts` | List posts, problems, repeats and batches | read | ✓ | – | – | ✓ |
| 10 | `manage_accounts` | Pause, resume or disconnect accounts | publish (disconnect: accounts) | – | ✓ | – | ✓ |
| 11 | `publish_post` | Publish, schedule or send a draft for approval | publish (approval: write) | – | ✓ | ✓ | – |
| 12 | `remove_post` | Cancel, take down or delete a post | publish (delete_record: write) | – | ✓ | ✓ | ✓ |
| 13 | `repeat_post` | Repeat a post on a schedule | publish | – | ✓ | ✓ | – |
| 14 | `reply_to_comment` | Reply to a comment on a post | publish | – | ✓ | ✓ | – |
| 15 | `report_problem` | Report a problem to the A1 Lane team | read | – | – | – | – |
| 16 | `resolve_attention` | Fix a delivery problem | publish | – | ✓ | ✓ | – |
| 17 | `save_draft` | Create, edit or copy a social post draft | write | – | ✓ | – | – |
| 18 | `search_instagram_audio` | Search Instagram audio for a Reel | read | ✓ | – | ✓ | ✓ |
| 19 | `submit_batch` | Create many posts at once | write | – | ✓ | ✓ | – |

## What each tool is for

Each line is the tool's title and the opening sentence of the description the server serves.

- `add_media` — **Add a video or image to the media library.** Use when the user wants to post a video or photo from a link (a public https URL) or from a file on their phone or computer, or to upload one.
- `get_analytics` — **Get engagement, best times and delivery recaps.** Use when the user asks how a post or their accounts performed, when to post (the best time or day they should post), or what went out recently.
- `get_platform_schema` — **Get a platform's posting rules.** Use before writing or scheduling a post, or when the user asks what a platform allows: caption length, video and image limits, carousel size, whether threads and first comments work, disclosure flags, and every per-post option with its type and allowed values.
- `get_receipt` — **Get a post's delivery receipt.** Use when the user asks whether a post went out, where it is live, what its link is, what happened to it, or how to finish it in a platform's app.
- `get_workspace` — **Get A1 Lane workspace, plan and limits.** Use when the user asks about their A1 Lane workspace: which one this is, its plan, whether they can create another workspace, how many accounts or queued posts it can still hold, whether posts need approval, its timezone, or why publishing is paused; and before writing a caption, for the brand's rules.
- `list_accounts` — **List connected social accounts.** Use when the user asks which social media accounts are connected to A1 Lane for posting, which account to post to, whether one needs reconnecting, or how to connect a new one.
- `list_media` — **List the media library or check an upload.** Use when the user asks what videos or images are already in their A1 Lane media library, wants to reuse an earlier file, or after add_media with source upload_link to see whether their file has arrived.
- `list_post_comments` — **Read comments on a published post.** Use when the user asks what people said on one of their published posts, or which comments need an answer.
- `list_posts` — **List posts, problems, repeats and batches.** Use when the user asks to see the posts they drafted, scheduled or published through A1 Lane, what needs fixing, which posts repeat, or how a batch is going.
- `manage_accounts` — **Pause, resume or disconnect accounts.** Use when the user asks to stop all posting for now, put publishing on hold, start again, or disconnect a social account.
- `publish_post` — **Publish, schedule or send a draft for approval.** Use when the user asks to post, publish or share a saved draft: right now, at a specific date and time, or in an account's next free posting slot; or, in a workspace that needs approval, to send it to their team, client or manager for sign-off.
- `remove_post` — **Cancel, take down or delete a post.** Use when the user asks to cancel or unschedule a post, take a published post down, or delete a post.
- `repeat_post` — **Repeat a post on a schedule.** Use when the user asks to repeat, recycle or re-share a post on a schedule (for example every 7 days or 5 times), or to pause, resume or stop a repeating post.
- `reply_to_comment` — **Reply to a comment on a post.** Use when the user asks to answer or reply to a comment on their own published post.
- `report_problem` — **Report a problem to the A1 Lane team.** Use when one of this server's tools failed, returned something unexpected, lacks a capability the user needed, or its instructions were unclear, after you have followed the error's fix_hint.
- `resolve_attention` — **Fix a delivery problem.** Use when the user asks to fix, retry or re-send a failed post, or to clear an item from list_posts view attention.
- `save_draft` — **Create, edit or copy a social post draft.** Use when the user asks to write, prepare, cross-post or set up a social media post, video, carousel or thread, to change a draft or a scheduled post before it starts delivering, or to start a new post from an existing one.
- `search_instagram_audio` — **Search Instagram audio for a Reel.** Use when the user wants music, a trending sound or other audio on an Instagram Reel.
- `submit_batch` — **Create many posts at once.** Use when the user wants several different posts set up at once: a week of content, a content calendar or a bulk schedule.
