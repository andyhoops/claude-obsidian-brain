# Claude Obsidian Brain

Turn [Claude Code](https://docs.anthropic.com/en/docs/claude-code) into a personal operating system for your [Obsidian](https://obsidian.md) vault. Three daily skills — `/start`, `/sync`, and `/end-of-day` — handle your morning briefing, mid-day processing, and end-of-day filing, all powered by Claude Code's tool use with Google Calendar, Gmail, and Google Tasks via MCP.

I based the system on, and was inspired to get started by, this post by https://michaelcrist.substack.com/ : https://substack.com/inbox/post/184955320

## How It Works

You keep an Obsidian vault as your second brain. Throughout the day, you drop notes into a **Scratch Pad**. Claude Code processes everything through three rituals:

| Skill | When | What it does |
|-------|------|-------------|
| `/start` | Morning | Reads your task board, context memory, calendar, Gmail, and Google Tasks. Presents a prioritized briefing. |
| `/sync` | Mid-day (as needed) | Processes scratch pad notes and meeting transcripts. Files knowledge, extracts action items, syncs Google Tasks. |
| `/end-of-day` | End of day | Archives the scratch pad, files remaining knowledge, syncs tasks, updates context memory for tomorrow. |

**Data flow:**

```
Scratch Pad → /sync or /end-of-day → Task Board + Filing Cabinet + Daily Note
                                       ↕
                                  Google Tasks (two-way sync)
                                  Google Calendar (read)
                                  Gmail (read + draft)
```

Context memory (`.claude/context.md`) carries priorities and open threads forward between sessions so each day starts informed.

## Prerequisites

- **[Claude Code](https://docs.anthropic.com/en/docs/claude-code)** — Anthropic's CLI tool for Claude
- **[Obsidian](https://obsidian.md)** — For viewing and editing your vault (any markdown editor works, but Obsidian's wiki-links and graph view are ideal)
- **[workspace-mcp](https://github.com/nicholasgriffintn/workspace-mcp)** — Google Workspace MCP server for Calendar, Gmail, and Tasks integration
- **Python 3.10+** with `uvx` or `pip` — For running the MCP server
- **Google Cloud OAuth credentials** — For authenticating with Google Workspace APIs

## Quick Start

### 1. Clone this repo

```bash
git clone https://github.com/YOUR_USERNAME/claude-obsidian-brain.git
cd claude-obsidian-brain
```

### 2. Set up your Obsidian vault

Copy the `vault/` directory to wherever you keep your Obsidian vaults:

```bash
cp -r vault/ ~/Documents/Obsidian/my-brain/
```

Open this folder as a vault in Obsidian.

### 3. Install the Claude Code skills

Copy the skill files to your Claude Code commands directory:

```bash
mkdir -p ~/.claude/commands
cp commands/*.md ~/.claude/commands/
```

### 4. Configure the Google Workspace MCP

First, set up OAuth credentials (see [Google Workspace MCP Setup](#google-workspace-mcp-setup) below).

Then create your `.mcp.json` from the example:

```bash
cd ~/Documents/Obsidian/my-brain/  # your vault directory
cp .mcp.json.example .mcp.json
```

Edit `.mcp.json` and replace the placeholder values with your OAuth credentials:
- `YOUR_OAUTH_CLIENT_ID.apps.googleusercontent.com` → your actual client ID
- `YOUR_OAUTH_CLIENT_SECRET` → your actual client secret

### 5. Customize the skills

Open the three files in `~/.claude/commands/` and replace placeholder values:

- `your-email@example.com` → your Google Workspace email address
- `@your-domain.com` → your organization's email domain (used to identify external meeting attendees)

### 6. Customize your Filing Cabinet

Edit `Filing Cabinet/README.md` in your vault to plan your categories, then update the routing rules in `commands/sync.md` and `commands/end-of-day.md` (look for the `<!-- CUSTOMIZATION -->` comments).

### 7. First run

Open Claude Code in your vault directory and run:

```
/start
```

The first time, the MCP server will prompt you to authenticate with Google. Follow the OAuth flow in your browser. After that, you'll get your first morning briefing.

## Vault Structure

```
your-vault/
├── CLAUDE.md                    # Instructions for Claude Code
├── .mcp.json                    # MCP server config (git-ignored)
├── .claude/
│   └── context.md               # Rolling context memory between sessions
├── Scratch Pad.md               # Drop notes here throughout the day
├── Task Board.md                # Action items with checkboxes
├── Daily Notes/                 # Auto-generated daily entries
│   └── 2025-01-15.md
├── Meetings/                    # Drop meeting notes/transcripts here
│   └── 2025-01-15 Team Sync.md
├── archive/
│   └── scratch-pad/             # Archived scratch pad snapshots
│       └── 2025-01-15.md
└── Filing Cabinet/              # Your organized knowledge base
    ├── People/
    ├── Projects/
    └── README.md                # Guide for organizing categories
```

| File/Folder | Purpose |
|-------------|---------|
| **Scratch Pad.md** | Informal inbox. Drop anything here — the skills will sort it. |
| **Task Board.md** | All action items. Skills extract tasks from scratch pad and meetings, sync with Google Tasks. |
| **Daily Notes/** | Auto-generated log of each day's briefings, syncs, and processing. |
| **Meetings/** | Drop meeting notes or transcripts here. `/sync` will process unread ones. |
| **.claude/context.md** | Rolling memory that carries priorities and open threads between sessions. |
| **Filing Cabinet/** | Organized reference knowledge. Skills file things here based on topic. |
| **archive/scratch-pad/** | Raw scratch pad snapshots preserved before processing. |

## Skills Reference

### `/start` — Morning Briefing

**When:** Start of each work day

**What it does:**
1. Reads context memory for carry-forward priorities
2. Reviews the Task Board for open items
3. Checks yesterday's daily note for loose ends
4. Pulls today's calendar and next 2 days for lookahead
5. Scans Gmail (last 7 days) for missed actions, unanswered questions, commitments
6. Lists Google Tasks and cross-references with Task Board
7. Presents a prioritized morning briefing
8. Creates today's daily note with confirmed priorities (after your response)

### `/sync` — Mid-Day Processing

**When:** After dropping notes in Scratch Pad, or after meetings

**What it does:**
1. Reads and processes Scratch Pad contents
2. Processes any new meeting transcripts in `Meetings/`
3. Checks remaining calendar for the day
4. Extracts action items to Task Board
5. Syncs Google Tasks (pull new, push completions)
6. Files reference knowledge to Filing Cabinet
7. Appends a sync entry to today's daily note
8. Clears the Scratch Pad
9. Updates context memory

### `/end-of-day` — EOD Filing

**When:** End of each work day

**What it does:**
1. Reads Scratch Pad contents
2. Extracts final action items to Task Board
3. Files remaining knowledge to Filing Cabinet
4. Appends EOD summary to daily note
5. Syncs Google Tasks
6. Archives Scratch Pad to `archive/scratch-pad/`
7. Updates context memory for tomorrow

## Customization

### Filing Cabinet Categories

The default setup includes `People/` and `Projects/`. To add your own:

1. Create the subfolder in `Filing Cabinet/`
2. Update the routing rules in `commands/sync.md` and `commands/end-of-day.md` — look for the `<!-- CUSTOMIZATION -->` comment blocks
3. See `Filing Cabinet/README.md` for examples

### Adding a Second Vault

The `/start` skill includes a commented-out section for dual-vault support. To enable it:

1. Set up a second Obsidian vault with the same folder structure (Task Board, Scratch Pad, Daily Notes, etc.)
2. Uncomment the `<!-- DUAL-VAULT OPTION -->` block in `commands/start.md`
3. Update the vault detection logic to match your directory names
4. Label items `[Work]` / `[Personal]` in briefings

The `/sync` and `/end-of-day` skills operate on the current vault only, so run them from whichever vault has new content.

### External Attendee Detection

The skills flag meeting attendees whose email domain differs from yours as `[External]`. Update `@your-domain.com` in the skill files to match your organization's domain.

### Adjusting the Gmail Scan Window

The `/start` skill scans the last 7 days of Gmail by default. Adjust the search window in `commands/start.md` Step 5 if you prefer a different range.

## Google Workspace MCP Setup

The skills integrate with Google Calendar, Gmail, and Tasks through the [workspace-mcp](https://github.com/nicholasgriffintn/workspace-mcp) MCP server.

### 1. Create Google Cloud OAuth Credentials

1. Go to the [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project (or use an existing one)
3. Enable the following APIs:
   - Gmail API
   - Google Calendar API
   - Google Tasks API
4. Go to **Credentials** → **Create Credentials** → **OAuth client ID**
5. Application type: **Desktop app**
6. Download the credentials — you'll need the **Client ID** and **Client Secret**

### 2. Configure OAuth Consent Screen

1. Go to **OAuth consent screen** in Google Cloud Console
2. Set up as **External** (or Internal if using Google Workspace)
3. Add the required scopes:
   - `https://www.googleapis.com/auth/gmail.modify`
   - `https://www.googleapis.com/auth/calendar`
   - `https://www.googleapis.com/auth/tasks`
4. Add your Google account as a test user

### 3. Install workspace-mcp

```bash
# Using uvx (recommended)
uvx workspace-mcp --help

# Or install via pip
pip install workspace-mcp
```

### 4. Configure .mcp.json

Copy the example and add your credentials:

```bash
cd your-vault-directory
cp .mcp.json.example .mcp.json
```

Edit `.mcp.json` with your actual OAuth Client ID and Client Secret.

### 5. First Authentication

The first time a skill triggers the MCP server, it will open a browser window for Google OAuth. Sign in with the Google account you want to use. The token is cached locally for future sessions.

If you're on a headless machine or WSL, set `OAUTHLIB_INSECURE_TRANSPORT=1` in the `.mcp.json` env (already included in the example) and follow the URL printed to the terminal.

## Tips

- **Scratch Pad is your inbox.** Don't organize — just dump. The skills will sort it.
- **Drop meeting notes in `Meetings/`** with the date in the filename (e.g., `2025-01-15 Team Sync.md`). The `/sync` skill will process them automatically.
- **Tag tasks with `[GTask]`** if you want them pushed to Google Tasks for mobile access.
- **Context memory is automatic.** You don't need to maintain `.claude/context.md` manually — the skills keep it updated. But you can edit it to nudge priorities.
- **Run `/sync` as often as you want.** Multiple syncs per day stack as separate entries in the daily note.
- **The Task Board is append-only.** Completed items get a `[x]` checkbox but stay visible. Periodically review and archive old sections if it gets long.
- **CLAUDE.md protects you.** The absolute rules prevent Claude from sending emails, modifying calendar events, or deleting anything without explicit approval.

## License

MIT
