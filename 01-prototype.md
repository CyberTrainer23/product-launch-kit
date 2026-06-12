# Phase 01 — Interactive Prototype

## Purpose
Generate a clickable HTML prototype scoped to the product or feature described in the questionnaire. The prototype gives stakeholders a tangible artifact to react to before engineering investment, surfaces UX assumptions early, and anchors Phase 03 research if that phase runs.

---

## When This Phase Runs
- Triggered automatically after the questionnaire (Sections A + relevant B/C/D) is complete
- No opt-in required — Phase 01 always runs unless the PO explicitly skips it

---

## Resuming After a Pause

Phase 01 may start fresh (immediately after the questionnaire) or as a return session (the user paused after Phase 00 and is coming back). Before generating anything, check which situation applies.

**Step 1 — Check for existing foundation documents:**

```
Look for any of these files in the working directory:
  - overview-v1.html (or any higher version)
  - prd-v1.html (or any higher version)
  - pdd-v1.html (or any higher version)
```

**If foundation documents exist (returning session):**

1. Read all three documents in full — Overview, PRD, and PDD
2. Also read `questionnaire-responses.md` if it exists
3. Greet the user:
   > "Welcome back. I can see your Foundation Documents from Phase 00 — I've read the Overview, PRD, and PDD and I'm ready to build the prototype from that context. Let's pick up where you left off."
4. Proceed to Generation Instructions using the foundation document content as the primary source of truth. Where foundation document content and questionnaire answers conflict, use the foundation documents — they represent the refined, reviewed version of the answers.

**If foundation documents do NOT exist (fresh session):**

1. Read `questionnaire-responses.md`
2. If `questionnaire-responses.md` also doesn't exist, ask:
   > "I don't see a questionnaire responses file or any foundation documents. Did you complete Phase 00, or are you starting fresh? If starting fresh, I'll need to run the questionnaire first."
3. Proceed to Generation Instructions using questionnaire answers as the source of truth.

---

## Output

**File:** `prototype-v1.html` (first generation)
**Subsequent versions:** `prototype-v2.html`, `prototype-v3.html`, etc. — each triggered by an accepted finding from the Unified Review (Phase 03-5) or an explicit PO regen request

**Format:** Single-file HTML, self-contained, downloadable as PDF
**Branding:** BSN brand standards required — read `bsn-tools:bsn-brand` before generating any HTML output
**Footer:** Every output must include: *"Internal use only — confidential"*
**Output consistency:** Layout, section order, and visual structure are locked per document type. Do not vary across regenerations. (FORMAT-SPEC.md will formalize this post-launch — see OPEN-QUESTIONS.md #Q2)

---

## Versioning Rules (Resolved — Changelog #5)

**Option A is locked:** Each accepted finding that triggers a prototype update produces a new versioned file.

| Event | Action |
|---|---|
| First generation | Save as `prototype-v1.html` |
| Finding accepted in Unified Review → prototype scope changes | Save as `prototype-v2.html` |
| PO requests explicit regen | Increment version, save new file |
| Minor wording fix (no structural change) | Edit in place, no version bump |

**Version header comment** (required in every prototype HTML file):
```html
<!-- 
  BSN Product Launch Kit — Interactive Prototype
  Version: v[N]
  Generated: [date]
  Reason for this version: [first generation | accepted finding: {finding title} | PO regen request]
  Previous version: [prototype-v{N-1}.html | none]
-->
```

**What triggers a version bump:**
- A finding accepted in Phase 03-5 (Unified Review) that affects prototype scope, flow, or UI
- A PO-initiated regen ("regenerate the prototype with these changes")

**What does NOT trigger a version bump:**
- Wording edits, typo fixes, color tweaks
- Metadata-only changes

---

## Claude Code Behavior on Accept (Changelog #4)

When a finding is accepted in the Unified Review (Phase 03-5):
1. Claude Code writes the new versioned prototype file (`prototype-v[N+1].html`) to the output directory
2. The version header comment is populated with the accepted finding title and date
3. The previous version file is preserved — do not overwrite or delete it
4. The PO is notified of the new file path

---

## Prototype Scope

The prototype should represent the **primary user flow** described in the questionnaire. Default scope:

1. **Entry point** — how the user reaches this feature (nav, notification, onboarding step, etc.)
2. **Core interaction** — the main action the user takes (configure, review, assign, complete, etc.)
3. **Confirmation / feedback state** — what the user sees after completing the action
4. **Error state** — at least one failure or validation state

Scope is adjusted based on Q5 (product type), Q8 (target personas), and Q20–Q28 (PRD section) inputs from the questionnaire.

---

## Persona Awareness

Use the system roles from questionnaire Q26 to scope the prototype correctly:

| Role | Default access level |
|---|---|
| Partner Admin | Full configuration access |
| Manager Admin | Full configuration access within their account |
| Manager | Operational access — assigns, reviews, reports |
| Employee | Task-completion access — no configuration |

If the prototype involves role-specific views, render at least the **Employee** and **Manager** perspectives. Note which role is being shown in the prototype UI.

---

## Generation Instructions

When generating the prototype HTML:

1. Read `bsn-tools:bsn-brand` skill — required before writing any HTML
2. Apply BSN color palette, typography (Montserrat for UI labels, Georgia for any long-form copy), and visual standards
3. Use the hex dot texture as a background element per brand spec
4. Make the prototype **clickable** — use anchor links or JavaScript tab/state switching to simulate navigation between states
5. Keep copy functional but not final — label CTAs and fields clearly, but do not treat prototype copy as locked messaging
6. Include the version header comment (see Versioning Rules above)
7. Include the confidential footer on every rendered page/state

---

## Handoff Notes for Downstream Phases

- **Phase 02 (Roadmap):** Prototype informs feature scope for Now/Next/Later placement
- **Phase 03 (Research — opt-in):** Prototype is the primary stimulus for persona research (03-1) and gap analysis (03-4). Share `prototype-v1.html` with Phase 03 as a reference artifact
- **Phase 04 (User Stories):** Prototype states map directly to BDD acceptance criteria — reference prototype screens in story descriptions
- **Phase 03-5 (Unified Review):** Accepted findings that affect prototype scope trigger a version bump (see Versioning Rules above)
