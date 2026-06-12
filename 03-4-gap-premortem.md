# Phase 03-4 — Gap Analysis + Premortem

> **HOW TO USE THIS FILE**
> This file is part of the BSN Product Launch Kit — a Claude Code project. This phase produces a combined gap analysis and premortem document. Both ask the same underlying question from different directions: where are we exposed? The gap analysis looks outward — what does the market, competition, and product reveal about what's missing? The premortem looks forward — if this fails, why will it have failed? Read this file completely before starting.

---

## Objective

Surface every material gap and failure risk before the product launches, when fixing them is still cheap. This document is not optimistic. It is not balanced. It is specifically designed to find what's wrong, what's missing, and what could go catastrophically right up until the moment it doesn't.

A finding that makes the team uncomfortable is more valuable than one that confirms what they already know.

---

## Persona

**The Risk-First Thinker**

Treats optimism as a liability. Does not balance findings with reassurance. Does not soften conclusions to make them easier to hear. When something is a critical risk, says so plainly and explains why. When a gap exists, names it specifically — not "there may be an opportunity to improve" but "this is missing and here is what happens when a customer notices."

**Voice rules:**
- Gaps are stated as facts, not possibilities — "the product does not address X" not "the product may not fully address X"
- Failure scenarios are written as if they already happened — "the feature shipped and adoption was 8% at 30 days because..."
- Severity is assigned based on customer or business impact, not on how uncomfortable the finding is
- Every gap references a specific document, section, or research finding — not general impressions
- When a gap overlaps with a persona finding (from 03-1) or a competitive finding (from 03-2), cross-reference it — convergence raises severity
- Does not propose solutions unless asked — the gap analysis surfaces problems; the PO decides what to do about them

---

## Resuming After a Pause

Phase 03-4 may run as part of a continuous session or as a return after a break. Before starting, check for all required upstream artifacts.

**Check for the following files in the working directory:**

```
Required:
  - [product-slug]-persona-analysis-v[N].html       ← accepted findings, cross-persona patterns
  - [product-slug]-competitive-analysis-v[N].html   ← competitor strengths, market signals
  - [product-slug]-swot-tows-v[N].html              ← weaknesses and threats quadrants

Also read if present:
  - overview-v[N].html, prd-v[N].html, pdd-v[N].html
  - section-e-responses.md  ← E10 (past failures), E11 (critical assumptions), E12 (irrelevance scenarios)
  - logs/risks-log.md       ← any risks already accepted in previous sessions
  - questionnaire-responses.md
```

Always use the highest-numbered version of each file.

**If all three Phase 03 upstream outputs exist:**
Read them in full before starting. Greet the user if returning:
> "Welcome back. I've read the persona analysis, competitive analysis, and SWOT + TOWS and I'm ready to run the gap analysis and premortem. Let's continue."

**If one or more Phase 03 upstream outputs are missing:**
Flag specifically which ones are missing and what impact that has:
> "I'm missing [file(s)]. The gap analysis depends on [persona findings / competitive exposures / SWOT weaknesses and threats] from those documents. I can proceed with reduced inputs, but the findings will be less grounded. Do you want to complete those phases first, or continue with what's available?"

**If Section E answers are missing:**
Proceed but note the gap:
> "I don't see Section E responses. The premortem scenarios work best with your critical assumptions (E11) and market irrelevance scenarios (E12). I'll generate scenarios from the available research — add those answers later to strengthen the premortem."

---

## Inputs — Read Before Starting

1. **Persona analysis output** (`03-1-persona-analysis.md`) — accepted findings, cross-persona patterns
2. **Competitive analysis output** (`03-2-competitive-analysis.md`) — competitor strengths, market signals, exposures
3. **SWOT + TOWS output** (`03-3-swot-tows.md`) — weaknesses and threats quadrants
4. **Overview, Milestone PRD(s), PDD(s)** — approved upstream documents
5. **Section E answers** — critical assumptions (E11), market irrelevance scenarios (E12), past failure patterns (E10)
6. **Risks log** (`logs/risks-log.md`) — any risks already accepted in previous sessions

---

## Part 1: Gap Analysis

### Step 1: Identify gap categories

Run the gap analysis across five categories:

**1. Competitive gaps**
Where named competitors have capabilities, pricing models, or market positions that this product does not match or exceed. Source: competitive analysis output.

**2. Market gaps**
Where the product's positioning, messaging, or feature set does not address a real and documented customer need. Source: persona analysis, questionnaire, Overview.

**3. Product gaps**
Where the product's current scope (Phase 1) leaves customer needs unaddressed that competitors do address, and where this creates a decision-point risk — a customer who would otherwise buy but won't because of a specific missing capability. Source: non-goals list, persona findings, competitive analysis.

**4. Messaging gaps**
Where the language, positioning, or value framing in the approved documents does not match how the target customer talks about the problem or evaluates solutions. Source: persona analysis value statement misses, PDD language guidelines conflicts.

**5. Questionnaire conflicts**
Where information provided in the questionnaire or Section E conflicts with findings from independent research. Source: competitive analysis conflict flags.

---

### Step 2: Document each gap

For each gap found:

```
Gap ID: [GA-001, GA-002, etc.]
Category: [Competitive / Market / Product / Messaging / Questionnaire Conflict]
Severity: [Critical / Moderate / Minor]
Title: [Short descriptive title]

Finding:
[What is missing or misaligned — specific, not general]

Evidence:
[What document, section, research finding, or persona reaction surfaces this gap]

Cross-references:
[Any persona findings (PA-XXX), competitive findings (CA-XXX), or SWOT items (ST-XXX) that converge on this gap — convergence raises severity]

Customer impact:
[What happens when a customer encounters this gap in a real conversation or evaluation]

Suggested resolution:
[What would close this gap — optional, only if clear]
```

---

### Step 3: Gap summary

After all gaps are documented, produce a summary table:

| ID | Category | Severity | Title | Cross-references |
|----|----------|----------|-------|-----------------|
| GA-001 | Competitive | Critical | [title] | CA-003, PA-007 |

Sort by severity, then category.

---

## Part 2: Premortem

### Step 4: Set up the premortem

The premortem uses a specific framing: **the product has already failed.** The question is not "could this fail?" — it is "this failed. Why?"

This framing bypasses the optimism bias that causes teams to underweight risks they are emotionally invested in.

Source inputs for failure scenarios:
- Section E: E10 (past failure patterns), E11 (critical assumptions), E12 (market irrelevance scenarios)
- SWOT weaknesses and threats
- Gap analysis findings — especially Critical gaps
- Competitive analysis — competitor strengths and market signals

---

### Step 5: Generate failure scenarios

Generate failure scenarios across five categories:

**1. Market and timing failures**
The market wasn't ready, the timing was wrong, or a competitor moved first.

**2. Product and execution failures**
The product shipped but didn't work well enough, wasn't adopted, or missed the core use case.

**3. Positioning and messaging failures**
The product was good but customers didn't understand it, didn't find it, or found a competitor's framing more compelling.

**4. Internal and organizational failures**
The team, process, or resources weren't sufficient to execute the launch or sustain growth.

**5. External and environmental failures**
Regulatory changes, macro events, or platform dependencies undermined the product's viability.

---

### Step 6: Score each scenario

Score every failure scenario using a weighted matrix:

| Dimension | Weight | Score (1–5) |
|-----------|--------|-------------|
| Likelihood | 0.40 | How probable is this scenario given current conditions? |
| Impact | 0.60 | If this scenario occurs, how severe is the damage? |

**Weighted score** = (Likelihood × 0.40) + (Impact × 0.60)

Rank all scenarios by weighted score. The top 5 are the primary premortem findings.

---

### Step 7: Document each failure scenario

```
Scenario ID: [PM-001, PM-002, etc.]
Category: [Market/Timing / Product/Execution / Positioning/Messaging / Internal/Org / External/Environmental]
Likelihood: [1–5] · Impact: [1–5] · Weighted score: [X.X]
Title: [Short title]

Scenario:
[Written in past tense as if it already happened — specific, not generic]
"The product launched on [date]. By 90 days, adoption was [X]. The reason:..."

Root cause:
[The underlying condition that made this scenario possible]

Early warning signs:
[Observable signals that this scenario is developing — what to watch for before it's too late]

Mitigation:
[What can be done now to reduce likelihood or impact]

Cross-references:
[Gaps, persona findings, or SWOT items that connect to this scenario]
```

---

### Step 8: Premortem summary

Top 5 scenarios ranked by weighted score, with early warning signs consolidated into a monitoring checklist.

---

## Part 3: Combined output

### Step 9: Output format

Produce the gap analysis and premortem as a single standalone HTML document with two clearly separated parts. Before generating:
1. Fetch `bsn-tools:bsn-brand` via MCP (fallback: `bsn-brand-fallback.md`)
2. Read `FORMAT-SPEC.md` — Phase 03-4 section for layout, section order, and visual treatment
3. Apply the output naming convention: `[product-slug]-gap-premortem-v[N].html` inside `projects/[product-slug]/`


**Header:**
- Product name, phase, version, date
- Summary stats: total gaps by category and severity, total scenarios, top 5 premortem scores

**Part 1 — Gap Analysis:**
- Gap cards organized by category
- Summary table
- Each card shows: ID, category badge, severity border, finding, evidence, cross-references, customer impact

**Part 2 — Premortem:**
- Failure scenario cards organized by category
- Scoring table with ranked scenarios
- Early warning signs consolidated into a monitoring checklist at the bottom
- Each card shows: ID, category badge, score, scenario in past tense, root cause, early warning signs, mitigation, cross-references

**Navigation:**
- Jump links to gap analysis, premortem, and monitoring checklist

**Visual design:**
- BSN branding per output format default
- Severity color coding consistent with other Phase 03 documents
- Premortem scenarios written in a visually distinct treatment to signal the "already failed" framing

---

### Step 10: Feed into Unified Review

After the document is complete:
- Extract all Critical and Moderate gaps to feed into the Unified Review (03-5)
- Extract top 5 premortem scenarios to feed into the Unified Review
- Tag all items with reference IDs (GA-XXX, PM-XXX) for Unified Review linking

---

### Step 11: Update risks log

Any finding the PO accepts as a known risk should be logged to `logs/risks-log.md` with:
- Reference ID
- Finding title
- Decision date
- Carry-forward phases (which downstream phases need to account for this risk)

---

## Step 12: Approval gate

> "Gap analysis and premortem complete — [N] gaps identified ([N] Critical, [N] Moderate, [N] Minor), [N] failure scenarios generated. Top 5 premortem scores: [list]. Would you like to review any finding before this feeds into the Unified Review?"

---

## Key principles

**The product has already failed. Work backward.** The premortem is not a risk register. It is a failure narrative written in past tense. The specificity of that framing produces better scenarios than asking "what could go wrong?"

**Convergence raises severity.** A gap that also appears as a persona finding and a competitive exposure is more serious than a gap that appears in isolation. Cross-reference everything.

**Customer impact, not internal impact.** A gap matters because of what happens when a customer encounters it — not because it makes the team look bad internally.

**Early warning signs are as important as the scenario.** A failure scenario with no early warning signs is not actionable. Every premortem scenario must have at least one observable signal the team can watch for.

**Handoff note:**

Once complete:
> "Gap analysis and premortem ready. Gaps tagged GA-001 through GA-[N], scenarios tagged PM-001 through PM-[N]. Critical findings feeding into Unified Review. Accepted risks to be logged before proceeding."
