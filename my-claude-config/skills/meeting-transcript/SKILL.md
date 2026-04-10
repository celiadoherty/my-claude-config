---
name: meeting-transcript
description: >
  Downloads and saves Gemini meeting notes — both the email summary AND the full transcript from Google Docs — into clean markdown files in the "tem Meeting Notes" folder. Use this skill whenever Celia asks to download meeting notes, save meeting transcripts, grab 1:1 notes, get Gemini transcripts, archive meeting recordings, or anything involving capturing meeting content from Gmail/Google Meet. Also trigger when she says things like "save my meeting notes", "download the transcript from my call with [person]", "get my 1:1 notes", "pull the notes from today's meeting", or "archive my meeting transcripts". This skill handles the full pipeline: finding Gemini emails, extracting summaries, opening the linked Google Doc via Claude in Chrome to get the transcript, and saving everything as a formatted markdown file. Works for any meeting type — 1:1s, growth 121s, team calls, or any Google Meet with Gemini notes enabled.
---

# Meeting Transcript Skill

Downloads Gemini meeting notes from Gmail and retrieves the full transcript from the linked Google Doc using Claude in Chrome. Produces clean, complete markdown files with both the summary and full transcript.

## Why this skill exists

Gemini sends meeting summaries via email (from gemini-notes@google.com), but the full word-for-word transcript lives in a separate Google Doc that's only accessible through a link in the email. This skill bridges that gap — it pulls the summary from the email and the transcript from the Google Doc, combining them into one clean file.

## Prerequisites

- **Gmail MCP** must be connected (to search and read Gemini emails)
- **Claude in Chrome** must be available (to open the Google Doc and extract the transcript)
- Celia must be **signed into Google** in her browser (so the Google Doc is accessible)
- The workspace folder should be available for saving files

## Step-by-step workflow

### Step 1: Identify which meetings to download

Ask Celia what she wants — options include:

- A specific meeting ("download my 1:1 with Ari from today")
- A type of meeting ("all my 1:1s this week")
- Everything recent ("all Gemini notes from this week")

If she's vague, default to the most recent week of meetings.

### Step 2: Search Gmail for Gemini notes

Use the Gmail MCP to search for meeting note emails:

```
gmail_search_messages with query: "from:gemini-notes@google.com"
```

Add filters based on what Celia asked for:

- For a specific person: `from:gemini-notes@google.com subject:[person's name]`
- For a date range: `from:gemini-notes@google.com after:YYYY/MM/DD before:YYYY/MM/DD`
- For a specific meeting: `from:gemini-notes@google.com subject:"[meeting name]"`

### Step 3: Read each email to get the summary

For each matching email, use `gmail_read_message` to get the full body. The email body contains:

- **Meeting name** — in the first line: "Notes from '[Meeting Name]'"
- **Summary sections** — structured with headers and bullet points
- **Suggested next steps** — action items with assignees
- **"Open meeting notes" link** — this is the link to the Google Doc with the full transcript

Extract and save the summary content from the email body.

### Step 4: Get the full transcript via Claude in Chrome

This is the critical step. The transcript lives in a Google Doc that requires authentication.

1. **Navigate to the email in Gmail** using Claude in Chrome:
   ```
   navigate to: https://mail.google.com/mail/u/0/#all/[messageId]
   ```

2. **Find and click the "Open meeting notes" link** in the email. This opens the Google Doc containing the full transcript.

3. **Wait for the Google Doc to load**, then use `get_page_text` to extract the full content.

4. The Google Doc typically contains these sections:
   - Summary (same as the email)
   - Detailed notes
   - **Transcript** — the full word-for-word transcript with speaker labels and timestamps

5. Extract the transcript section from the page content.

**Important notes on Chrome steps:**
- If Google asks for authentication, pause and tell Celia — she'll need to sign in manually
- Google Docs can take a moment to fully render — wait for the page to load before extracting text
- If the transcript is very long, you may need to scroll to load all content before extracting

### Step 5: Combine and format as markdown

Create a clean markdown file combining both sources:

```markdown
# [Meeting Name]

**Date:** [Date from email]
**Participants:** [Extract from email subject/body]
**Source:** Gemini Meeting Notes (email summary + Google Doc transcript)

---

## Summary

[Summary content from the email, cleaned up and formatted]

### [Section heading from email]
[Content]

### [Section heading from email]
[Content]

---

## Next steps

- [ ] [Assignee] Action item description
- [ ] [Assignee] Action item description

---

## Full Transcript

[Complete transcript from the Google Doc, preserving speaker labels and timestamps]
```

### Step 6: Save the file

Save to the tem Meeting Notes folder using this naming convention:

```
YYYY-MM-DD - [Meeting Name].md
```

Examples:
- `2026-04-09 - Celia and Ari 1:1.md`
- `2026-04-09 - Growth 121 - Celia and Tom.md`
- `2026-04-07 - Team Standup.md`

The save location is the user's workspace folder under `tem Meeting Notes/`.

If a file with the same name already exists but only contains the summary (no transcript section), update it with the full transcript rather than creating a duplicate.

### Step 7: Confirm what was saved

After saving, tell Celia:
- How many files were saved
- The filenames
- Whether each file has the full transcript or just the summary (in case any Google Docs were inaccessible)

## Handling edge cases

**Google Doc won't open (auth issue):**
Tell Celia she needs to sign into Google in her browser first. Offer to save the email summary now and come back for the transcript.

**Transcript section not found in Google Doc:**
Some meetings may not have transcription enabled. Save whatever content is available and note in the file that the transcript wasn't available.

**Multiple meetings with similar names:**
Use the full date and time to distinguish. If two meetings happen on the same day with the same participants, add the time: `2026-04-09 1600 - Celia and Ari 1:1.md`

**Very long transcripts:**
Google Docs may require scrolling to load all content. Use Claude in Chrome to scroll to the bottom of the document before extracting text, to ensure the full transcript is captured.

## Email structure reference

Gemini note emails follow this pattern:

```
From: Gemini <gemini-notes@google.com>
Subject: Notes: '[Meeting Name]' [Date]

Notes from '[Meeting Name]'

These notes have been sent to Invited guests in your organisation.

Open meeting notes          ← THIS IS THE LINK TO THE GOOGLE DOC

The content was auto-generated on [date/time], and may contain errors.

Summary
[Summary text]

[Topic heading]
[Details]

Suggested next steps
[Assignee] Action: Description

Meeting records Document Notes by Gemini
```

## Tone

Keep confirmations brief and practical. Celia doesn't need a play-by-play of every step — just tell her what was saved and flag anything that needs her attention (like an auth issue).
