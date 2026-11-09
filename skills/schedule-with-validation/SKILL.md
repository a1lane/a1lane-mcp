---
name: schedule-with-validation
description: Use when the user wants posts scheduled for later — a single post at a set time, the next free slot, or a run of posts — and each destination's posting rules (caption limits, media requirements, platform options) must be checked before anything is queued.
---

# Schedule posts with destination-specific validation (A1 Lane)

Scheduling is where platform rules bite: a caption that fits one platform
fails on another. Validate every destination **before** the draft is
created, not after it errors.

> Tool-name note: the frozen v1.8 surface checks posting rules with
> `get_platform_schema` (a platform's caption limits, media requirements
> and options). There is no `get_posting_requirements` tool in v1.8.

## Steps

1. **Find the accounts.** Call `list_accounts`; confirm each destination
   account is connected and healthy.
2. **Validate against every destination's schema.** For each platform the
   post will go to, call `get_platform_schema` and check the actual
   content against it: caption length, media type/size requirements, and
   platform options (for example a video's privacy setting). If the
   content violates a destination's rules, fix the content for that
   destination or drop that destination and tell the user exactly why —
   never silently truncate a caption or drop a destination.
3. **Pick the time with evidence.** If the user has no fixed time, call
   `get_best_times` for the account and propose the best weekday and hour;
   also check `list_posts` for already-scheduled posts so the new one
   doesn't collide or duplicate one that's queued.
4. **Create and adjust the draft.** Call `create_draft`, then
   `update_draft_settings` for any per-destination caption, media or
   timing adjustments the validation step produced.
5. **Approval, then schedule.** Call `request_approval`; only after the
   human approval lands, call `schedule_draft` with the agreed time (or
   the next free slot). To change plans before it sends, use
   `update_draft_settings`; to stop it entirely, `cancel_scheduled` —
   both are safe because nothing has been sent yet.
6. **Confirm what's queued.** Report the scheduled time per destination
   from `list_posts`, and after the send time passes, verify with
   `get_receipt` rather than assuming it went out.

For many posts at once, use `submit_batch` and follow it with
`get_batch_status`, validating each post against each destination's schema
first.

## Rules (from the A1 Lane skill — they bind every step)

- Nothing publishes without the workspace's approval where approval is required — never bypass the approval step, even if the user asks to skip it.
- Taking a post down (unpublish_post) always needs the user's explicit confirmation in the conversation first.
- An uncertain delivery is never re-sent automatically; the user must accept the duplicate-post risk before any resend.
- A destination is only called live when the platform's read-back confirms it; where a platform offers no read-back, report it as Delivered (limited), never as verified.
