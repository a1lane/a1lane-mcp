# A1 Lane MCP — tool inventory (contract v1.8)

26 tools served at `https://a1lane.ai/mcp/v1`. `tools/list` is filtered by the
token's OAuth scope: `read` sees 14 tools, `read write` sees 21,
`read write publish` sees all 26. Annotations follow the MCP specification;
"destructive" includes public sends that cannot be recalled, so clients ask
the user before those calls. The hints below are the live values the server
serves (`tools/list`, enumerated from `postlane/mcp.py` on 2026-11-09).

| # | Tool | Title | Scope | Read-only | Destructive | Open-world | Idempotent |
|---|---|---|---|---|---|---|---|
| 1 | `cancel_scheduled` | Cancel a scheduled post | publish | – | ✓ | ✓ | ✓ |
| 2 | `create_draft` | Create a draft post | write | – | – | – | – |
| 3 | `create_upload_link` | Create a file upload link | write | – | – | – | – |
| 4 | `delete_draft` | Delete a post record | write | – | ✓ | – | ✓ |
| 5 | `get_batch_status` | Check a batch's delivery | read | ✓ | – | – | ✓ |
| 6 | `get_best_times` | Get best times to post | read | ✓ | – | – | ✓ |
| 7 | `get_delivery_digest` | Summarize recent deliveries | read | ✓ | – | – | ✓ |
| 8 | `get_engagement_coverage` | See which metrics each platform reports | read | ✓ | – | – | ✓ |
| 9 | `get_engagement_rollup` | Get engagement totals | read | ✓ | – | – | ✓ |
| 10 | `get_handoff_pack` | Get steps to finish a post in-app | read | ✓ | – | – | ✓ |
| 11 | `get_platform_schema` | Get a platform's posting rules | read | ✓ | – | – | ✓ |
| 12 | `get_post_engagement` | Get a post's engagement | read | ✓ | – | – | ✓ |
| 13 | `get_receipt` | Get a post's delivery receipt | read | ✓ | – | – | ✓ |
| 14 | `get_upload_status` | Check an upload link | read | ✓ | – | – | ✓ |
| 15 | `get_verification_status` | Check if posts are verified live | read | ✓ | – | – | ✓ |
| 16 | `list_accounts` | List connected social accounts | read | ✓ | – | – | ✓ |
| 17 | `list_attention_items` | List posts that need attention | read | ✓ | – | – | ✓ |
| 18 | `list_posts` | List and filter posts | read | ✓ | – | – | ✓ |
| 19 | `pause_workspace` | Pause or resume publishing | publish | – | – | – | ✓ |
| 20 | `request_approval` | Send a draft for approval | write | – | – | – | – |
| 21 | `resolve_attention` | Fix a delivery problem | publish | – | ✓ | ✓ | – |
| 22 | `schedule_draft` | Publish or schedule a draft | publish | – | ✓ | ✓ | – |
| 23 | `submit_batch` | Create many posts at once | write | – | ✓ | ✓ | – |
| 24 | `unpublish_post` | Delete a live post from platforms | publish | – | ✓ | ✓ | ✓ |
| 25 | `update_draft_settings` | Edit a draft or scheduled post | write | – | ✓ | – | – |
| 26 | `upload_media` | Import media from a link | write | – | – | ✓ | – |

Deprecated alias: `create_handoff_pack` stays callable for one release as an
alias of `get_handoff_pack`; it is not listed in `tools/list` (the count above
is the listed count) and its result says to use the new name.

Every mutating tool also accepts an optional `idempotency_key`; replaying a
call with the same key returns the original result and does nothing again.

Full per-tool descriptions are what the server itself returns in `tools/list`
— connect and ask your client to list them.
