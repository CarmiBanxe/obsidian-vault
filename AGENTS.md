# AGENTS.md — obsidian-vault

**Repository:** `~/obsidian-vault/`
**Version:** 1.0 | 2026-04-12
**Purpose:** BANXE shared knowledge base (Obsidian)
**Stack:** Markdown, Obsidian, GitHub Actions (markdown lint)

---

## Core mission

Centralised knowledge management for BANXE AI Bank.
Architecture decisions, compliance research, session logs, and project documentation.

---

## Instruction hierarchy

1. Explicit user instruction
2. `CLAUDE.md` — vault context
3. `AGENTS.md` — this file
4. `~/.claude/CLAUDE.md` — global defaults

---

## Content structure

| Directory | Purpose |
|-----------|---------|
| `00-home/` | Dashboard + navigation + templates |
| `atlas/` | Architecture maps, system diagrams |
| `inbox/` | Raw capture — process within 48h |
| `knowledge/` | Permanent notes (evergreen) |
| `sessions/` | Session logs + handoffs |

---

## Note conventions

```yaml
---
date: 2026-04-12
tags: [banxe, compliance, aml]
status: permanent  # or: inbox, processing
---
```

---

## Rules

| Rule | Details |
|------|---------|
| **No PII** | No customer data, no real transaction IDs |
| **No binaries** | Images via external links only |
| **Filename** | `YYYY-MM-DD-topic.md` or `topic.md` for evergreen |
| **Inbox** | Process inbox notes within 48 hours |

---

## Definition of done

- [ ] Note has frontmatter (date, tags, status)
- [ ] No PII in content
- [ ] Inbox processed (moved to knowledge/ or sessions/)
- [ ] `pre-commit run --all-files` green (markdown lint)
