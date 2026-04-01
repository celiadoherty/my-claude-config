Search Gmail for Gemini meeting note emails from gemini-notes@google.com for the date provided as an argument (e.g. "2026-03-30"), defaulting to today's date if no argument is given.

For each email found:
1. Read the full email body to extract the meeting title (from the Subject line, stripping the "Notes: '" prefix and "' DD Mon YYYY" suffix), the time the notes were auto-generated (listed in the email body as "auto-generated on [date], [time] GMT/BST"), the Summary section, all topic sections and their content, and the Suggested next steps.
2. Determine the output filename: `YYYY-MM-DD - [Meeting Title].md` inside `~/Downloads/tem Meeting Notes/`. Create the folder if it doesn't exist.
3. Skip any file that already exists at that path.
4. **Fetch the transcript:** The email body contains a plain-text link labelled "Open meeting notes" that points to a Google Doc with the full transcript. To get the actual URL, use WebFetch on the Gmail message URL (format: `https://mail.google.com/mail/u/0/#all/MESSAGE_ID`) and look for an anchor tag whose text contains "Open meeting notes" — extract the `href`. Then use WebFetch on that Google Docs URL. Parse the page content to extract the verbatim transcript text (everything after the heading "Transcript" or the main body of the document). If WebFetch fails or the transcript cannot be extracted, fall back to noting it's unavailable.
5. For new files, save a markdown file with this exact structure:

```
# [Meeting Title]

*Date:* YYYY-MM-DD
*Time:* HH:MM GMT

---

## Summary

[summary paragraph]

## Notes

### [Topic 1 heading]

[topic 1 content]

### [Topic 2 heading]

[topic 2 content]

## Next Steps

- *[Owner]* [action description]

---

## Transcript

[verbatim transcript text from the Google Doc, or "*Transcript unavailable — full notes accessible via "Open meeting notes" in the original email.*" if it could not be fetched]
```

Notes on formatting:
- If the email has no topic sections (e.g. the call dropped), write `*No topic sections captured.*` under ## Notes
- If there are no next steps, write `*No next steps recorded.*` under ## Next Steps
- Time should be in GMT (convert from BST by subtracting 1 hour if the email says BST)
- Strip any trailing whitespace from the meeting title

After processing all emails, report:
- Which files were saved (filename + meeting title)
- Which files were skipped (already existed)
- Or: "No new Gemini meeting notes found for [date]" if none were found
