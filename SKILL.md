---
name: wiki-writing-guidelines
description: Guidelines for writing and maintaining a Memory Wiki with proper structure, naming conventions, content standards, and cross-linking. Use when creating new wiki pages, organizing knowledge bases, or maintaining wiki indexes. Covers file organization, YAML frontmatter, naming conventions, content principles, and index maintenance workflows.
---

# Wiki Writing Guidelines

Guidelines for creating and maintaining a well-structured Memory Wiki.

## Overview

This skill provides standards and workflows for building organized, cross-referenced knowledge wikis using Obsidian-compatible markdown files.

## Session Startup - Wiki 初始化检查

每次会话开始时，智能体应执行以下检查：

1. **检查 wiki 文件夹是否存在**
   - 路径：`wiki/` (相对工作目录)
   - 如果不存在，询问用户："需要我帮你创建 wiki 知识库文件夹吗？"

2. **检查 wiki 结构是否完整**
   - 至少应有 `wiki/README.md`
   - 如果没有，主动创建基础结构

3. **加载工作模式**
   - 查阅 `MEMORY.md` 了解用户的 wiki 使用偏好
   - 明确记录模式：**主动询问制**

## 知识捕获工作流 (主动询问制)

**核心原则**：在对话中遇到有价值的技术内容时，**主动询问**用户"这个要记到 wiki 吗？"

### 触发条件

以下情况应主动询问用户是否记录 wiki：

| 场景 | 示例 |
|------|------|
| 系统配置步骤 | "conda 环境配置流程" |
| 故障排查方案 | "解决 xxx 错误的方法" |
| 最佳实践总结 | "推荐的项目结构是..." |
| 工具使用技巧 | "可以这样用 git rebase..." |
| 重要决策记录 | "我们决定采用 xxx 方案因为..." |

### 询问话术

> "刚才我们讨论的 [主题] 很有价值，要记到 wiki 里吗？方便以后查阅。

## When to Use This Skill

Use this skill when:
- **Session startup**: Checking and initializing wiki folder structure
- Creating a new wiki page or knowledge base entry
- Organizing wiki structure and file hierarchy
- Maintaining wiki indexes (__index.md, README.md)
- Establishing wiki conventions for a project or team
- Adding a new page and need to update related indexes
- **Knowledge capture**: Asking user if valuable technical content should be recorded

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