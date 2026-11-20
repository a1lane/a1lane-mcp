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
| Cancel the post I scheduled for Friday — stop it going out. | `cancel_scheduled` |
| Write up a post for my launch and cross-post it to my accounts — set it up but don't send it yet. | `create_draft` |
| The video is on my phone and has no link. How do I get it into A1 Lane? | `create_upload_link` |
| Clear that old draft out of my post list; I don't need the record. | `delete_post_record` |
| Post last week's announcement again — same caption, same accounts. | `duplicate_post` |
| How did that batch of five do — were they all accepted? | `get_batch_status` |
| When is the best time to post on my YouTube channel? | `get_best_times` |
| Write a caption for tomorrow's launch post in our brand's style — what are we allowed to claim? | `get_brand_instructions` |
| I want to add my Instagram. What do I need, and where do I go? | `get_connect_link` |
| Give me a summary of what was delivered in the last day. | `get_delivery_digest` |
| What were my total views and likes this month? | `get_engagement_rollup` |
| TikTok says I have to finish the post in the app. What exactly do I do? | `get_handoff_pack` |
| What does TikTok allow for a photo carousel — how many images, and can it have a first comment? | `get_platform_schema` |
| How did Tuesday's post perform — views, likes, comments? | `get_post_engagement` |
| Did yesterday's post actually go out? Where is it live, and what's its link? | `get_receipt` |
| Has the file I uploaded from my phone arrived yet? | `get_upload_status` |
| Are my recent posts verified live on the platforms? | `get_verification_status` |
| What plan is this workspace on, and how many more accounts can I connect? | `get_workspace` |
| Here's an https link to the video I want to post — bring it into my library. | `import_media` |
| Which social media accounts do I have connected, and does any of them need reconnecting? | `list_accounts` |
| What's wrong with my posts — why did that one fail, and what's waiting on me? | `list_attention_items` |
| What videos do I already have in my library? I want to reuse last month's teaser. | `list_media` |
| Show me my posts: what's scheduled or queued, and what already went out? | `list_posts` |
| Which of my posts are set to repeat, and when does each one go out next? | `list_repeats` |
| Stop everything from publishing for now — we have a situation. | `pause_workspace` |
| Post that draft now. | `publish_post` |
| Repeat that post every 14 days until the end of March. | `repeat_post` |
| Send this draft to my client for sign-off before it's posted. | `request_approval` |
| Fix the failed post — retry sending it. | `resolve_attention` |
| Find a trending sound I can put on my next Instagram Reel. | `search_instagram_audio` |
| Pause the weekly repeat of my tips post until I'm back from holiday. | `set_repeat_state` |
| Set up a week of content in one go — here's my content calendar, five different posts. | `submit_batch` |
| Take yesterday's post down from Bluesky. | `unpublish_post` |
| Change the scheduled post: new caption, and move it to Friday afternoon. | `update_draft_settings` |
