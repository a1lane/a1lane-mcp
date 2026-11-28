# Examples

- `clients/`: the exact server entry each client's config file takes (generated from the same
  builders as https://a1lane.ai/mcp).
- `verification-sample.json`: a sample `get_verification_status` result (not a real post), built
  through the server's own `verified` and `message` rules.

## One prompt per tool

From A1 Lane's prompt battery (golden-prompts-v1.9.md): a prompt, and the tool an assistant
should pick first for it.

| Prompt | First tool |
|---|---|
| What does TikTok allow for a photo carousel — how many images, and can it have a first comment? | `get_platform_schema` |
| Did yesterday's post actually go out? Where is it live, and what's its link? | `get_receipt` |
| What plan is this workspace on, and how many more accounts can I connect? | `get_workspace` |
| Which social media accounts do I have connected, and does any of them need reconnecting? | `list_accounts` |
| What videos do I already have in my library? I want to reuse last month's teaser. | `list_media` |
| Show me my posts: what's scheduled or queued, and what already went out? | `list_posts` |
| Post that draft now. | `publish_post` |
| Repeat that post every 14 days until the end of March. | `repeat_post` |
| Fix the failed post — retry sending it. | `resolve_attention` |
| Find a trending sound I can put on my next Instagram Reel. | `search_instagram_audio` |
| Set up a week of content in one go — here's my content calendar, five different posts. | `submit_batch` |
