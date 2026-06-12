# Phase 07 — Demo Script

## Purpose
Generate demo scripts for the product or feature. Three variants are produced: a Discovery call script (pre-demo), a Full Demo script (main product walkthrough), and a Client Enablement script (for MSP partners demoing to their SMB clients). Each variant is a distinct artifact with its own audience, goal, and structure.

---

## When This Phase Runs
- Triggered after Phase 06 (Objection Handling) completes
- This is the final phase of the core launch sequence

---

## Output

**File:** `demo-script.html`
**Format:** Single-file HTML, self-contained, downloadable as PDF
**Branding:** BSN brand standards required — read `bsn-tools:bsn-brand` before generating any HTML output
**Footer:** Every output must include: *"Internal use only — confidential"*
**Output consistency:** Layout, section order, and visual structure are locked per document type. Do not vary across regenerations. (FORMAT-SPEC.md will formalize this post-launch — see OPEN-QUESTIONS.md #Q2)

---

## Three Demo Variants

| Variant | Audience | Goal | Typical length |
|---|---|---|---|
| **Discovery** | Prospect / potential buyer | Qualify, uncover pain, earn the full demo | 15–20 min |
| **Full Demo** | Qualified prospect, internal stakeholder | Show the product, build conviction, advance to trial or close | 30–45 min |
| **Client Enablement** | MSP partner (demoing to their SMB client) | Enable MSP to run a confident, credible demo without BSN present | 20–30 min |

All three variants are included in `demo-script.html` as navigable sections.

---

## Variant 1 — Discovery Script

**Audience:** Prospect or potential buyer
**Goal:** Qualify fit, surface pain, earn the right to run a full demo
**Voice:** Consultative, curious, low-pressure

### Structure

**Opening (2–3 min)**
- Brief agenda-setting: *"I've got [X] minutes — I want to spend most of it learning about your situation. Fair?"*
- One sentence about BSN — not a pitch, just context

**Discovery Questions (8–10 min)**
Generate 6–8 questions that surface:
- Current state: what they're doing today (or not doing)
- Pain: where the current state is failing them
- Stakes: what happens if the pain isn't addressed
- Decision context: who else is involved, what's the timeline

Questions should be open-ended. Do not include leading questions that assume the buyer has a problem.

**Qualification signals** (internal — not read aloud):
- ✓ Signs this is a good fit (green flags from questionnaire persona inputs)
- ✗ Signs this is not a good fit (disqualification signals)

**Transition to full demo (2–3 min)**
- Summarize what you heard
- Propose the full demo: *"Based on what you've shared, I think it would be worth 30 minutes showing you [specific capability]. Does that make sense?"*

**Objection handling hooks:**
- Reference the 3 highest-frequency SMB objections from Phase 06 — include brief handling language if they arise during discovery

---

## Variant 2 — Full Demo Script

**Audience:** Qualified prospect, internal stakeholder, evaluation team
**Goal:** Show the product, demonstrate value against stated pain, advance to trial or decision
**Voice:** Confident, narrative-driven, problem-first

### Structure

**Opening frame (3–5 min)**
- Reference the discovery conversation: *"You mentioned [pain point] — everything I'm going to show you today is oriented around that."*
- Set agenda: what you'll show, in what order, how long
- Defer questions to the end (or invite them at natural breaks — the script will indicate)

**Demo narrative sections**
Generate sections based on the Phase 01 Prototype screen sequence and Phase 04 User Stories (Now column). Each section follows this pattern:

```
Section title: [Feature or capability name]
Setup: [1–2 sentences — the problem this solves, before showing the UI]
Demo action: [What you do in the product — step by step]
Talk track: [What you say while doing it — 3–5 sentences]
Pause for reaction: [Yes / No — when to stop and invite the prospect to respond]
Objection anticipation: [If a Phase 06 objection is likely here, include the reframe]
Prototype reference: [prototype-v[N].html — Screen: [screen name]]
```

**Proof point moment**
- One dedicated moment in the demo to drop in a proof point (stat, customer outcome) from Phase 05 Marketing Messaging
- Placement: after the core capability demonstration, before the close

**Close / next steps (3–5 min)**
- Summarize value delivered in the demo against stated pain
- Propose a concrete next step: trial, POC, follow-up call, pricing discussion
- Do not end with "Any questions?" — end with a proposed action

---

## Variant 3 — Client Enablement Script

**Audience:** MSP partner, demoing to their SMB client
**Goal:** Give MSPs a confident, credible script they can run without BSN present
**Voice:** MSP-peer tone — practical, direct, assumes MSP sales experience

### Structure

**Prep section (for MSP — not read aloud)**
- What to know before the demo: 3–5 bullet points
- What to have ready: prototype link or live environment, relevant case study, pricing tier
- Common client profiles and how to tailor the demo for each

**Opening frame (2–3 min)**
- MSP introduces the product in their own words — script provides suggested language, not a verbatim pitch
- Positions BSN as a trusted partner, not a vendor the MSP is reselling

**Demo walkthrough (15–20 min)**
- Simplified version of the Full Demo — focused on the 3–4 capabilities most relevant to SMB clients
- Each section includes: setup sentence, demo action, talk track, MSP tip (e.g., *"Clients often ask X here — say Y"*)

**Handling client objections mid-demo**
- Pull the top 3 MSP-track objections from Phase 06
- Include brief in-line handling language at the moment in the script where the objection is most likely to arise

**Close**
- How to advance to next steps when demoing as an MSP: trial enrollment, pricing conversation, introduction to BSN specialist if needed

---

## Prototype Integration

Every demo section that shows product UI must reference the corresponding prototype screen:
```
Prototype reference: prototype-v[N].html — Screen: [screen name]
```

If the prototype has been versioned (v2, v3), reference the most current accepted version unless the PO specifies otherwise.

---

## Risk-Aware Scripting

If `risks-log.md` exists:
- Do not script demo sections around capabilities flagged as **High** risk or **Unresolved**
- If a demo section relies on a capability with an accepted risk, add a note:
  ```
  [RISK FLAG: RISK-04] This demo section relies on [capability]. 
  Confirm availability before running live. Have a fallback ready.
  ```

---

## Generation Instructions

1. Read `bsn-tools:bsn-brand` skill — required before writing any HTML
2. Three variants render as navigable sections — use a sticky tab bar or anchor navigation at the top of the document
3. Internal-only sections (qualification signals, prep notes, MSP tips) render in a visually distinct style (e.g., light gray background, "Internal" badge)
4. `[RISK FLAG]` entries render as inline callouts (amber/warning)
5. Prototype references render as inline badges linking to the file
6. Include a runtime summary at the top: *"Discovery: ~15–20 min | Full Demo: ~30–45 min | Client Enablement: ~20–30 min"*
7. Include the confidential footer

---

## Source Inputs

| Input | Used in |
|---|---|
| Questionnaire Section A (Q1–Q12) | Product scope, persona, pain points |
| Phase 01 Prototype | Demo screen sequence, UI references |
| Phase 04 User Stories | Feature narrative for Full Demo sections |
| Phase 05 Marketing Messaging | Positioning frame, elevator pitch, proof points |
| Phase 06 Objection Handling | In-script objection handling language |
| `risks-log.md` | Risk flags on demo sections |
