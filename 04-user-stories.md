# Phase 04 — User Stories

## Purpose
Generate a structured backlog of user stories scoped to the v1 feature set. Stories follow BDD (Behavior-Driven Development) format, are organized by Epic → Feature → Story, and are written to be imported directly into Jira. Confluence is used for supporting documentation — stories themselves live in Jira.

---

## When This Phase Runs
- Triggered after Phase 02 (Roadmap) completes, or after Phase 03-5 (Unified Review) if Phase 03 ran
- Scoped to the **Now** column of the roadmap only — Next/Later items are excluded unless the PO explicitly pulls them in

---

## Output

**File:** `user-stories.html`
**Format:** Single-file HTML, self-contained, downloadable as PDF
**Branding:** BSN brand standards required — read `bsn-tools:bsn-brand` before generating any HTML output
**Footer:** Every output must include: *"Internal use only — confidential"*
**Output consistency:** Layout, section order, and visual structure are locked per document type. Do not vary across regenerations. (FORMAT-SPEC.md will formalize this post-launch — see OPEN-QUESTIONS.md #Q2)

---

## Story Format — BDD (Changelog #17)

All stories use Behavior-Driven Development format. Every story has:

### Story Header
```
Epic: [Epic name]
Feature: [Feature name]
Story ID: [Epic abbreviation]-[sequence number] (e.g., ONBRD-04)
Story title: [Verb phrase — what the user does]
Persona: [Role from system roles or BSN persona]
Priority: [Must Have | Should Have | Nice to Have]
```

### Story Body
```
As a [role],
I want to [action],
So that [outcome / value].
```

### Acceptance Criteria (Given/When/Then)
```
Given [precondition / context],
When [action the user takes],
Then [observable outcome].

Given [precondition],
When [action],
Then [outcome].
```

Include **at least 2 acceptance criteria per story**. Complex stories may have 3–5. Do not write acceptance criteria so broad that they cannot be tested.

### Additional Story Fields
```
Prototype reference: [e.g., prototype-v1.html — Screen: Assign Training]
Dependencies: [Story IDs this story depends on, or "None"]
Risk flags: [Risk ID from risks-log.md if applicable, or "None"]
Notes: [Engineering notes, open questions, ASSUMPTION tags]
```

Use `[ASSUMPTION]` tags for anything not confirmed by the PO:
```
[ASSUMPTION] Employee role cannot self-assign training — confirm with product owner.
```

---

## System Roles (Changelog #15)

All stories are written against one of these four system roles. Use the exact role names — do not abbreviate or vary:

| Role | Description |
|---|---|
| **Partner Admin** | Full configuration access across all managed accounts |
| **Manager Admin** | Full configuration access within their own account |
| **Manager** | Operational access — assigns training, reviews reports, manages employees |
| **Employee** | Task-completion access — completes assigned training, no configuration |

If a story applies to multiple roles (e.g., both Manager and Manager Admin can assign training), write one story with the broadest applicable role and note the role variants in the Notes field. Do not duplicate stories across roles unless the behavior genuinely differs.

---

## Story Hierarchy

Organize stories in this structure:

```
Epic
└── Feature
    └── Story
        └── Acceptance Criteria (Given/When/Then)
```

**Epic** = a major capability area (e.g., "Employee Onboarding," "Training Assignment," "Reporting")
**Feature** = a discrete unit of functionality within an epic (e.g., "Bulk Assignment," "Completion Notifications")
**Story** = a single user-facing behavior (e.g., "Manager assigns training to a new employee")

Each story should be completable in one sprint. If a story is too large, split it.

---

## Confluence → Jira Workflow (Changelog #16)

Stories are the source of truth in **Jira**. Confluence is used for:
- Epic-level context documents (background, goals, out-of-scope notes)
- Persona and journey context linked from stories
- Design specs and prototype links

**Workflow:**
1. This phase generates the full story set as an HTML document
2. The PO reviews and approves the HTML output
3. Approved stories are imported into Jira (manually or via CSV import)
4. Epic context documents are created in Confluence and linked from Jira epics
5. Prototype references in story fields link to the relevant `prototype-v[N].html` file

**Do not maintain a parallel story list in Confluence.** Confluence documents context; Jira owns stories.

---

## Scoping Rules

**In scope for Phase 04:**
- All features in the **Now** column of the Phase 02 roadmap
- Any features pulled in explicitly by the PO from Next/Later
- Findings from Phase 03-5 Unified Review that were accepted and affect feature scope

**Out of scope:**
- Next/Later roadmap items (unless explicitly pulled in)
- Infrastructure, DevOps, and backend stories with no user-facing behavior
- Stories that duplicate existing functionality already in production (unless the PO is explicitly replacing it)

---

## Handling Gaps and Risks

- If a gap identified in Phase 03-4 (Gap + Premortem) is not addressed by any story, flag it explicitly:
  ```
  [GAP] The following gap from Phase 03-4 has no corresponding story: [gap title]. 
  Confirm with PO whether this is accepted risk or requires a story.
  ```
- If a risk from `risks-log.md` is associated with a story, reference the risk ID in the story's Risk flags field

---

## Generation Instructions

1. Read `bsn-tools:bsn-brand` skill — required before writing any HTML
2. Render stories in the Epic → Feature → Story hierarchy, visually distinct at each level
3. Use collapsible sections (HTML `<details>`/`<summary>`) for Epics and Features to manage document length
4. Highlight `[ASSUMPTION]` and `[GAP]` tags visually (e.g., yellow badge or inline callout)
5. Include a story count summary at the top: *"X epics, Y features, Z stories"*
6. Include the confidential footer

---

## Handoff Notes for Downstream Phases

- **Phase 05 (Marketing Messaging):** Story titles and acceptance criteria are a reliable source of feature language — use them to stay consistent between product and marketing copy
- **Phase 06 (Objection Handling):** Stories with `[ASSUMPTION]` tags are potential objection surface areas — review before writing objection responses
- **Phase 07 (Demo Script):** Prototype references in stories map to the demo script screen sequence
