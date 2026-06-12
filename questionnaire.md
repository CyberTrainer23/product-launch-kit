# PRD / PDD Questionnaire

Use these questions to gather everything needed before writing. Ask all questions for the selected document type(s). If generating all three docs at once, collect everything in one pass — the sections build on each other.

---

## Before Starting: Document Upload

**Always ask this first, before any questions:**

> "Do you have any existing documents you'd like me to review before we start — things like a product brief, one-pager, pitch deck, existing PRD or PDD, research notes, or anything else relevant? Any file type works.
>
> If you've already uploaded files, let me know which ones to use or point me to a folder. If you haven't uploaded anything yet, go ahead and do that now and let me know when you're ready, or just say 'no documents' and we'll start from scratch."

**Wait for the user's response before proceeding.**

- If **documents are provided** → Read all of them in full before asking a single question. Extract every piece of information that could answer a questionnaire question. Then proceed to the questions using the pre-fill behavior below.
- If **no documents** → Proceed directly to the questions as normal.

---

## Pre-Fill Behavior

When documents have been uploaded and read, apply this behavior for every question:

### If you found a clear answer in the documents:
Present it as a suggestion — do not treat it as confirmed until the user says so.

> "**[Question topic]:** Based on [document name], I think the answer here is:
> *[suggested answer]*
> Does that look right, or would you like to change it?"

### If you found a partial or uncertain answer:
Flag the uncertainty — do not guess.

> "**[Question topic]:** I found something that might relate to this in [document name]:
> *[brief summary or quote]*
> Is that what you had in mind, or should we use something different?"

### If you found nothing relevant:
Ask the question directly.

> "**[Question topic]:** [Question as written below]"

### If two documents conflict on the same answer:
Show both versions side by side and ask the user to resolve it. Do not pick one.

> "**[Question topic]:** I found two different answers across your documents:
>
> | Source | Answer |
> |--------|--------|
> | [Document A] | [answer from A] |
> | [Document B] | [answer from B] |
>
> Which should we use, or would you like to write a new answer?"

---

## Core Rules

- **Never assume an answer is correct and move on.** Every answer — whether pre-filled from a document or typed by the user — must be explicitly confirmed before proceeding to the next question.
- **Never skip a question** because you think you already have the answer. Present the suggestion and wait for confirmation.
- **Never combine multiple questions** into one prompt. Ask one question at a time.
- **Carry confirmed answers forward** — never re-ask for information already confirmed.
- **Note the source** of pre-filled answers (e.g., "from product brief") in the final summary, but do not make it the focus — it's reference information, not a highlight.

---

## Final Confirmation Pass

After all questions are answered and confirmed, present a complete summary before generating any documents:

> "Here are all the answers we'll use to generate your documents. Answers noted with a source came from your uploaded documents — all others were entered directly.
>
> **[Section A answers]**
> 1. Product name: [answer] *(from: [source or "entered directly"])*
> 2. One-line description: [answer]
> ...
>
> Everything look right? Say 'yes' to generate, or tell me what to change."

**Wait for final confirmation before generating any document.**

---

## Section A: Universal (Ask for Any Document)

1. **Product / Feature Name** — What is this called?
2. **One-Line Description** — How would you describe it in a single sentence?
3. **Launch Type** — Is this a new product, a new feature on an existing product, or an enhancement?
4. **Primary Contact / Owner** — Who owns this? (PM, team lead, etc.)
5. **Team / Contributors** — Who else is involved? (design, engineering, analytics, etc.)
6. **Target Launch Date** — When do you want to ship?
7. **Who is this for?** — Describe the target customer specifically: role, industry, company size, and situation. Avoid "everyone." *(Used for: customer segment, market segment, and persona across all three docs.)*
8. **The Problem** — What problem does this solve, from the customer's point of view? Why does it matter to them today, and what's the broader business or market challenge driving it? *(Used for: problem statement, business challenge, and entry point — how customers describe the pain before they find you.)*
9. **Current Alternatives & Competitors** — How do customers solve this problem today? Name the specific products, tools, or methods they use. *(Used for: competitive landscape across all three docs.)*
10. **Why Those Fall Short** — What's missing or broken about those existing solutions?
11. **Your Solution** — How does your product solve the problem? What does it do, specifically, and what key features define it? *(Used for: solution description, core features, and key benefits — the value flows directly from what it does and what was missing before.)*
12. **What Makes You Different** — In what specific way is your product better, faster, or cheaper than the alternatives listed above? *(Used for: key differentiator, differentiators, and competitive differentiation across all three docs.)*

---

## Section B: Overview (Working Backwards PR/FAQ)

*Builds on Section A. These questions complete the PR/FAQ format.*

13. **Total Addressable Market** — How many people have this problem, and how much would they pay to solve it? What's the estimated market size?
14. **Top 3 Risks** — What are the most likely reasons this product could fail?
15. **Biggest Unsolved Problem** — What is the hardest technical, legal, or business challenge you'll need to overcome to build this?
16. **Upfront Investment** — What people, technology, or other resources are required to build it?
17. **Profitability Timeline** — How long before this product is profitable or self-sustaining?
18. **Company / Spokesperson Quote** — What would your company's spokesperson say about this product? (can be drafted)
19. **Customer Quote** — What would a happy early customer say? (can be hypothetical)

---

## Section C: Milestone PRD (Kevin Yien Format)

*Builds on Section A. These questions complete the sprint-level planning doc.*

20. **Scoped Problem Statement** — In 1-2 tight sentences, what specific problem does this milestone solve? (Narrower than the full vision from A8 — just what this release addresses.)
21. **High-Level Approach** — What's the general shape of the solution? (e.g., "a notification center for relevant features")
22. **Goals (in priority order)** — What are the top 2-4 measurable outcomes you're aiming for with this release?
23. **Non-Goals** — What are you explicitly NOT solving in this release, and why?
24. **Future Considerations** — What features are you intentionally saving for a later release?
25. **Key Logic / Business Rules** — What rules should guide design and development? (edge cases, constraints, permissions)
26. **System Roles Impacted** — Which of the four system roles does this feature or milestone affect? Select all that apply: Partner Admin / Manager Admin / Manager / Employee. *(Required for user story generation in Phase 04.)*
27. **Key Milestones** — List the major phases (e.g., Pilot, Beta, Early Access, Launch) with target dates and exit criteria.
28. **Operational Checklist** — Which teams need to be looped in? (Analytics, Sales, Marketing, Customer Success, Legal, etc.)
29. **Open Questions** — What decisions haven't been made yet?

---

## Section D: PDD (Product Description Document)

*Builds on Section A. These questions complete the go-to-market and positioning doc.*

30. **Strategic Objective & Market Position** — How does this release support company goals (retention, upsell, expansion, etc.), and how should it be perceived in the market? (innovative, efficiency-focused, premium, etc.) *(Combines strategic fit and intended positioning.)*
31. **Audience Applicability** — Is this available to all customers, specific plan tiers, specific partners, or specific geographies?
32. **Dependencies / Integrations** — What other systems or products does this rely on or connect to?
33. **Pricing / Packaging** — Is this included in an existing package, a new standalone offering, or an add-on?
34. **Positioning Statement** *(optional)* — "For [target audience] who [need], [product] is the [category] that [key benefit]. Unlike competitors, it [unique differentiator]."
35. **Success Metrics / KPIs** — What does success look like? How will you measure it?
36. **Beta / Pilot Feedback** — Has this been tested? What did users say?
37. **Resources Available at Launch** — What materials exist to support launch? (screenshots, demos, FAQs, documentation, estimated availability dates)
38. **Partner / Distributor Considerations** — Any variations needed for channel partners or resellers?
39. **Language Do's and Don'ts** — What terms should always or never be used when describing this product?
