# Product Launch Kit — Kickoff

> **HOW TO USE THIS FILE**
> This is the first file Claude Code reads at the start of every Product Launch Kit session. This kit is deployed as a Claude Code project — not the BSN skills library. It establishes document context, determines which documents are needed, detects phases, runs the questionnaire, and governs document generation. Read this file completely before doing anything else.

---

## Step 0: Document Upload

**Always ask this before anything else:**

> "Before we start — do you have any existing documents you'd like me to review? Things like a product brief, one-pager, pitch deck, existing PRD or PDD, research notes, competitive analysis, or anything else relevant. Any file type works.
>
> If you've already uploaded files, let me know which ones to use or point me to a folder. If you haven't uploaded anything yet, go ahead and do that now and let me know when you're ready — or just say 'no documents' and we'll start from scratch."

**Wait for the user's response before proceeding.**

- If **documents are provided** → Read all of them in full before asking any questions. These documents will be passed into the questionnaire for pre-fill. Note what was found so the questionnaire can reference it.
- If **no documents** → Proceed to Step 1.

---

## Output Format Default

Unless a phase explicitly specifies otherwise, all outputs are **HTML files** that can be downloaded and saved as PDFs. This applies to the Overview, Milestone PRD, PDD, prototype, roadmap, gap analysis, marketing messaging, objection handling guide, and demo script.

**Known exceptions:**
- **Phase 04 — User Stories** → Confluence-compatible markdown (for team grooming before Jira export)

Any phase that requires a different format will state it explicitly. If a format is not specified in a phase file, default to HTML.

### BSN Branding

**Before generating any HTML output**, fetch `bsn-tools:bsn-brand` via MCP. If unavailable, read `bsn-brand-fallback.md`. All outputs must use BSN colors, typography, and visual style. If both are unavailable, apply minimum brand tokens and flag in the HTML version header comment. See `CLAUDE.md` — Brand standards section.

All output files must reference `FORMAT-SPEC.md` for layout, section order, and visual treatment before generating.

### Output consistency

**Format, design, and visual decisions are locked per document type.** Once a format is established for any output — layout, color system, typography, section structure, visual treatments — that format is reused exactly every time that document type is generated. Do not improvise on format between runs. Do not drift in color, spacing, or layout.

If a format decision needs to change, it must be logged in `KIT-CHANGELOG.md` and the relevant example or phase file must be updated before the new format is used. The updated format then applies to all future generations of that document type.

This applies to all HTML outputs: Overview, Milestone PRD, PDD, roadmap, gap analysis, unified review, marketing messaging, objection handling guide, demo script, and any future outputs added to the skill.

**Every HTML output must include a footer with the following text:**

> Internal use only — confidential

Apply this footer consistently across all outputs. It does not need to include a date, author, or document name — the footer text is fixed.

---

## Document Types

| Doc | Purpose | Per Phase? |
|-----|---------|-----------|
| **Overview** | Full project scope using Amazon's Working Backwards PR/FAQ format | No — one per product |
| **Milestone PRD** | Granular, sprint/feature-level planning using Kevin Yien's PRD format | Yes — one per phase |
| **PDD** | Go-to-market positioning and launch preparation | Yes — one per phase |

---

## Workflow

### Step 1: Determine Which Documents Are Needed

Ask the user which document(s) they need if not already clear:
- Overview only
- Milestone PRD only
- PDD only
- All three *(recommended for new product launches)*

---

### Step 2: Ask About Phases

**Always ask this before running the questionnaire:**

> "Does this product have multiple phases or milestones (e.g., Phase 1: MVP, Phase 2: Scale, Phase 3: Enterprise)? If yes, list every phase now with a short name and rough target date."

- If **single phase**: set `phases = ["v1"]`. Run the questionnaire once. Generate one Milestone PRD and one PDD.
- If **multiple phases**: record all phase names and dates upfront before asking any other questions. Then:
  - Run Section A once (universal — applies to all phases)
  - Run Section B once if Overview is needed
  - Run Section C **once per phase** — announce each phase clearly before asking: *"Now let's cover the Milestone PRD questions for [Phase Name]…"* — complete all questions for that phase before moving to the next
  - Run Section D **once per phase** — same approach: announce the phase, complete all questions, then move on
  - Never mix phase answers together or ask about multiple phases in a single question

---

### Step 3: Run the Questionnaire

Reference `questionnaire.md` for the full question set. Walk through the questions for the selected document types and phases as described in Step 2.

If documents were uploaded in Step 0, the questionnaire will use them to pre-fill answers as suggestions. Every suggested answer must be confirmed by the user — nothing is assumed final.

Carry all confirmed answers forward — never re-ask for information already confirmed.

---

### Step 4: Generate the Documents

- Before generating each document type, read the corresponding example file:
  - Overview → `example-overview.md`
  - Milestone PRD → `example-milestone-prd.md`
  - PDD → `example-pdd.md`
- Use the example as the structural, tonal, and voice guide
- Replace all example content with the user's confirmed answers
- Flag any gaps with `[ASSUMPTION: ...]`
- Generate in order: Overview → then for each phase: Milestone PRD → PDD
- Label each phase document clearly: e.g., *"Milestone PRD — Phase 1: MVP"*
- After each document, ask if the user wants changes before continuing to the next
- Output each document as an **HTML file** per the output format default above

---

### Step 5: Deliver and Offer Revisions

After all documents are complete ask:

> "All documents are ready — would you like to revise any section, adjust tone, or regenerate a specific document?"

**Once the user approves all documents, this session is complete. Do not proceed to any further phases without explicit instruction.**

---

## Key Principles

**Overview:** Start with the customer, not the technology. Write as an externally facing document — direct, human, and empathetic. The problem section must make the reader recognize their own experience before the solution is introduced. Section headers are fixed — never rename them. See `example-overview.md` for full tone and voice guidance.

**Milestone PRD:** Define the problem before solutions. Goals and non-goals are equally important. Launch plan must include exit criteria, not just dates. Section headers are fixed — never rename them.

**PDD:** Positioning inputs are separate from product features. Language guidelines must be explicit. Every section feeds a different downstream team: marketing, sales, CS, partners. Section headers are fixed — never rename them.
