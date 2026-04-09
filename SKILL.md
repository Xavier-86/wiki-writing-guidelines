---
name: wiki-writing-guidelines
description: Guidelines for writing and maintaining a Memory Wiki with proper structure, naming conventions, content standards, and cross-linking. Use when creating new wiki pages, organizing knowledge bases, or maintaining wiki indexes. Covers file organization, YAML frontmatter, naming conventions, content principles, and index maintenance workflows.
---

# Wiki Writing Guidelines

Guidelines for creating and maintaining a well-structured Memory Wiki.

## Overview

This skill provides standards and workflows for building organized, cross-referenced knowledge wikis using Obsidian-compatible markdown files.

## When to Use This Skill

Use this skill when:
- Creating a new wiki page or knowledge base entry
- Organizing wiki structure and file hierarchy
- Maintaining wiki indexes (__index.md, README.md)
- Establishing wiki conventions for a project or team
- Adding a new page and need to update related indexes

## File Organization

```
wiki/
├── README.md                    # Root entry - overview of all sections
├── __memory-wiki-index.md       # Global index for Obsidian (auto-generated)
├── section-name/               # Knowledge sections
│   ├── __index.md              # Section entry - lists all pages in this section
│   └── *.md                    # Knowledge pages
```

### Key Files

- **README.md** - Root overview with links to all section indexes
- **__index.md** - Section-level index listing all pages in that section
- **__memory-wiki-index.md** - Obsidian's global graph index (usually auto-generated)

## Naming Conventions

- **Section entry**: `__index.md` (distinguished from root README)
- **Knowledge pages**: lowercase English, kebab-case (e.g., `agent-modeling.md`, `getting-started.md`)
- **Links**: Use Obsidian format `[[filename]]` (e.g., `[[agent-modeling]]`)

## Content Standards

### YAML Frontmatter (Required)

Every wiki page must include:

```yaml
---
title: Page Title
description: Brief description of the page content
date: YYYY-MM-DD
tags: [tag1, tag2]
sources:
  - "Paper citation or source reference"
---
```

### Content Principles

1. **Extract knowledge** - Extract general concepts from sources, don't just list papers or documents
2. **Avoid specific method names** - Write "Bayesian adaptive methods can..." instead of "VariBAD uses..."
3. **Cross-link pages** - Use `[[...]]` to connect related knowledge across pages
4. **Use clear language** - Write for clarity and reusability

### Prohibited Practices

- ❌ Listing source filenames directly in README without context
- ❌ Writing only titles and abstracts without extracted knowledge
- ❌ Using specific implementation names as knowledge page titles
- ❌ Orphaned pages (pages not linked from any index)

## Adding New Pages

When creating a new wiki page, update these indexes:

1. **Section `__index.md`** - Add your page to the relevant category in the appropriate section
2. **Root `README.md`** - Update the Knowledge Sections overview if adding a new major section
3. **`__memory-wiki-index.md`** - Obsidian will auto-update this; for other editors, regenerate the global index

### Workflow Example

```
Create new page: wiki/section-name/new-topic.md
    ↓
Update: wiki/section-name/__index.md (add to relevant category)
    ↓
(If new major section) Update: wiki/README.md Knowledge Sections
    ↓
Commit with clear message
```

## Linking Best Practices

- Use `[[page-name]]` for internal wiki links
- Use `[[page-name|Display Text]]` for custom display text
- Cross-link related concepts to build a knowledge graph
- Include "See also" sections at the end of pages for related topics

## Examples

For concrete examples of wiki pages, indexes, and organizational patterns, see [references/examples.md](references/examples.md). This includes:

- Complete section index (__index.md) examples
- Knowledge page examples with proper frontmatter
- Root README.md structure examples
- Step-by-step workflow for adding new pages
- Bad vs good content comparisons