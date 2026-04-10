---
name: log
description: >
  End-of-chat learning logger. Trigger when the user types "/log" (with or without
  additional text) at the end of a conversation. Extracts what was learned, built,
  decided, and any follow-ups — then writes a structured entry to the Notion
  "Learning Log" database. Two modes: (1) Quick — asks 4 short questions if no
  context is provided. (2) Rich — if the user pastes text or conversation snippets
  after "/log", extracts the summary automatically using the Claude API before
  writing. Always confirm what was logged at the end.
---

# /log Skill — End-of-Chat Learning Logger

Captures a structured summary of the current conversation and writes it to the
Notion Learning Log database. One entry per chat, one source of truth.

**Notion database:** https://www.notion.so/9cd11a05360e4a2b85f04dcf879b0607
**Data source ID:** ced26ee0-73ab-4a48-9c24-94caf696538b

---

## Step 1 — Detect mode

Look at what the user typed after `/log`:

- **Nothing after `/log`** → Quick Mode (Step 2A)
- **Text, bullet points, or pasted conversation after `/log`** → Rich Mode (Step 2B)

---

## Step 2A — Quick Mode (no context provided)

Ask the user these 4 questions **in a single message**, numbered and compact:

```
Got it — logging this chat. Answer these and I'll save it straight to Notion:

1. **Chat title** — What's a good 5–8 word title for this conversation?
2. **Learned** — What did you learn? (bullet points fine)
3. **Built** — What did you create, write, or ship? (or "nothing" if not applicable)
4. **Follow-ups** — Any open threads or things to revisit? (or "none")

Also, any tags? → engineering / sales / strategy / product / research / ops
```

Wait for their response, then go to Step 3.

---

## Step 2B — Rich Mode (context was pasted)

Call the Anthropic Claude API to extract a structured summary from the pasted content using specified model and parameters.

Parse the JSON response and proceed to Step 3.

---

## Step 3 — Confirm before saving

Show the user a brief summary of what will be logged:

```
Here's what I'll log to Notion:

📌 **[Chat Title]**
📅 Date: [today's date]

🧠 Learned: [learned content]
🔨 Built: [built content]
⚖️ Decisions: [decisions]
🔁 Follow-ups: [followups]
🏷️ Tags: [tags]

Save this? (say yes, or edit anything above)
```

Wait for confirmation. If they say yes or something affirmative, go to Step 4.
If they want to edit, incorporate their changes and re-show the summary before saving.

---

## Step 4 — Write to Notion

Use the Notion MCP `notion-create-pages` tool with the Learning Log data source and specified properties.

---

## Step 5 — Confirm success

After Notion responds with a success, reply with confirmation and provide the Learning Log URL.

If Notion returns an error, tell the user what went wrong and offer to retry or give them the data to paste in manually.

---

## Edge cases

- **User types `/log done` or `/log wrap`** — treat as Quick Mode, ignore the extra word
- **User provides partial context** (e.g. just a title and some bullets) — use what they gave, ask only for what's missing
- **Multiple things built** — format as a bulleted list in the Built field
- **No follow-ups / no decisions** — write "None" rather than leaving the field blank
- **User wants to log a meeting, not a Claude chat** — change Source to "Meeting" and adapt the questions slightly
