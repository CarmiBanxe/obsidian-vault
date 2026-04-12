# obsidian-vault

**BANXE AI Bank — Obsidian Knowledge Base**

Shared knowledge management vault for the BANXE project. Contains architecture decisions, session notes, compliance research, and project documentation formatted for Obsidian.

---

## Structure

```
obsidian-vault/
├── 00-home/        ← Dashboard and navigation
├── atlas/          ← Architecture maps and diagrams
├── inbox/          ← Capture inbox (process regularly)
├── knowledge/      ← Permanent notes and references
└── sessions/       ← Session logs and handoffs
```

---

## Usage

1. Open this directory in [Obsidian](https://obsidian.md/)
2. Enable community plugins from `.obsidian/plugins/`
3. Use templates from `00-home/templates/`

---

## CI/CD

- `.github/workflows/` — markdown lint + link check

---

## Conventions

- Filename format: `YYYY-MM-DD-topic.md`
- Frontmatter required: `date`, `tags`, `status`
- No binary files (images via links only)
