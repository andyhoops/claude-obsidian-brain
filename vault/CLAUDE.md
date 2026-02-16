# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with this vault.

## What This Is

This is an **Obsidian vault** (not a software project). It serves as a personal knowledge management system — a "second brain" for notes, tasks, contacts, projects, and reference material.

There is no build system, test suite, linter, or source code. All content is Markdown files organized in folders.

## Vault Structure

- **Filing Cabinet/** — Primary knowledge repository
  - **People/** — Contacts directory. Each person gets a page with relevant notes, context, and tags.
  - **Projects/** — Project notes, decisions, and reference material
  <!-- CUSTOMIZATION: Add your own categories here. Examples:
  - **Products/** — Product documentation organized by product line
  - **Customers/** — Customer documentation and contacts
  - **Research/** — Research notes and references
  -->
- **Daily Notes/** — Date-stamped daily entries (format: `YYYY-MM-DD.md`)
- **Meetings/** — Meeting notes and transcripts
- **Task Board.md** — Task tracking (action items with checkboxes)
- **Scratch Pad.md** — Ad-hoc notes inbox (see End-of-Day Processing below)

## Daily Processing

This vault is designed to work with three Claude Code skills (`/start`, `/sync`, `/end-of-day`) that automate daily knowledge management:

- **/start** — Morning briefing: reviews tasks, calendar, email, and context memory to set priorities
- **/sync** — Mid-day processing: files scratch pad notes, processes meetings, syncs Google Tasks
- **/end-of-day** — EOD filing: archives scratch pad, files knowledge, updates context memory

**Scratch Pad.md** is the informal inbox — drop notes there throughout the day in any format. The sync and end-of-day skills will extract action items, file knowledge, and archive the raw notes.

## Absolute Rules

These rules apply at all times, with no exceptions:

- **NEVER send email** through the Google Workspace MCP — read and draft only
- **Changes to email settings** (filters, labels, forwarding, etc.) require explicit user approval before execution
- **Editing or modifying calendar events** requires explicit user approval before execution
- **NEVER delete anything** — vault files, calendar events, Google Tasks, emails, labels, filters, etc. The only destructive action permitted is marking tasks as complete

## Working With This Vault

- All files are Markdown with Obsidian-flavored syntax (wiki-links `[[like this]]`, tags, frontmatter properties)
- Attachments go in the `attachments/` folder (configured in Obsidian settings)
- When creating or editing notes, preserve existing Obsidian conventions (wiki-links, tags, frontmatter) found in surrounding files
- File and folder names may contain spaces — always quote paths in shell commands
