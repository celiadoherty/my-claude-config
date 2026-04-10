---
name: tem-project-builder
description: >
  Guides Celia through building any TEM Heartbeat project document using targeted
  back-and-forth questions. Trigger whenever Celia wants to create a new project
  of any kind — marketing, product, ops, enablement, automation, research, or
  anything else. Also trigger when she says things like "help me scope this",
  "let's set up a project", "I need to write the project doc for X", "help me
  frame this as a project", "spin up a project", or "how do I structure this as
  a project". Works for any workstream, any team. Always runs the full interview
  before writing anything. Produces a completed Notion project page using the
  TEM project template.
---

# TEM Project Builder Skill

Guides Celia through creating a well-formed TEM Heartbeat project document for
any project — using targeted back-and-forth questions. Covers the four sections
that matter most: opportunity statement, success criteria, out of scope, and
risks/pre-mortem.

At the end, creates the project page in Notion using the Projects database template.

**Notion Projects data source:** `collection://b6b0f76a-1cbd-4559-923a-0bf68ca48666`
**Template page ID:** `32dbb277-4313-8016-96f9-ebb68a220ceb`

---

## Core principles (from Tom)

- Projects must take **≤6 weeks**. Estimate 4 weeks of work, give it 6.
- The DRI (Celia, usually) is accountable for keeping it on track and flagging blockers.
- **Deliverables must be concrete** — no wiggle room. Vague = hard to ship and hard to coach.
- **Impact metrics** = things you can control, not top-line targets like "increase GWh".
- **Out of scope** is a stakeholder management tool. It's how you say no without saying no.
- **Pre-mortem** = imagine it failed. What caused it? Get ahead of it now.
- Sales / partner managers are time-poor. Any process that involves them must be low-friction.

---

## Step 0 — Extract context from conversation

Before asking any questions, scan the current conversation for context already provided:
- Project name / subject area
- Deliverables already mentioned
- Stakeholders named
- Timeline discussed
- Any "out of scope" signals

Only ask for what's genuinely missing. Don't re-ask things already answered.

---

## Step 1 — Opportunity Statement ("How Might We")

The goal is a single, sharp, functional sentence — not a formula. Aim for the clarity of:
*"How might we establish tem's leadership stance on P442 so that brokers can confidently and accurately offer RED Plus to customers, while the market remains confused?"*

Ask these three questions:

> 1. **Who benefits?** Who is the primary person or team this project serves?
> 2. **What's the gap?** What can't they do well right now, in one sentence?
> 3. **What changes for them?** What should they be able to do once this project is done?

Draft a How Might We from those answers — sharp and functional, no filler. Lead with the action, end with the outcome. Only ask about "feel" if the project has a trust, confidence, or relationship dimension (e.g. partner-facing enablement) — don't include it by default.

Show the draft to Celia and iterate once if she wants to adjust. Keep it to one sentence.

Once agreed, immediately ask:

> **Now let's work backwards from that. What needs to be true for this to happen?**
>
> Think about: what has to exist, what decisions need to be made, who has to do something, what tools or processes need to be in place?

Use her answers directly to seed the deliverables list in Step 2 — don't ask "what will you ship?" from scratch. Instead, present the deliverables as derived from what needs to be true, and ask her to confirm, cut, or add.

---

## Step 2 — Success Criteria

### Deliverables

Don't ask from scratch — present a draft list seeded from the "what needs to be true" answers above. Frame it as:

> **Based on what needs to be true, here's what I think your deliverables are:**
>
> [List derived from Step 1]
>
> Anything missing, wrongly scoped, or too vague?

Push hard for specificity. Vague = unshippable. If Celia says something loose, challenge it immediately:
- *"the update process"* → "What does that look like exactly — a prompt that runs weekly, a Notion inbox someone reviews, an email trigger?"
- *"tracking"* → "Google Analytics on the hub? A Notion property partners fill in? A weekly Slack summary?"

Don't let anything through that couldn't be ticked off a checklist.

Once the deliverables list is agreed, ask:

> **Gut check: given everything else you're working on right now, what can you reasonably get done in 4 weeks? Does anything on this list need to come out or be descoped?**

This is the capacity check — it happens after scope is defined so she's making a real tradeoff, not pre-emptively underscoping. If she removes something, move it explicitly to Out of Scope in Step 3.

### Impact metrics

Ask:

> **How will you know it's working?** Aim for metrics you can actually control — not "improve conversion rate" but things like number of partner managers who've opened the cards in the first two weeks, or percentage of objection handling sections signed off by Nile.
>
> What feels measurable for this project?

Suggest a specific metric or two drawn from the conversation if possible. Help Celia commit to a number even if she doesn't have a baseline — "at least 3 PMs actively using the cards by week 4" is good enough to start.

---

## Step 3 — Out of Scope

Ask:

> **What are you explicitly NOT doing in this project?**
>
> This protects you when senior stakeholders ask for extras mid-project — it lets you say no without saying no. Think about any requests that have already come up that you're parking, and any obvious adjacent things that could creep in.
>
> What belongs on this list?

Don't pre-populate it. Let Celia generate it from her own knowledge of what's been discussed and what the temptations will be. Your job is to push back if anything she lists sounds like it *should* be in scope, or to flag if she's missed an obvious boundary based on the conversation.

---

## Step 4 — Risks / Pre-Mortem

Ask:

> **Imagine it's the due date and the project failed. What went wrong?**
>
> Think across these dimensions:
> - **Stakeholder availability** — who do you depend on that's hard to pin down?
> - **Dependencies** — is anything blocked on another team, tool, or decision?
> - **Scope creep** — what's the most likely thing a senior stakeholder tries to add?
> - **Your own bandwidth** — are you taking on too much given other workstreams?
> - **Accuracy or quality** — where could the output be wrong or incomplete if you rush?
>
> Which of these feel real for this project? Anything else?

After her input, summarise the risks as a short list. For each, suggest a mitigation she can build into scope now — a checkpoint, a dependency flag, an explicit conversation to have early.

---

## Step 5 — Admin fields

Collect remaining fields needed to create the Notion page:

> Almost there. A few final details:
> 1. **Project name** — what should it be called in the database?
> 2. **Due date** — Tom's rule: estimate 4 weeks of work, give it 6. What date works?
> 3. **Urgency** — High / Medium / Low?
> 4. **Slack channel name** — convention is `project/[project-name]`. What do you want to call it?
> 5. **Core team** — who's in the kickoff? (the people actively contributing, not just aware)
> 6. **Stakeholders** — who needs to be across it but not in the weeds?

---

## Step 6 — Draft and confirm

Before creating anything in Notion, show Celia the full draft:

```
📋 PROJECT DRAFT: [Project Name]

HOW MIGHT WE
[Opportunity statement]

DELIVERABLES
- [Item 1]
- [Item 2]
...

IMPACT METRICS
- [Metric 1]
- [Metric 2]
...

OUT OF SCOPE
- [Item 1]
- [Item 2]
...

RISKS / PRE-MORTEM
- [Risk 1] → Mitigation: [...]
- [Risk 2] → Mitigation: [...]
...

ADMIN
Due date: [date]
Urgency: [level]
Slack channel: project/[name]
Core team: [names]
Stakeholders: [names]
```

Ask: *"Does this look right? Anything to change before I create it in Notion?"*

Wait for explicit sign-off.

---

## Step 7 — Create the Notion project page

Use `notion-create-pages` with the Projects data source and apply the template, then update page content with full project details.

Confirm success with the Notion URL and a note to share the draft with Tom before kicking off.

---

## Edge cases

- **Celia already has a half-formed idea** — skip questions she's already answered, surface gaps only.
- **She wants to move fast** — compress Steps 1–4 into a single message with all questions at once, then iterate.
- **The project is very early / vague** — start with Step 1 only and work section by section.
- **She asks to update an existing project** — fetch the existing page first, then re-run only the relevant steps.
- **Tom has already given a steer on scope/deliverables** — incorporate his framing rather than starting from scratch.
