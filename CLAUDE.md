# CLAUDE.md — Product Launch Kit
## BSN (Breach Secure Now) · Claude Code deployment

This is the master orchestrator for the BSN Product Launch Kit. It governs how Claude Code runs all phases, routes between full launch and à la carte modes, enforces dependencies, manages versioning, applies brand standards, and handles feedback loops.

Read this file fully before executing any phase.

---

## Kit version

```
KIT_VERSION: 1.0.0
CANONICAL_REPO: https://github.com/breachsecurenow/product-launch-kit
CHANGELOG: KIT-CHANGELOG.md
```

This version field is the source of truth for which release of the kit is installed locally. When the canonical repo receives updates, the `KIT_VERSION` is incremented. Users should `git pull` before starting any new launch session to ensure they are running the latest kit files.

---

## Update Mode Detection

At the start of every session, before entering the launch flow, scan the user's first message for update intent signals.

**Trigger phrases (any of these activate Update Mode):**
- "I need to make a change to the kit"
- "update [any filename]"
- "fix [any filename or phase name]"
- "edit the kit"
- "something is wrong with [any file or phase]"
- "add [something] to the kit"
- "modify [any filename]"
- "I found an issue in [any file or phase]"
- "the kit needs a change"

**If any trigger phrase is detected:**

1. Do NOT enter the launch session flow
2. Output this message:

> "🔧 Update Mode
>
> Looks like you want to make a change to the kit. I'll walk you through the whole process — no Git knowledge needed.
>
> Reading update-kit.md..."

3. Read `update-kit.md` in full
4. Follow the instructions in `update-kit.md` exclusively for the remainder of the session

**If no trigger phrase is detected:**
Proceed with the normal launch session flow as defined below.

**Returning to Launch Mode:** If the user completes an update and wants to start a launch session in the same Claude Code window, they can say "start a launch session" or "back to launch mode." Re-read `CLAUDE.md` from the top to reset context.

---

## What this kit does

This kit guides a product team at BSN through the full go-to-market launch lifecycle — from foundation documents through GTM execution. It produces a structured set of versioned, BSN-branded HTML artifacts at each phase that can be downloaded, shared, imported into Jira, or used to inform development.

It runs in two modes:
- **Full launch** — complete sequenced run from questionnaire through GTM
- **À la carte** — one or more phases run independently, with the kit asking for any context it needs at entry

---

## File structure

```
product-launch-skill/
├── CLAUDE.md                        ← you are here
├── OPEN-QUESTIONS.md               ← outstanding decisions and future work
├── KIT-CHANGELOG.md              ← all decisions logged with entry numbers
├── dependency-map.html             ← visual reference for phase dependencies
│
├── questionnaire.md                ← Sections A–D + Step 0 doc upload
├── 00-kickoff.md                   ← Step 0 orchestrator, doc upload handler
│
├── example-overview.md             ← Overview output example + Direct+Human persona
├── example-milestone-prd.md        ← PRD output example + Precision PM persona
├── example-pdd.md                  ← PDD output example + Confident Strategist persona
│
├── 01-prototype.md                 ← Phase 01: Interactive HTML prototype
├── 02-roadmap.md                   ← Phase 02: Now/Next/Later roadmap
├── phase-03-intake.md              ← Phase 03 opt-in intake (Section E)
├── 03-1-persona-analysis.md        ← Phase 03-1: Persona analysis
├── 03-2-competitive-analysis.md    ← Phase 03-2: Competitive analysis
├── 03-3-swot-tows.md               ← Phase 03-3: SWOT + TOWS
├── 03-4-gap-premortem.md           ← Phase 03-4: Gap + premortem
├── 03-5-unified-review.md          ← Phase 03-5: Unified review + risks-log
├── 04-user-stories.md              ← Phase 04: User stories (BDD, Jira-ready)
├── 05-marketing-messaging.md       ← Phase 05: Marketing messaging
├── 06-objection-handling.md        ← Phase 06: Objection handling
├── 07-demo-script.md               ← Phase 07: Demo script (3 variants)
│
├── bsn-personas.md                 ← 8 default BSN personas
├── bsn-brand-fallback.md           ← Local brand fallback (used if MCP unavailable)
├── sharepoint.md                   ← SharePoint upload config, folder logic, replace rules
│
└── logs/
    ├── risks-log.md                ← Accepted risks, carried into Phases 05 and 06
    └── staged-changes.md           ← Pending prototype changes awaiting user approval
```

Output files are written to the working directory alongside source files, using the versioning conventions defined below.

---

## Kickoff — first thing Claude Code does

When this kit is invoked, Claude Code runs the following before anything else:

### Step 1 — Version check and greet

Before greeting the user, read the `KIT_VERSION` field above and check whether the working directory is a Git repo:

```bash
git status
```

- **If it is a Git repo:** Include an update reminder in the greeting
- **If it is not a Git repo:** Skip the update reminder

Greet the user:

> "Welcome to the BSN Product Launch Kit **v1.0.0**. Before we start — if you haven't pulled the latest kit files recently, run `git pull` now to make sure you have any updates.
>
> Are you running a **full launch sequence** from the beginning, or do you need to run a **specific phase** on its own?"

If the user says they just pulled or confirms they are up to date, proceed. If they say they haven't pulled recently, pause and let them run `git pull` before continuing:

> "Go ahead and run `git pull` in your terminal, then come back and we'll start."

**Do not block on this** — if the user wants to proceed without pulling, that is their choice. Note it and continue.

- **Full launch** → proceed to Step 2
- **À la carte** → jump to [À la carte routing](#à-la-carte-routing)

**Note:** Foundation Documents (Phase 00) is available as an à la carte option. Someone who wants an Overview, PRD, and PDD to socialize internally before any build work starts should select à la carte → Phase 00 — not full launch.

### Step 2 — Document upload (full launch only)

Read `00-kickoff.md` for the complete Step 0 document upload flow before proceeding.

Ask the user if they have any existing documents to upload:
> "Do you have any existing documents — a brief, PRD, one-pager, positioning doc, or anything else — that you'd like me to use as context? If so, share them now. If not, we'll build everything from scratch."

- If documents are provided: ingest them, extract relevant information, and use to pre-fill questionnaire answers where possible. Note any pre-filled answers with `[PRE-FILLED from: {source document}]` so the user can review.
- If no documents: proceed to questionnaire

### Step 3 — Questionnaire (full launch only)

Read `questionnaire.md`. Run Sections A through D in order. Apply pre-filled answers where available. Confirm pre-filled answers with the user before treating them as locked.

At the end of the questionnaire, proceed to Phase 00. Phase 00 always pauses cleanly after generating Foundation Documents — see Phase 00 below.

---

## Phase sequence — full launch mode

```
Questionnaire
    ↓
Phase 00 — Foundation documents (Overview v1, PRD v1, PDD v1)
    ↓ PAUSE — user confirms to continue
Phase 01 — Prototype v1
    ↓ (feeds)
Phase 02 — Roadmap
    ↓
Phase 03 — Research (opt-in)
  └── 03 intake → 03-1 → 03-2 → 03-3 → 03-4 → 03-5 Unified Review
    ↓
Phase 04 — User stories (skippable)
    ↓
Phases 05 / 06 / 07 — GTM (independent, can run in parallel)
```

Phase 00 is always a checkpoint — Claude Code pauses here regardless of mode and waits for the user to confirm before continuing. See Phase 00 below.

At all other phase transitions, announce the next phase and ask:
> "Ready to move to [Phase name], or would you like to pause here?"

Never auto-advance without confirmation.

---

## Phase 00 — Foundation documents

**Triggered by:** End of questionnaire (full launch) or à la carte entry

**Reads:** `example-overview.md`, `example-milestone-prd.md`, `example-pdd.md` for output format and persona guidance before generating

**Produces:**
- `overview-v1.html`
- `prd-v1.html`
- `pdd-v1.html`
- `questionnaire-responses.md` — saved copy of all questionnaire answers for resuming later

**HTML output format:** Tabbed interface — one tab per document (Overview / PRD / PDD). All three documents live in a single HTML file with tab navigation. Do not produce three separate files unless the user explicitly requests it.

**PDF output format:** If the user requests a PDF export, each document gets its own page break and a header at the top of its section clearly stating which document it is (e.g. "Product Overview", "Milestone PRD", "Product Description Document"). See [Output formatting rules](#output-formatting-rules).

### Phase 00 checkpoint — always pause here

After generating Foundation Documents, Claude Code always stops and delivers this message regardless of mode:

> "Your Foundation Documents are ready — Overview, PRD, and PDD are saved. Your questionnaire answers are also saved in `questionnaire-responses.md` so you won't have to repeat them when you come back.
>
> When you're ready to continue — prototype, roadmap, research, or GTM — start a new session and I'll pick up from here."

**If mode is full launch:** Stop after delivering this message. Do not auto-advance to Phase 01. The user must return and explicitly continue.

**If mode is à la carte → Phase 00:** Stop after delivering this message. Session is complete.

**When the user returns to continue:** Claude Code reads `questionnaire-responses.md` at the start of the session to restore context. Ask:
> "Welcome back. I have your questionnaire responses from the previous session. Ready to continue with Phase 01 — Prototype?"

### Bringing your own documents

If the user provides existing Overview, PRD, or PDD documents:
1. Ingest the provided documents
2. Assess whether they match BSN format and brand standards
3. If they do not match: ask the user whether to reformat to BSN spec (producing `overview-v1.html` etc.) or use as-is
4. If reformatting: produce new versioned files based on the provided content, noting what was changed
5. If using as-is: reference the original filenames in subsequent phases rather than generating new files

### Version bump triggers for Phase 00 documents

- Prototype version bump that affects feature scope, product description, or requirements
- Accepted finding from Phase 03-5 Unified Review that changes product definition
- Explicit PO request to update

On version bump: write a new versioned file (`overview-v2.html`, `prd-v2.html`, `pdd-v2.html`). Preserve all previous versions. Add a version header comment to every generated HTML file (see [Versioning conventions](#versioning-conventions)).

---

## Phase 01 — Prototype

**Reads:** `01-prototype.md` before generating any output

**Depends on:** Phase 00 (Overview, PRD) — if running à la carte, ask for this context at entry

**Produces:** `prototype-v1.html`

**The prototype is a hub.** It is not just a downstream output — it feeds back upstream. A prototype version bump triggers updates to:
- Roadmap (Phase 02) — scope changes affect Now/Next/Later placement
- Foundation documents (Phase 00) — Overview, PRD, and PDD may need new versions

**Claude Code never writes a new prototype version automatically.** All changes — from any source — are staged first and require explicit user approval before a new versioned file is written. See [Prototype staging pattern](#prototype-staging-pattern) for the full behavior.

After a new prototype version is written, Claude Code must:
1. Notify the user: *"prototype-v[N].html written. This may affect the Roadmap and Foundation Documents. Would you like me to stage those updates now?"*
2. If yes: add cascade updates to `logs/staged-changes.md` for the affected files
3. If no: log the deferred updates in `logs/staged-changes.md` with status `Deferred`

---

## Prototype staging pattern

All prototype changes go through staging before any file is written. There are no exceptions — a casual PO request and a formal Unified Review finding follow the same path.

### Three sources that feed the staging list

| Source | Example | How it enters staging |
|---|---|---|
| Accepted finding (03-5) | Gap analysis reveals a missing Manager view state | Claude Code adds automatically after Accept decision |
| Ad-hoc PO request | "Can we move that button to the top?" | Claude Code adds immediately, confirms with user |
| Cascade update | Foundation doc change that affects prototype scope | Claude Code proposes addition, user confirms |

### staged-changes.md format

Every staged change uses this structure:

```
CHANGE-[ID]: [Short title]
Source: [Unified Review finding: {title} | PO request | Cascade from: {document}]
Description: [What changes in the prototype and why]
Status: [Pending | Approved | Deferred | Removed]
Target version: [v2 | v3 | TBD]
Added: [date]
Notes: [optional context]
```

### Handling ad-hoc requests

When the user makes a conversational change request mid-session:

1. Claude Code acknowledges the request and adds it to staging:
   > "Got it — I've added that to the staged changes list. It won't be written until you approve a version bump. `staged-changes.md` has been updated."
2. If the user immediately reverses: "actually never mind" — remove it from staging:
   > "Removed. No changes written."
3. Staged changes accumulate across the session. Claude Code does not prompt for approval after every single addition — it waits until the user signals readiness or asks.

### Approval prompt

When the user is ready to write a new prototype version — or after a Unified Review completes — Claude Code presents the full staged list:

> "You have [N] staged changes for the prototype:
>
> 1. [Source] [Description] — Status: Pending
> 2. [Source] [Description] — Status: Pending
> 3. [Source] [Description] — Status: Deferred (from previous session)
>
> Options:
> - Approve all and write prototype-v[N]
> - Approve specific changes only
> - Edit a change description before approving
> - Defer one or more to a future version
> - Cancel — keep all as Pending"

Claude Code only writes the new versioned file after the user selects an approve option and confirms.

### After writing a new version

1. Write  with the version header comment
2. Update all approved changes in  — status → Written, add version number
3. Remove Written entries from the active list (or archive them in a  section at the bottom of the file)
4. Keep Deferred entries at the top of the active list for the next version
5. Append to 
6. Prompt about cascade updates to Roadmap and Foundation Documents (see Phase 01)

### Deferred changes

Deferred changes stay in `staged-changes.md` with status `Deferred` and a `Target version` note. At the start of any subsequent prototype version bump approval prompt, Claude Code surfaces them first:

> "You have [N] deferred change(s) from a previous session. Would you like to include any of them in this version?"

If `staged-changes.md` does not exist, treat it as empty. Create it on the first staged change.

---

## Phase 02 — Roadmap

**Reads:** `02-roadmap.md` before generating any output

**Depends on:** Phase 01 (Prototype) — features visible in the prototype anchor the Now column

**Produces:** `[slug]-roadmap-v1.html`

**Feedback loop:** If Phase 05, 06, or 07 surfaces competitive or market findings that reprioritize features, the user may request a roadmap update. On update: write a new versioned file (`roadmap-v2.html`, etc.) per Option A versioning. Log the update in `KIT-CHANGELOG.md`.

---

## Phase 03 — Research (opt-in)

**Reads:** `phase-03-intake.md` before asking Section E questions

**Opt-in trigger:** After Phase 02 completes, ask:
> "Would you like to run Phase 03 research before moving to user stories? This includes persona analysis, competitive analysis, SWOT + TOWS, and a gap/premortem. It's optional but produces stronger downstream outputs. You can also run it later."

Options:
- **Yes, run it now** → proceed with full Phase 03
- **Run a lighter version** → ask which sub-phases to include
- **Ask me later** → skip for now, offer again before Phase 04
- **Skip entirely** → proceed to Phase 04

**Sub-phase order:** 03 intake → 03-1 → 03-2 → 03-3 → 03-4 → 03-5 (Unified Review)

Sub-phases 03-1 through 03-4 can run in any order, but all must complete before 03-5 (Unified Review) runs.

**Phase 03-5 Unified Review outputs:**
- Decision on each finding: Accept / Accept Risk / Reject
- Accepted risks written to `logs/risks-log.md`
- Accepted findings that affect prototype scope trigger a prototype version bump (see Phase 01)

**Reads before generating each sub-phase:**
- `03-1-persona-analysis.md` for Phase 03-1
- `03-2-competitive-analysis.md` for Phase 03-2
- `03-3-swot-tows.md` for Phase 03-3
- `03-4-gap-premortem.md` for Phase 03-4
- `03-5-unified-review.md` for Phase 03-5

---

## Phase 04 — User stories

**Reads:** `04-user-stories.md` before generating any output

**Depends on:** Phase 01 (Prototype) and Phase 02 (Roadmap) — stories are scoped to the Now column and reference prototype screens

**Skippable:** Yes. If the user does not need a Jira-ready story backlog, Phase 04 can be skipped entirely. Phases 05, 06, and 07 do not depend on it.

**If running à la carte:** Ask at entry:
> "Do you have an existing prototype or roadmap I should reference? If so, share the files or describe the feature scope. Otherwise I'll ask a few questions to establish scope."

**Produces:** `user-stories.html`

---

## Phases 05, 06, 07 — GTM phases

These three phases are **independent peers**. They:
- Do not depend on each other
- Can run in parallel or in any order
- Can each be run standalone via à la carte mode
- All pull from the same upstream context (questionnaire, Phase 00 docs, prototype, Phase 03 findings if available, `logs/risks-log.md`)

**Reads before generating each phase:**
- `05-marketing-messaging.md` for Phase 05
- `06-objection-handling.md` for Phase 06
- `07-demo-script.md` for Phase 07

**Produces:**
- `marketing-messaging.html`
- `objection-handling.html`
- `demo-script.html`

**Feedback loops from GTM phases:**
- If a gap or competitive finding surfaces during Phase 05, 06, or 07 that affects user stories: note it and ask the user whether to add a story or flag for the next sprint
- If a finding affects roadmap prioritization: offer to update `roadmap.html`
- Neither update is automatic — always ask before writing

---

## À la carte routing

When the user selects à la carte mode at kickoff, ask:

> "Which phase do you need?
>
> **00 — Foundation documents** (Overview, PRD, PDD) — good starting point if you're not ready to build yet
> 01 — Prototype
> 02 — Roadmap
> 03 — Research (persona, competitive, SWOT, gap/premortem)
> 04 — User stories
> 05 — Marketing messaging
> 06 — Objection handling
> 07 — Demo script"

### Resuming from a previous session

If a `questionnaire-responses.md` file exists in the working directory, Claude Code detects it at startup and asks:

> "I found saved questionnaire responses from a previous session. Would you like me to use those as context for this phase, or start fresh?"

- If yes: load responses and pre-fill all relevant context
- If no: proceed without them

### À la carte → Phase 00 behavior

Phase 00 selected à la carte runs the questionnaire, generates Foundation Documents, saves `questionnaire-responses.md`, and stops. See [Phase 00 checkpoint](#phase-00-checkpoint--always-pause-here) for the exact stop message.

### All other à la carte phases

Once the user selects a phase:
1. Check for `questionnaire-responses.md` — offer to load if present
2. Read that phase's `.md` file
3. Check what inputs the phase requires (defined in each phase file under "Source inputs")
4. Ask for any missing inputs:
   > "To run [Phase name], I need [input]. Do you have an existing file for this, or would you like to provide the key information directly?"
5. If the user provides existing files: ingest them
6. If the user provides information directly: capture it before generating output
7. Generate the phase output

**Never refuse to run a phase because upstream phases haven't been run.** Always find a path forward — either by ingesting existing documents or by asking targeted questions.

---

## Brand standards

### Primary method — MCP fetch

Before generating any HTML output, fetch the current brand specification from the BSN skills library MCP server:

```
Fetch: bsn-tools:bsn-brand
MCP server: https://mcp.dev2.api.pii-protect.com/mcp
```

Apply the full brand specification from the fetched skill to every HTML output.

### Fallback — local file

If the MCP server is unreachable, read `bsn-brand-fallback.md` and apply those rules instead. When using the fallback, append this notice to the generated file's HTML comment header:

```html
<!-- NOTICE: Brand applied from local fallback (bsn-brand-fallback.md).
     MCP server was unavailable at generation time.
     Verify output against current brand standards before sharing. -->
```

### Non-negotiable brand rules (enforced regardless of source)

These rules apply even if the MCP fetch fails and the fallback file is missing:

- Primary dark background: Navy `#082f49`
- Primary accent: Teal `#308c83`
- Accent-only color: Electric Mint `#01ffe1` — never as fill, only thin lines and badge borders
- Headings: Jubilat Bold (fallback: Georgia, serif)
- Body: Halyard Display (fallback: Montserrat, sans-serif)
- Thin `#01ffe1` accent line under every header, above every footer
- Footer text: "Internal use only — confidential"
- Hex dot texture on hero/header backgrounds

---

## Output organization and naming conventions

### Project folders

Every product launch gets its own project folder inside `projects/`. All generated output files for that launch live there.

```
product-launch-kit/
├── projects/
│   ├── ai-risk-adoption/        ← one folder per product launch
│   │   ├── ai-risk-adoption-overview-v1.html
│   │   ├── ai-risk-adoption-prd-v1.html
│   │   ├── ai-risk-adoption-pdd-v1.html
│   │   ├── ai-risk-adoption-prototype-v1.html
│   │   ├── ai-risk-adoption-roadmap-v1.html
│   │   ├── ai-risk-adoption-persona-analysis-v1.html
│   │   ├── ai-risk-adoption-competitive-analysis-v1.html
│   │   ├── ai-risk-adoption-swot-tows-v1.html
│   │   ├── ai-risk-adoption-gap-premortem-v1.html
│   │   ├── ai-risk-adoption-unified-review-v1.html
│   │   ├── ai-risk-adoption-user-stories-v1.html
│   │   ├── ai-risk-adoption-marketing-messaging-v1.html
│   │   ├── ai-risk-adoption-objection-handling-v1.html
│   │   ├── ai-risk-adoption-demo-script-v1.html
│   │   └── questionnaire-responses.md
│   └── training-only-mvp/       ← second launch, separate folder
│       └── ...
├── logs/
│   ├── risks-log.md
│   └── staged-changes.md
├── CLAUDE.md
└── ... (all kit files)
```

**At kickoff, Claude Code must:**
1. Ask for the product name if not already known
2. Derive the product slug: lowercase, hyphenated, no spaces, no special characters (e.g. "AI Risk Adoption Program" → `ai-risk-adoption`)
3. Confirm the slug with the user: *"I'll save all outputs for this launch to `projects/ai-risk-adoption/`. Does that slug look right?"*
4. Create the folder: `projects/[product-slug]/`
5. Write all outputs for this launch to that folder

**Never write output files to the kit root directory.** The root is for kit source files only.

---

### File naming convention

All generated output files follow this pattern:

```
[product-slug]-[doc-type]-v[N].html
```

| Output | File name pattern | Example |
|---|---|---|
| Overview | `[slug]-overview-v[N].html` | `ai-risk-adoption-overview-v1.html` |
| Milestone PRD | `[slug]-prd-v[N].html` | `ai-risk-adoption-prd-v1.html` |
| PDD | `[slug]-pdd-v[N].html` | `ai-risk-adoption-pdd-v1.html` |
| Prototype | `[slug]-prototype-v[N].html` | `ai-risk-adoption-prototype-v1.html` |
| Roadmap | `[slug]-roadmap-v[N].html` | `ai-risk-adoption-roadmap-v1.html` |
| Persona analysis | `[slug]-persona-analysis-v[N].html` | `ai-risk-adoption-persona-analysis-v1.html` |
| Competitive analysis | `[slug]-competitive-analysis-v[N].html` | `ai-risk-adoption-competitive-analysis-v1.html` |
| SWOT + TOWS | `[slug]-swot-tows-v[N].html` | `ai-risk-adoption-swot-tows-v1.html` |
| Gap + premortem | `[slug]-gap-premortem-v[N].html` | `ai-risk-adoption-gap-premortem-v1.html` |
| Unified review | `[slug]-unified-review-v[N].html` | `ai-risk-adoption-unified-review-v1.html` |
| User stories | `[slug]-user-stories-v[N].html` | `ai-risk-adoption-user-stories-v1.html` |
| Marketing messaging | `[slug]-marketing-messaging-v[N].html` | `ai-risk-adoption-marketing-messaging-v1.html` |
| Objection handling | `[slug]-objection-handling-v[N].html` | `ai-risk-adoption-objection-handling-v1.html` |
| Demo script | `[slug]-demo-script-v[N].html` | `ai-risk-adoption-demo-script-v1.html` |
| Questionnaire responses | `questionnaire-responses.md` | No slug prefix — one per project folder |

**Naming rules:**
- Slug: lowercase, hyphens only, no spaces, no special characters
- Doc type: exact names from the table above — no variations
- Version: always present on all outputs
- Version bumps follow Option A — new file, previous version preserved
- Multi-phase products: PRD and PDD include the phase name in the slug: `ai-risk-adoption-phase1-prd-v1.html`

---

## Output formatting rules

### Single-document export
One phase, one output file. Standard BSN HTML with header and footer.

### Multi-document export (two or more documents in one file)

**HTML:** Tabbed interface — one tab per document. Tab labels match document names (e.g. "Overview", "Milestone PRD", "PDD", "User Stories"). All tabs render in a single self-contained HTML file.

**PDF:** Each document gets:
- A page break before it
- A header at the top of its first page clearly stating what it is, e.g.:
  - "Product Overview"
  - "Milestone PRD — [Product Name]"
  - "Product Description Document"
  - "Phase 03 Research — Persona Analysis"
- BSN running header (thin teal line + small BSN mark) on subsequent pages within that document

This rule applies to all multi-document exports — Foundation Documents (Phase 00), combined GTM exports (05 + 06 + 07), or any other combination the user requests.

### Version header comment (required in every generated HTML file)

```html
<!--
  BSN Product Launch Kit
  Document: [document name]
  Version: v[N]
  Generated: [date]
  Reason: [first generation | accepted finding: {title} | prototype v{N} update | PO request]
  Previous version: [filename | none]
-->
```

---

## Versioning conventions

All four primary artifacts follow **Option A versioning**: new file on each meaningful update, previous versions preserved.

| Artifact | First file | On update |
|---|---|---|
| Overview | `overview-v1.html` | `overview-v2.html`, etc. |
| PRD | `prd-v1.html` | `prd-v2.html`, etc. |
| PDD | `pdd-v1.html` | `pdd-v2.html`, etc. |
| Prototype | `prototype-v1.html` | `prototype-v2.html`, etc. |
| Roadmap | `roadmap-v1.html` | `roadmap-v2.html`, etc. |

**What triggers a version bump:**
- Accepted finding from Phase 03-5 that affects scope, requirements, or positioning
- Prototype update that cascades to Foundation Documents or Roadmap
- GTM phase finding that reprioritizes roadmap features
- Explicit PO request to regenerate

**What does NOT trigger a version bump:**
- Wording edits, typo fixes, minor copy changes
- Metadata-only changes (date, version comment)

**GTM phase outputs** (`marketing-messaging.html`, `objection-handling.html`, `demo-script.html`) are updated in place unless the PO explicitly requests a versioned archive.

---

## risks-log.md

`logs/risks-log.md` is a shared state file that carries accepted risks across phases.

**Written by:** Phase 03-5 Unified Review (on Accept Risk decisions)

**Read by:** Phase 05 (messaging guardrails), Phase 06 (objection risk flags), Phase 07 (demo script risk flags), Phase 01 (on version bump — check if any risks affect new prototype scope)

**Format for each entry:**
```
RISK-[ID]: [Risk title]
Source: Phase [03-4 | other]
Severity: [High | Medium | Low]
Status: [Accepted | Pending Update]
Description: [What the risk is]
Affected phases: [list]
Early warning signs: [from Phase 03-4]
Notes: [any context]
```

If `logs/risks-log.md` does not exist when a phase that reads it runs, treat it as empty — do not error.

---

## KIT-CHANGELOG.md

All decisions, version bumps, phase completions, and significant changes are logged to `KIT-CHANGELOG.md` with:
- Entry number (sequential)
- Date
- Phase
- What changed
- Who triggered it (PO request / accepted finding / prototype update)

Claude Code appends to this file — never overwrites it.

---

## Dev track — future phases

The dev track is not yet built. When it is, it will produce:
- Dependency map for development tasks
- Architecture diagrams scoped to the BSN codebase
- Workflow diagrams for key user flows
- Sprint planning starting point

**Inputs it will consume:** Prototype, Roadmap, User Stories

**Feedback it will produce:** Implementation constraints that may require updates to Prototype, User Stories, and Roadmap

**Note:** Claude Code does not have access to the BSN codebase. Dev track artifacts are structured starting points that the engineering team adapts — not final specifications.

When the dev track is built, it will be added here as Phase 08+.

---

## Error handling and edge cases

**User wants to skip a phase mid-sequence:**
> "Understood — skipping [Phase]. Moving to [next phase]. Note: [downstream phase] uses [skipped output] — I'll ask you for that context when we get there."

**User provides a document that doesn't match BSN format:**
> "This document doesn't match BSN format. Would you like me to reformat it to BSN spec (producing `[filename]-v1.html`), or use it as-is for reference?"

**MCP server unreachable:**
Apply fallback brand rules. Notify the user in the file's HTML comment header. Do not block generation.

**Conflicting information between uploaded document and questionnaire answers:**
Flag the conflict explicitly:
> "[CONFLICT] Your uploaded brief says [X], but you answered [Y] in the questionnaire. Which should I use?"
Never silently resolve conflicts — always surface them.

**User asks to run a GTM phase before upstream phases exist:**
Do not refuse. Ask targeted questions to establish the minimum context needed. Proceed with what's available.

---

## Persona reference

Each phase has a named persona that governs its voice and reasoning approach. Claude Code adopts the persona for that phase's output only — it does not carry across phases.

| Phase / Document | Persona | Key traits |
|---|---|---|
| Overview | Direct + Human | Problem earns solution, real-world scenarios, plain language |
| PRD | Precision PM | Engineering-friendly, economical, ASSUMPTION tags, measurable goals |
| PDD | Confident Strategist | Marketing-first, names competitors, never hedges |
| 03-1 Persona Analysis | Empathetic Researcher | Evidence-backed, first-person voice, signal strength labeled |
| 03-2 Competitive Analysis | Intelligence Analyst | All claims sourced, Confirmed/Inferred/Unverified |
| 03-3 SWOT + TOWS | Clear-Eyed Strategist | Honest weaknesses, options not recommendations, scored |
| 03-4 Gap + Premortem | Risk-First Thinker | Facts not possibilities, past-tense failure scenarios |
| 03-5 Unified Review | — | Decision tool, no persona — neutral and structured |
| 04 User Stories | — | Functional and precise — no persona, BDD format governs |
| 05 Messaging | — | See dual mandate in `05-marketing-messaging.md` |
| 06 Objections | — | Per-track voice defined in `06-objection-handling.md` |
| 07 Demo Script | — | Per-variant voice defined in `07-demo-script.md` |

Full persona specs live in the example files and phase files listed above.

---

## Quick reference — what to read before each phase

| Phase | Read before generating |
|---|---|
| 00 | `example-overview.md`, `example-milestone-prd.md`, `example-pdd.md` |
| 01 | `01-prototype.md` |
| 02 | `02-roadmap.md` |
| 03 intake | `phase-03-intake.md` |
| 03-1 | `03-1-persona-analysis.md` |
| 03-2 | `03-2-competitive-analysis.md` |
| 03-3 | `03-3-swot-tows.md` |
| 03-4 | `03-4-gap-premortem.md` |
| 03-5 | `03-5-unified-review.md` |
| 04 | `04-user-stories.md` |
| 05 | `05-marketing-messaging.md` |
| 06 | `06-objection-handling.md` |
| 07 | `07-demo-script.md` |
| Any HTML output | `bsn-tools:bsn-brand` via MCP, fallback to `bsn-brand-fallback.md` |
| Any approved output | `sharepoint.md` — read before uploading to SharePoint |

---

## What good execution looks like

A well-run session using this kit:
- Reads the relevant phase file before generating — every time, no exceptions
- Fetches brand standards before writing HTML — every time
- Announces phase transitions and asks for confirmation before advancing
- Never silently resolves conflicts or assumptions — always surfaces them with `[ASSUMPTION]` or `[CONFLICT]` tags
- Writes version header comments in every generated HTML file
- Appends to `KIT-CHANGELOG.md` on every meaningful change
- Checks `logs/risks-log.md` in any phase that uses it — treats a missing file as empty, not as an error
- Asks targeted questions when upstream context is missing — never refuses to proceed
- Keeps the prototype's hub status in mind — a prototype version bump is never just a prototype change
