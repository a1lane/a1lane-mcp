---
name: engagement-and-attention
description: Use when the user wants a review of how their posting is doing — what went out recently, how posts performed, when to post next — or a clear list of everything waiting on them across their accounts.
---

# Review engagement and clear the Attention queue (A1 Lane)

A short, honest review: what went out, what it earned, and what needs the
user. Report only the metrics each platform actually returns.

## Steps

1. **What went out.** Call `get_delivery_digest` for the period and
   summarise settled sends, verified-live count, and failures.
2. **How it performed.** Call `get_engagement_rollup` for totals across
   accounts and posts, and `get_post_engagement` for any single post the
   user asks about (views, likes, comments, shares, per destination).
3. **Say what isn't measured.** Call `get_engagement_coverage` and state
   plainly which metrics each platform does not report — never present a
   missing metric as zero, and never compare platforms on a metric only
   one of them reports.
4. **When to post next.** Call `get_best_times` per account and turn it
   into a concrete suggestion ("Thursday around 10 AM on Bluesky").
5. **What's waiting on the user.** Call `list_attention_items` and end
   the review with that list: failures, uncertain deliveries, and
   anything awaiting approval. For anything urgent, offer
   `pause_workspace` to pause all publishing for the workspace while it
   is sorted out. Handle uncertain deliveries only via the
   delivery-receipts skill's rules — never resend one from here.

## Rules (from the A1 Lane skill — they bind every step)

- Nothing publishes without the workspace's approval where approval is required — never bypass the approval step, even if the user asks to skip it.
- Taking a post down (unpublish_post) always needs the user's explicit confirmation in the conversation first.
- An uncertain delivery is never re-sent automatically; the user must accept the duplicate-post risk before any resend.
- A destination is only called live when the platform's read-back confirms it; where a platform offers no read-back, report it as Delivered (limited), never as verified.
