# End-of-Day Processing

Today's date: `!date +%Y-%m-%d`

Process the Scratch Pad inbox for end-of-day filing. Follow each step below in order.

## Step 1: Read Scratch Pad

Read `Scratch Pad.md` at the vault root. If it is empty or contains only whitespace, stop here and tell me there's nothing to process.

## Step 2: Extract Action Items

Identify any **actionable tasks** in the scratch pad — things that need to be done, followed up on, scheduled, or decided. Append them to `Task Board.md` using this format:

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

Use Obsidian conventions: wiki-links `[[like this]]`, tags, and frontmatter where appropriate. If the scratch pad content is purely action-oriented with no standalone reference knowledge, skip this step and note that in the summary.

## Step 4: Update Daily Note

Append a processing summary to `Daily Notes/YYYY-MM-DD.md` (using today's date). Use this format:

```
## End-of-Day Processing

**Actions filed:** <count> items added to Task Board
**Knowledge filed:** <brief list of where knowledge was filed, or "None — all items were actionable">
**Google Tasks synced:** <count> completed, <count> new pulled in (or "No changes")
**Context carried forward:** <one-line summary of what's top-of-mind>
```

If the daily note doesn't exist yet, create it with a top-level heading `# YYYY-MM-DD` before appending.

## Step 5: Sync Google Tasks

Use the Google Workspace MCP to reconcile the Task Board with Google Tasks:

1. **Pull new tasks:** List all Google Tasks. If any are not yet on the Task Board, add them with a `[GTask]` label.
2. **Push completions:** Scan the Task Board for completed items (lines with `- [x]`) that have a `[GTask]` label or match a Google Task by title. Mark the corresponding Google Task as complete via the MCP.
3. **Push new items:** If Task Board items were explicitly tagged `[GTask]` when created (i.e., the user wants them in Google Tasks too), create them in Google Tasks.

Don't over-match — only mark a Google Task complete if you're confident the Task Board item corresponds to it (title similarity). When in doubt, flag it in the summary for my review.

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
