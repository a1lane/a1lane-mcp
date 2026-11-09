---
name: delivery-receipts
description: Use when the user asks what actually happened to posts that went out — did they land, which destinations are confirmed live, what failed, and what to do about a delivery whose outcome is uncertain.
---

# Inspect delivery receipts and handle uncertain delivery (A1 Lane)

A1 Lane's promise is that a receipt never claims more than the platform
proved. Keep that promise in how you report and in what you do next.

## Steps

1. **Start with the summary.** Call `get_delivery_digest` for the recent
   window (or `list_posts` filtered to published/failed) so the user sees
   what went out and what landed before any detail.
2. **Read the receipts.** For each post in question, call `get_receipt`:
   what was sent, where it is live, and the platform link. Use
   `get_verification_status` to distinguish read-back-verified posts from
   merely delivered ones.
3. **Classify every destination honestly:**
   - **Live** — the platform's own read-back confirms the post is there.
   - **Delivered (limited)** — sent, but the platform offers no read-back,
     so it cannot be called verified.
   - **Failed** — the platform refused or the send errored.
   - **Uncertain** — the send's outcome is unknown; the post may or may
     not be live. This is the dangerous state — treat it as below.
4. **Work the Attention queue.** Call `list_attention_items` and take each
   item in turn:
   - *Failed:* explain the platform's reason from the receipt, then offer
     `resolve_attention` to fix or retry where the failure is eligible
     for retry.
   - *Uncertain:* **never re-send it automatically, and never retry it
     yourself.** Explain the duplicate-post risk plainly: resending may
     publish the post twice. Only if the user explicitly accepts that
     risk do you call `resolve_attention` to resolve it.
   - *Needs finishing in the platform's app:* call `get_handoff_pack` and
     give the user those steps rather than forcing it through A1 Lane.
5. **Taking something down.** If the user wants a live post removed, get
   their explicit confirmation in the conversation first, then call
   `unpublish_post`, then verify with `get_receipt` /
   `get_verification_status` that it is gone. `delete_draft` is different:
   it only deletes A1 Lane's own record and never removes anything from a
   platform — say so if the user confuses the two.

## Rules (from the A1 Lane skill — they bind every step)

- Nothing publishes without the workspace's approval where approval is required — never bypass the approval step, even if the user asks to skip it.
- Taking a post down (unpublish_post) always needs the user's explicit confirmation in the conversation first.
- An uncertain delivery is never re-sent automatically; the user must accept the duplicate-post risk before any resend.
- A destination is only called live when the platform's read-back confirms it; where a platform offers no read-back, report it as Delivered (limited), never as verified.
