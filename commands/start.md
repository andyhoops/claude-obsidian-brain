# Start of Day

Today's date: `!date +%Y-%m-%d`
Day of week: `!date +%A`

You're my assistant running a quick morning standup across my second brain vault. Be concise and conversational — no walls of text. Help me walk into the day with a clear head.

---

<!-- DUAL-VAULT OPTION:
If you maintain two vaults (e.g., work and personal), you can extend this skill
to scan both. Determine which vault you're in from the working directory name,
derive the sibling path (e.g., ../other-vault), and read Task Board.md,
.claude/context.md, and Daily Notes/ from both. Label items [Work] / [Personal]
in the briefing. Both vaults should share the same folder structure. -->

## Step 1: Check Context Memory

Read `.claude/context.md`. This has carry-forward context from previous sessions — priorities, open threads, and recent activity. Use it to frame today's briefing.

## Step 2: Review Task Board

Read `Task Board.md`. Summarize what's on my plate:
- Group tasks by theme or category
- Flag anything that looks time-sensitive or overdue based on when it was filed
- Note how many open items there are total

## Step 3: Check Yesterday's Daily Note

Find the most recent daily note before today in `Daily Notes/`. Read it for context on what happened yesterday — what was processed, what actions were taken, any loose ends.

## Step 4: Check Google Calendar

Use the Google Workspace MCP to pull today's events from my primary calendar (`your-email@example.com`). Also glance at the next 2 working days so we can flag anything looming.

- List today's events (all-day and timed)
- List the next 2 working days' events for lookahead
- Note any scheduling conflicts or back-to-back blocks
- Ignore working-location events (type `workingLocation`) — they're just "Home" / "Office" markers
- **External attendee check:** For each meeting, check if any attendees have email addresses that are NOT `@your-domain.com`. External attendees usually indicate a customer or partner meeting — flag these prominently as they're higher priority and may need prep.

Use this calendar data to inform priority-setting: if I have a meeting on a topic, related prep tasks should be prioritised. If my day is meeting-heavy, flag that I'll have limited deep-work time. Customer-facing meetings should generally rank above internal ones.

## Step 5: Scan Gmail for Actions

Use the Google Workspace MCP to scan my Gmail for missed actions. Search the last 7 days of inbox and sent mail. Look for:

1. **Action requests** — emails where someone asked me to do something and I haven't replied or the task appears unresolved
2. **Review requests** — documents, PRs, proposals, or approvals waiting on me
3. **Unanswered questions** — direct questions sent to me that I haven't responded to
4. **Commitments I made** — things I said I would do in my sent mail that may not be completed yet
5. **Deadlines mentioned** — any upcoming deadlines referenced in recent threads
6. **Meeting follow-ups** — action items from meeting-related emails or calendar invites

**Exclude:** newsletters, marketing emails, automated notifications with no required action, and anything I've already clearly responded to or resolved.

De-duplicate against existing Task Board items and calendar events. Label actionable items with `[Gmail]` in the briefing.

## Step 6: Pull Google Tasks

Use the Google Workspace MCP to list all tasks from my Google Tasks lists. For each task:

- Note the title, due date (if any), and which task list it belongs to
- Cross-reference against the Task Board — flag any that are already tracked (duplicates)
- Flag overdue tasks prominently
- Add net-new Google Tasks items to the briefing with a `[GTask]` label

**Two-way sync:** When presenting the briefing, note any items on the Task Board that appear to match completed Google Tasks (or vice versa) so we can reconcile them.

## Step 7: Scan for Time-Sensitive Items

Check for anything that implies a deadline or urgency:
- Tasks mentioning specific days ("Monday", "by EOD", "this week")
- Items that have been on the Task Board for more than a few days
- Cross-reference tasks with today's calendar — if a meeting relates to a task, flag it as prep-needed
- Check `Meetings/` for today's date in filenames for any pre-written agendas

## Step 8: Present the Briefing

Give me a morning briefing in this format:

```
## Good morning — here's your $DAY_OF_WEEK briefing

**Today's calendar:**
- Chronological list of meetings (time, title, attendees summary)
- Flag customer/partner meetings with [External] and note who
- Note total meeting hours and available deep-work windows

**Carry-forward:**
- Key context items from context memory

**On your plate today:**
- Prioritized task list across all sources, most urgent first
- Label each item with its source: [Gmail], [GTask], or [Task Board]
- (flag time-sensitive items, especially anything tied to today's meetings)
- Include Gmail action items and Google Tasks, de-duped against existing Task Board items

**Heads up:**
- Anything that's been sitting too long or needs attention soon
- Notable meetings in the next 2 days to prep for

**Quick question:**
- Are there any tasks on the board you've already completed that I should clear?
- Anything new to add before we get started?
```

Keep priorities to a reasonable number. If there are more than 5-6 items, group the less urgent ones under an "Also on the radar" section so I'm not overwhelmed.

## Step 9: Update Daily Note

Create today's daily note at `Daily Notes/YYYY-MM-DD.md` if it doesn't exist (with a `# YYYY-MM-DD` heading). Append:

```
### Start of Day — HH:MM

**Priorities set:**
- Priority 1
- Priority 2
- ...
```

Wait until after I respond to the briefing so you can capture my actual confirmed priorities, not just your suggestions.
