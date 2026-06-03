# Repository Structure

Detailed explanation of the Python-Learnings repository organization.

## Main Folders

### 📁 resources/
Contains reference materials and PDFs.

**pdf_sources/**
- Original PDF learning materials
- Used as source for markdown content
- Backup references

**quick_reference/**
- Cheatsheets and quick lookups
- Syntax guides
- Common patterns
- Gotchas and tips

**interview-prep/**
- Interview-specific material
- Common questions by category
- Problem-solving strategies
- Code patterns for interviews

### 📁 topics/
Core learning material organized by complexity.

**Naming Convention**: `NN-topic-name/`
- 01-fundamentals
- 02-data-structures
- 03-oop
- etc.

**Each Topic Contains**:
- `README.md` - Overview and learning path
- Multiple markdown files - Specific concepts
- Examples embedded in text
- Links to related topics

### 📁 code-examples/
Standalone, runnable code examples.

**Organization by Difficulty**:
- `basics/` - Simple, single-concept examples
- `intermediate/` - Multi-concept combinations
- `advanced/` - Complex real-world scenarios
- `problem-solving/` - Algorithm and problem solutions

**Naming**: `example-description.py`

### 📁 interview-questions/
Interview preparation material.

**By Difficulty Level**:
- `beginner-level.md` - Basic concepts
- `intermediate-level.md` - Problem-solving
- `advanced-level.md` - System design, optimization
- `coding-challenges.md` - Algorithmic challenges
- `company-specific.md` - Known company questions

### 📁 projects/
Project ideas and applications.

- Project templates
- Requirements and hints
- Solution references
- Real-world applications

## File Naming Conventions

| Type | Convention | Example |
|------|-----------|---------|
| Topic Folder | `NN-topic-name` | `01-fundamentals` |
| Topic File | `kebab-case.md` | `control-flow.md` |
| Code Files | `kebab-case.py` | `list-methods.py` |
| Main Docs | `CAPS.md` | `README.md` |

## Content Flow

```
Learner Journey:
README.md (Overview)
    ↓
ROADMAP.md (Choose path)
    ↓
topics/0N-topic/README.md (Topic intro)
    ↓
topics/0N-topic/specific-concept.md (Deep dive)
    ↓
code-examples/ (Practice)
    ↓
interview-questions/ (Assessment)
```

## Cross-Linking

Topics should link to:
- **Prerequisites**: "See [Fundamentals](../01-fundamentals/)"
- **Related**: "See also [OOP](../03-oop/)"
- **Next**: "Next topic: [Advanced Topics](../08-advanced-topics/)"
- **Examples**: "[See code examples](../../code-examples/)"

## Search Strategy

To find content:
1. Browse topic folders by number (01, 02, 03)
2. Look in quick_reference for syntax
3. Search by concept in interview_questions
4. Find examples in code_examples
5. Use repository search (Ctrl+F)

## Maintenance Notes

- Update links when renaming files
- Keep examples working and tested
- Review for accuracy quarterly
- Add new topics as needed
- Archive outdated content

---

**Total Organization**: 8 major topics → 40+ subtopics → 100+ code examples
