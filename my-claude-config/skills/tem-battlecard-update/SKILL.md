---
name: tem-battlecard-update
description: >
  Updates existing tem competitor battlecards with new intel. Trigger this skill when the user
  drops in new information about a competitor — a Notion page, pasted Slack messages, call notes,
  deal outcomes, pricing intel, or any other competitive intelligence — and wants to incorporate it
  into an existing battlecard. Also trigger when the user says "update the [competitor] card",
  "add this to the battlecard", "I just got off a call with...", or pastes intel alongside a
  link to an existing battlecard. Acts as a thinking partner before implementing: discusses where
  intel fits, flags contradictions, and iterates until the user says go. Never makes changes
  without explicit sign-off.
---

# tem Battlecard Update Skill

Updates existing buy-side and/or sell-side battlecards with new competitive intel. Works as a
thinking partner first — discussing placement, surfacing contradictions, and iterating — before
touching the card. Nothing is implemented until the user explicitly approves.

---

## Step 1 — Identify what's been shared

From the user's message, extract:
1. **The new intel** — could be any of: Notion page link, pasted Slack messages, call notes,
   bullet points, a forwarded email, pricing data, deal outcome. If a Notion link is provided,
   fetch it immediately.
2. **Which battlecard(s) to update** — competitor name and buy/sell side. If not specified,
   infer from the intel content. If still unclear, ask.
3. **The existing card** — ask for a Notion link to the card if not provided. Fetch it
   immediately once you have it.

Once you have both the intel and the existing card in hand, proceed to Step 2.

---

## Step 2 — Ask about Slack re-scrape

Before the discussion, ask:
> "Should I also re-scrape #red-tendering, #engine-buy-side, and #engine-sell-side for anything
> new on [competitor] before we dig in? Useful if it's been a while since the card was last updated."

If yes: run `slack_search_public_and_private` for the competitor name across all three channels.
Fold any new findings into the discussion in Step 3 alongside the user-provided intel.
If no: proceed with only the user-provided intel.

---

## Step 3 — Discussion phase (open-ended)

This is the core of the skill. Work through the new intel with the user before touching anything.

### How to run the discussion

**Read the existing card in full first.** Understand what's already there — every section,
every existing proof point, every open question — before making any recommendations.

**Parse the new intel into discrete pieces.** Break it down into individual facts, claims,
quotes, deal outcomes, or pricing data points. Work through them one at a time or in logical
groups — don't dump everything at once.

**For each piece of intel, lead with a recommendation:**
State where you think it fits best and why. Be specific — name the section, the row, or the
exact cell. Then invite pushback:
> "My instinct is this goes in [section] because [reason]. Does that feel right, or do you see
> it fitting somewhere else?"

**Flag contradictions explicitly before touching anything.** If new intel conflicts with
existing content on the card, stop and surface it clearly before proceeding:
> "This conflicts with what's currently on the card — [existing content] says X, but this
> suggests Y. I won't touch either until we've resolved this. What's the correct version?"
Do this even for minor discrepancies. Never silently overwrite existing content.

**Surface strategic implications, not just placements.** If a piece of intel changes the
competitive picture more broadly — e.g. a pricing quote that undermines a "Where We Win"
scenario, or a lost deal that suggests a new Disqualifier — say so. You're a thinking partner,
not just a filing system.

**Iterate until the user says go.** Keep the discussion open. The user may refine, add context,
or change their mind. Incorporate updates to the plan as you go. Don't implement anything until
you receive an explicit signal: "go", "implement", "make those changes", or similar.

### What to track during the discussion

Maintain a running mental list of agreed changes. Before implementing, summarise the full
change set for confirmation:

```
Here's what I'm about to change — confirm and I'll implement:

1. Proof Points — add new row: [client], [context], [why we won]
   > ⚠️ Source: [channel/notes/call, date]. Confirm accuracy before publishing.
2. Open Questions — close item: "[question]" — resolved as [answer]
3. Head-to-Head — update pricing cell: [change]
4. Where They Win — add scenario: [scenario]
```

Only proceed once the user confirms this summary.

---

## Step 4 — Implement changes

Make only the changes agreed in Step 3. Do not rephrase, reformat, or tidy sections that
weren't discussed. Untouched content stays exactly as it is.

**For Proof Points added from any intel source:**
Always add a source blockquote beneath the row:

```
| [Client or anonymous] | [Context — size, sector, competitor quote if known] | [Why we won / outcome] |
> ⚠️ Source: [Notion link / #channel / call notes, date, author if named]. Confirm accuracy before publishing.
```

If outcome is still uncertain, mark the Why We Won cell as `Outcome pending`.

**For changes to existing content:**
Note what was changed and what the previous version said, as a Notion comment or inline note
if the card format supports it — so there's an audit trail.

**Update the `Last updated` field** at the top of the card to today's date.

---

## Step 5 — Save and confirm

After implementing, summarise what was changed in a brief message:
> "Done. Here's what I updated on the [Competitor] [Buy/Sell] card: [list]. The `last updated`
> date is now [date]. Anything else to adjust?"

Do not ask the user to keep iterating unprompted — hand back control and wait.

---

## Voice and sourcing rules

- Follow all voice rules in `references/tem-voice.md` for any new copy written
- Never bash competitors by name in card copy — critique market design, not companies
- Every proof point added must have a source blockquote, regardless of intel format
- Unverified intel gets flagged — never presented as confirmed fact on the card
- If the user provides intel without a clear source, ask before adding it:
  > "Where did this come from? I want to make sure the source note is accurate."

---

## What this skill does NOT do

- Does not create new battlecards from scratch → use `tem-battlecard` for that
- Does not restructure or reformat existing cards unprompted
- Does not implement changes without explicit user sign-off
- Does not silently resolve contradictions — always surfaces them first
