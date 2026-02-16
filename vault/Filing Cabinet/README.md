# Filing Cabinet

This is your primary knowledge repository. Organize it into subfolders by topic.

## Default Categories

- **People/** — One file per person. Use tags and wiki-links to cross-reference. Good for contacts, team members, collaborators.
- **Projects/** — One folder per project. Store decisions, context, reference material, and notes here.

## Adding Your Own Categories

Create subfolders for the domains you work in. Some examples:

- **Products/** — Product documentation, feature specs, roadmaps
- **Customers/** — Customer profiles, meeting notes, account context
- **Research/** — Research notes, articles, references
- **Processes/** — SOPs, workflows, templates
- **Companies/** — Company profiles, org charts, key contacts

## Conventions

- Use Obsidian wiki-links `[[like this]]` to cross-reference between files
- Add frontmatter tags to make files discoverable (e.g., `tags: [customer, acme-corp]`)
- When updating existing files, append or merge — don't overwrite
- The `/sync` and `/end-of-day` skills will route knowledge here automatically based on content

## Updating the Skills

When you add new categories, update the Filing Cabinet routing rules in `commands/sync.md` and `commands/end-of-day.md` so the skills know where to file things. Look for the `<!-- CUSTOMIZATION -->` comments in each file.
