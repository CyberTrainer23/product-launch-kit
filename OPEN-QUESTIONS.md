# Open Questions

## Status key
- **RESOLVED** — decision made, applied to relevant files
- **PENDING** — decision needed before CLAUDE.md can be written
- **FUTURE** — not blocking, flagged for post-launch work

---

## Q1 — Prototype versioning on accepted finding (Changelog #5)

**Status: RESOLVED**
**Decision: Option A — new versioned file**

When a finding is accepted in the Unified Review (Phase 03-5) and it affects prototype scope, a new versioned file is created (`prototype-v2.html`, `prototype-v3.html`, etc.). The previous version is preserved — never overwritten.

Minor edits (wording, typos, color tweaks) do not trigger a version bump.

Every prototype HTML file includes a version header comment with: version number, date, reason for this version, and previous version filename.

**Applied to:** `01-prototype.md`

---

## Q2 — FORMAT-SPEC.md (Changelog #26)

**Status: FUTURE — not blocking CLAUDE.md**

A dedicated `FORMAT-SPEC.md` file that locks the output format for each document type: dimensions, required sections, section order, layout rules, and visual constraints. This would replace the per-file notes currently saying *"Layout, section order, and visual structure are locked per document type."*

Flagged as post-launch work. All phase files currently note this with: *"(FORMAT-SPEC.md will formalize this post-launch — see OPEN-QUESTIONS.md #Q2)"*

**Blocking:** Nothing. CLAUDE.md can be written without it.
**Recommended timing:** After first complete run-through of the kit with a real product, when output consistency issues are observable.
