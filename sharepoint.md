# sharepoint.md — SharePoint Integration

## Purpose
Defines how approved outputs from the Product Launch Kit are uploaded to SharePoint. This file is read by `CLAUDE.md` at every review gate where the user approves an output. It owns all SharePoint configuration, folder logic, upload behavior, and replace rules.

---

## Configuration

These values are set once at the start of a launch session and reused across all phases. If they are not already stored in `questionnaire-responses.md`, ask the user at kickoff:

```
SHAREPOINT_PARENT_FOLDER: [e.g. "Product Launch Outputs"]
SHAREPOINT_SITE:          [e.g. "BSN Internal" or a full site URL]
SHAREPOINT_MODE:          [full-launch | a-la-carte]
```

Store these values in `questionnaire-responses.md` under a `## SharePoint` section so they persist across sessions. Do not ask again if already present.

---

## Folder structure

### Full launch mode

Each product launch gets its own subfolder inside the parent folder:

```
[SHAREPOINT_PARENT_FOLDER]/
├── ai-risk-adoption/
│   ├── ai-risk-adoption-overview-v2.html      ← latest approved version
│   ├── ai-risk-adoption-prd-v1.html
│   ├── ai-risk-adoption-prototype-v3.html
│   ├── ai-risk-adoption-roadmap-v1.html
│   └── ...
└── training-only-mvp/
    └── ...
```

The subfolder name matches the product slug exactly — same slug used for local file naming. Claude Code creates the subfolder on the first approved upload for that launch if it does not already exist.

### À la carte mode

Outputs go directly into the parent folder — no subfolder:

```
[SHAREPOINT_PARENT_FOLDER]/
├── ai-risk-adoption-demo-script-v1.html
├── training-only-mvp-objection-handling-v1.html
└── ...
```

The slug-prefixed filename is sufficient to identify which launch and document type each file belongs to.

---

## Upload behavior — replace previous version

When an approved output is uploaded to SharePoint, the previous version of the same document type for the same launch is deleted first. Only the latest approved version is kept.

**Replace logic:**

1. List files in the target folder (project subfolder or parent folder for à la carte)
2. Search for any file matching the pattern: `[slug]-[doc-type]-v*.html`
3. If a match is found: delete it
4. Upload the new file

**Example:**

`ai-risk-adoption-prototype-v2.html` is approved →
- Search folder for `ai-risk-adoption-prototype-v*.html`
- Find `ai-risk-adoption-prototype-v1.html` → delete it
- Upload `ai-risk-adoption-prototype-v2.html`

**Result:** Folder always contains exactly one file per document type per launch.

**Note on local files:** The replace rule applies to SharePoint only. Local files in `projects/[slug]/` follow Option A versioning — all versions are preserved locally. SharePoint is the clean shared view; the local repo is the full history.

---

## Review gate — when uploads happen

Uploads only happen after explicit user approval. The review gate runs at the end of every phase that produces an output file.

### Review gate prompt

After generating an output, Claude Code presents:

> "**[Document name] — v[N] ready for review.**
>
> [Brief summary of what was generated or what changed from the previous version]
>
> Options:
> - **Approve** — save locally and upload to SharePoint
> - **Approve locally only** — save locally, skip SharePoint upload
> - **Revise** — describe what to change, regenerate, review again
> - **Reject** — discard this output, do not save"

On **Approve:**
1. Write the file locally to `projects/[slug]/`
2. Run the replace logic above against SharePoint
3. Confirm: *"[filename] uploaded to SharePoint — [folder path]. Previous version removed."*
4. Append to `KIT-CHANGELOG.md`

On **Approve locally only:**
1. Write the file locally to `projects/[slug]/`
2. Skip SharePoint
3. Confirm: *"[filename] saved locally. Not uploaded to SharePoint."*
4. Append to `KIT-CHANGELOG.md`

On **Revise:**
1. Capture the requested changes
2. Regenerate the output
3. Re-present the review gate — do not increment version number until approved

On **Reject:**
1. Discard the output — do not write locally or upload
2. Log the rejection in `KIT-CHANGELOG.md` with a note
3. Ask: *"Would you like to try again or skip this phase for now?"*

---

## MCP connection

SharePoint access uses the Microsoft 365 MCP connector already configured in the kit environment:

```
MCP server: Microsoft 365
Connection: https://microsoft365.mcp.claude.com/mcp
```

**Required permissions:** Sites.ReadWrite.All (delegated) — needed to list, delete, and upload files.

If the MCP server is unreachable at upload time:

> "[SharePoint upload skipped — Microsoft 365 MCP unavailable. File saved locally at projects/[slug]/[filename]. Upload manually when the connection is restored.]"

Log the skipped upload in `KIT-CHANGELOG.md` with status `Pending manual upload`. Do not block the session — continue to the next phase.

---

## Error handling

**Subfolder does not exist:**
Create it. Do not ask the user — subfolder creation is automatic.

**File matching the pattern is not found during replace search:**
Proceed with upload only — no delete step needed.

**Multiple files matching the pattern are found:**
This should not happen under normal operation, but if it does: delete all matches, then upload the new file. Log the cleanup in `KIT-CHANGELOG.md`.

**Upload fails (non-auth error):**
Retry once. If it fails again, skip and log as `Pending manual upload` in `KIT-CHANGELOG.md`. Do not block the session.

**Auth error:**
> "SharePoint upload failed — authentication issue with the Microsoft 365 MCP connector. You may need to reconnect it in your Claude settings. File saved locally at [path]."
Log as `Pending manual upload`.

---

## Quick reference for CLAUDE.md

| Event | SharePoint action |
|---|---|
| Output approved (full launch) | Replace previous version in `[parent]/[slug]/` |
| Output approved (à la carte) | Replace previous version in `[parent]/` |
| Output approved locally only | No SharePoint action |
| Output revised | No action — wait for re-approval |
| Output rejected | No action |
| MCP unavailable | Log as pending, continue session |
