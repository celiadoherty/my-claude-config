---
name: tem-battlecard
description: >
  Generates competitor battlecards for tem's sales team, structured to the official WIP Competitor
  Battlecard Template. Use this skill whenever someone asks to create, write, build, draft or generate
  a battlecard, competitive comparison, competitor analysis, or sales card for any competitor.
  Also trigger when someone asks "how do we beat [competitor]", "what's our position against [X]",
  or "help me prep for a deal against [competitor]". Always generates BOTH buy side and sell side
  cards by default. Pulls live intel from Slack (#red-tendering, #engine-buy-side, #engine-sell-side)
  and web research before generating. Known competitors include: Volter, EDF, British Gas, Good Energy,
  Urban Chain, E.ON Next, Smartest Energy, Drax, Yu Energy — but works for any competitor.
---

# tem Battlecard Skill

Generates complete buy-side and sell-side competitor battlecards for tem's sales reps. Pulls live
intel from Slack and the web before writing. Grounds all copy in tem's transaction-layer POV and
voice. Proof points are auto-populated from Slack intel with sourcing flags for human verification.

---

## Step 1 — Gather inputs

From the user's message, extract:
1. **Competitor name** — required
2. **Additional notes** — internal intel, deal context, specific objections heard (optional)
3. **Upcoming interview or meeting?** — if the user mentions they're prepping for a call with a
   named person (e.g. "I'm meeting Lewis tomorrow"), note the name(s). This triggers `ASK [NAME]`
   flags throughout the card for knowledge gaps that person could fill.

If competitor name isn't clear, ask. Otherwise proceed immediately to Step 2.

---

## Step 2 — Live intelligence scrape

Run all of the following **in parallel**:

### A. Slack search (3 channels)
Search each channel for the competitor name. Extract:
- Deal wins and losses mentioning the competitor
- Pricing intel (quotes, rates, structures they offered)
- Sales tactics or FUD the competitor used
- Any named proof points (customer names, deal sizes, outcomes)
- Open questions or unresolved intel

Channels to search:
- `#red-tendering`
- `#engine-buy-side`
- `#engine-sell-side`

Use `slack_search_public_and_private` with the competitor name as the query for each channel.

### B. Web research (3–5 searches)
Find:
- Their core product/service offering in UK business energy
- Pricing model and contract structures
- Target customer verticals and company sizes
- Key marketing claims and differentiators
- Known weaknesses or complaints (reviews, news, Trustpilot)

Prioritise their own website, recent press, and energy industry sources.

---

## Step 3 — Generate both cards

Generate a **Buy Side** card and a **Sell Side** card for the competitor. Use separate pages.
Both follow the template below. Tailor the Head-to-Head, Where We Win/Lose, and Counter sections
to the relevant buyer (energy buyer for buy side; generator/asset owner for sell side).

Read `references/tem-voice.md` before writing any copy. All card and script copy must follow
tem's voice rules — especially "How to Counter Them" and "Weakness Questions".

**Section ownership:**
- ✅ AI generates: all sections except Proof Points and Disqualifiers
- ⚡ AI auto-populates from Slack: Proof Points (with source flags — see below)
- 🙋 Human fills in: Disqualifiers, any Proof Points not found in Slack

Mark human-fill items clearly with `[TO FILL IN]`.

**ASK flags:** If the user mentioned an upcoming meeting with a named person in Step 1, add
`> 🙋 ASK [NAME] — [specific gap]` beneath any section where that person's expertise is directly
relevant. Only add these flags where the gap is genuine and the named person could plausibly answer.

---

## Battlecard Template

Use this template for both buy side and sell side. Adjust Head-to-Head categories and
Where We Win/Lose scenarios to reflect the relevant perspective.

```markdown
# ⚔️ Battlecard: [Competitor Name] — [Buy Side / Sell Side]

> Last updated: [Date] | Owner: [TO FILL IN]

---

## 🏢 Competitor Overview
[2–3 sentences: who they are, market position, what they're known for in UK business energy.
For sell side: frame from a generator's perspective — what do they offer asset owners?]

---

## ⚡ Their Core Offering

**Products / Services**
[e.g. fixed-rate tariffs, PPAs, REGOs, flex purchasing — framed for buy or sell perspective]

**Typical Deal Size**
[Range if known]

**Contract Structures**
[e.g. fixed, flex, PPA, subscription]

---

## 🎯 Target Customer Profile

**Verticals:** [Industries / asset types they focus on]
**Company Size:** [SMB / C&I / Utility-scale / Generator size]
**Geography:** [UK regions or national]
**Buyer Persona:** [Who they typically sell to — Procurement, CFO, Asset Manager, etc.]

---

## 📊 Head-to-Head

| Category | [Competitor] | tem |
|---|---|---|
| Technology / Product | | RED — Renewable Energy Direct™, proprietary pricing engine, itemised billing |
| Pricing Model | | Pay closer to the true cost of energy. Wholesale mark-ups removed. |
| Contract Terms | | |
| Transparency / Billing | | Every charge itemised. RED score on every bill. |
| Track Record | | £30m value returned. 3,000+ sites across the UK. |
| Financial Backing / Security | | £75m Series B — Lightspeed, Schroders, Allianz. Atradius credit insurance. |
| [Sell side: Payment Terms] | | Monthly — the only supplier confirmed to offer this. |
| [Sell side: Green Matching] | | Half-hourly, named-customer traceability via RED™ |

[Add or remove rows as relevant. For sell side, prioritise: payment frequency, counterparty risk,
P442 NCC savings, generator portal, PPA panel access.]

---

## ✅ Where We Win

**Inclusion rule:** 3–5 scenarios only. For each, ask: *is there a deal, Slack thread, or field conversation where this scenario played out?* If the answer is no, cut it. If research surfaces more than 5, include the top 3–5 by frequency and move the rest to Open Questions with a note: *"Lower-priority win scenario — promote if confirmed in the field."*

1. **[Scenario]** — [Why we win. Lead with price, transparency, or proof. No hype.]
2. **[Scenario]** — [Why we win.]
3. **[Scenario]** — [Why we win.]

---

## ❌ Where They Win

> Be honest — knowing this helps reps qualify faster and avoid unwinnable deals.

1. **[Scenario]** — [Why they have the edge]
2. **[Scenario]** — [Why they have the edge]

---

## 🎭 Their Common Sales Tactics

- [Specific claim or FUD they use]
- [Tactic 2]
- [Tactic 3]

---

## 🛡️ How to Counter Them

**Inclusion rule:** Only include objections that reps actually encounter in live deals. For each objection, ask: *is there a Slack thread, deal note, or field conversation where this came up?* If the answer is no, cut it. In practice this lands most cards at 3–5 counters. If research surfaces more than 5 credible objections, include the top 5 by frequency and move the rest to Open Questions with a note: *"Lower-priority counter — promote if heard in the field."*

Write each response in two registers:
- **(Card)** — tem brand voice: structural, proof-led, calm
- **(Script)** — Sales rep voice: conversational, direct, confident

**"[Their claim or objection]"**
- **(Card)** [Structured, factual rebuttal grounded in mechanism + proof]
- **(Script)** "[What the rep says out loud — short, natural, confident]"

**"[Their claim or objection]"**
- **(Card)** [Rebuttal]
- **(Script)** "[Script]"

**"[Their claim or objection]"**
- **(Card)** [Rebuttal]
- **(Script)** "[Script]"

---

## 🪤 Competitor Weakness Questions

Questions reps can ask the prospect that expose competitor weaknesses — without naming them.

- "[Question that surfaces a billing/transparency weakness]"
- "[Question that surfaces a pricing/mark-up weakness]"
- "[Question that surfaces a renewable claim weakness]"
- "[Additional question if relevant]"

---

## 🏆 Proof Points

[Auto-populated from Slack intel where available. Each row sourced and flagged for verification.]

| Deal | Context | Why We Won |
|---|---|---|
| [Client or anonymous] | [Brief context — size, sector, competitor quote if known] | [Key differentiator] |

> ⚠️ Source: [#channel, date, author if named]. **Confirm accuracy before publishing.**

[If no Slack intel found: TO FILL IN — 2–3 wins against this competitor. Anonymise if needed.]

---

## 🚪 Disqualifiers

[TO FILL IN — situations where you should walk away rather than compete.]

- [Situation 1]
- [Situation 2]

---

## ❓ Open Questions

[Always include. Populate with genuine gaps from Slack and web research — unverified claims,
missing pricing data, unresolved deal outcomes, intel that needs a source.
If no gaps exist, write "None identified at this time."]

- [ ] [Gap 1 — what's unknown and where to look]
- [ ] [Gap 2]
```

---

## Step 4 — Save to Notion

After generating both cards, ask:
> "Ready to save both cards to Notion, or do you want to review first?"

On confirmation, create two new Notion pages under Marketing Home:
`https://www.notion.so/9dc5f5300aea4b949963de2588db2e6b`

- `⚔️ Battlecard: [Competitor] — Buy Side` (icon: ⚔️)
- `⚔️ Battlecard: [Competitor] — Sell Side` (icon: ⚔️)

If the user prefers markdown files instead:
- `/mnt/user-data/outputs/battlecard-[competitor]-buy.md`
- `/mnt/user-data/outputs/battlecard-[competitor]-sell.md`

---

## Proof point sourcing format

When auto-populating Proof Points from Slack, format each row like this:

```
| Ystum Colwyn Farms Ltd | AD generator, ~3 GWh, March 2026. Competitor quoted £140 all-in. | Renewed at lower rate; incumbency held. |
> ⚠️ Source: #red-tendering, 17 Mar 2026 (Ruaridh). Confirm accuracy before publishing.
```

Rules:
- One `⚠️ Source` blockquote immediately beneath each proof point row
- Always include: channel name, date, author name if visible
- Always end with: "Confirm accuracy before publishing."
- If outcome is uncertain, mark Why We Won cell as `Outcome pending` and note in source line

---

## Voice rules (summary — full guide in `references/tem-voice.md`)

- Lead with the transaction problem, not the generation claim
- Use proof over promise: numbers, line items, RED scores
- Never say: platform, disrupt, 100% renewable, green energy, smart, unlock, empower
- Challenge systems, not people: critique market design, never bash competitors by name
- Counter-scripts: direct and confident, not aggressive
- Weakness questions expose problems without sounding like a gotcha

---

## Known competitors cheat sheet

| Competitor | Watch out for |
|---|---|
| **Volter** | Claims direct generator matching; aggressive on brokers; mimics tem's transparency positioning |
| **EDF** | Large incumbent; wins on brand trust and long relationships; REGO-based matching |
| **British Gas** | Scale and brand recognition; leads with "reliability" FUD |
| **Good Energy** | REGO-heavy green claims; weak on transaction transparency |
| **Urban Chain** | Peer-to-peer/blockchain claims; physics-safety and counterparty risk |
| **E.ON Next** | Broad portfolio; strong on commercial contracts |
| **Smartest Energy** | Flex purchasing focus; strong with C&I buyers |
| **Drax** | Generation-asset credibility; claims vertical integration as benefit |
| **Yu Energy** | SME-focused; competitive on price but weak on billing transparency |

For unlisted competitors, research from scratch using Step 2.
