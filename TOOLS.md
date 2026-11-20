# A1 Lane MCP — tool inventory (contract v1.10)

35 tools served at `https://a1lane.ai/mcp/v1`. `tools/list` is filtered by the token's scope: `read` sees 19, `read write` sees 27, `read write publish` sees 34, and all four scopes (adding `accounts`) see all 35. The annotations below are the values the server serves; "destructive" includes public sends that cannot be recalled, so clients that honour annotations ask before those calls.

Generated from `postlane/mcp.py` by `tools/public_repo_pack.py` in the A1 Lane product repo; do not edit by hand.

| # | Tool | Title | Scope | Read-only | Destructive | Open-world | Idempotent |
|---|---|---|---|---|---|---|---|
| 1 | `cancel_scheduled` | Cancel a scheduled post | publish | – | ✓ | ✓ | ✓ |
| 2 | `create_draft` | Create a social post draft | write | – | – | – | – |
| 3 | `create_upload_link` | Create a file upload link | write | – | – | – | – |
| 4 | `delete_post_record` | Delete a post record | write | – | ✓ | – | ✓ |
| 5 | `disconnect_account` | Disconnect a social account | accounts | – | ✓ | – | ✓ |
| 6 | `duplicate_post` | Copy a post into a new draft | write | – | – | – | – |
| 7 | `get_batch_status` | Check a batch's delivery | read | ✓ | – | – | ✓ |
| 8 | `get_best_times` | Get best times to post | read | ✓ | – | – | ✓ |
| 9 | `get_brand_instructions` | Get the workspace's brand instructions | read | ✓ | – | – | ✓ |
| 10 | `get_connect_link` | Get the link to connect an account | read | ✓ | – | – | ✓ |
| 11 | `get_delivery_digest` | Summarize recent deliveries | read | ✓ | – | – | ✓ |
| 12 | `get_engagement_rollup` | Get engagement totals | read | ✓ | – | – | ✓ |
| 13 | `get_handoff_pack` | Get steps to finish a post in-app | read | ✓ | – | – | ✓ |
| 14 | `get_platform_schema` | Get a platform's posting rules | read | ✓ | – | – | ✓ |
| 15 | `get_post_engagement` | Get a post's engagement | read | ✓ | – | – | ✓ |
| 16 | `get_receipt` | Get a post's delivery receipt | read | ✓ | – | – | ✓ |
| 17 | `get_upload_status` | Check an upload link | read | ✓ | – | – | ✓ |
| 18 | `get_verification_status` | Check if posts are verified live | read | ✓ | – | – | ✓ |
| 19 | `get_workspace` | Get A1 Lane workspace, plan and limits | read | ✓ | – | – | ✓ |
| 20 | `import_media` | Import media from a link | write | – | – | ✓ | – |
| 21 | `list_accounts` | List connected social accounts | read | ✓ | – | – | ✓ |
| 22 | `list_attention_items` | List posts that need attention | read | ✓ | – | – | ✓ |
| 23 | `list_media` | List the A1 Lane media library | read | ✓ | – | – | ✓ |
| 24 | `list_posts` | List and filter posts | read | ✓ | – | – | ✓ |
| 25 | `list_repeats` | List repeating posts | read | ✓ | – | – | ✓ |
| 26 | `pause_workspace` | Pause or resume publishing | publish | – | – | – | ✓ |
| 27 | `publish_post` | Publish or schedule a draft | publish | – | ✓ | ✓ | – |
| 28 | `repeat_post` | Repeat a post on a schedule | publish | – | ✓ | ✓ | – |
| 29 | `request_approval` | Send a draft for approval | write | – | – | – | – |
| 30 | `resolve_attention` | Fix a delivery problem | publish | – | ✓ | ✓ | – |
| 31 | `search_instagram_audio` | Search Instagram audio for a Reel | read | ✓ | – | ✓ | ✓ |
| 32 | `set_repeat_state` | Pause, resume or stop a repeat | publish | – | ✓ | – | ✓ |
| 33 | `submit_batch` | Create many posts at once | write | – | ✓ | ✓ | – |
| 34 | `unpublish_post` | Delete a live post from platforms | publish | – | ✓ | ✓ | ✓ |
| 35 | `update_draft_settings` | Edit a draft or scheduled post | write | – | ✓ | – | – |

## What each tool is for

Each line is the tool's title and the opening sentence of the description the server serves.

- `cancel_scheduled` — **Cancel a scheduled post.** Use when the user asks to cancel, stop or unschedule a queued or scheduled post.
- `create_draft` — **Create a social post draft.** Use when the user asks to write, prepare, cross-post or set up a social media post, video, carousel or thread, including one post going to several accounts: that is one draft with one destinations entry per account.
- `create_upload_link` — **Create a file upload link.** Use when the user wants to post a video or photo from their phone or computer that has no public link.
- `delete_post_record` — **Delete a post record.** Use only to delete A1 Lane's own record of a post: this does NOT remove anything from any social platform, and a live post stays live.
- `disconnect_account` — **Disconnect a social account.** Use only when the user explicitly asks to disconnect, remove or unlink a social media account from this workspace, for example to free a slot for a different account.
- `duplicate_post` — **Copy a post into a new draft.** Use when the user asks to post something again, reuse an earlier post, repost it, or start a new post from an existing one.
- `get_batch_status` — **Check a batch's delivery.** Use when the user asks how a batch of posts or a bulk schedule is going.
- `get_best_times` — **Get best times to post.** Use when the user asks when to post or what time to schedule on one account.
- `get_brand_instructions` — **Get the workspace's brand instructions.** Use before writing or rewriting a caption for this workspace, or when the user asks what the brand allows.
- `get_connect_link` — **Get the link to connect an account.** Use when the user asks to connect, add, link or reconnect a social media account, or asks what they need before connecting one.
- `get_delivery_digest` — **Summarize recent deliveries.** Use when the user asks what went out, how their posting went today or this week, or for a recap or status update.
- `get_engagement_rollup` — **Get engagement totals.** Use when the user asks how their accounts or posts did over a period, for engagement totals, or for a performance report.
- `get_handoff_pack` — **Get steps to finish a post in-app.** Use when the user asks how to finish a post in the platform's own app, or what a needs-attention post is waiting on.
- `get_platform_schema` — **Get a platform's posting rules.** Use before writing or scheduling a post, or when the user asks what a platform allows: caption length, video and image limits, carousel size, whether threads and first comments work, disclosure flags, and every per-post option with its type and allowed values (for example YouTube title, privacy, tags and made-for-kids, Pinterest board, Mastodon content warning).
- `get_post_engagement` — **Get a post's engagement.** Use when the user asks how a post performed: its views, likes, comments, shares or stats.
- `get_receipt` — **Get a post's delivery receipt.** Use when the user asks whether a specific post went out, where it is live, what its link is, or what happened to it.
- `get_upload_status` — **Check an upload link.** Use after create_upload_link to see whether the user's file has arrived.
- `get_verification_status` — **Check if posts are verified live.** Use when the user asks whether their posts actually went live, or wants a post they just published double-checked.
- `get_workspace` — **Get A1 Lane workspace, plan and limits.** Use when the user asks about their A1 Lane workspace: which one this is, its plan, whether they can create another workspace, how many social accounts or queued posts it can still hold, whether posts need approval, its timezone, or why publishing is paused.
- `import_media` — **Import media from a link.** Use when the user gives a public https link to a video or image file they want to post.
- `list_accounts` — **List connected social accounts.** Use when the user asks which social media accounts are connected to A1 Lane for posting, which account to post to, whether one needs reconnecting, or how to connect a new one.
- `list_attention_items` — **List posts that need attention.** Use when the user asks what needs fixing, why a post failed, what went wrong, or what is waiting on them.
- `list_media` — **List the A1 Lane media library.** Use when the user asks what videos or images are already in their A1 Lane media library, or wants to reuse a file they uploaded earlier instead of uploading it again.
- `list_posts` — **List and filter posts.** Use when the user asks to see the posts they drafted, scheduled or published through A1 Lane: drafts, what is scheduled or queued, what was published, or what failed.
- `list_repeats` — **List repeating posts.** Use when the user asks which posts repeat, when the next repeat goes out, how many repeats have been posted, or why a repeat stopped.
- `pause_workspace` — **Pause or resume publishing.** Use when the user asks to stop all posting for now, put publishing on hold, or start again.
- `publish_post` — **Publish or schedule a draft.** Use when the user asks to post, publish or share a saved draft: right now, at a specific date and time, or in an account's next free posting slot.
- `repeat_post` — **Repeat a post on a schedule.** Use when the user asks to repeat, recycle or re-share a post on a schedule, for example every 7 days, every 2 weeks until a date, or 5 times.
- `request_approval` — **Send a draft for approval.** Use when the user asks to send a draft to their team, client or manager for review or sign-off before it is posted.
- `resolve_attention` — **Fix a delivery problem.** Use when the user asks to fix, retry or re-send a failed post, or to clear an item from list_attention_items.
- `search_instagram_audio` — **Search Instagram audio for a Reel.** Use when the user wants music, a trending sound or other audio on an Instagram Reel.
- `set_repeat_state` — **Pause, resume or stop a repeat.** Use when the user asks to pause, hold, resume, restart, stop or cancel a repeating post.
- `submit_batch` — **Create many posts at once.** Use when the user wants several different posts set up at once: a week of content, a content calendar or a bulk schedule.
- `unpublish_post` — **Delete a live post from platforms.** Use when the user asks to take a published post down or delete it from a platform.
- `update_draft_settings` — **Edit a draft or scheduled post.** Use when the user asks to change a draft or a scheduled post before it starts delivering: its caption, media, accounts, per-platform options (for example YouTube privacy or tags), scheduled time, thread parts, first comment or UTM tags.
