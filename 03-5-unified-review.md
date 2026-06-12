# Phase 03-5 — Unified Review

> **HOW TO USE THIS FILE**
> This file is part of the BSN Product Launch Kit — a Claude Code project. This phase produces the Unified Review — a summary and decision tool fed by all four Phase 03 documents. It is not a research document. It is a decision surface. The depth lives in the source documents. This document surfaces the findings that require a decision and links back to the source for anyone who wants to dig deeper. Read this file completely before starting.

---

## Objective

Give the product owner and stakeholders a single place to review findings from all four Phase 03 documents, make Accept / Accept Risk / Reject decisions on each, and generate a post-review summary document that becomes the record of what was decided and why.

The Unified Review contains the conclusions. The source documents contain the evidence. Links between them are mandatory.

---

## Resuming After a Pause

Phase 03-5 may run as part of a continuous session or as a return after a break. All four source documents must be complete before the Unified Review can be generated — this is a hard dependency, not a recommendation.

**Check for the following files in the working directory:**

```
All four required:
  - [product-slug]-persona-analysis-v[N].html     ← findings tagged PA-XXX
  - [product-slug]-competitive-analysis-v[N].html ← findings tagged CA-XXX
  - [product-slug]-swot-tows-v[N].html            ← items tagged ST-XXX
  - [product-slug]-gap-premortem-v[N].html        ← gaps tagged GA-XXX, scenarios tagged PM-XXX

Also read if present:
  - logs/risks-log.md  ← any risks already logged from prior sessions
```

Always use the highest-numbered version of each file.

**If all four source documents exist:**
Read them in full before extracting findings. Greet the user if returning:
> "Welcome back. I've read all four Phase 03 documents and I'm ready to generate the Unified Review. Let me extract and deduplicate findings before we begin."

**If any source document is missing:**
Stop completely — do not attempt a partial Unified Review:
> "The Unified Review requires all four Phase 03 documents to be complete. I'm missing: [list]. A partial Unified Review would produce an incomplete decision record. Complete the missing phase(s) and come back — the work you've done so far is saved in the output files."

---

## Inputs — Read Before Starting

All four Phase 03 source documents must be complete before the Unified Review is generated:

1. `03-1-persona-analysis.md` output — findings tagged PA-XXX
2. `03-2-competitive-analysis.md` output — findings tagged CA-XXX
3. `03-3-swot-tows.md` output — items tagged ST-XXX
4. `03-4-gap-premortem.md` output — gaps tagged GA-XXX, scenarios tagged PM-XXX

If any source document is incomplete, stop and flag:
> "The Unified Review requires all four Phase 03 documents to be complete. [Document name] is not yet finished. Complete it before generating the Unified Review."

---

## What the Unified Review contains

**It surfaces — from source documents:**
- All Critical findings (all sources)
- All Moderate findings (all sources)
- Top 5 premortem scenarios by weighted score
- All cross-persona patterns from persona analysis
- All questionnaire conflicts from competitive analysis
- Top-ranked TOWS strategies from SWOT

**It does not contain:**
- Minor findings — these remain in the source documents only
- Full research profiles — those live in 03-2
- Full persona simulations — those live in 03-1
- Full SWOT item lists — those live in 03-3
- Full failure scenario narratives — those live in 03-4

**Every finding card links to its source document and section.**

---

## Step 1: Extract and deduplicate findings

Before generating the Unified Review, extract all Critical and Moderate findings from all four source documents. Then deduplicate:

- If the same underlying issue surfaces in multiple documents (e.g., a competitive gap in 03-2 and a product gap in 03-4), merge them into a single finding card
- Note all source IDs on the merged card (e.g., CA-003, GA-007)
- Use the highest severity of the contributing findings
- Cross-referenced findings have elevated priority — note this visually

Present the deduplicated finding count before generating:
> "I've extracted [N] findings from all four documents. After deduplication, [N] unique findings will appear in the Unified Review ([N] Critical, [N] Moderate). Ready to generate?"

**Wait for confirmation.**

---

## Step 2: Generate the Unified Review HTML

The Unified Review is an interactive HTML document. Before generating:
1. Fetch `bsn-tools:bsn-brand` via MCP (fallback: `bsn-brand-fallback.md`)
2. Read `FORMAT-SPEC.md` — Phase 03-5 section for layout and visual treatment
3. Apply the output naming convention: `[product-slug]-unified-review-v[N].html` inside `projects/[product-slug]/`
 Build it with the following structure and behavior.

### Header
- Product name, phase, version, date
- Four-column scorecard: Total findings / Critical / Moderate / Decisions made
- Link to each source document: "Full Persona Analysis →" / "Full Competitive Analysis →" etc.

### Identity bar
- Name input and role selector (Stakeholder / Product Owner / Marketing / Engineering / Sales / Leadership)
- Only Product Owner role can make Accept / Accept Risk / Reject decisions

### Tabs
Four tabs — one per source document type:
- Persona findings (PA-XXX)
- Competitive findings (CA-XXX)
- SWOT + strategic findings (ST-XXX)
- Gap + premortem findings (GA-XXX, PM-XXX)

Each tab shows:
- Progress bar (decisions made / total)
- Stats row (findings by type)
- Finding cards

### Finding cards
Each finding card follows the progressive disclosure format established in the unified review design:

**Collapsed (always visible):**
- Finding ID and source document link
- Title
- Type badge + severity badge
- Source tags (which documents contributed — e.g., PA-003, CA-007)
- One-line summary
- Decision bar (Accept / Accept Risk / Reject) — PO only

**Expanded drawer — three tabs:**
- **Details** — finding, suggested solution, mitigation, document affected, link to source document section
- **Source reactions** — persona quotes (persona tab), competitor evidence (competitive tab), scenario narrative (premortem tab)
- **Comments** — stakeholder thread with identity tracking

**After decision:**
- Decision bar replaced by confirmation strip (green/amber/red)
- Change button visible to PO only
- Source document link remains visible

### Meeting summary panel
- Toggle from header
- Shows all findings with comments, their decision status
- Serves as live agenda during review meeting

### TOWS strategies panel
- Separate collapsible section below the finding tabs
- Shows top-ranked TOWS strategies from 03-3
- Not subject to Accept/Accept Risk/Reject decisions — these are strategic options for discussion
- PO can mark each as "Pursuing," "Considering," or "Not pursuing"

---

## Step 3: Generate the review summary document

After all decisions are made, generate a review summary HTML document containing:

**Scorecard:**
- Total findings reviewed / Accepted / Risks accepted / Rejected

**Document changes queued (green block):**
- Every accepted finding with: document, section, what changes, new version number
- This becomes the instruction set for document updates

**Risks log preview (amber block):**
- Every accepted risk with carry-forward flags to downstream phases
- Links to risks-log.md entries

**Three decision sections:**
- Accepted — full detail per finding
- Risk accepted — full detail per finding
- Rejected — full detail per finding

Each finding shows: decision rationale (PO's text), stakeholder comments, who decided, timestamp

**TOWS strategy decisions:**
- Which strategies the PO is pursuing / considering / not pursuing

**Next steps:**
- Apply accepted changes to documents
- Log accepted risks to risks-log.md
- Brief relevant teams on accepted risks before launch
- Move to Phase 04

---

## Step 4: Update source documents

After the review summary is approved, apply accepted changes to the relevant documents:

- Write the change to the affected document
- Add a changelog entry to that document (version bump per versioning convention)
- Log accepted risks to `logs/risks-log.md` with carry-forward flags

---

## Step 5: Approval gate

After the review summary is generated:

> "Review complete. Here is what was decided:
> - [N] findings accepted — document changes queued
> - [N] risks accepted — logged to risks-log.md, carrying forward to phases 05 and 06
> - [N] findings rejected
>
> Ready to apply document changes and move to Phase 04?"

---

## Link format

Every finding card in the Unified Review links back to the source document. Link format:

```
Source: [Document name] → [Section name]
```

In the HTML output this renders as a clickable link that opens the source document at the relevant section. If the source documents are hosted in a known location (SharePoint, repo), use the actual URL. If not, note the document name and section so the reader can navigate manually.

---

## Key principles

**The Unified Review surfaces conclusions. The source documents contain evidence.** A PO who wants to understand why a finding is rated Critical should be able to click through to the source document in one action.

**Deduplication is mandatory.** The same issue appearing in three documents should not generate three separate decision points. One issue, one decision.

**Decisions are made here, not in the source documents.** The source documents are reference materials. The Unified Review is where decisions are recorded.

**Links are not optional.** Every finding card must link to its source. A finding without a source link is not verifiable — and a decision made on an unverifiable finding is a liability.

**Handoff note:**

Once the review summary is approved and document changes are applied:
> "Unified Review complete. Review summary saved. Document changes applied. Accepted risks logged. Ready to move to Phase 04 — User Stories when you are."
