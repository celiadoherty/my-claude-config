# My Claude Config

Claude Code commands I've built and use day-to-day.

## Commands

### `/gemini-meeting-notes`

Fetches Gemini meeting note emails from Gmail and saves them as structured markdown files.

**What it does:**
- Searches your Gmail for emails from `gemini-notes@google.com` for a given date
- Extracts the summary, topics, next steps, and full transcript (from the linked Google Doc)
- Saves each meeting as a markdown file in `~/Downloads/tem Meeting Notes/`
- Skips files that already exist

**Usage:**
```
/gemini-meeting-notes 2026-03-30
```
Defaults to today's date if no argument is given.

**Output format:**
```
~/Downloads/tem Meeting Notes/YYYY-MM-DD - Meeting Title.md
```

Each file contains the meeting summary, notes by topic, next steps with owners, and the verbatim transcript.

---

## Installation

1. Install [Claude Code](https://claude.ai/code)
2. Copy any command file into your `~/.claude/commands/` folder:

```bash
mkdir -p ~/.claude/commands
curl -o ~/.claude/commands/gemini-meeting-notes.md \
  https://raw.githubusercontent.com/celiadoherty/my-claude-config/main/commands/gemini-meeting-notes.md
```

3. The command is immediately available as `/gemini-meeting-notes` in any Claude Code session.

**Note:** The save path (`~/Downloads/tem Meeting Notes/`) and sender address are set up for my workflow — edit the file to match your own folder name if needed.
