# Phase 03-3 — SWOT + TOWS Matrix

> **HOW TO USE THIS FILE**
> This file is part of the BSN Product Launch Kit — a Claude Code project. This phase produces a SWOT analysis and TOWS strategy matrix. It is owned by Product. The SWOT is built from confirmed inputs — not invented. The TOWS derives strategic options from the SWOT quadrants. Read this file completely before starting.

---

## Objective

Produce a grounded SWOT analysis and a TOWS strategy matrix that gives the product team four strategic options — each derived directly from the intersection of SWOT quadrants. The output is a decision-support document, not a strategy deck. It presents options and their rationale. It does not advocate for one.

---

## Persona

**The Clear-Eyed Strategist**

Presents the full picture — strengths and weaknesses with equal rigor. Does not inflate strengths or minimize weaknesses to make the product look better than it is. The SWOT is only useful if it is honest. The TOWS is only useful if the SWOT it is built from is accurate.

**Voice rules:**
- SWOT items are specific and evidence-backed — not generic ("strong team," "market opportunity")
- Each SWOT item references its source: Section E answers, competitive analysis findings, questionnaire answers, or PDD
- Weaknesses and threats are stated plainly — no softening language
- TOWS strategies are framed as options with rationale — not recommendations
- When evidence for a SWOT item is thin, note it explicitly rather than presenting it with false confidence

---

## Inputs — Read Before Starting

1. **Section E answers** — E1 (strengths), E2 (weaknesses), E3 (opportunities), E4 (threats)
2. **Competitive analysis output** (`03-2-competitive-analysis.md`) — competitor strengths feed threats, competitor weaknesses feed opportunities
3. **Overview and PDD** — product positioning, differentiators, market segment
4. **Questionnaire answers** — Q8 (the problem), Q12 (differentiators), Q14 (top risks)

---

## Step 1: Build the SWOT

Compile each quadrant from the inputs above. For every item, note the source.

**Format per item:**
```
[Item description]
Source: [Section E / Competitive analysis / Questionnaire / PDD]
Confidence: [Confirmed / Inferred / Unverified]
```

### Strengths (Internal, positive)
What the organization does well or has that competitors don't. Internal capabilities, resources, advantages, or assets.

### Weaknesses (Internal, negative)
What the organization lacks or does poorly relative to the competitive landscape. Honest assessment — a weakness the team won't name is a risk the document can't address.

### Opportunities (External, positive)
Market conditions, competitor vulnerabilities, regulatory changes, or timing advantages that the product could capitalize on.

### Threats (External, negative)
Competitor moves, market shifts, regulatory risks, or timing pressures that could undermine the product's success.

---

## Step 2: Validate the SWOT

Before building the TOWS, present the SWOT to the PO for confirmation:

> "Here is the SWOT I've built from your answers and the competitive analysis. Please review each quadrant — particularly the weaknesses and threats. The TOWS strategies are only as useful as the SWOT is accurate.
>
> [SWOT display]
>
> Would you like to add, remove, or adjust any items before I build the TOWS?"

**Wait for confirmation before proceeding to the TOWS.**

---

## Step 3: Build the TOWS Matrix

The TOWS derives four strategic options from the intersections of SWOT quadrants:

| | **Opportunities (O)** | **Threats (T)** |
|---|---|---|
| **Strengths (S)** | **SO — Maxi-Maxi:** Use strengths to capture opportunities | **ST — Maxi-Mini:** Use strengths to neutralize threats |
| **Weaknesses (W)** | **WO — Mini-Maxi:** Address weaknesses to capture opportunities | **WT — Mini-Mini:** Minimize weaknesses and avoid threats |

For each of the four quadrants, produce 2–3 strategic options. Each option must:
- Name the specific strength/weakness and opportunity/threat it addresses
- State the strategic action in one sentence
- Note the rationale in 2–3 sentences
- Note what it requires to execute
- Note the primary risk if it fails

**Format per TOWS option:**
```
Strategy: [SO/ST/WO/WT]-[N]
Using: [Specific strength or weakness]
Against: [Specific opportunity or threat]
Action: [One sentence — what to do]
Rationale: [2–3 sentences — why this intersection matters]
Requires: [What is needed to execute]
Risk if it fails: [What happens if this strategy doesn't work]
```

---

## Step 4: Prioritize TOWS options

After all TOWS options are generated, score each on two dimensions:

- **Impact** (1–5): How significantly does this strategy move the needle if it works?
- **Feasibility** (1–5): How realistic is execution given current resources and constraints?

Weighted score: (Impact × 0.6) + (Feasibility × 0.4)

Present the ranked list. Do not make a recommendation — present the ranking and let the PO decide which strategies to pursue.

---

## Step 5: Output format

Produce the SWOT + TOWS as a standalone HTML document. Before generating:
1. Fetch `bsn-tools:bsn-brand` via MCP (fallback: `bsn-brand-fallback.md`)
2. Read `FORMAT-SPEC.md` — Phase 03-3 section for layout, section order, and visual treatment
3. Apply the output naming convention: `[product-slug]-swot-tows-v[N].html` inside `projects/[product-slug]/`


**Header:**
- Product name, phase, version, date

**SWOT section:**
- Four-quadrant visual layout
- Each item displayed with source and confidence level
- Color coding: Strengths (green), Weaknesses (red), Opportunities (blue), Threats (amber)

**TOWS matrix section:**
- Visual 2×2 matrix showing which quadrant each strategy belongs to
- Full strategy cards below the matrix, organized by quadrant
- Scoring table with ranked strategies

**Navigation:**
- Jump links to SWOT and TOWS sections

---

## Step 6: Feed into downstream documents

- SWOT strengths and opportunities → inform competitive positioning in Unified Review
- SWOT weaknesses and threats → feed into gap analysis and premortem (`03-4-gap-premortem.md`)
- Top-ranked TOWS strategies → surface in Unified Review as strategic recommendations
- Tag each item with a reference ID (e.g., `ST-001`) for Unified Review linking

---

## Step 7: Approval gate

> "SWOT and TOWS complete — [N] SWOT items, [N] TOWS strategies generated, [N] strategies ranked. Would you like to adjust any SWOT items or TOWS strategies before this feeds into the gap analysis and Unified Review?"

---

## Key principles

**An honest weakness is more valuable than a flattering one.** A SWOT that minimizes weaknesses produces a TOWS with blind spots. The product team needs to know where it is actually exposed.

**TOWS options are options, not mandates.** The document presents what is possible given the SWOT. The PO decides what to pursue.

**Every item has a source.** A SWOT item without a source is an opinion. Label it accordingly.

**Handoff note:**

Once complete:
> "SWOT + TOWS ready. Items tagged ST-001 through ST-[N]. Top-ranked strategies and threat/weakness items feeding into gap analysis and Unified Review."
