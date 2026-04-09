# Wiki Examples

This file contains concrete examples of wiki pages, indexes, and organizational patterns.

## Example 1: Section Index (__index.md)

```markdown
# Project Management Wiki

Knowledge base for project management methodologies and practices.

## Topics

### [[agile-methodology|Agile Methodology]]
Scrum, Kanban, and iterative development practices:
- Sprint planning and retrospectives
- User story writing
- Estimation techniques

### [[risk-management|Risk Management]]
Identifying and mitigating project risks:
- Risk assessment frameworks
- Mitigation strategies
- Contingency planning

### [[stakeholder-communication|Stakeholder Communication]]
Managing project communications:
- Status reporting
- Escalation procedures
- Meeting facilitation

---

*Wiki Section: `/wiki/project-management/`*
```

## Example 2: Knowledge Page

```markdown
---
title: Agile Methodology
description: Core principles and practices of Agile software development
date: 2024-01-15
tags: [agile, scrum, kanban, project-management]
sources:
  - "Manifesto for Agile Software Development (2001)"
  - "Schwaber, K. & Sutherland, J. - The Scrum Guide"
---

# Agile Methodology

Agile is an iterative approach to software delivery that builds solutions incrementally from the start of the project, instead of trying to deliver it all at once near the end.

## Core Values

1. **Individuals and interactions** over processes and tools
2. **Working software** over comprehensive documentation
3. **Customer collaboration** over contract negotiation
4. **Responding to change** over following a plan

## Common Frameworks

### Scrum
- Fixed-length iterations (sprints, typically 2 weeks)
- Daily standup meetings
- Sprint planning and retrospectives
- Product backlog prioritization

### Kanban
- Continuous flow of work
- Visual board with work-in-progress limits
- Pull-based system
- Focus on cycle time reduction

## Best Practices

- Keep iterations short and focused
- Maintain a prioritized backlog
- Regular reflection and adaptation
- Close collaboration with stakeholders

## See Also

- [[scrum-guide|Scrum Guide]] - Detailed Scrum practices
- [[user-stories|User Stories]] - Writing effective user stories
- [[estimation-techniques|Estimation Techniques]] - Story points and planning poker
```

## Example 3: Root README.md

```markdown
# Team Knowledge Wiki

Central knowledge base for engineering practices, processes, and guidelines.

## Knowledge Sections

### [[project-management/__index|Project Management]]
Agile methodologies, risk management, and stakeholder communication:
- Scrum, Kanban, and iterative development
- Risk assessment and mitigation
- Status reporting and communication

### [[engineering-practices/__index|Engineering Practices]]
Code quality, testing, and development workflows:
- Code review guidelines
- Testing strategies
- CI/CD best practices

### [[architecture/__index|System Architecture]]
Design patterns, system design, and technical decisions:
- Microservices patterns
- Database design
- API design guidelines

---

## Wiki Writing Guidelines

See [[wiki-writing-guidelines|Wiki Writing Guidelines]] for standards on creating and maintaining this knowledge base.

---

*Wiki Root: `/wiki/`*
*Last Updated: 2024-01-15*
```

## Example 4: Adding a New Page Workflow

**Scenario**: Adding a page about "Retrospective Facilitation" to the Project Management section.

### Step 1: Create the page

File: `wiki/project-management/retrospective-facilitation.md`

```markdown
---
title: Retrospective Facilitation
description: Techniques for effective sprint retrospectives
date: 2024-01-20
tags: [agile, scrum, facilitation, retrospective]
sources:
  - "Derby, E. & Larsen, D. - Agile Retrospectives"
---

# Retrospective Facilitation

Effective retrospective facilitation ensures teams continuously improve by reflecting on their processes.

## The Prime Directive

"Regardless of what we discover, we understand and truly believe that everyone did the best job they could, given what they knew at the time, their skills and abilities, the resources available, and the situation at hand."

## Common Formats

### Start-Stop-Continue
- What should we start doing?
- What should we stop doing?
- What should we continue doing?

### 4Ls
- Liked
- Learned
- Lacked
- Longed for

## See Also

- [[agile-methodology|Agile Methodology]] - Overview of Agile practices
```

### Step 2: Update the section index

Edit `wiki/project-management/__index.md`:

```markdown
### [[retrospective-facilitation|Retrospective Facilitation]]
Techniques for effective sprint retrospectives:
- The Prime Directive
- Retrospective formats
- Action item tracking
```

### Step 3: Cross-link related pages

Edit `wiki/project-management/agile-methodology.md` and add to "See Also":

```markdown
## See Also

- [[scrum-guide|Scrum Guide]] - Detailed Scrum practices
- [[user-stories|User Stories]] - Writing effective user stories
- [[retrospective-facilitation|Retrospective Facilitation]] - Running effective retrospectives
```

## Example 5: Bad vs Good Content

### ❌ Bad: Just listing sources

```markdown
# Machine Learning

Papers to read:
- paper1.pdf
- paper2.pdf
- Attention Is All You Need (Vaswani et al.)
- BERT: Pre-training of Deep Bidirectional Transformers
```

### ✅ Good: Extracted knowledge

```markdown
# Transformer Architecture

The transformer architecture revolutionized natural language processing by replacing recurrent layers with attention mechanisms.

## Key Innovation: Self-Attention

Self-attention allows the model to weigh the importance of different words in a sentence when encoding each word. This enables:
- Parallel processing (unlike sequential RNNs)
- Long-range dependencies
- Contextualized word representations

## Architecture Components

1. **Multi-Head Attention** - Multiple attention heads capture different types of relationships
2. **Position Encoding** - Inject sequence order information (since self-attention is position-invariant)
3. **Feed-Forward Networks** - Process attended representations
4. **Layer Normalization** - Stabilize training

## See Also

- [[attention-mechanisms|Attention Mechanisms]] - Detailed explanation of attention
- [[bert-model|BERT Model]] - Bidirectional encoder representations
```