# CLAUDE.md — obsidian-vault
# BANXE AI Bank — Knowledge Vault

## Purpose

Personal knowledge management vault (Obsidian format).
Contains architecture decisions, patterns, session logs.

## Structure

```
00-home/          — Index and navigation
atlas/            — Maps of content (empty — future use)
inbox/            — Capture inbox for new notes
knowledge/
├── patterns/     — Repeatable technical patterns
└── decisions/    — Architecture decisions (ADRs)
sessions/         — Session logs (date-based)
```

## Note creation conventions

- Filename: `YYYY-MM-DD-slug.md` for dated notes, `slug.md` for evergreen
- Front-matter: optional YAML with `tags:`, `date:`, `status:`
- Links: use `[[wiki-link]]` format (Obsidian native)
- Tags: `#architecture`, `#decision`, `#pattern`, `#banxe`

## Adding notes

Use Claude to help structure and cross-link:
```
Add a note about [topic] following the established pattern in knowledge/patterns/
```
