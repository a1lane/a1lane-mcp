# Claude Directory plugin submission — notes for the A1 Lane bundle

Status: bundle assembled 2026-11-08. **Not submitted.** Synced to MCP v1.9 (package version 1.9.0, 31 tools) on 2026-11-11. This file records
what Anthropic's plugin submission requires (from Anthropic's official
plugin documentation, claude.com/docs/plugins/build, updated 2026-10-30)
and what remains before Pax can file it.

## What the submission is

A second, distinct Directory submission alongside the existing A1 Lane
connector listing: a plugin bundle = the same remote MCP connector
(`https://a1lane.ai/mcp/v1`, referenced in `.mcp.json` by URL so connector
and plugin users see one set of tools) plus workflow skills that teach
Claude the A1 Lane sequences (approval flow, validated scheduling, receipt
honesty). Anthropic's docs describe the bundle path as: plugin hosted on
GitHub, submitted through the developer portal (claude.ai/directory/manage);
anyone on a paid Claude plan can submit without a partner program; on Team
and Enterprise plans an Owner submits.

## Bundle contents (this folder)

- `.claude-plugin/plugin.json` — manifest. Only the manifest lives in
  `.claude-plugin/`; everything else sits at the plugin root, per the docs.
  Fields used: `name` (`a1-lane` — permanent identity, never change after
  release), `displayName`, `version` (`1.9.0`, matching the MCP surface), `description`, `author`, `license`.
- `.mcp.json` — the connector, referenced by URL. No secrets in this file
  (every installer receives the plugin's files): sign-in happens through
  the server's own OAuth flow.
- `skills/` — four workflow skills, built only on the real v1.9 tools:
  - `draft-approve-publish` — draft → approval → publish → receipt.
  - `schedule-with-validation` — per-destination rule checks before
    scheduling (uses `get_platform_schema` — see the tool-name note below).
  - `delivery-receipts` — receipt inspection + uncertain-delivery safety.
  - `engagement-and-attention` — engagement review + Attention queue.
  Each carries the A1 Lane safety rules verbatim (no approval bypass,
  unpublish needs explicit confirmation, never auto-resend an uncertain
  delivery, read-back honesty).
- `README.md` — directory-facing; comfortably above the docs' 40-word
  minimum.
- `LICENSE` — proprietary license file (docs require a license in the
  manifest or as a LICENSE file).
- `icon-1024.png` — the product icon, same artwork as the other filings.
  NOTE: Anthropic's build doc does not specify where a plugin icon is
  declared; if the portal asks for one at submission, use this file.
  How/where the icon is supplied is UNVERIFIED.

## Pre-submission checks Anthropic documents

1. Run `claude plugin validate ./a1-lane` (Claude Code) — parses the
   manifest and component files and names any field to fix.
   **Not run in this assembly pass** (no build/validate step was in scope);
   Pax runs it before submission.
2. Select **Validate** in the developer portal — runs every portal check
   (the portal validates manifest, README, license and scripts at submit).
3. Test the bundle per surface before filing:
   - Claude Code: `claude --plugin-dir ./a1-lane`; skills appear as
     `/a1-lane:<skill>`; `/mcp` shows the connector state.
   - claude.ai / Cowork: zip the folder (manifest at
     `.claude-plugin/plugin.json` at the zip root or inside a single
     top-level folder), upload via Customize → Plugins → Add → Upload
     plugin, connect the bundled connector from the plugin's Connectors
     tab, and confirm each skill loads.

## What remains before it can ship

| # | Item | Owner |
|---|---|---|
| 1 | **Public GitHub repository** for the bundle (the bundle submission path is GitHub-hosted). No repo exists yet and creating/pushing one is outside this package's scope. Note the existing public repo `github.com/a1lane/a1lane-mcp` holds the registry `server.json`; whether the plugin ships in that repo or a new one is a Pax call | Pax (repo), founder (org/visibility confirmation if a new repo) |
| 2 | Run `claude plugin validate` + fix anything it names | Pax |
| 3 | Per-surface test (Claude Code + claude.ai/Cowork upload) incl. connecting the bundled connector and running one full draft→approve→publish journey | Pax |
| 4 | License decision: manifest says `Proprietary` with a LICENSE file. If the validator/portal wants an SPDX identifier or the skills should be openly licensed, that's a founder decision | Founder |
| 5 | Submit in the developer portal; on Team/Enterprise an Owner submits | Founder/Pax sitting |
| 6 | Pairing check after publication: someone holding both the existing connector listing and this plugin must see one tool set (same server URL in `.mcp.json` is the documented mechanism — verify live) | Pax |

## UNVERIFIED items (flagged, not guessed)

- **`author` field shape** in the manifest (object with `name`/`url` is
  used here, following published examples; the build doc lists the field
  without its schema). The full manifest reference lives in the Claude
  Code docs; `claude plugin validate` is the authority.
- **`.mcp.json` remote entry shape**: `{"type": "http", "url": …}` is the
  conventional form for a remote streamable-HTTP server; the build doc
  says only "reference your server by URL in .mcp.json". Validator decides.
- **`license` field value**: `Proprietary` is descriptive, not an SPDX
  identifier. UNVERIFIED whether the directory accepts it as-is.
- **Icon declaration** for directory plugins: not specified in the build
  doc (see above).
- **Review timeline / scan details** for plugin bundles: the portal runs
  automated validation and human review per the launch coverage; exact
  criteria for bundles vs. single connectors are UNVERIFIED.

## Tool-name correction recorded here

The build brief for skill (b) named a `get_posting_requirements` tool.
The MCP surface has no such tool — the posting-rules tool is
`get_platform_schema` (verified live on 2026-11-08 against the then-current
26-tool surface). The skill uses `get_platform_schema` and says so in its
own text. The surface has since moved to v1.9 (31 tools) under the founder's
2026-11-11 ruling that version discipline does not bind while there are no
external MCP users; the bundle was re-synced to the v1.9 names the same day.
