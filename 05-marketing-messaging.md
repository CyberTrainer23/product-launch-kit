# Phase 05 — Marketing Messaging

## Purpose
Generate a complete marketing messaging framework for the product or feature. This phase serves a **dual mandate**: it produces both the external-facing messaging the market will see and the internal enablement messaging that helps BSN's channel partners (MSPs) sell confidently. These are distinct outputs with different audiences, voices, and goals.

---

## When This Phase Runs
- Triggered after Phase 04 (User Stories) completes
- If Phase 03 ran: accepted risks from `risks-log.md` are factored into messaging — avoid building campaigns around capabilities flagged as high-risk or unresolved

---

## Output

**File:** `marketing-messaging.html`
**Format:** Single-file HTML, self-contained, downloadable as PDF
**Branding:** BSN brand standards required — read `bsn-tools:bsn-brand` before generating any HTML output
**Footer:** Every output must include: *"Internal use only — confidential"*
**Output consistency:** Layout, section order, and visual structure are locked per document type. Do not vary across regenerations. (FORMAT-SPEC.md will formalize this post-launch — see OPEN-QUESTIONS.md #Q2)

---

## Dual Mandate

This phase generates two messaging tracks in a single document:

| Track | Audience | Goal |
|---|---|---|
| **Market Messaging** | SMB end-customers (via MSP), direct buyers | Create demand, communicate value, drive action |
| **Channel Enablement Messaging** | MSP partners | Build confidence to sell, surface objection responses, align on pitch |

Both tracks are included in `marketing-messaging.html`. They are visually distinct sections — do not blend them.

---

## Document Structure

### Section 1 — Positioning Foundation
*Shared across both tracks. Establishes the strategic frame.*

- **Positioning statement** (internal only — not ad copy):
  ```
  For [target persona], who [need or pain],
  [Product name] is a [category]
  that [key benefit / differentiator].
  Unlike [primary alternative],
  [Product name] [key differentiator].
  ```
- **One-sentence value prop** (external-ready, plain language)
- **Three core proof points** (each: claim + supporting rationale)
- **Key differentiators vs. competition** (pull from Phase 03-2 Competitive Analysis if it ran; otherwise from questionnaire Q29–Q32)

---

### Section 2 — Market Messaging

**Audience:** SMB end-customers, direct buyers

**Voice:** Direct, human, problem-first. The problem earns the solution. No jargon. No feature laundry lists. (Mirrors Overview document persona — see `example-overview.md`)

**Required elements:**

- **Headline** — primary campaign headline (one line, ≤12 words)
- **Subheadline** — supporting context (one line, ≤20 words)
- **Body copy block** — 3–4 sentences. Open with the problem. Close with a clear action.
- **3 message pillars** — each pillar has: a label (2–3 words), a supporting sentence, and a proof point or example
- **CTA options** — 3 variations (e.g., "Start free trial," "Talk to a specialist," "See it in action")
- **Objection-aware framing** — for each of the top 3 objections from Phase 06 (if available), include one reframe sentence that can be embedded in copy

**Tone guardrails:**
- Do not use: "world-class," "cutting-edge," "revolutionary," "game-changing," "seamless," "robust"
- Do not open with the product name
- Do not start with "Introducing"
- Problem statement must be specific — not "cybersecurity is hard" but what *specifically* is hard for this persona

---

### Section 3 — Channel Enablement Messaging

**Audience:** MSP partners

**Voice:** Confident, peer-to-peer, sales-enabling. Assumes the MSP knows their SMB clients. Gives them language, not lectures.

**Required elements:**

- **MSP elevator pitch** — 3–4 sentences. What to say to a client in the first 60 seconds.
- **"Why now" frame** — the market or compliance driver that makes this timely (pull from questionnaire Q6 or Phase 03-2 if available)
- **Top 3 client objections + MSP responses** — mirror Phase 06 SMB track, reframed for the MSP as seller (not the end-customer)
- **Competitive positioning notes** — brief, direct. How to handle "we already have X" or "we're looking at Y."
- **Proof points for MSP conversations** — stats, case study hooks, or customer outcome language the MSP can drop into client conversations
- **Internal talking points** — bullet list of 5–7 things every MSP should know about this product before their first client conversation

---

### Section 4 — Message Matrix (Summary)

A quick-reference grid:

| Audience | Headline | Core value | CTA |
|---|---|---|---|
| SMB / End-customer | [headline] | [value] | [CTA] |
| MSP Partner | [headline] | [value] | [CTA] |
| [Additional segment if applicable] | | | |

---

## Risk-Aware Messaging (Changelog connection)

If `risks-log.md` exists and contains accepted risks:
- Do not build messaging claims around any capability flagged as **High** risk or **Unresolved**
- If a risk affects a proof point, add an `[ASSUMPTION]` tag: *"[ASSUMPTION] Proof point depends on [capability] — confirm with product before publishing"*
- Flag messaging that may need to be pulled back if an accepted risk materializes

---

## Generation Instructions

1. Read `bsn-tools:bsn-brand` skill — required before writing any HTML
2. Use BSN color palette, Montserrat for headlines and labels, Georgia for body copy blocks
3. Visually separate Market Messaging (Section 2) and Channel Enablement Messaging (Section 3) — different section headers, possibly different background treatment
4. Message Matrix (Section 4) renders as a table with BSN table styling
5. `[ASSUMPTION]` tags render as inline callouts (yellow background, small text)
6. Include the confidential footer

---

## Source Inputs

| Input | Used in |
|---|---|
| Questionnaire Section A (Q1–Q12) | Positioning, personas, problem statement |
| Questionnaire Section B (Q13–Q19) | Market messaging copy, PR FAQ language |
| Questionnaire Section D (Q29–Q39) | PDD positioning, competitive framing |
| Phase 03-1 Persona Analysis (if ran) | Audience-specific message tuning |
| Phase 03-2 Competitive Analysis (if ran) | Competitive positioning notes, differentiators |
| Phase 03-5 Unified Review accepted findings | Risk flags, capability scope adjustments |
| `risks-log.md` | Risk-aware messaging guardrails |

---

## Handoff Notes for Downstream Phases

- **Phase 06 (Objection Handling):** Market messaging pillar language should be consistent with objection reframes — share Section 2 before finalizing Phase 06
- **Phase 07 (Demo Script):** Positioning statement and elevator pitch are the opening frame for all three demo variants
