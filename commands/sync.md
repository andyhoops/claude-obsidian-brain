# Sync

Today's date: `!date +%Y-%m-%d`
Current time: `!date +%H:%M`

You're my assistant processing a pile of loose notes. Read everything, file it where it belongs, and give me a quick debrief. Be thorough but don't over-organize — match the level of detail I wrote with the level of detail you file.

---

## Step 1: Read Scratch Pad & Mobile Inbox

Read `Scratch Pad.md`. Note its contents for processing in the steps below.

If it's empty or only whitespace, note that and move on — there may still be new meetings or mobile notes to process.

Also check the **"Mobile Inbox"** Google Tasks list (`your-email@example.com`) for any quick-capture notes from mobile. Read each task's title and notes. Treat these exactly like Scratch Pad entries — they feed into the same action item extraction (Step 4) and knowledge filing (Step 6) pipeline. After processing, mark each Mobile Inbox task as complete to clear the list.

## Step 2: Check for New Meeting Transcripts

List all files in `Meetings/`. Read `.claude/context.md` to check the `## Meetings Processed` section for which files have already been processed in a previous sync.

For each **unprocessed** meeting file:
1. Read the file
2. Append a concise summary to today's daily note (see Step 7 format)
3. Extract any action items or decisions into the task list (Step 4)
4. File any reference knowledge — product decisions, customer info, people updates — into the appropriate location under `Filing Cabinet/`
5. Mark the file as processed by adding it to the `## Meetings Processed` list in `.claude/context.md`
6. **Archive one-off meeting files:** If the filename starts with a date prefix (e.g., `2026-02-18 NBCU Proposal Review.md`), it's a one-off — move it to `Meetings/archive/YYYY-MM/` after processing. Create the month folder if it doesn't exist. Files without a date prefix are recurring docs and stay in `Meetings/`.

If there are no new meetings, skip this step.

## Step 3: Check Google Calendar

Use the Google Workspace MCP to review the remainder of today's calendar from my primary calendar (`your-email@example.com`).

- List today's remaining events (from the current time onward)
- Ignore working-location events (type `workingLocation`)
- **External attendee check:** Flag any meetings where attendees have email addresses that are NOT `@your-domain.com` — these are usually customer or partner meetings and may need prep
- Note if any new meetings have appeared since the start-of-day briefing (compare against the daily note's start-of-day calendar section if it exists)
- If a meeting is coming up within the next 2 hours, call it out as imminent

Use this to inform task prioritisation — imminent meeting prep should bubble up, and if the rest of the day is meeting-heavy, flag limited time for deep work.

## Step 4: Update Task Board

Gather all action items found in the scratch pad, mobile inbox, and any new meeting transcripts. Append them to `Task Board.md` under a time-stamped section:

```
## YYYY-MM-DD HH:MM

- [ ] Action item description
- [ ] Another action item
```

If `Task Board.md` already has a section for this exact timestamp, append to it. Otherwise create a new section at the end.

**Sharpen vague items** into concrete next actions. "Talk to Sarah about the timeline" → "Follow up with Sarah on project timeline and confirm delivery dates."

**What counts as an action item:** anything with an implied "I need to do X" — tasks, follow-ups, reminders, scheduling needs, pending reviews, decisions to make.

If there are no action items from any source, skip this step.

## Step 5: Sync Google Tasks

Use the Google Workspace MCP to reconcile the Task Board with Google Tasks:

1. **Pull new tasks:** List all Google Tasks (incomplete). If any are not yet on the Task Board, add them with a `[GTask]` label.
2. **Pull completions:** For each task list, also query with `show_completed=true` and `completed_min` set to 24 hours ago. If a recently completed Google Task matches an open `[GTask]` item on the Task Board (by title), mark that Task Board item as `[x]`. This is essential — the user often completes tasks directly in Google Tasks.
3. **Push completions:** Scan the Task Board for completed items (lines with `- [x]`) that have a `[GTask]` label or match an incomplete Google Task by title. Mark the corresponding Google Task as complete via the MCP.
4. **Push new items:** If Task Board items were explicitly tagged `[GTask]` when created (i.e., the user wants them in Google Tasks too), create them in Google Tasks.

Don't over-match — only sync a completion if you're confident the titles correspond. When in doubt, flag it in the debrief for my review.

## Step 6: File Knowledge

Identify any **reference knowledge** from the scratch pad or meetings — facts, product notes, customer info, people updates, or project context worth preserving.

Create or update the appropriate file under `Filing Cabinet/`:
- People/team notes → `Filing Cabinet/People/<name>.md`
- Project notes → `Filing Cabinet/Projects/<project>/<file>.md`
- Other reference material → create appropriate subfolders under `Filing Cabinet/` as needed

<!-- CUSTOMIZATION: Add your own Filing Cabinet categories here. For example:
- Product notes → Filing Cabinet/Products/<product>/<file>.md
- Customer notes → Filing Cabinet/Customers/<customer>.md
- Research → Filing Cabinet/Research/<topic>.md
See Filing Cabinet/README.md for guidance on organizing your categories. -->

Use Obsidian conventions: wiki-links `[[like this]]`, tags, and frontmatter where appropriate. When updating an existing file, append or merge — don't overwrite existing content.

If everything is purely actionable with no reference knowledge, skip this step.

## Step 7: Update Daily Note

Append a sync entry to `Daily Notes/YYYY-MM-DD.md`. If the file doesn't exist, create it with a `# YYYY-MM-DD` heading first.

Format:

```
### Sync — HH:MM

**Progress since morning:**
- List anything completed or meaningfully progressed since the morning briefing (cross-reference Task Board `[x]` items added today, and anything mentioned as done in the scratch pad or meetings)
- If nothing has changed yet, say "Nothing completed yet"

**From scratch pad / mobile inbox:**
- Brief summary of what was captured (or "Nothing new")

**From meetings:**
- Meeting title → summary of key points (or "No new meetings")

**Calendar update:**
- Any new/changed meetings since last check
- Upcoming meetings for rest of day (flag [External] where applicable)
- (or "No changes")

**Actions added:** <count> items to Task Board (or "None")
**Google Tasks:** <count> completed, <count> new pulled in (or "No changes")
**Knowledge filed:** <where, or "None">
```

Multiple syncs per day should stack as separate entries — never overwrite earlier ones.

## Step 8: Clear Scratch Pad

Once everything from `Scratch Pad.md` has been processed and filed (and Mobile Inbox tasks marked complete), reset the scratch pad to:

```
# Scratch Pad
```

Only clear it if there was content to process. If it was already empty, leave it alone.

## Step 9: Update Context Memory

Update `.claude/context.md` with any new priorities, open threads, or context from this sync. Merge with existing content — don't wipe previous entries. Remove items only if they're clearly resolved.

The file should always maintain this structure:

```markdown
# Context Memory

_Last updated: YYYY-MM-DD HH:MM_

## Current Priorities
- ...

## Open Threads
- ...

## Recent Context
- ...

## Meetings Processed
- filename.md (YYYY-MM-DD)
- ...
```

---

## Output

Give me a quick debrief — like an assistant handing back a sorted stack:
- What you found in the scratch pad and mobile inbox
- Any meetings processed and key takeaways
- Calendar check: new meetings, imminent meetings, or external meetings needing prep
- Google Tasks sync: completions pushed, new tasks pulled
- How many actions were filed
- Where knowledge was routed
- Anything ambiguous that needs my input
