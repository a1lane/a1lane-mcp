# A1 Lane MCP — tool inventory (contract v1.6)

26 tools served at `https://a1lane.ai/mcp/v1`. `tools/list` is filtered by the
token's OAuth scope: `read` sees 14 tools, `read write` sees 21,
`read write publish` sees all 26. Annotations follow the MCP specification;
"destructive" includes public sends that cannot be recalled, so clients ask
the user before those calls.

| # | Tool | Title | Scope | Read-only | Destructive | Open-world |
|---|---|---|---|---|---|---|
| 1 | `list_accounts` | List connected social accounts | read | ✓ | – | – |
| 2 | `get_platform_schema` | Get a platform's posting rules | read | ✓ | – | – |
| 3 | `upload_media` | Import media from a link | write | – | – | ✓ |
| 4 | `create_draft` | Create a draft post | write | – | – | – |
| 5 | `schedule_draft` | Publish or schedule a draft | publish | – | ✓ | ✓ |
| 6 | `update_draft_settings` | Edit a draft or scheduled post | write | – | ✓ | – |
| 7 | `cancel_scheduled` | Cancel a scheduled post | publish | – | ✓ | ✓ |
| 8 | `delete_draft` | Delete a post record | write | – | ✓ | – |
| 9 | `submit_batch` | Create many posts at once | write | – | ✓ | ✓ |
| 10 | `get_batch_status` | Check a batch's delivery | read | ✓ | – | – |
| 11 | `get_receipt` | Get a post's delivery receipt | read | ✓ | – | – |
| 12 | `get_verification_status` | Check if posts are verified live | read | ✓ | – | – |
| 13 | `list_attention_items` | List posts that need attention | read | ✓ | – | – |
| 14 | `resolve_attention` | Fix a delivery problem | publish | – | ✓ | ✓ |
| 15 | `create_handoff_pack` | Get steps to finish a post in-app | read | ✓ | – | – |
| 16 | `request_approval` | Send a draft for approval | write | – | – | – |
| 17 | `list_posts` | List and filter posts | read | ✓ | – | – |
| 18 | `get_delivery_digest` | Summarize recent deliveries | read | ✓ | – | – |
| 19 | `create_upload_link` | Create a file upload link | write | – | – | – |
| 20 | `get_upload_status` | Check an upload link | read | ✓ | – | – |
| 21 | `pause_workspace` | Pause or resume publishing | publish | – | – | – |
| 22 | `unpublish_post` | Delete a live post from platforms | publish | – | ✓ | ✓ |
| 23 | `get_post_engagement` | Get a post's engagement | read | ✓ | – | – |
| 24 | `get_engagement_rollup` | Get engagement totals | read | ✓ | – | – |
| 25 | `get_best_times` | Get best times to post | read | ✓ | – | – |
| 26 | `get_engagement_coverage` | See which metrics each platform reports | read | ✓ | – | – |

Every mutating tool also accepts an optional `idempotency_key`; replaying a
call with the same key returns the original result and does nothing again.

Full per-tool descriptions are what the server itself returns in `tools/list`
— connect and ask your client to list them.
