# Overview Reference: Working Backwards PR/FAQ Format

> **HOW TO USE THIS FILE**
> This is a real-world example of an Overview (Working Backwards PR/FAQ) document. When generating a new Overview, match this document's structure, section order, and writing style exactly. Replace all example content with answers from the user's questionnaire.
>
> **CRITICAL — Section Headers:** The following headers are fixed and must be copied verbatim every time. Do not rename, reword, reframe, or creatively substitute any of them:
> - `# PRESS RELEASE`
> - `### The Problem`
> - `### Our Solution`
> - `# FAQ`
> - `## External FAQs`
> - `## Internal FAQs`
>
> ---
>
> **TONE AND VOICE — Read before writing a single word**
>
> The Overview is an externally facing document. The voice must earn the reader's attention in the first sentence and hold it through the solution. Follow these rules exactly:
>
> **Direct and human.** State the problem plainly. No preamble, no "in today's landscape," no corporate throat-clearing. If the first sentence could appear in a vendor brochure, rewrite it.
>
> **Empathetic but not sentimental.** The problem section must make the reader recognize their own experience. Use 1–2 short real-world scenarios — "this is what Tuesday looks like" moments — that are specific enough to feel lived-in. Scenarios are 2–3 sentences maximum. Do not invent dramatic narratives. Do not name fictional characters. Write it as: "You finish the report at 9pm. Your client is in London. You write the message and delete it."
>
> **The problem earns the solution.** The goal of the problem section is to get the reader to internally say "yes, that's exactly it — how do I fix this?" Do not resolve the tension in the problem section. Leave it open. The solution section answers the question the problem just raised.
>
> **The solution is credible, not promotional.** State what the product does and what changes as a result. Be specific. Every claim must be supportable by the Milestone PRD or approved prototype. Do not use superlatives. Do not say "revolutionary," "game-changing," "seamless," or "powerful." If a sentence sounds like marketing copy, rewrite it as a fact.
>
> **One voice throughout.** The tone does not shift between problem and solution. It does not become more formal in the FAQ. Write the entire document as if a smart, direct colleague is explaining something important — not as if a company is broadcasting at you.
>
> ---
>
> **AUDIENCE AND POV — Driven by questionnaire answer**
>
> The questionnaire captures who this Overview is written for: MSP partner, SMB client, or both. Apply the following rules:
>
> **MSP partner only:** Write problem and solution entirely from the MSP partner's perspective.
>
> **SMB client only:** Write problem and solution entirely from the SMB client's perspective.
>
> **Both:** Write two problem blocks and two solution blocks — one per audience — with the following visual distinction applied consistently across both sections:
> - Add a small label above each block: `**For MSP partners**` or `**For SMB clients**`
> - Indent block content with a blockquote marker (`>`) so the two audiences are visually trackable
> - Write each scenario from that specific audience's perspective
> - Apply the same distinction in the solution section so the reader can track their audience through the full document
>
> ---
>
> **REAL-WORLD SCENARIOS — Format guide**
>
> Each problem block must contain 1–2 scenarios. Format:
> - 2–3 sentences maximum
> - Written in second person ("you") or present tense
> - Specific situation, ends at the point of friction — do not resolve it
>
> Good: *"It's 9pm and you've just finished something your client in London needs to see first thing. You write the Slack message. You delete it."*
>
> Bad: *"Many professionals struggle with communication across time zones, leading to inefficiencies and missed opportunities."*

---

# PRESS RELEASE

## Amazon Launches AWS — Unlimited Scalable Computing Power, On Demand

**Businesses of any size can now access enterprise-grade infrastructure without buying a single server.**

*Seattle, WA — March 14, 2006* — Amazon Web Services today announced the general availability of Amazon S3 (Simple Storage Service) and Amazon EC2 (Elastic Compute Cloud), giving developers and businesses access to the same scalable cloud infrastructure that powers Amazon.com — for a fraction of the cost of building it themselves.

### The Problem

For years, launching a technology product meant one thing: buy servers. Companies had to predict their computing needs months in advance, purchase hardware, find rack space, hire operations teams to manage it all — and then watch that hardware sit idle 70% of the time. Startups couldn't afford to scale. Enterprises wasted millions on infrastructure they barely used. And every engineering team spent precious time managing servers instead of building products.

The total cost of computing infrastructure — hardware, operations, maintenance, and the opportunity cost of delayed launches — was the single biggest barrier to building technology products at scale.

### Our Solution

AWS removes infrastructure from the equation entirely. With S3 and EC2, any developer or business can store unlimited data and run any application in the cloud — paying only for what they use, only when they use it.

- **Amazon S3** stores any amount of data reliably and retrieves it from anywhere in the world, at $0.15/GB per month with no minimums.
- **Amazon EC2** gives developers virtual servers on demand — launch a new server in minutes, scale to thousands during peak traffic, and turn them off when you're done.

Today, companies use co-location facilities, their own data centers, or managed hosting providers. These approaches require significant capital investment, long procurement cycles, and dedicated operations teams. They are inherently inflexible — you pay for capacity you may never use, and you can't scale quickly when demand spikes. AWS addresses these unmet needs by making compute and storage variable costs, not fixed ones, and eliminating the need for infrastructure teams entirely.

> *"We've been building web-scale infrastructure for over a decade, and we're making it available to every developer in the world. What used to take months and millions now takes minutes and cents."*
> — Jeff Bezos, CEO, Amazon

> *"We launched our entire platform on EC2 in a weekend. We'd have spent six months and $200,000 doing it the old way. AWS let us go from idea to customers in days."*
> — Early AWS Customer, Technology Startup

To get started, visit [aws.amazon.com](https://aws.amazon.com).

---

# FAQ

## External FAQs

**Q: What does AWS cost?**
S3 costs $0.15 per GB/month stored, plus $0.20 per GB transferred out. EC2 starts at $0.10/hour for a small instance. There are no setup fees and no minimum commitments. You pay only for what you use.

**Q: How do I get started?**
Sign up at aws.amazon.com with a credit card. You can launch your first EC2 instance or S3 bucket within minutes. Detailed documentation, SDKs for all major languages, and step-by-step tutorials are available at launch.

**Q: What kind of customer support is available?**
AWS offers basic email support included with all accounts. Premium support plans with phone access and dedicated technical account managers are available for enterprise customers.

**Q: Where is data stored? What happens if there's an outage?**
Data in S3 is automatically replicated across multiple facilities in a region. S3 is designed for 99.99% availability. EC2 instances run in isolated availability zones within each region. Customers can architect for redundancy across zones.

---

## Internal FAQs

**Q: What solutions does the target customer use today?**
Most businesses use one of three approaches: (1) co-location facilities where they own hardware but rent rack space, (2) dedicated managed hosting where a provider manages their servers for a fixed monthly fee, or (3) building and running their own data centers. All three require significant capital expenditure, long lead times, and dedicated operations staff.

**Q: How large is the TAM?**
Global IT infrastructure spending exceeded $400B in 2005. Cloud computing is nascent but growing — Gartner estimates it will represent 25% of total IT spend within a decade. The addressable market includes every company that runs software. Initial focus is on developers and startups, where speed-to-market is the primary value driver.

**Q: What assumptions need to be true for AWS to succeed?**
1. Internet connectivity continues to improve so cloud-hosted applications perform comparably to locally-hosted ones.
2. Customers trust Amazon to store their data and run their workloads reliably.
3. The variable cost model is sufficiently compelling to overcome the inertia of existing infrastructure investments.
4. We can maintain pricing that undercuts the total cost of ownership of traditional infrastructure.

**Q: What are the top three reasons AWS will not succeed?**
1. **Security and compliance concerns block adoption.** Regulated industries may be prohibited from storing data in shared infrastructure.
2. **Performance doesn't meet expectations.** If latency or uptime doesn't match on-premise infrastructure, customers will not trust AWS for production workloads.
3. **Pricing doesn't hold.** If infrastructure costs don't decline faster than our pricing, margins will compress.

**Q: What are the hardest engineering problems to solve?**
Multi-tenant isolation is the most critical. We also need to solve for data durability at scale and live instance migration without downtime.

**Q: What is the upfront investment required?**
Approximately $50M in capital investment to reach general availability and sustain 12 months of operations.

**Q: What are the per-unit economics?**
Gross margin per GB-month is approximately 40% at current pricing, improving significantly at scale. We expect the business to become contribution-positive within 18 months.

**Q: Are there regulatory or legal considerations?**
Data sovereignty laws may restrict where customer data can be stored. Export control regulations may restrict certain customers. Legal review is ongoing.

**Q: What third-party dependencies exist?**
Hardware vendors, bandwidth providers, and power utilities. Existing relationships through Amazon.com operations provide favorable pricing and terms.

---

*Document Status: Draft*
*Last Updated: March 2006*
*Owner: Andy Jassy, SVP Amazon Web Services*
*Contributors: Engineering Lead, Finance, Legal, Marketing*
