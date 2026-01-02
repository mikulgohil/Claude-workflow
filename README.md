# AI-Assisted Frontend Development Workflow

A comprehensive workflow and ruleset for AI (Claude) to follow when assisting with frontend development projects.

## Purpose

This workflow ensures:
- Consistent, high-quality development practices
- Proper understanding of projects before making changes
- Clear communication and decision-making
- Documentation of lessons learned to prevent repeated mistakes
- Proper testing strategies (automated or manual)
- Complete component documentation

## Files

### Main Workflow
- **`WORKFLOW.md`** - The main workflow document that AI should follow

### Templates (in `/templates`)
- **`PROJECT_OVERVIEW.template.md`** - Template for documenting project understanding
- **`COMPONENT_DOC.template.md`** - Template for component documentation
- **`ADR.template.md`** - Architectural Decision Record template
- **`LESSONS_LEARNED.template.md`** - Template for tracking failed approaches
- **`TESTING_STRATEGY.template.md`** - Template for testing approach documentation
- **`MANUAL_TEST_CHECKLIST.template.md`** - Template for manual testing

## How to Use

### For New Projects

1. Copy this workflow folder to your project or reference it globally
2. AI will ask initial setup questions (Phase 0)
3. AI will analyze and document project structure (Phase 1)
4. Create project-specific docs using templates in `./docs/`

### During Development

1. AI follows phases 2-7 for each task
2. Lessons learned are recorded in `LESSONS_LEARNED.md`
3. Decisions are documented in `DECISIONS.md` (using ADR template)
4. Components are documented using the component template

### Key Principles

1. **Never assume** - Always ask when unclear
2. **Document everything** - Especially failures
3. **Follow existing patterns** - Match project conventions
4. **Test appropriately** - Playwright if available, manual if not
5. **Track progress** - Use TODO lists consistently

## Quick Reference

### When AI Should Ask Questions

- Multiple valid approaches exist
- Requirements are ambiguous
- Design decisions needed
- Breaking changes possible

### MCP Tools

| Tool | When to Use |
|------|-------------|
| Perplexity | Web search, latest practices |
| Context7 | Language/framework docs |
| Playwright | E2E browser testing |
| Figma | Design-to-code |

### Testing Decision Tree

```
Playwright available?
├── YES → Use Playwright E2E
└── NO → Manual testing + debug logs
```

## Version

**Current Version:** 1.0.0

## Contributing

Update `WORKFLOW.md` as new patterns and learnings emerge.
