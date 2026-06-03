# Contributing Guidelines

Thank you for your interest in contributing to Python-Learnings! This document provides guidelines for contributing.

## How to Contribute

### 1. Report Issues
- Found an error or outdated information?
- Use GitHub Issues to report
- Include topic, error, and suggestion

### 2. Add New Content
- **Add Topic**: Create markdown file in appropriate folder
- **Add Examples**: Include in `code-examples/`
- **Add Questions**: Add to `interview-questions/`

### 3. Improve Existing Content
- Enhance explanations
- Add code examples
- Fix typos or errors
- Reorganize for clarity

## Contribution Process

1. **Fork** the repository
2. **Create** a feature branch: `git checkout -b feature/topic-name`
3. **Make** your changes
4. **Commit**: `git commit -m "Add: descriptive message"`
5. **Push**: `git push origin feature/topic-name`
6. **Submit** a Pull Request

## Content Guidelines

### Markdown Files
- Use clear headings (H2, H3)
- Include code examples
- Add practical explanations
- Link to related topics

### Code Examples
```python
# Good: Clear, well-commented
def greet(name):
    """Return a greeting message."""
    return f"Hello, {name}!"

# Avoid: Vague or unclear
def g(n):
    return f"Hi, {n}!"
```

### File Naming
- Use kebab-case: `file-name.md`
- Descriptive names: `list-methods.md`
- Topic files: start with number: `01-fundamentals.md`

## Standards

- **Clarity**: Write for beginners and advanced users
- **Accuracy**: Verify all examples work
- **Completeness**: Cover topic thoroughly
- **Organization**: Logical flow and structure
- **References**: Link related topics

## Pull Request Template

```
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix
- [ ] New content
- [ ] Improvement
- [ ] Correction

## Related Issues
Fixes #(issue number)

## Checklist
- [ ] Content is accurate
- [ ] Examples are tested
- [ ] Links are working
- [ ] Formatting is consistent
```

## Questions?

- Open an issue
- Start a discussion
- Check existing documentation

Thank you for contributing! 🙏
