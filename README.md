# Wiki Writing Guidelines

> **Drop this skill into your OpenClaw workspace and let your AI agent build organized, cross-referenced knowledge bases.**

[![OpenClaw](https://img.shields.io/badge/OpenClaw-Skill-blue)](https://openclaw.ai)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

---

## What is this?

An [OpenClaw Skill](https://docs.openclaw.ai/tools/creating-skills) that teaches AI agents how to create and maintain well-structured Memory Wikis with proper organization, naming conventions, and cross-linking.

No complicated setup. Just drop the `.skill` file into your skills directory and your agent instantly knows how to:

- Organize wiki pages into logical sections
- Use consistent naming conventions (kebab-case, Obsidian links)
- Write proper YAML frontmatter for every page
- Build a cross-referenced knowledge graph
- Maintain indexes when adding new content

| File | Who reads it | What it defines |
|------|--------------|-----------------|
| `SKILL.md` | OpenClaw agents | How to write and organize wiki content |
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
1. Choose the right section
2. Use proper frontmatter
3. Update the section `__index.md`
4. Cross-link related pages

---

## What's Inside

### File Organization

```
wiki/
├── README.md                    # Root entry - overview of all sections
├── __memory-wiki-index.md       # Global index for Obsidian
├── section-name/               # Knowledge sections
│   ├── __index.md              # Section entry
│   └── *.md                    # Knowledge pages
```

### Naming Conventions

| Pattern | Example | Used For |
|---------|---------|----------|
| `__index.md` | `project-management/__index.md` | Section indexes |
| kebab-case | `agile-methodology.md` | Knowledge pages |
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
---
```

### Adding New Pages

When creating content, the agent automatically:

1. **Updates section `__index.md`** - Adds page to relevant category
2. **Updates root `README.md`** - If adding a new major section
3. **Cross-links pages** - Builds a knowledge graph with `[[...]]` links

---

## Examples

See [references/examples.md](references/examples.md) for complete examples including:

- ✅ Section index (`__index.md`) structure
- ✅ Knowledge page with full frontmatter
- ✅ Root README organization
- ✅ Step-by-step "add new page" workflow
- ✅ Bad vs good content comparison

---

## Why This Matters

| Without guidelines | With this skill |
|-------------------|-----------------|
| Inconsistent file naming | Standardized kebab-case everywhere |
| Orphaned pages | Every page linked from indexes |
| Missing metadata | Complete YAML frontmatter |
| Flat structure | Organized sections with indexes |
| Dead links | Cross-referenced knowledge graph |

---

## Compatible With

- [Obsidian](https://obsidian.md) - Native wikilink support
- [OpenClaw Memory Wiki](https://docs.openclaw.ai) - Built-in wiki system
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