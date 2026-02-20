# End-of-Day Processing

Today's date: `!date +%Y-%m-%d`

Process the Scratch Pad inbox for end-of-day filing. Follow each step below in order.

## Step 1: Read Scratch Pad & Mobile Inbox

Read `Scratch Pad.md` at the vault root. Also check the **"Mobile Inbox"** Google Tasks list (`your-email@example.com`) for any quick-capture notes from mobile. Read each task's title and notes — treat them exactly like Scratch Pad entries for the steps below. After processing, mark each Mobile Inbox task as complete to clear the list.

If both sources are empty, stop here and tell me there's nothing to process.

## Step 2: Extract Action Items

Identify any **actionable tasks** in the scratch pad and mobile inbox — things that need to be done, followed up on, scheduled, or decided. Append them to `Task Board.md` using this format:

```
## YYYY-MM-DD

- [ ] Action item description
- [ ] Another action item
```

If `Task Board.md` already has content, append a new date-headed section at the end. If an item is vague, sharpen it into a concrete next action (e.g., "need to get on top of employee goals" → "Review and finalize employee goals; schedule 1:1 reviews").

**What counts as an action item:** anything with an implied "I need to do X" — tasks, follow-ups, reminders, scheduling needs, pending reviews, decisions to make.

## Step 3: File Knowledge

Identify any **reference knowledge** — facts, product notes, customer info, people info, or project context that should be preserved beyond today.

Create or update the appropriate file under `Filing Cabinet/` based on topic:
- People/team notes → `Filing Cabinet/People/<name>.md`
- Project notes → `Filing Cabinet/Projects/<project>/<file>.md`
- Other reference material → create appropriate subfolders under `Filing Cabinet/` as needed

<!-- CUSTOMIZATION: Add your own Filing Cabinet categories here. For example:
- Product notes → Filing Cabinet/Products/<product>/<file>.md
- Customer notes → Filing Cabinet/Customers/<customer>.md
- Research → Filing Cabinet/Research/<topic>.md
See Filing Cabinet/README.md for guidance on organizing your categories. -->

Use Obsidian conventions: wiki-links `[[like this]]`, tags, and frontmatter where appropriate. If the scratch pad and mobile inbox content is purely action-oriented with no standalone reference knowledge, skip this step and note that in the summary.

## Step 4: Write Day Summary to Daily Note

First, read the existing `Daily Notes/YYYY-MM-DD.md` to understand what the day looked like — the morning briefing, any sync entries, and any meetings or actions recorded. Then append a `## Day Summary` section that consolidates everything into a clean, skimmable record of what actually happened.

```
## Day Summary

**Accomplished today:**
- Concrete things completed or moved forward (cross-reference Task Board `[x]` items from today; also pull from scratch pad and sync entries)
- Be factual and specific — "Submitted Versant RFP" not "worked on RFP"

**Key meetings:**
- Meeting name — one-line note on outcome, decision, or next step (skip routine standups unless something notable came up)

**Carried forward:**
- Open items that were on the plate today but not completed
- Keep concise — these will feed the next day's morning briefing

**Filed/noted:**
- Any knowledge or reference material filed to the vault today (or "Nothing filed")

**EOD stats:**
Actions filed: <count> | Knowledge filed: <count or "None"> | Google Tasks: <X> completed, <X> new
```

If the daily note doesn't exist yet, create it with a top-level heading `# YYYY-MM-DD` before appending.

The morning briefing and any sync entries are retained above this section as raw context. The Day Summary is the canonical "what happened" record for future reference.

## Step 5: Sync Google Tasks

Use the Google Workspace MCP to reconcile the Task Board with Google Tasks:

1. **Pull new tasks:** List all Google Tasks (incomplete). If any are not yet on the Task Board, add them with a `[GTask]` label.
2. **Pull completions:** For each task list, also query with `show_completed=true` and `completed_min` set to 24 hours ago. If a recently completed Google Task matches an open `[GTask]` item on the Task Board (by title), mark that Task Board item as `[x]`. This is essential — the user often completes tasks directly in Google Tasks.
3. **Push completions:** Scan the Task Board for completed items (lines with `- [x]`) that have a `[GTask]` label or match an incomplete Google Task by title. Mark the corresponding Google Task as complete via the MCP.
4. **Push new items:** If Task Board items were explicitly tagged `[GTask]` when created (i.e., the user wants them in Google Tasks too), create them in Google Tasks.

Don't over-match — only sync a completion if you're confident the titles correspond. When in doubt, flag it in the summary for my review.

## Step 6: Archive Scratch Pad

1. Copy the **exact original contents** of `Scratch Pad.md` to `archive/scratch-pad/YYYY-MM-DD.md`
2. Clear `Scratch Pad.md` by writing it as an empty file (or just a heading `# Scratch Pad` if you prefer to keep structure)

This preserves the raw notes before any processing.

## Step 7: Update Context Memory

Write or update `.claude/context.md` with a rolling summary that helps the next session start informed. Use this structure:

```markdown
# Context Memory

_Last updated: YYYY-MM-DD_

## Current Priorities
- Priority 1
- Priority 2

## Open Threads
- Thread or pending item that needs follow-up
- Another open item

## Recent Context
- Brief note about what happened today that's relevant going forward
```

Merge new information with any existing content in the file. Remove items that are clearly resolved. Keep this file concise — it should be a quick-read briefing, not a log.

## Final Output

After completing all steps, give me a brief summary of what was processed:
- How many action items were extracted
- What knowledge was filed and where
- Google Tasks sync: how many completions pushed, how many new tasks pulled
- Any items that were ambiguous or need my review
