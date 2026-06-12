# Product Launch Kit — Design Changelog

> **HOW TO USE THIS FILE**
> This file tracks design decisions made during the build of the Product Launch Kit. Each entry logs what was decided, why, and which phase files need to be updated to reflect it. Before writing `CLAUDE.md`, run a reconciliation pass using this file to update all affected phase files.

---

## Reconciliation status

| File | Status | Last updated |
|------|--------|--------------|
| `00-kickoff.md` | ✅ Current | Session 1 |
| `questionnaire.md` | ✅ Current | Session 2 — entries #15 (verified present), #16 applied |
| `examples/example-overview.md` | ✅ Current | Session 1 |
| `examples/example-milestone-prd.md` | ✅ Current | Session 1 |
| `examples/example-pdd.md` | ✅ Current | Session 1 |
| `01-prototype.md` | ✅ Current | Session 2 — entries #4, #5, #20, #21, #22, #26 applied |
| `02-roadmap.md` | ✅ Current | Session 2 — entries #20, #21, #22, #26, #27 applied |
| `03-1-persona-analysis.md` | ✅ Current | Session 2 — entries #1, #2, #3, #6, #7, #8, #20, #21, #22 applied |
| `03-2-competitive-analysis.md` | ✅ Current | Session 2 — entries #1, #2, #3, #8, #9, #20, #21, #22 applied |
| `03-3-swot-tows.md` | ✅ Current | Session 2 |
| `03-4-gap-premortem.md` | ✅ Current | Session 2 |
| `03-5-unified-review.md` | ✅ Current | Session 2 |
| `phase-03-intake.md` | ✅ Current | Session 2 |
| `bsn-personas.md` | ✅ Current | Session 1 |
| `logs/risks-log.md` | ✅ Current | Session 1 |
| `logs/staged-changes.md` | ✅ Current | Session 2 — new file defined |
| `04-user-stories.md` | ✅ Current | Session 2 — entries #15, #16, #17, #20, #21, #22 applied |
| `05-marketing-messaging.md` | ✅ Current | Session 2 — entries #20, #21, #22 applied |
| `06-objection-handling.md` | ✅ Current | Session 2 — entries #20, #21, #22 applied |
| `07-demo-script.md` | ✅ Current | Session 2 — entries #20, #21, #22 applied |
| `CLAUDE.md` | ✅ Current | Session 2 — written and updated |
| `OPEN-QUESTIONS.md` | ✅ Current | Session 2 — Q1 resolved, Q2 still open |
| `bsn-brand-fallback.md` | ✅ Current | Session 2 — new file |
| `dependency-map.html` | ✅ Current | Session 2 — new file |
| `FORMAT-SPEC.md` | ✅ Current | Session 2 — built |

---

## Design decisions log

---

### Entry #1 — Unified review document
**Date:** Session 1
**Decision:** Persona simulation (03-1) and gap analysis (03-2) outputs are presented in a single unified HTML document with two tabs rather than two separate documents.
**Rationale:** Product owner reviews both in one session. Unified view makes it easier to spot overlapping findings (e.g., P4 and G1 both surface the admin controls gap).
**Files to update:**
- `03-1-persona-analysis.md` — output section should reference the unified review document, not a standalone persona output
- `03-2-competitive-analysis.md` — same; output section should reference the unified review document

---

### Entry #2 — Classification layer before decisions
**Date:** Session 1
**Decision:** Findings are classified first (before the product owner decides). Persona finding types: Value Statement Miss / Gap / Risk / Suggested Update. Gap analysis finding types: Competitive Gap / Market Gap / Product Gap / Premortem Risk / Questionnaire Conflict.
**Rationale:** Classification helps the product owner understand what kind of problem it is before deciding what to do. A Risk finding gets more scrutiny than a Suggested Update before being rejected.
**Files to update:**
- `03-1-persona-analysis.md` — add classification step and finding types to the output section
- `03-2-competitive-analysis.md` — finding types already documented; confirm classification step is explicit before decisions

---

### Entry #3 — Three-way decision flow: Accept / Accept Risk / Reject
**Date:** Session 1
**Decision:** Product owner responds to each finding with one of three decisions. Each decision has a clearly defined outcome shown on the finding tile before the decision is made.
- **Accept** — Claude updates the affected document, writes changelog entry, saves file
- **Accept Risk** — No document change; risk logged to `risks-log.md` and noted in document changelog; carries forward to phases 05 and 06
- **Reject** — Finding dismissed; noted in session summary only; no other action
**Rationale:** Accept Risk preserves important signal for downstream phases that a finding was valid but consciously not acted on. Reject means the finding was not valid.
**Files to update:**
- `03-1-persona-analysis.md` — approval gate section needs decision key and explicit outcome descriptions per decision
- `03-2-competitive-analysis.md` — approval gate section needs decision key and explicit outcome descriptions per decision (partially done — confirm completeness)

---

### Entry #4 — Prototype: Claude Code writes files directly
**Date:** Session 1
**Decision:** When Accept is chosen on any finding, Claude Code writes the change to the actual `.md` file, commits the changelog entry, and saves. This is not a conversational copy-paste workflow.
**Rationale:** The team uses Claude Code as the primary environment. File writes should be automated, not manual.
**Files to update:**
- `01-prototype.md` — update post-approval document sync section to specify Claude Code writes files directly
- `03-1-persona-analysis.md` — same
- `03-2-competitive-analysis.md` — same

---

### Entry #5 — Prototype versioning on accepted findings
**Date:** Session 1 (pending) → Session 2 (resolved)
**Decision:** When a finding affects the prototype, Claude Code generates a new versioned prototype file (e.g., `prototype-v2.html`). The previous version is preserved. Minor edits (wording, typos, color tweaks) do not trigger a version bump.
**Resolution:** Option A confirmed — new versioned file on each meaningful update. See also Entry #46 (staging pattern) which governs when the version bump actually executes.
**Status:** ✅ Resolved
**Files updated:**
- `01-prototype.md` — versioning logic updated
- `CLAUDE.md` — prototype staging pattern section added

---

### Entry #6 — Persona findings: each persona gets its own finding tile
**Date:** Session 1
**Decision:** When multiple personas flag the same issue, each persona gets a separate finding tile rather than collapsing them into one. The nuance in how each persona reacted is preserved.
**Rationale:** Marcus Webb objecting for price reasons and Greg Palermo objecting for enterprise control reasons are different problems even if the surface finding looks the same.
**Files to update:**
- `03-1-persona-analysis.md` — findings output section should specify one tile per persona per finding, not collapsed

---

### Entry #7 — Persona findings: severity assigned by Claude
**Date:** Session 1
**Decision:** Claude assigns severity (Critical / Moderate / Minor) to persona findings, not just gap analysis findings.
**Rationale:** Consistency across both tabs of the unified review. Helps the product owner prioritize which findings to discuss first in the meeting.
**Files to update:**
- `03-1-persona-analysis.md` — add severity assignment instruction to findings output section

---

### Entry #8 — Review summary document
**Date:** Session 1
**Decision:** After the product owner completes all decisions in the unified review, Claude generates a review summary HTML document. This is the document that goes to SharePoint for stakeholder record-keeping.
**Summary document contains:**
- Scorecard (total findings / accepted / risks accepted / rejected)
- Document changes queued (green block) — lists every accepted change with document, section, and new version number
- Risks log preview (amber block) — lists every accepted risk with carry-forward flags
- Three sections: Accepted, Risk Accepted, Rejected — each with finding detail, decision rationale, stakeholder comments, and decision attribution (name, role, timestamp)
- Next steps — action items with owners
**Files to update:**
- `03-1-persona-analysis.md` — add review summary generation step after all decisions are made
- `03-2-competitive-analysis.md` — same; summary covers both tabs so it's generated once after both tabs are complete

---

### Entry #9 — Gap analysis: premortem included as a phase
**Date:** Session 1
**Decision:** The premortem is a structured phase within the gap analysis (Step 4), not a separate file. It generates failure scenarios across five categories (Market & Timing, Product & Execution, Positioning & Messaging, Internal & Organizational, External & Environmental), scores them using a weighted matrix (Likelihood 0.40, Impact 0.60), and ranks the top 5.
**Rationale:** Premortem findings feed the same approval gate and risks log as competitive and market gap findings. Keeping it within the gap analysis phase avoids a separate approval step.
**Files to update:**
- `03-4-gap-premortem.md` — confirm premortem step and scoring methodology are fully documented

---

### Entry #10 — Suggested solutions and mitigation on all findings
**Date:** Session 1
**Decision:** Every finding tile (both tabs) includes:
- **Suggested solution** — strategic fix for review (separate from the Accept outcome description)
- **Mitigation** — what to do regardless of the decision
- **Early warning signs** — premortem findings only
**Rationale:** Suggested solutions are strategic and for stakeholder discussion. Accept outcomes are operational (what Claude does to the files). They are deliberately separate and will eventually have their own approval layer that cascades changes across all phases.
**Carry forward:** The cascading approval of suggested solutions is a future workflow to be designed separately.
**Files to update:**
- `03-1-persona-analysis.md` — add suggested solution and mitigation to findings output spec
- `03-2-competitive-analysis.md` — confirm all three insight blocks are specified in the output section

---

### Entry #11 — Stakeholder comments with identity tracking
**Date:** Session 1
**Decision:** The unified review HTML captures stakeholder comments per finding. Each commenter enters their name and role. Comments show name, role, and timestamp. Only the Product Owner role can make Accept / Accept Risk / Reject decisions. Decisions require a confirmation modal. Decisions can be changed by the PO with a second confirmation.
**Rationale:** The document is sent async before a meeting, stakeholders comment, then the PO makes decisions during or after the meeting.
**Files to update:**
- `03-1-persona-analysis.md` — output section should specify the interactive HTML format with identity tracking
- `03-2-competitive-analysis.md` — same

---

### Entry #12 — Meeting summary panel
**Date:** Session 1
**Decision:** The unified review HTML includes a meeting summary panel (toggled from the header) that shows only findings with stakeholder comments, with their decision status. This serves as the live agenda during the review meeting.
**Files to update:**
- `03-1-persona-analysis.md` — reference meeting summary panel in output spec
- `03-2-competitive-analysis.md` — same

---

### Entry #13 — Dual risk logging: risks-log.md + document changelog
**Date:** Session 1
**Decision:** Accepted risks are logged in two places:
1. `logs/risks-log.md` — running master log across all phases
2. The affected document's own changelog — so each document is self-contained
**Rationale:** Master log gives phases 05 and 06 a single place to read all accepted risks. Document changelog keeps each document self-contained.
**Files to update:**
- `03-1-persona-analysis.md` — risk logging step already drafted; confirm both locations are specified
- `03-2-competitive-analysis.md` — same

---

### Entry #14 — Versioning convention
**Date:** Session 1
**Decision:** Document versioning follows this convention:
- `v1.0` — original document as generated from the questionnaire
- `v1.x` — section-level updates (e.g., v1.1, v1.2)
- `v2.0` — full document regeneration only
**Files to update:**
- All phase files that reference changelogs — confirm consistent versioning language

---

### Entry #15 — System roles added to questionnaire
**Date:** Session 1
**Decision:** The questionnaire must capture which of the four system roles are impacted per feature. The four roles are: Partner Admin, Manager Admin, Manager, Employee. This field should be captured in Section C (Milestone PRD questions) at the feature level — not assumed by Claude.
**Rationale:** User stories are written "As a [role]" where role maps to one of these four system roles. If roles aren't captured in the questionnaire, Claude cannot generate accurate stories.
**Role definitions:**
- **Partner Admin** — MSP-side admin who sets up and manages the platform for SMB clients
- **Manager Admin** — SMB-side admin, typically office manager or IT contact at the client company
- **Manager** — Team lead or department manager at the SMB client
- **Employee** — End user at the SMB client who completes training and receives communications
**Files to update:**
- `questionnaire.md` — Add role impact field to Section C per feature
- `04-user-stories.md` — Reference role field from questionnaire as input ✅ applied Session 2

---

### Entry #16 — Confluence → Jira workflow for user stories
**Date:** Session 1
**Decision:** User stories are generated in Confluence-compatible format first. Team reviews and grooms in Confluence. After grooming, stories are exported to Jira. Stories are never entered directly into Jira without Confluence review first.
**Rationale:** Reviewing stories in Confluence is cleaner than navigating individual Jira tickets during grooming. Keeps the backlog clean — only groomed stories enter Jira.
**Output format requirements:**
- Readable and structured in Confluence (headings, tables, BDD blocks)
- Fields that map directly to Jira: story title, role, acceptance criteria, edge cases, priority, story points (optional at grooming stage)
- Epics → Features → Stories hierarchy preserved in Confluence headings
**Files to update:**
- `04-user-stories.md` — Specify Confluence output format and Jira field mapping ✅ applied Session 2

---

### Entry #17 — User story structure: Epics, Features, Stories
**Date:** Session 1
**Decision:** User stories are structured as Epics → Features → Stories. BDD format for acceptance criteria (Given/When/Then). Edge cases listed as numbered conditions below each scenario. One set of stories per phase.
**Rationale:** 20+ years of scrum/agile best practice. Epics give leadership a high-level view. Features group related stories. Stories are the dev-ready unit. BDD keeps criteria testable and removes ambiguity.
**Files to update:**
- `04-user-stories.md` — Full structure definition ✅ applied Session 2

---

### Entry #18 — Questionnaire: document upload and pre-fill behavior
**Date:** Session 1
**Decision:** The questionnaire now supports document upload at the start of the session. Claude reads all uploaded documents before asking any questions and uses them to pre-fill answers as suggestions. Every suggested answer must be confirmed by the user — Claude never assumes a pre-filled answer is correct and moves on.
**Behavior:**
- Always ask first if documents exist before any questions
- If documents uploaded, ask which to use or where to find them
- Read all documents in full before the first question
- For each question: suggest if found, flag if uncertain, ask if nothing found
- If two documents conflict: show side by side, user resolves
- Note answer source in final summary (not highlighted)
- Final confirmation pass before generating any document
**Files updated:**
- `questionnaire.md` — updated with full document upload and pre-fill logic
- `00-kickoff.md` — needs update to reference document upload step before questionnaire

---

### Entry #19 — Document upload moved to kickoff
**Date:** Session 1
**Decision:** Document upload now happens in Step 0 of `00-kickoff.md` before anything else. Documents are read at kickoff and passed into the questionnaire for pre-fill. The questionnaire no longer has its own document upload prompt — it references what was already uploaded at kickoff instead.
**Rationale:** Upload should happen once, at the start of the session, not be repeated when the questionnaire begins. Cleaner flow, no duplication.
**Files updated:**
- `00-kickoff.md` — Step 0 added for document upload
- `questionnaire.md` — duplicate upload section replaced with reference to kickoff

---

### Entry #20 — Output format default: HTML downloadable as PDF
**Date:** Session 1
**Decision:** All outputs default to HTML files that can be downloaded and saved as PDFs unless a phase explicitly specifies otherwise. Stated once in `00-kickoff.md` — does not need to be repeated in every phase file.
**Known exception:** Phase 04 (User Stories) outputs Confluence-compatible markdown.
**Rationale:** HTML is more flexible than PDF for review and sharing, renders well across devices, and can be saved as PDF when needed. Consistent default reduces ambiguity across phases.
**Files updated:**
- `00-kickoff.md` — Output Format Default section added
- All phase files — ✅ applied Session 2

---

### Entry #21 — BSN branding on all HTML outputs
**Date:** Session 1
**Decision:** All HTML outputs must read the BSN branding skill before generating. BSN colors, typography, and visual style apply to every output. If the branding skill is unavailable, Claude flags it before generating rather than proceeding with default styling.
**Rationale:** Consistency across all deliverables. Every output should look like it came from BSN, not a generic tool.
**Files updated:**
- `00-kickoff.md` — BSN branding requirement added to Output Format Default section
- All phase files — ✅ applied Session 2

---

### Entry #22 — Confidential footer on all outputs
**Date:** Session 1
**Decision:** Every HTML output includes a footer with fixed text: "Internal use only — confidential." No variation. No additional metadata required in the footer.
**Rationale:** All outputs are internal documents. A consistent footer makes this clear without requiring anyone to remember to add it.
**Files updated:**
- `00-kickoff.md` — Confidential footer requirement added to Output Format Default section
- All phase files — ✅ applied Session 2

---

### Entry #23 — Milestone PRD persona: The Precision PM
**Date:** Session 1
**Decision:** The Milestone PRD is written from the perspective of The Precision PM — an experienced PM who writes for engineers. Economical, authoritative, precise, and unambiguous. Data is used when it exists; assumptions are flagged explicitly. Non-goals are as important as goals.
**Files updated:**
- `examples/example-milestone-prd.md` — full persona spec added to HOW TO USE block

---

### Entry #24 — Milestone PRD: inline SVG flow diagrams
**Date:** Session 1
**Decision:** Key Flows section now includes inline SVG diagrams for each flow (primary, edit, cancel). Diagrams show linear steps as nodes with arrows, decision points as diamonds, and branching paths with dashed lines color-coded by outcome.
**Files updated:**
- `examples/example-milestone-prd.md` — flow diagram spec added

---

### Entry #25 — Milestone PRD: edge case decision table
**Date:** Session 1
**Decision:** A structured edge case table sits directly below the flow diagrams in the Key Flows section. Columns: Trigger / System behavior / Notes. Every failure path from Key Logic appears in this table. ASSUMPTION tags appear inline for unconfirmed behaviors.
**Files updated:**
- `examples/example-milestone-prd.md` — edge case table spec added

---

### Entry #26 — Output consistency: format locked per document type
**Date:** Session 1
**Decision:** Whatever format, design, layout, color system, and visual treatment is established for any document type, those decisions are locked and must be reused consistently on every generation. No improvisation between runs. If a format decision changes, it is logged here and the relevant file is updated.
**Future work:** `FORMAT-SPEC.md` to be created as the single reference for all output format decisions.
**Files updated:**
- `00-kickoff.md` — output consistency principle added
- `OPEN-QUESTIONS.md` — FORMAT-SPEC.md flagged as future work
- All phase files — ✅ applied Session 2

---

### Entry #27 — Roadmap: solid phase tag colors
**Date:** Session 1
**Decision:** Phase tags on roadmap cards use solid background colors — no gradients, no opacity variations. Locked color assignments: Core = Navy `#082f49`, Growth = Teal `#308c83`, Partner = Purple `#39426f`, Platform = Mint `#3DD6C8`, Compliance = Slate `#4A5568`. Tag text always white. Pill-shaped, small, uppercase, letter-spaced.
**Files updated:**
- `02-roadmap.md` — ✅ applied Session 2

---

### Entry #28 — Deployment target: Claude Code
**Date:** Session 2
**Decision:** This kit deploys as a Claude Code project skill — markdown files in a repo, orchestrated via `CLAUDE.md`. Not deployed to the BSN skills library. All library-specific references updated accordingly.
**Files updated:**
- `CLAUDE.md` — deployment target confirmed throughout

---

### Entry #29 — Brand fetching: MCP at runtime with local fallback
**Date:** Session 2
**Decision:** Brand standards are fetched from `bsn-tools:bsn-brand` via MCP at runtime before every HTML generation. If the MCP server is unreachable, `bsn-brand-fallback.md` is used instead. If both are unavailable, minimum brand tokens are applied and output is flagged in the version header comment.
**Files updated:**
- `CLAUDE.md` — brand standards section
- `bsn-brand-fallback.md` — new file created

---

### Entry #30 — Phase 00: Foundation Documents established
**Date:** Session 2
**Decision:** Phase 00 is a formal phase that produces Overview, PRD, and PDD as its primary outputs. These three documents are outputs of the questionnaire, not standalone example files. All three follow Option A versioning (overview-v1.html, prd-v1.html, pdd-v1.html). The example files (`example-overview.md` etc.) remain as format/persona reference only.
**Files updated:**
- `CLAUDE.md` — Phase 00 section
- `OPEN-QUESTIONS.md` — updated

---

### Entry #31 — Multi-document export: tabbed HTML and paginated PDF
**Date:** Session 2
**Decision:** When two or more documents are exported together, HTML output uses a tabbed interface (one tab per document). PDF output uses a page break and document header per section. Applies to Phase 00 Foundation Documents and all other combined exports (e.g. 05 + 06 + 07 together).
**Files updated:**
- `CLAUDE.md` — output formatting rules section

---

### Entry #32 — Phase 00 is always a checkpoint
**Date:** Session 2
**Decision:** Phase 00 always stops cleanly after generating Foundation Documents regardless of mode. Full launch pauses and waits for the user to return and explicitly continue. À la carte Phase 00 stops entirely. `questionnaire-responses.md` is saved at the end of Phase 00 for session resumption. Claude Code detects this file at startup in subsequent sessions and offers to pre-fill context.
**Files updated:**
- `CLAUDE.md` — Phase 00 checkpoint section, à la carte routing section

---

### Entry #33 — Dependency model finalized
**Date:** Session 2
**Decision:** Phase 01 (Prototype) is a hub — version bumps cascade to Roadmap and Foundation Documents. Phases 05, 06, 07 are independent peers with no dependency on each other and can run in parallel or standalone. Phase 04 (User Stories) is skippable — GTM phases do not require it.
**Files updated:**
- `CLAUDE.md` — phase sequence, Phase 01, Phases 05/06/07 sections
- `dependency-map.html` — visual reference updated to v3

---

### Entry #34 — Feedback loops defined
**Date:** Session 2
**Decision:** Full set of feedback loops established and documented:
- 03-5 Unified Review → Prototype (accepted finding triggers version bump)
- Prototype update → Foundation Documents (Overview, PRD, PDD)
- Prototype update → Roadmap
- Phases 05/06/07 → User Stories (gaps surface new stories)
- Phases 05/06/07 → Roadmap (reprioritization)
- Dev track (future) → Prototype + User Stories + Roadmap
**Files updated:**
- `CLAUDE.md` — feedback loops referenced throughout phase sections
- `dependency-map.html` — feedback loops visualized

---

### Entry #35 — Dev track placeholder established
**Date:** Session 2
**Decision:** Dev track reserved as Phase 08+ for a future session. Inputs: Prototype, Roadmap, User Stories. Outputs: dependency map, architecture diagrams, workflow diagrams, sprint planning starting point. Claude Code does not have access to the BSN codebase — dev track artifacts are structured starting points the engineering team adapts.
**Files updated:**
- `CLAUDE.md` — dev track section
- `dependency-map.html` — dev track placeholder node

---

### Entry #36 — Prototype staging pattern
**Date:** Session 2
**Decision:** Claude Code never writes a new prototype version automatically. All changes — from any source (Unified Review findings, ad-hoc PO requests, cascade updates) — are staged in `logs/staged-changes.md` and require explicit user approval before a new versioned file is written. Staged changes accumulate; Claude Code presents the full list and waits for user to approve, modify, defer, or cancel before writing.
**Files updated:**
- `CLAUDE.md` — prototype staging pattern section (new)
- `01-prototype.md` — version bump behavior updated

---

### Entry #37 — staged-changes.md lifecycle
**Date:** Session 2
**Decision:** `logs/staged-changes.md` is a persistent file that survives across sessions. Entry format includes: change ID, source, description, status (Pending / Approved / Deferred / Removed), target version, date added, notes. After a version is written, approved entries are archived. Deferred entries stay active and are surfaced at the start of the next version bump prompt. "Actually never mind" conversational reversals remove the entry immediately with no file write.
**Files updated:**
- `CLAUDE.md` — prototype staging pattern section
- File structure — `logs/staged-changes.md` added

---

### Entry #38 — bsn-brand-fallback.md created
**Date:** Session 2
**Decision:** Local brand fallback file created with minimum brand tokens: full color palette, typography with fallback stacks, required structural elements (accent lines, header, footer, hex dot texture, cards, pill badges, teal checkmarks), layout modes, HTML output pattern, hard rules, and a third-tier fallback for when even this file is missing.
**Files updated:**
- `bsn-brand-fallback.md` — new file

---

## Entries pending confirmation

| Entry | Status |
|-------|--------|
| #5 | ✅ Resolved — Session 2. Option A confirmed. See Entry #36 for staging pattern that governs when version bump executes. |

---

## Reconciliation pass instructions

When all phase files are built and it is time to write `CLAUDE.md`, run through each entry above in order and update the files listed under "Files to update." Mark each file as ✅ Current in the reconciliation status table above when done. Do not write `CLAUDE.md` until all files show ✅ Current.

**Session 2 status:** All files current. Full reconciliation complete.
