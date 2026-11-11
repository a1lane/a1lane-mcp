# A1 Lane MCP — tool inventory (contract v1.9)

31 tools served at `https://a1lane.ai/mcp/v1`. `tools/list` is filtered by the
token's OAuth scope: `read` sees 17 tools, `read write` sees 25,
`read write publish` (plus `accounts` for one tool) sees all 31. Annotations follow the MCP specification;
"destructive" includes public sends that cannot be recalled, so clients ask
the user before those calls. The hints below are the live values the server
serves (`tools/list`, enumerated from `postlane/mcp.py` on 2026-11-11).

| # | Tool | Title | Scope | Read-only | Destructive | Open-world | Idempotent |
|---|---|---|---|---|---|---|---|
| 1 | `cancel_scheduled` | Cancel a scheduled post | publish | – | ✓ | ✓ | ✓ |
| 2 | `create_draft` | Create a draft post | write | – | – | – | – |
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
| 19 | `get_workspace` | Get workspace, plan and limits | read | ✓ | – | – | ✓ |
| 20 | `import_media` | Import media from a link | write | – | – | ✓ | – |
| 21 | `list_accounts` | List connected social accounts | read | ✓ | – | – | ✓ |
| 22 | `list_attention_items` | List posts that need attention | read | ✓ | – | – | ✓ |
| 23 | `list_media` | List media in the library | read | ✓ | – | – | ✓ |
| 24 | `list_posts` | List and filter posts | read | ✓ | – | – | ✓ |
| 25 | `pause_workspace` | Pause or resume publishing | publish | – | – | – | ✓ |
| 26 | `publish_post` | Publish or schedule a draft | publish | – | ✓ | ✓ | – |
| 27 | `request_approval` | Send a draft for approval | write | – | – | – | – |
| 28 | `resolve_attention` | Fix a delivery problem | publish | – | ✓ | ✓ | – |
| 29 | `submit_batch` | Create many posts at once | write | – | ✓ | ✓ | – |
| 30 | `unpublish_post` | Delete a live post from platforms | publish | – | ✓ | ✓ | ✓ |
| 31 | `update_draft_settings` | Edit a draft or scheduled post | write | – | ✓ | – | – |
