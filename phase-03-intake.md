# Phase 03 — Strategic Analysis Intake

> **HOW TO USE THIS FILE**
> This file is part of the BSN Product Launch Kit — a Claude Code project. This file is read only when Phase 03 is about to run AND the PO has opted into the full strategic analysis. It is never read at kickoff. It contains Section E — the additional questions needed to generate the Persona Analysis, Competitive Analysis, SWOT + TOWS, and Gap Analysis + Premortem documents. Read this file completely before asking any questions.

---

## Resuming After a Pause

Phase 03 intake may run as part of a continuous session or as a return. Before asking any Section E questions, check whether answers have already been captured.

**Check for the following in the working directory:**

```
  - section-e-responses.md     ← previously captured Section E answers
  - questionnaire-responses.md ← may contain partial Section E answers from kickoff
  - Any uploaded documents     ← competitive briefs, SWOTs, win/loss reports
```

**If `section-e-responses.md` exists:**
Read it in full. Identify which questions are already answered. Do not re-ask answered questions — only ask for what's missing or needs confirmation:
> "Welcome back. I can see Section E was partially completed. I have answers for [E1, E2, E5...]. I still need [E3, E8, E11]. Want to continue from where we left off?"

**If only `questionnaire-responses.md` exists:**
Scan it for any Section E content that may have been captured there. Apply the same pre-fill logic — suggest confirmed answers, flag partial ones, ask only what's missing.

**If neither exists:**
Proceed with the full Section E interview from the top.

---

## Opt-in trigger

Before reading this file or asking any Section E questions, confirm the PO's intent:

> "Before we run Phase 03 — do you want the full strategic analysis? That includes:
> - Persona Analysis (deep simulation against each document)
> - Competitive Analysis (web-researched, data-backed competitor profiles)
> - SWOT + TOWS Matrix (strengths, weaknesses, opportunities, threats + strategy)
> - Gap Analysis + Premortem (market gaps, product gaps, and failure scenarios)
>
> If yes, I have a few additional questions before we start — most can be pre-filled from your uploaded documents. If you'd prefer to answer them later, say 'ask me later' and I'll remind you before Phase 03 generates.
>
> If you only want the lighter analysis (persona simulation and gap analysis without the full strategic layer), say 'lighter analysis' and I'll proceed without Section E."

- **Full analysis** → proceed with Section E questions below
- **Ask me later** → log as pending in the session summary, remind before Phase 03 generates
- **Lighter analysis** → skip Section E, proceed with `03-1-persona-analysis.md` and `03-4-gap-premortem.md` only

---

## Document pre-fill

Before asking any Section E questions, check for uploaded documents that may contain answers — competitive briefs, previous SWOTs, analyst reports, win/loss summaries, sales notes, or any strategic planning documents. Apply the same pre-fill behavior as the main questionnaire:

- Found a clear answer → suggest it and wait for confirmation
- Found a partial answer → flag uncertainty and ask to confirm or update
- Found nothing → ask the question directly
- Conflict between documents → show side by side, PO resolves

Partial answers are acceptable for Section E. Unlike Sections A–D, gaps in Section E are filled by research rather than blocking document generation. If the PO doesn't know an answer, Claude will attempt to find it through web research and flag what was researched vs. what was provided.

---

## Section E: Strategic Analysis

*These questions are only asked when the full strategic analysis is selected. Carry all confirmed answers forward — never re-ask.*

---

### E1: Internal Strengths

**What are your organization's internal strengths relative to this product?**

Consider: existing customer relationships, proprietary technology or IP, team expertise, brand recognition, distribution advantages, cost structure, partnerships, speed to market.

*If pre-filled from documents, suggest and confirm. If not, ask directly.*

---

### E2: Internal Weaknesses

**What are your internal weaknesses or constraints for this product?**

Consider: gaps in capability, resource limitations, technical debt, team gaps, brand perception, pricing constraints, operational limitations.

*Be specific — generic weaknesses produce generic strategy. If the PO is vague, ask for one concrete example.*

---

### E3: External Opportunities

**What external opportunities exist right now that this product could capitalize on?**

Consider: regulatory changes, competitor weaknesses, market shifts, emerging customer segments, technology changes, timing advantages, partnership opportunities.

*If the PO is unsure, Claude will surface opportunities from web research after Section E is complete.*

---

### E4: External Threats

**What external threats concern you most for this product?**

Consider: competitors building similar capabilities, market conditions, regulatory risk, pricing pressure, customer behavior changes, macro trends.

*Do not soften this question. The premortem and TOWS strategy depend on honest threat assessment.*

---

### E5: Named Competitors

**Who are the top 3–5 direct competitors for this product? Name them specifically.**

*Generic categories ("enterprise software vendors") are not sufficient. Named competitors are required for the competitive analysis. Claude will research each named competitor independently and cross-check against what is provided here.*

---

### E6: Indirect Competitors and Substitutes

**Who are the indirect competitors or substitutes?**

These are products or approaches that solve the same problem differently — not head-to-head competitors but alternatives your customers might choose instead, including doing nothing.

---

### E7: Existing Competitive Intelligence

**Do you have any existing competitive intelligence you can share?**

Acceptable inputs: win/loss analysis, sales call notes, analyst reports (Gartner, Forrester, G2 data), customer interviews, pricing research, or anything else. Any file type.

*If documents were uploaded at kickoff that contain competitive intelligence, reference them here rather than asking the PO to re-upload.*

---

### E8: Why You Lose Deals

**What does the sales team hear most often when they lose a deal to a competitor?**

*This is the single most useful input for competitive positioning. If the PO doesn't know, flag it as a gap — this is worth finding out from the sales team before the competitive analysis is finalized.*

---

### E9: Why Customers Switch to You

**What do customers say when they switch from a competitor to your product?**

*The mirror of E8. These two questions together define the competitive battleground more accurately than any feature comparison.*

---

### E10: Past Failure Patterns

**Has your company launched similar products before? If so, what caused them to underperform or fail?**

*This is a premortem input. Internal failure history is more predictive than external benchmarks. If the PO is uncomfortable with this question, acknowledge it and explain why it produces better premortem scenarios.*

---

### E11: Critical Assumptions

**What assumptions is this product most dependent on being true?**

*List the top 3–5. These become the foundation of the premortem failure scenarios. An assumption that turns out to be wrong is the most common cause of product failure.*

---

### E12: Market Irrelevance Scenarios

**What would have to change in the market for this product to become irrelevant?**

Consider: a competitor move, a regulatory change, a technology shift, a customer behavior change, or a macro event.

*Do not skip this question. The answer directly informs the highest-severity premortem scenarios.*

---

## After Section E is complete

*Note: Phase 03 sub-phase outputs are HTML files. Before generating any HTML, fetch `bsn-tools:bsn-brand` via MCP (fallback: `bsn-brand-fallback.md`) and read `FORMAT-SPEC.md` for output layout and visual treatment.*


Summarize what was gathered and what will be researched:

> "Here's what I have from your answers and uploaded documents:
>
> [Summary of confirmed answers]
>
> The following will be supplemented by web research during the competitive analysis:
> - [items that need research]
>
> The following were not answered and will be flagged in the relevant documents:
> - [unanswered items]
>
> Ready to proceed with Phase 03?"

**Wait for confirmation before generating any Phase 03 document.**

---

## Pending flag behavior

If the PO said "ask me later" at kickoff, remind them before Phase 03 generates:

> "Before I run the Phase 03 documents — you flagged Section E as 'ask me later' at the start of this session. Do you want to answer those questions now, or proceed with the lighter analysis?"

Log the final decision in the session summary regardless of which option is chosen.
