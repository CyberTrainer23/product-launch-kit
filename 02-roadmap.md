# Phase 02 — Product Roadmap

## Purpose
Generate a visual Now/Next/Later roadmap scoped to the product or feature. The roadmap gives stakeholders a shared view of what's in scope for launch (Now), what follows immediately after (Next), and what's on the horizon but not committed (Later). It is a communication artifact, not a sprint plan.

---

## When This Phase Runs
- Triggered automatically after Phase 01 (Prototype) completes
- Runs in sequence unless the PO explicitly skips it

---

## Resuming After a Pause

Phase 02 may run immediately after Phase 01 in a continuous session, or as a return session where the user is picking up after a break. Before generating anything, check which context files are available.

**Step 1 — Check for upstream artifacts in the working directory:**

```
Priority order (highest to lowest):
  1. prototype-v[N].html        ← primary source for Now column
  2. prd-v[N].html              ← feature scope and milestone detail
  3. overview-v[N].html         ← product framing and launch goals
  4. pdd-v[N].html              ← positioning context
  5. questionnaire-responses.md ← fallback if no HTML artifacts exist
```

Always use the highest-numbered version of each file if multiple versions exist (e.g. `prototype-v2.html` over `prototype-v1.html`).

**If prototype exists (normal or returning session):**

1. Read the prototype file in full — features visible in the prototype belong in the Now column
2. Read any foundation documents that exist (Overview, PRD, PDD)
3. Also read `questionnaire-responses.md` if it exists
4. Greet the user if this is a return session:
   > "Welcome back. I've read your prototype and foundation documents and I'm ready to build the roadmap. The prototype will anchor the Now column — let's continue."
5. Proceed to Generation Instructions

**If prototype does NOT exist but foundation documents do:**

1. Read all available foundation documents
2. Notify the user:
   > "I don't see a completed prototype file. I'll build the roadmap from your Foundation Documents instead — the Now column will be based on the PRD scope rather than prototype screens. You can rerun Phase 01 at any time and the roadmap can be updated to reflect it."
3. Proceed to Generation Instructions using PRD feature scope to populate the Now column

**If neither prototype nor foundation documents exist:**

1. Read `questionnaire-responses.md` if available
2. If that also doesn't exist, ask:
   > "I don't see a prototype, foundation documents, or a questionnaire responses file. Did you complete earlier phases, or are you starting the roadmap from scratch? If starting fresh, I'll need to run the questionnaire first."
3. If proceeding from questionnaire only, note it prominently in the roadmap output:
   > *"This roadmap was generated from questionnaire answers. Running Phase 01 (Prototype) will provide a more grounded basis for the Now column."*

---

## Output

**File:** `[slug]-roadmap-v[N].html`
**Format:** Single-file HTML, self-contained, downloadable as PDF
**Branding:** BSN brand standards required — read `bsn-tools:bsn-brand` before generating any HTML output
**Footer:** Every output must include: *"Internal use only — confidential"*
**Output consistency:** Layout, section order, and visual structure are locked per document type. Do not vary across regenerations. (FORMAT-SPEC.md will formalize this post-launch — see OPEN-QUESTIONS.md #Q2)

---

## Roadmap Structure

The roadmap is organized into three columns:

| Column | Meaning | Horizon |
|---|---|---|
| **Now** | In active development or launching at v1 | Current quarter |
| **Next** | Planned and scoped, not yet in development | Next 1–2 quarters |
| **Later** | Directional — not committed, subject to change | 3+ quarters out or post-launch |

Each column contains **cards**. Each card represents one feature, capability, or initiative.

---

## Card Anatomy

Every card must include:
- **Title** — feature or capability name (short, noun-phrase)
- **Description** — 1–2 sentences: what it does and why it matters
- **Phase tag** — see Phase Tag System below
- **Persona tag(s)** — which BSN persona(s) this card primarily serves (from `bsn-personas.md`)

Optional (include when available from questionnaire):
- **Dependency note** — if this card depends on another card or external system
- **Risk flag** — if a risk from Phase 03-4 or the risks-log.md is associated with this card

---

## Phase Tag System (Changelog #27 — Solid Colors, Locked)

Phase tags use solid background colors — no gradients, no opacity variations. These are locked.

| Tag label | Color | Hex |
|---|---|---|
| Core | BSN Navy | `#1B2A4A` |
| Growth | BSN Teal | `#00A89D` |
| Partner | BSN Purple | `#6B4C9A` |
| Platform | BSN Mint | `#3DD6C8` |
| Compliance | Slate | `#4A5568` |

Tag text is always white (`#FFFFFF`). Tags are pill-shaped (border-radius: 999px), small (font-size: 11px), uppercase, letter-spaced.

Do not introduce new tag colors without a changelog entry.

---

## Generation Instructions

When generating the roadmap HTML:

1. Read `bsn-tools:bsn-brand` skill — required before writing any HTML
2. Apply the Now/Next/Later three-column layout
3. Use solid phase tag colors per the table above — no gradients
4. Cards should use BSN card styling: white background, subtle border, drop shadow
5. Include the confidential footer on the rendered page
6. The hex dot texture may be used as a section background or header background per brand spec

---

## Source Inputs

The roadmap is populated from:
- **Questionnaire Section A** — product scope, target personas, launch goals
- **Questionnaire Section C** (if PRD track) — milestone and feature scope
- **Phase 01 Prototype** — features visible in the prototype belong in Now
- **Phase 03-3 SWOT+TOWS** (if Phase 03 ran) — strategic options may surface Next/Later items
- **Phase 03-4 Gap+Premortem** (if Phase 03 ran) — gaps not addressed at launch belong in Next or Later with a risk flag

---

## Handling Uncertainty

If the PO has not specified what belongs in Next or Later, do not fabricate. Use one of:
- A placeholder card labeled **"[To be scoped]"** with a note that the PO should confirm
- An explicit note below the roadmap: *"Next and Later columns are directional and subject to refinement."*

Never present speculative features as committed.

---

## Handoff Notes for Downstream Phases

- **Phase 04 (User Stories):** Now column items map directly to stories in scope for v1. Next/Later items are out of scope for the current story backlog unless the PO explicitly pulls them in.
- **Phase 05 (Marketing Messaging):** Now column drives the launch message. Next/Later can be referenced as "what's coming" in messaging, but must be clearly framed as roadmap, not commitments.
- **Phase 06 (Objection Handling):** If a commonly raised objection is addressed by a Next or Later card, reference the roadmap card in the objection response.
