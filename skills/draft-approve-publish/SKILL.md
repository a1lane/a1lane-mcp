---
name: draft-approve-publish
description: Use when the user wants to write a social post and send it to one or more of their connected accounts now — drafting the post, getting it approved, publishing it, and reporting a verified delivery receipt for each destination.
---

# Draft, approve, and publish a post (A1 Lane)

Run the full journey in order. Do not skip the approval step, and do not
call a destination live until its receipt says the platform confirmed it.

## Steps

1. **Find the accounts.** Call `list_accounts` to see which social accounts
   are connected in the user's A1 Lane workspace, with platform and health.
   If the account the user named is not connected or not healthy, say so
   and stop — do not draft for an account that cannot receive it.
2. **Check the rules before writing.** For each destination platform, call
   `get_platform_schema` and write within its caption limits, media
   requirements and options. Never guess a platform's limits.
3. **Bring in media, if any.** If the user supplies a public https link,
   call `import_media`. If they have a file on their phone or computer,
   call `create_upload_link` and check arrival with `get_upload_status`.
4. **Create the draft.** Call `create_draft` for the chosen accounts, then
   show the user the exact caption, media and destinations and wait for
   their go-ahead on the content.
5. **Send it for approval.** Call `request_approval`. The draft now sits in
   the workspace's approval flow — a human approves it in A1 Lane.
6. **Publish only after approval.** Once the user confirms the draft is
   approved, call `publish_post` to publish it now. If it is not yet
   approved, wait; do not try to publish around the gate.
7. **Report the receipt.** Call `get_receipt` (and
   `get_verification_status` where read-back matters) and report each
   destination separately: **live** only when the platform's read-back
   confirms it, otherwise **Delivered (limited)**. Include the platform
   link for each live destination.

For a week of posts at once, prefer `submit_batch` and track it with
`get_batch_status`, keeping the same approval and receipt steps per post.

## Rules (from the A1 Lane skill — they bind every step)

- Nothing publishes without the workspace's approval where approval is required — never bypass the approval step, even if the user asks to skip it.
- Taking a post down (unpublish_post) always needs the user's explicit confirmation in the conversation first.
- An uncertain delivery is never re-sent automatically; the user must accept the duplicate-post risk before any resend.
- A destination is only called live when the platform's read-back confirms it; where a platform offers no read-back, report it as Delivered (limited), never as verified.
