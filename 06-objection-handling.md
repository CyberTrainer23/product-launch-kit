# Phase 06 — Objection Handling

## Purpose
Generate a comprehensive objection handling guide covering the objections most likely to arise from both SMB end-customers and MSP partners. The guide gives sales teams, MSP partners, and customer success reps a ready-to-use resource — not a script to read verbatim, but a framework they can internalize and adapt.

---

## When This Phase Runs
- Triggered after Phase 05 (Marketing Messaging) completes
- Accepted risks from `risks-log.md` are reviewed before generation — objections tied to known risks receive additional handling depth

---

## Output

**File:** `objection-handling.html`
**Format:** Single-file HTML, self-contained, downloadable as PDF
**Branding:** BSN brand standards required — read `bsn-tools:bsn-brand` before generating any HTML output
**Footer:** Every output must include: *"Internal use only — confidential"*
**Output consistency:** Layout, section order, and visual structure are locked per document type. Do not vary across regenerations. (FORMAT-SPEC.md will formalize this post-launch — see OPEN-QUESTIONS.md #Q2)

---

## Two-Track Structure

This phase generates two objection tracks in a single document:

| Track | Audience | Voice |
|---|---|---|
| **SMB Track** | End-customers (SMBs buying directly or through MSPs) | Empathetic, plain-language, ROI-aware |
| **MSP Track** | MSP partners selling to their SMB clients | Peer-to-peer, sales-enabling, assumes MSP knowledge |

The two tracks are visually distinct sections in the output. Objections may overlap (the same concern arises in both audiences) but the responses are written separately — different framing, different language, different proof points.

---

## Objection Anatomy

Every objection entry follows this structure:

```
Objection ID: [Track abbreviation]-[sequence] (e.g., SMB-03, MSP-07)
Objection: [The exact words or sentiment — as the buyer says it, not a paraphrase]
Frequency: [High | Medium | Low]
Context: [When this objection typically surfaces — e.g., "early discovery," "post-demo," "renewal"]
Root concern: [What the buyer actually fears or doubts beneath the stated objection]
Response: [2–4 sentences. Acknowledge → reframe → evidence → invite forward.]
Proof point: [Stat, case study hook, or specific example that supports the response]
Escalation note: [When to escalate to a specialist or offer a trial/POC instead of continuing to handle verbally]
Risk flag: [Risk ID from risks-log.md if this objection is connected to a known risk, or "None"]
```

---

## Frequency System

Frequency is set based on questionnaire inputs (Q34–Q37 in Section D) and, if Phase 03 ran, competitive analysis findings and persona research signals.

| Frequency | Meaning | Handling depth |
|---|---|---|
| **High** | Expected in most sales conversations | Full response required, proof point required, escalation note required |
| **Medium** | Arises in roughly half of conversations | Full response required, proof point recommended |
| **Low** | Occasional — specific contexts or persona types | Shorter response acceptable, proof point optional |

High-frequency objections are surfaced at the top of each track. Do not bury them.

---

## SMB Track

**Audience:** SMB decision-makers (typically owners, office managers, HR leads, or IT contacts at small businesses)

**Voice:** Empathetic, plain-language. Assume the buyer is busy and skeptical. Do not lecture. Do not over-explain. Acknowledge the concern before responding to it.

**Required SMB objections (always generate, even if not in questionnaire):**
1. "We already have something for this" / "We're covered"
2. "This is too expensive" / "We don't have the budget"
3. "Our employees won't do it" / "We can't get people to engage with training"
4. "We're too small to be a target" / "This doesn't apply to us"
5. "We don't have time to manage this"

**Additional SMB objections:** Generate from questionnaire Section D (Q34–Q37) inputs and Phase 03 findings if available. Minimum 8 objections total for the SMB track.

---

## MSP Track

**Audience:** MSP sales reps and account managers selling BSN products to SMB clients

**Voice:** Peer-to-peer, sales-enabling. The MSP knows their client. Give them language to use, not a lecture on why the product matters. Short, direct, quotable.

**Required MSP objections (always generate):**
1. "My client doesn't think they need this"
2. "My client had a bad experience with security training before"
3. "My client wants to wait until after [trigger event — renewal, audit, breach]"
4. "My client is already using [competitor]"
5. "I don't know enough about this product to sell it confidently"

**Additional MSP objections:** Generate from questionnaire Section D inputs. Minimum 8 objections total for the MSP track.

---

## Risk-Aware Handling

If `risks-log.md` exists and contains accepted risks:
- Cross-reference each objection against the risk log
- If an objection touches a known risk (e.g., "Does this work with [integration] our client uses?" and that integration is a known gap), set the Risk flag and add a handling note:
  ```
  [RISK FLAG: RISK-03] This objection touches a known gap. Do not over-promise. 
  Recommended response: acknowledge the roadmap item, offer an escalation to a specialist.
  ```
- Do not write objection responses that promise capabilities flagged as high-risk or unresolved

---

## Generation Instructions

1. Read `bsn-tools:bsn-brand` skill — required before writing any HTML
2. SMB Track and MSP Track are visually distinct sections — use section headers, possibly alternating background treatment
3. High-frequency objections render at the top of each track, visually flagged (e.g., "HIGH" badge in BSN Teal)
4. `[RISK FLAG]` entries render as inline callouts (amber/warning color, small text)
5. Use collapsible sections (`<details>`/`<summary>`) for individual objection entries to manage document length
6. Include an objection count summary at the top: *"SMB: X objections | MSP: Y objections"*
7. Include the confidential footer

---

## Source Inputs

| Input | Used in |
|---|---|
| Questionnaire Section D (Q34–Q37) | Objection identification, frequency calibration |
| Phase 03-1 Persona Analysis (if ran) | Root concern framing, persona-specific objection nuance |
| Phase 03-2 Competitive Analysis (if ran) | Competitive displacement objections, proof points |
| Phase 05 Marketing Messaging | Consistent reframe language across messaging + objections |
| `risks-log.md` | Risk flags on relevant objections |

---

## Handoff Notes for Downstream Phases

- **Phase 07 (Demo Script):** High-frequency objections from both tracks should be anticipated in the demo script — especially in the Discovery variant (which is pre-demo) and the objection handling section of the Full Demo variant
