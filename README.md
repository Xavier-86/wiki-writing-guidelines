# Wiki Writing Guidelines

> **Drop this skill into your OpenClaw workspace and let your AI agent build organized, cross-referenced knowledge bases that compound over time.**

[![OpenClaw](https://img.shields.io/badge/OpenClaw-Skill-blue)](https://openclaw.ai)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

---

## What is this?

An [OpenClaw Skill](https://docs.openclaw.ai/tools/creating-skills) that teaches AI agents how to create and maintain well-structured Memory Wikis with proper organization, naming conventions, and cross-linking.

**Key innovation: The Filing Loop** — every AI answer gets evaluated for saving back to the wiki, creating compounding knowledge value.

No complicated setup. Just drop the `.skill` file into your skills directory and your agent instantly knows how to:

- **Capture knowledge** with the filing loop (archive valuable AI answers)
- **Organize** wiki pages into the three-layer architecture (`raw/`, `wiki/`, `AGENTS.md`)
- **Execute** four standard operations: `/ingest`, `/compile`, `/query`, `/lint`
- **Use** consistent naming conventions (kebab-case, Obsidian links)
- **Write** proper YAML frontmatter for every page
- **Build** a cross-referenced knowledge graph
- **Maintain** indexes and operation logs

| File | Who reads it | What it defines |
|------|--------------|-----------------|
| `SKILL.md` | OpenClaw agents | How to write and organize wiki content |
| `AGENTS.md` | Agents (per session) | Wiki structure, operations, and startup workflow |
| `references/examples.md` | Agents (on demand) | Concrete examples of wiki pages and indexes |

---

## Quick Start

```bash
# Install the skill
cp wiki-writing-guidelines.skill ~/.openclaw/skills/

# Or use ClawHub
clawhub install wiki-writing-guidelines
```

Then simply tell your agent:

> "Create a wiki page about [topic]"

The agent will automatically:
1. Use the filing loop to evaluate if the answer should be archived
2. Choose the right section
3. Use proper frontmatter
4. Update the section `__index.md`
5. Cross-link related pages

---

## What's Inside

### Core Concepts

#### 📥 The Filing Loop

Most people use AI like a search engine with amnesia — ask, get answer, close tab, start over tomorrow.

The filing loop changes this:
```
Ask → Get Answer → Evaluate → Archive to wiki → Future questions benefit
```

Every saved answer enriches the knowledge base for future queries. **Compound returns on every interaction.**

#### 🏗️ Three-Layer Architecture

```
workspace/
├── raw/                    # Layer 1: Raw sources (AI reads only)
│   ├── articles/          # Web clippings, articles
│   ├── papers/            # PDFs, research papers
│   ├── transcripts/       # Video/podcast transcripts
│   └── assets/            # Images, attachments
├── wiki/                   # Layer 2: Compiled knowledge (AI reads/writes)
│   ├── README.md          # Root overview
│   ├── __memory-wiki-index.md
│   ├── log.md             # Operation log (append-only)
│   ├── outputs/           # Archived query answers
│   └── section-name/      # Knowledge sections
│       ├── __index.md     # Section index
│       └── *.md           # Knowledge pages
└── AGENTS.md              # Layer 3: Schema (defines structure & operations)
```

**Layer 1 (raw/)**: Your single source of truth. The AI reads but never modifies.

**Layer 2 (wiki/)**: AI-generated and AI-maintained. Summaries, concepts, connections, indexes.

**Layer 3 (AGENTS.md)**: Configuration that tells the AI how to operate. Add wiki-related content here.

#### 🔄 Four Standard Operations

| Operation | Command | Purpose |
|-----------|---------|---------|
| **Ingest** | `/ingest` | Process new sources from `raw/` into wiki |
| **Compile** | `/compile` | Update wiki pages, maintain indexes, weave connections |
| **Query** | `/query` | Research wiki content, archive answers to `outputs/` |
| **Lint** | `/lint` | Health checks: fix broken links, merge duplicates, flag stale content |

```
┌─────────┐    ┌──────────┐    ┌───────┐    ┌──────┐
│ Ingest  │ -> │ Compile  │ -> │ Query │ -> │ Lint │
│ (摄取)   │    │ (编译)    │    │ (查询) │    │ (检查)│
└─────────┘    └──────────┘    └───────┘    └──────┘
```

### File Organization

```
wiki/
├── README.md                    # Root entry - overview of all sections
├── __memory-wiki-index.md       # Global index for Obsidian
├── log.md                       # Operation log: ingest → compile → query → lint
├── outputs/                     # Query answers archived here (filing loop)
└── section-name/               # Knowledge sections
    ├── __index.md              # Section entry
    ├── _index.md               # Detailed category index (optional)
    └── *.md                    # Knowledge pages
```

### Naming Conventions

| Pattern | Example | Used For |
|---------|---------|----------|
| `__index.md` | `project-management/__index.md` | Section indexes |
| `_index.md` | `concepts/_index.md` | Detailed category indexes |
| kebab-case | `agile-methodology.md` | Knowledge pages |
| `author-year-title.md` | `karpathy-2024-llm-kb.md` | Source summaries |
| `[[link]]` | `[[agile-methodology]]` | Internal wiki links |

### Content Standards

Every wiki page includes:

```yaml
---
title: Page Title
description: Brief description
date: YYYY-MM-DD
tags: [tag1, tag2]
sources:
  - "Source citation"
last_modified: YYYY-MM-DD  # Optional
---
```

### Index Format

Each entry in `__index.md`:

```markdown
- [[page-name]] - 50-word summary #tag1 #tag2 (3 sources)
```

### Operation Log Format

`wiki/log.md` (append-only):

```markdown
# Wiki Operation Log

## 2026-04-10
- [14:32] Ingest: Added 3 articles to raw/articles/
- [14:35] Compile: Generated 5 concept pages, updated index
- [15:10] Query: "How to configure proxy?" → archived to outputs/proxy-setup.md
- [15:30] Lint: Fixed 2 broken links, merged 1 duplicate concept
```

### Adding New Pages

When creating content, the agent automatically:

1. **Applies the filing loop** — Evaluates if the answer should be archived
2. **Updates section `__index.md`** — Adds page to relevant category
3. **Updates root `README.md`** — If adding a new major section
4. **Cross-links pages** — Builds a knowledge graph with `[[...]]` links
5. **Logs the operation** — Appends to `wiki/log.md`

---

## Recommended Tools

### Obsidian Plugins

| Plugin | Purpose | Why It Helps |
|--------|---------|--------------|
| **Dataview** | Database queries | Query YAML frontmatter, build dashboards |
| **Templater** | Auto-fill templates | Populate dates, filenames automatically |
| **Obsidian Git** | Version control | Auto-commit every 30 min, full history |
| **Tag Wrangler** | Bulk tag management | Rename/merge tags across vault |
| **Linter** | Auto-formatting | Consistent YAML, headings, spacing |
| **Web Clipper** | Browser integration | One-click save to `raw/articles/` |
| **Local Images Plus** | Offline images | Download images to `raw/assets/` |

#### Dataview Example

```markdown
```dataview
TABLE description, date, sources
FROM "wiki"
WHERE contains(tags, "concept")
SORT date DESC
```
```

This creates a live table of all concept articles, auto-updated.

---

## Examples

See [references/examples.md](references/examples.md) for complete examples including:

- ✅ Section index (`__index.md`) structure
- ✅ Knowledge page with full frontmatter
- ✅ Root README organization
- ✅ Index entry format with summary + tags
- ✅ Operation log examples
- ✅ Step-by-step "add new page" workflow
- ✅ Bad vs good content comparison
- ✅ Sample AGENTS.md wiki section

---

## Why This Matters

| Without guidelines | With this skill |
|-------------------|-----------------|
| Inconsistent file naming | Standardized kebab-case everywhere |
| Orphaned pages | Every page linked from indexes |
| Missing metadata | Complete YAML frontmatter |
| Flat structure | Three-layer architecture |
| One-off AI answers | Filing loop → compounding knowledge |
| Manual maintenance | Four standard operations |
| No tracking | Operation logs in `log.md` |
| Dead links | Cross-referenced knowledge graph |

---

## Compatible With

- [Obsidian](https://obsidian.md) — Native wikilink support, Dataview queries
- [OpenClaw Memory Wiki](https://docs.openclaw.ai) — Built-in wiki system
- Any Markdown-based knowledge base

---

## Repository Structure

```
wiki-writing-guidelines/
├── README.md              # This file - human-readable documentation
├── SKILL.md               # The skill - loaded by OpenClaw agents
├── references/
│   └── examples.md        # Concrete examples (loaded on demand)
└── LICENSE                # MIT License
```

> **Note:** The `.skill` package only includes `SKILL.md` and `references/` - exactly what agents need.

---

## Building the Skill

To package this skill for distribution:

```bash
# Clone the repository
git clone https://github.com/yourusername/wiki-writing-guidelines.git
cd wiki-writing-guidelines

# Package using OpenClaw's skill-creator
python3 -m openclaw.skills.package .

# Or use the skill-creator script directly
python3 /path/to/skill-creator/scripts/package_skill.py . ./dist
```

This creates `wiki-writing-guidelines.skill` ready for installation.

---

## Contributing

Found a better pattern? Want to add more examples?

1. Fork the repo
2. Add your improvements
3. Submit a PR

---

## License

MIT © [Your Name]

---

*Built for agents, by agents.* 🤖
