---
name: wiki-writing-guidelines
description: Guidelines for writing and maintaining a Memory Wiki with proper structure, naming conventions, content standards, and cross-linking. Use when creating new wiki pages, organizing knowledge bases, or maintaining wiki indexes. Covers file organization, YAML frontmatter, naming conventions, content principles, and cross-linking workflows.
---

# Wiki Writing Guidelines

Guidelines for creating and maintaining a well-structured Memory Wiki.

## Overview

This skill provides standards and workflows for building organized, cross-referenced knowledge wikis using Obsidian-compatible markdown files.

## Core Concepts

### 归档循环 (The Filing Loop)

**核心原则**：每次 AI 给出的答案都应该被评估是否保存到 wiki，形成复利效应。

传统 AI 使用方式：提问 → 获得答案 → 关闭标签页 → 明天从零开始。没有积累，没有复利。

归档循环改变了这一点：
1. **提问** - 向 AI 询问问题
2. **获得答案** - AI 基于当前知识给出回答
3. **评估保存** - 判断这个答案是否有长期价值
4. **归档回 wiki** - 将答案保存为 wiki 页面
5. **下次提问受益** - 未来的问题能基于更丰富的知识库

> 💡 **复利效应**：每个保存的答案都让知识库变得更丰富，产生指数级增长的价值。

### 三层架构

知识库采用三层架构设计：

```
workspace/
├── raw/                    # 原始材料层
│   ├── articles/          # 文章、网页剪辑
│   ├── papers/            # 论文、PDF
│   ├── transcripts/       # 视频/播客转录
│   └── assets/            # 图片、附件
├── wiki/                   # 编译知识层
│   ├── README.md          # 根入口
│   ├── __memory-wiki-index.md
│   ├── section-name/
│   │   ├── __index.md
│   │   └── *.md
│   └── log.md             # 操作日志（只追加）
└── AGENTS.md              # Schema 控制层
```

#### 各层职责

| 层级 | 文件夹 | 职责 | 修改者 |
|------|--------|------|--------|
| **原始材料层** | `raw/` | 存放原始内容：文章、论文、转录、PDF 等 | 用户添加，AI 只读 |
| **编译知识层** | `wiki/` | AI 生成的结构化知识：摘要、概念解释、连接、索引 | AI 读写 |
| **Schema 控制层** | `AGENTS.md` | 定义 wiki 结构、命名规范、可用操作 | 用户维护 |

#### Schema 文件 (AGENTS.md)

`AGENTS.md` 位于工作区根目录，是 AI 的操作手册。wiki 相关的内容应该添加在其中。

##### 应添加到 AGENTS.md 的内容

如果 AGENTS.md 中没有以下内容，提醒用户添加：

```markdown
### 📚 Wiki 知识库（三层架构）

**结构：**
- `raw/` - 原始材料层（用户添加，AI 只读）
- `wiki/` - 编译知识层（AI 读写）
- `AGENTS.md` - Schema 控制层

**四个标准操作：**
- `/ingest` - 摄取：处理 raw/ 中的新材料
- `/compile` - 编译：整合新知识到 wiki
- `/query` - 查询：研究问题并归档答案
- `/lint` - 检查：健康检查和维护

**归档循环：**
每次给出答案后，主动询问用户："这个答案要保存到 wiki 里吗？"
如果用户同意，保存到 `wiki/outputs/YYYYMMDD-topic.md`

**会话启动时：**
1. 阅读 `wiki/README.md` 和索引
2. 检查 `raw/` 是否有新材料
3. 阅读 `wiki/log.md` 了解最近更新
```

### 四个标准化操作

知识库维护的标准工作流：

```
┌─────────┐    ┌──────────┐    ┌───────┐    ┌──────┐
│ Ingest  │ -> │ Compile  │ -> │ Query │ -> │ Lint │
│ (摄取)   │    │ (编译)    │    │ (查询) │    │ (检查)│
└─────────┘    └──────────┘    └───────┘    └──────┘
```

#### 1. Ingest (摄取)
- 用户添加原始材料到 `raw/`
- AI 读取并创建摘要、概念页面、实体页面
- 建立初始连接

#### 2. Compile (编译)
- AI 构建和更新 wiki 页面
- 维护索引文件
- 将新信息编织进现有结构
- 更新交叉链接

#### 3. Query (查询)
- 用户提出问题
- AI 研究 wiki 内容
- 产生带引用的综合答案
- **关键：将答案归档回 `wiki/outputs/`**

#### 4. Lint (检查)
- 定期健康检查（建议每周一次）
- 发现矛盾、空白、过时信息
- 修复破损链接
- 合并重复概念

## Session Startup - Wiki 初始化检查

每次会话开始时，智能体应执行以下检查：

1. **检查 wiki 文件夹是否存在**
   - 路径：`wiki/` (相对工作目录)
   - 如果不存在，询问用户："需要我帮你创建 wiki 知识库文件夹吗？"

2. **检查 AGENTS.md 是否包含 wiki 规范**
   - 阅读 `AGENTS.md` 查看是否有三层架构和四个标准操作的内容
   - 如果没有，**提醒用户添加**（不要自动创建）：
     > "你的 AGENTS.md 还没有 wiki 三层架构和四个标准操作的说明，要我帮你添加吗？"

3. **检查三层架构是否完整**
   - `raw/` - 原始材料文件夹
   - `wiki/` - 编译知识文件夹
   - `AGENTS.md` - 检查是否有 wiki 相关规范

4. **如果 AGENTS.md 有 wiki 规范，遵循其流程**
   - 通常包括：阅读 wiki/README.md、检查 raw/、查看 log.md
   - 按 AGENTS.md 中定义的操作执行（/ingest, /compile, /query, /lint）

5. **检查 wiki 结构是否完整**
   - 至少应有 `wiki/README.md`
   - 如果没有，主动创建基础结构

6. **加载工作模式**
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
| AI 给出的优质答案 | "根据你的 wiki，答案是..." |

### 询问话术

> "刚才我们讨论的 [主题] 很有价值，要记到 wiki 里吗？方便以后查阅。"

### 归档评估标准

评估 AI 答案是否值得保存：

| 保存条件 | 示例 |
|----------|------|
| 包含新的操作步骤 | 命令序列、配置流程 |
| 解决了复杂问题 | 故障排查的完整方案 |
| 整合了多个来源 | 综合性的技术解释 |
| 包含决策依据 | 为什么选择方案 A 而非 B |
| 可复用的模板/代码 | 配置文件、脚本模板 |

## When to Use This Skill

Use this skill when:
- **Session startup**: Checking and initializing wiki folder structure
- Creating a new wiki page or knowledge base entry
- Organizing wiki structure and file hierarchy
- Maintaining wiki indexes (__index.md, README.md)
- Establishing wiki conventions for a project or team
- Adding a new page and need to update related indexes
- **Knowledge capture**: Asking user if valuable technical content should be recorded
- **Filing loop**: Evaluating whether to save AI answers back to wiki

## File Organization

```
wiki/
├── README.md                    # Root entry - overview of all sections
├── __memory-wiki-index.md       # Global index for Obsidian (auto-generated)
├── log.md                       # Append-only operation log
├── outputs/                     # Query outputs (AI answers archived here)
├── raw/                         # Source material (if not in workspace root)
│   ├── articles/
│   ├── papers/
│   └── transcripts/
└── section-name/                # Knowledge sections
    ├── __index.md               # Section entry - lists all pages
    ├── _index.md                # Detailed category index (optional)
    └── *.md                     # Knowledge pages
```

### Key Files

- **README.md** - Root overview with links to all section indexes
- **__index.md** - Section-level index listing all pages in that section
- **__memory-wiki-index.md** - Obsidian's global graph index (usually auto-generated)
- **log.md** - 只追加的操作日志，记录每次 ingest/compile/query/lint
- **outputs/** - 保存 AI 查询答案，实现归档循环

### 索引文件格式

索引条目应包含：

```markdown
- [[page-name]] - 50字左右摘要 #tag1 #tag2 (3 sources)
```

完整索引示例：

```markdown
# Wiki Index

## 系统配置
- [[conda-env-setup]] - 创建和管理 Python 环境的完整流程 #conda #python (5 sources)
- [[macos-ssh-config]] - 配置 SSH 密钥和远程连接 #ssh #macos (2 sources)

## 故障排查
- [[git-merge-conflict]] - 解决 Git 合并冲突的步骤 #git #troubleshooting (3 sources)
```

### 操作日志格式

`wiki/log.md` 采用只追加格式：

```markdown
# Wiki Operation Log

## 2026-04-10
- [14:32] Ingest: 添加 3 篇文章到 raw/articles/
- [14:35] Compile: 生成 5 个概念页面，更新索引
- [15:10] Query: "如何配置代理？" -> 归档到 outputs/proxy-setup.md
- [15:30] Lint: 修复 2 个破损链接，合并 1 个重复概念
```

## Naming Conventions

- **Section entry**: `__index.md` (distinguished from root README)
- **Knowledge pages**: lowercase English, kebab-case (e.g., `agent-modeling.md`, `getting-started.md`)
- **Source summaries**: `author-year-short-title.md` (e.g., `karpathy-2024-llm-kb.md`)
- **Links**: Use Obsidian format `[[filename]]` (e.g., `[[agent-modeling]]`)
- **Query outputs**: `YYYYMMDD-topic-name.md` in `outputs/` folder

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
last_modified: YYYY-MM-DD  # 可选，用于追踪更新
---
```

### Content Principles

1. **Extract knowledge** - Extract general concepts from sources, don't just list papers or documents
2. **Avoid specific method names** - Write "Bayesian adaptive methods can..." instead of "VariBAD uses..."
3. **Cross-link pages** - Use `[[...]]` to connect related knowledge across pages
4. **Use clear language** - Write for clarity and reusability
5. **Include sources** - 每个知识点标注来源，便于验证和追溯

### Prohibited Practices

- ❌ Listing source filenames directly in README without context
- ❌ Writing only titles and abstracts without extracted knowledge
- ❌ Using specific implementation names as knowledge page titles
- ❌ Orphaned pages (pages not linked from any index)
- ❌ Modifying raw/ folder contents (AI should only read)

## Adding New Pages

When creating a new wiki page, update these indexes:

1. **Section `__index.md`** - Add your page to the relevant category in the appropriate section
2. **Root `README.md`** - Update the Knowledge Sections overview if adding a new major section
3. **`__memory-wiki-index.md`** - Obsidian will auto-update this; for other editors, regenerate the global index
4. **`log.md`** - 记录这次添加操作

### Workflow Example

```
Create new page: wiki/section-name/new-topic.md
    ↓
Update: wiki/section-name/__index.md (add to relevant category)
    ↓
(If new major section) Update: wiki/README.md Knowledge Sections
    ↓
Append: wiki/log.md (记录操作)
    ↓
Commit with clear message
```

## Wiki 初始化工作流

当用户同意创建 wiki 时，按以下步骤初始化：

### 步骤 1: 创建文件夹结构

```bash
workspace/
├── raw/                    # 原始材料层
│   ├── articles/
│   ├── papers/
│   ├── transcripts/
│   └── assets/
├── wiki/                   # 编译知识层
│   ├── README.md
│   ├── __memory-wiki-index.md
│   ├── log.md
│   ├── outputs/
│   └── section-name/
│       └── __index.md
└── AGENTS.md              # Schema 控制层（已有文件，需添加 wiki 规范）
```

### 步骤 2: 检查并更新 AGENTS.md

**不要创建新的 AGENTS.md**，而是检查现有的 `AGENTS.md` 是否包含 wiki 规范。

如果 AGENTS.md 中**没有**以下内容，**提醒用户添加**：

> "你的 AGENTS.md 还没有 wiki 三层架构和四个标准操作的说明。建议添加以下内容："

```markdown
### 📚 Wiki 知识库（三层架构）

**结构：**
- `raw/` - 原始材料层（用户添加，AI 只读）
- `wiki/` - 编译知识层（AI 读写）

**四个标准操作：**
- `/ingest` - 摄取：处理 raw/ 中的新材料
- `/compile` - 编译：整合新知识到 wiki
- `/query` - 查询：研究问题并归档答案
- `/lint` - 检查：健康检查和维护

**归档循环：**
每次给出答案后，主动询问用户："这个答案要保存到 wiki 里吗？"

**会话启动时：**
1. 阅读 `wiki/README.md` 和索引
2. 检查 `raw/` 是否有新材料
3. 阅读 `wiki/log.md` 了解最近更新
```

如果用户同意，将上述内容追加到 AGENTS.md 的合适位置。

### 步骤 3: 创建 wiki/README.md

```markdown
# Wiki 名称

---
title: Wiki 名称
description: 个人知识库，记录...
date: YYYY-MM-DD
tags: [wiki, knowledge-base]
---

## 简介

这是一个使用 Obsidian 兼容格式维护的个人知识库。

## 知识板块

| 板块 | 描述 |
|------|------|
| [[section-name/__index\|板块名称]] | 描述内容 |

## 使用方式

- 将原始材料放入 `raw/` 文件夹
- AI 会定期编译到 `wiki/` 文件夹
- 查询答案会归档到 `wiki/outputs/`
```

### 步骤 4: 创建 log.md

```markdown
# Wiki Operation Log

## YYYY-MM-DD
- [HH:MM] Init: 初始化 wiki 结构
```

### 步骤 5: 告知用户

> wiki 初始化完成！结构如下：
> - `raw/` - 存放你的原始材料（文章、笔记等）
> - `wiki/` - AI 编译的结构化知识
>
> 使用方式：把想保存的内容放到 raw/，然后告诉我"/ingest"来处理。
>
> **注意**：如果 AGENTS.md 还没有 wiki 相关规范，建议添加（见步骤2）。

## Linking Best Practices

- Use `[[page-name]]` for internal wiki links
- Use `[[page-name|Display Text]]` for custom display text
- Cross-link related concepts to build a knowledge graph
- Include "See also" sections at the end of pages for related topics
- Use tags in frontmatter for semantic grouping

## Tools and Plugins

### Obsidian 推荐插件

#### 必备插件

**Dataview** - 把 vault 当数据库查询
- 自动读取所有 YAML frontmatter
- 支持嵌入式实时查询
- 示例：创建所有概念文章的动态表格

```markdown
```dataview
TABLE description, date, sources
FROM "wiki"
WHERE contains(tags, "concept")
SORT date DESC
```
```

**Templater** - 自动填充模板变量
- 自动填充日期、文件名
- 创建新笔记时应用标准模板

**Obsidian Git** - 自动版本控制
- 配置自动提交（建议每 30 分钟）
- 自动推送到远程仓库
- 所有变更可追溯、可回滚

#### 辅助插件

**Tag Wrangler** - 批量管理标签
- 重命名、合并标签
- 当标签体系增长后非常实用

**Linter** - 自动格式化
- 保存时自动格式化
- 强制一致的 YAML frontmatter 格式

**Homepage** - 设置首页仪表板
- 显示最近活动、统计数据
- 用 Dataview 查询构建动态内容

**Obsidian Web Clipper** - 浏览器剪辑
- 一键保存网页为 markdown
- 自动保存到 `raw/articles/`

**Local Images Plus** - 离线图片
- 下载引用的图片到本地
- 设置下载文件夹为 `raw/assets/`

### 其他工具

**MarkItDown** (Microsoft) - 转换 PDF/Word 为 markdown
```bash
pip install markitdown
markitdown document.pdf > raw/papers/document.md
```

## Quality Maintenance

### 定期健康检查 (Lint)

建议每周运行一次：

1. **检查破损链接** - 使用 `markdown-link-check` 或手动检查
2. **合并重复概念** - 同一概念的不同命名
3. **更新过时信息** - 标记或更新过期内容
4. **检查孤立页面** - 未被索引或链接的页面
5. **验证来源** - 确保知识点都有来源标注

### 两模型验证（高风险内容）

对于医疗、法律、投资等高风险知识：
- 用一个 AI 编写 wiki 页面
- 用另一个 AI（不同模型）独立验证
- 两者一致才进入"正式" wiki
- 防止幻觉累积

## Examples

For concrete examples of wiki pages, indexes, and organizational patterns, see [references/examples.md](references/examples.md). This includes:

- Complete section index (__index.md) examples
- Knowledge page examples with proper frontmatter
- Root README.md structure examples
- Step-by-step workflow for adding new pages
- Bad vs good content comparisons
- Sample AGENTS.md schema file
- Lint workflow examples
