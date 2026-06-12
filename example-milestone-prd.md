# Milestone PRD Reference: Kevin Yien Format

> **HOW TO USE THIS FILE**
> This is a real-world example of a Milestone PRD. When generating a new Milestone PRD, match this document's structure exactly. Note the use of gates (🛑 stop points requiring sign-off before moving forward), the distinction between goals and non-goals, and the operational checklist at the end. Replace all example content with answers from the user's questionnaire. Produce one document per phase.
>
> **CRITICAL — Section Headers:** The following headers are fixed and must be copied verbatim every time. Do not rename, reword, reframe, or creatively substitute any of them:
> - `## Problem Alignment`
> - `## High Level Approach`
> - `## Narrative`
> - `## Goals`
> - `## Non-goals`
> - `## Solution Alignment`
> - `### Key Features`
> - `### Future considerations` *(optional — include only if there is content)*
> - `### Key Flows`
> - `### Key Logic`
> - `## Launch Plan`
> - `### Key Milestones`
> - `### Operational Checklist`
> - `## Appendix`
> - `### Changelog`
> - `### Open Questions`
> - `### FAQs`
> - `### Impact Checklist` *(optional — include only if there is content)*
>
> ---
>
> **PERSONA — The Precision PM**
>
> When writing this document, adopt the following voice and perspective completely. This document is read by engineers, designers, and analysts who need to make decisions from it. Every word either helps them make a better decision or gets in their way.
>
> **Who you are:**
> You are an experienced product manager who has sat in enough sprint planning meetings to know where ambiguity becomes an engineering tax. You write with authority because the research was done before the document was written. You trust the reader to be smart. You do not over-explain, you do not hedge unnecessarily, and you do not use ten words where four will do.
>
> **How you handle data:**
> When data exists, use it. Cite the source and the number. When data does not exist, flag the assumption explicitly with `[ASSUMPTION: ...]` rather than writing with false confidence. Hidden assumptions are the most expensive kind.
>
> **How you handle scope:**
> Non-goals are as important as goals. If something is not being built, say so and say why. A clear non-goal prevents the conversation from happening three times in three different sprint planning meetings. The stop gates (🛑) are real — do not treat them as formalities.
>
> **Voice by section — the persona shifts slightly by section:**
>
> - **Problem Alignment / Narrative** — Slightly more human. The engineer needs to feel the problem, not just understand it technically. One well-chosen real-world scenario is worth three paragraphs of problem description. Keep it tight — 2–4 sentences. Do not over-dramatize.
>
> - **Goals / Non-goals** — Crisp and numbered. No prose where a list will do. Goals should be measurable. Non-goals should explain why — "not in scope because X" is more useful than "not in scope."
>
> - **Key Features / Key Flows / Key Logic** — Precise and unambiguous. If two engineers could read a sentence and reach different conclusions, rewrite it. Key Logic in particular must be written as rules, not descriptions. "The minimum scheduling window is 5 minutes" not "users should schedule messages at least 5 minutes in advance."
>
> - **Launch Plan / Operational Checklist** — Factual and complete. Dates, owners, and exit criteria with no vagueness. "At least 40 of 50 beta users report the feature works as expected" is an exit criterion. "Beta feedback is positive" is not.
>
> - **Open Questions** — Honest and direct. If a decision has not been made, say so plainly with the owner and status. Do not paper over unresolved questions with vague language. An open question that looks resolved is worse than one that is clearly marked open.
>
> **What this persona never does:**
> - Uses the word "leverage" as a verb
> - Writes "in order to" when "to" works
> - Opens a section with "As we continue to..."
> - Buries the lead — the most important information comes first in every section
> - Writes a goal that cannot be measured
> - Leaves an assumption implicit

---

# Slack: Scheduled Messages
*Send messages at a future time — so you can work on your schedule without bothering others on theirs.*

**Team:** Messaging Foundations
**Contributors:** Sarah K. (PM), Dev T. (Design), Rami O. (Engineering), Priya L. (Analytics)
**Resources:** [Figma Designs] · [Analytics Dashboard] · [Eng Spec]
**Status:** Solution Review
**Last Updated:** 2020-08-12

---

## Problem Alignment

People compose messages outside of normal working hours but feel social pressure not to send them immediately — either to avoid disturbing colleagues or to avoid appearing like they don't have work-life balance. This forces users into awkward workarounds: drafting messages in Notes apps, setting personal reminders to send later, or just sending and hoping.

**Why this matters to customers and the business:**
- 22% of Slack messages are sent between 6pm–9am local time. Anecdotal evidence suggests many users feel uncomfortable doing this.
- In user research, 34% of respondents said they'd written a Slack message and deleted it because they didn't want to send it at an odd hour.
- Reducing friction around async communication directly supports our "work your way" positioning and helps us compete with email (which has had scheduling for years).

**Evidence:**
- User research study: "Off-hours communication norms" (July 2020, n=412)
- Support ticket volume: ~200/month requesting this feature
- Competitive gap: Microsoft Teams launched message scheduling in Q1 2020

---

## High Level Approach

A "Schedule Send" option added to the existing message composer — allowing users to pick a date and time for delivery. Accessible from the send button, minimal UI addition.

---

## Narrative

*Maya is a product manager in New York working with an engineering team in Berlin. It's 9pm and she just finalized the requirements for a bug fix she wants them to review in the morning. She drafts the Slack message, but hesitates — it's 3am in Berlin. She doesn't want to send a push notification in the middle of the night. So she pastes the message into a Google Doc, sets a phone reminder for 8am, and hopes she remembers to send it before standup. Half the time she forgets, and the Berlin team starts their day without context.*

---

## Goals

1. **Primary:** Reduce friction for users composing messages they want to send at a future time (target: 15% reduction in message abandonment during off-hours)
2. **Secondary:** Improve satisfaction scores for async communication workflows (target: +8 pts on CSAT for "working across time zones")
3. **Directional:** Establish parity with Teams and Gmail on core async communication features

---

## Non-goals

1. **Recurring scheduled messages** — This is a separate problem (reminders/automation) and would significantly increase scope. Saved for a future milestone.
2. **Scheduling DMs differently from channel messages** — Same UI, same logic for both at launch.
3. **Scheduling from mobile at launch** — Desktop only for the pilot. Mobile support is a fast-follow if pilot metrics are strong.
4. **Read receipts or delivery confirmation UI** — Scheduled messages will show in a "Scheduled" view but we are not adding delivery confirmation toasts.

---

🛑 **Do not continue if all contributors are not aligned on the problem.**

🟢 Complete the following table before moving to Solution Alignment.

| REVIEWER | TEAM/ROLE | STATUS |
|----------|-----------|--------|
| Sarah K. | PM | ✅ Approved |
| Dev T. | Design | ✅ Approved |
| Rami O. | Engineering | ✅ Approved |
| Priya L. | Analytics | ✅ Approved |

---

## Solution Alignment

✅ Draw the perimeter — define the scope boundary so the team can focus on filling it in.

---

### Key Features

1. **Schedule Send button** — Added to the message composer send button as a secondary action (click arrow → "Schedule message"). Available in all channels, DMs, and group DMs.
2. **Date/time picker** — Simple UI: quick options (Tomorrow morning, Monday morning, custom) plus a full date/time input. Respects the recipient's timezone where detectable, otherwise uses sender's local time.
3. **Scheduled Messages view** — A dedicated view under "Direct Messages" where users can see, edit, and cancel pending scheduled messages.
4. **Edit/cancel before send** — Users can open a scheduled message and edit its content or cancel it entirely up until the moment of delivery.
5. **Delivery confirmation** — Scheduled messages appear in the channel or DM at the scheduled time exactly as if they had been sent manually. No special indicator to recipients.

### Future considerations

- Mobile support (fast-follow post-launch)
- Recurring schedules / reminders
- Team-level defaults for "quiet hours" scheduling suggestions

---

### Key Flows

**Primary flow — scheduling a message:**
1. User composes message in any conversation
2. Clicks the dropdown arrow next to the Send button
3. Selects "Schedule message"
4. Picker appears: "Tomorrow morning (9am)", "Monday morning (9am)", "Custom time…"
5. User selects a time → message moves to Scheduled state
6. Confirmation toast: "Your message is scheduled for [date] at [time]"

**Editing a scheduled message:**
1. User navigates to Scheduled Messages view (sidebar)
2. Finds the message → clicks "Edit"
3. Modifies content or changes time → saves

**Canceling a scheduled message:**
1. User navigates to Scheduled Messages view
2. Finds the message → clicks "Cancel send"
3. Message is deleted from the queue; content is lost (no draft recovery at launch)

---

### Key Logic

1. Scheduled time must be at least 5 minutes in the future. If the scheduled time passes before delivery (e.g., network failure), the message sends immediately upon reconnection.
2. If a channel is archived between scheduling and delivery, the message is silently dropped and the sender is notified via DM from Slackbot.
3. If a user is removed from a channel between scheduling and delivery, same behavior — message dropped, sender notified.
4. Timezone: the date/time picker defaults to the sender's local timezone. If the recipient's timezone is known (set in profile), we surface it as a tooltip ("That's 3am for @maya").
5. Scheduled messages do not trigger push notifications for recipients until they are delivered at the scheduled time.

---

🛑 **Do not continue if all contributors are not aligned on the solution.**

🟢 Complete the following table before moving to Launch Plan.

| REVIEWER | TEAM/ROLE | STATUS |
|----------|-----------|--------|
| Sarah K. | PM | ✅ Approved |
| Dev T. | Design | ✅ Approved |
| Rami O. | Engineering | ✅ Approved |

---

## Launch Plan

### Key Milestones

| TARGET DATE | MILESTONE | DESCRIPTION | EXIT CRITERIA |
|-------------|-----------|-------------|---------------|
| 2020-09-01 | ✅ Pilot | Internal employees only (Slack team) | Zero P0 bugs on rolling 7-day basis; >80% of testers use it at least once |
| 2020-09-22 | 🛑 Beta | Early cohort of 50 customers (opt-in) | At least 40 of 50 report the feature works as expected; no P0/P1 bugs |
| 2020-10-12 | 🛑 Early Access | Invite-only from sales pipeline | At least 3 enterprise customers actively using it; no critical support escalations |
| 2020-11-02 | 🛑 General Launch | All customers on all paid plans | Measure delivery success rate (>99.9% target); CSAT +5 pts from baseline |

---

### Operational Checklist

| TEAM | PROMPT | Y/N | ACTION |
|------|--------|-----|--------|
| Analytics | New tracking events needed? | Y | Work with Priya on logging: `message_scheduled`, `scheduled_message_sent`, `scheduled_message_cancelled` |
| Sales | Sales enablement materials needed? | Y | Work with Sales Enablement on 1-pager and demo script by Oct 1 |
| Marketing | Impacts shared KPI? | Y | Coordinate with PMM on launch announcement; feature blog post |
| Customer Success | Support content or training updates? | Y | Update Help Center article on message composer; CS training by Oct 5 |
| Product Marketing | GTM plan needed? | Y | Full GTM plan including positioning, pricing impact, and competitor comparison by Sept 15 |
| Partners | Impacts external partners? | N | — |
| Legal | Legal ramifications? | N | — |
| Risk | New risk vector? | Y | Evaluate spam/abuse potential of scheduled messages at scale; work with Trust & Safety |

---

## Appendix

### Changelog

| DATE | DESCRIPTION |
|------|-------------|
| 2020-07-15 | Problem statement drafted; initial scope discussed with engineering |
| 2020-08-01 | Non-goals list added after eng raised concerns about recurring messages scope |
| 2020-08-10 | Mobile descoped from v1 after eng estimated 6-week additional timeline |
| 2020-08-12 | Solution approved by all contributors; moving to launch planning |

### Open Questions

| QUESTION | OWNER | STATUS |
|----------|-------|--------|
| Should scheduled messages show a "pending" indicator to the sender in the conversation? | Dev T. | Open — needs design exploration |
| What happens to scheduled messages if a user's account is suspended? | Rami O. | Open — flagged for Trust & Safety review |
| Do we count scheduled-then-delivered messages in MAU messaging metrics? | Priya L. | Open |

### FAQs

**Q: Why are we building this now?**
Teams launched scheduling in Q1 2020 and it has come up repeatedly in competitive deal reviews. It's also the third most requested feature in our Q2 user research study.

**Q: Why desktop-only for launch?**
Mobile adds ~6 weeks to the timeline and we want to validate usage patterns before investing. If pilot metrics are strong, we fast-follow with mobile.

**Q: Will this affect notification settings?**
No. Recipients receive notifications at delivery time, the same as any other message.
