<div align="center">

```
   _   ___   ___       _  __  _____  _    ______   __
  /_\ |_ _| |   \__ __| |/ / | __\ \/ /  / ___\ \ / /
 / _ \ | |  | |) / _` | ' <  | _| >  <  | |    \ V /
/_/ \_\___| |___/\__,_|_|\_\ |___/_/\_\ |_|     |_|

         AI-Assisted Frontend Development Workflow
```

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)
[![Markdown](https://img.shields.io/badge/Made%20with-Markdown-1f425f.svg)](https://www.markdownguide.org/)
[![Claude Code](https://img.shields.io/badge/Claude-Code-blueviolet)](https://claude.ai)

**A comprehensive, battle-tested workflow framework for AI assistants (Claude, GPT, etc.) to follow when helping with frontend development projects.**

[Getting Started](#quick-start) · [Workflow Phases](#the-8-phase-workflow) · [Templates](#templates) · [Author](#author)

</div>

---

## Why Use This Workflow?

Building software with AI assistance is powerful, but without structure it can lead to:
- Inconsistent code patterns
- Undocumented decisions
- Repeated mistakes
- Poor testing coverage
- Incomplete implementations

**This workflow solves these problems** by providing a structured, phase-based approach that AI assistants follow, ensuring every task is properly planned, implemented, tested, and documented.

## Key Features

- **8-Phase Development Cycle** - From project discovery to review
- **Never Commits Code** - AI never runs git commit; you maintain full control
- **Lessons Learned Tracking** - Failed approaches are documented to prevent repetition
- **Testing Strategy** - Supports both Playwright automation and manual testing
- **Component Documentation** - Every component gets proper documentation
- **Decision Records (ADR)** - Significant decisions are tracked with context

## Project Structure

```
workflow/
├── .github/
│   ├── workflows/
│   │   └── validate-markdown.yml   # CI for markdown linting
│   └── mlc_config.json             # Markdown link checker config
├── templates/                       # Documentation templates
│   ├── PROJECT_OVERVIEW.template.md
│   ├── COMPONENT_DOC.template.md
│   ├── ADR.template.md
│   ├── LESSONS_LEARNED.template.md
│   ├── TESTING_STRATEGY.template.md
│   └── MANUAL_TEST_CHECKLIST.template.md
├── .gitignore                       # Git ignore rules
├── LICENSE                          # MIT License
├── README.md                        # This file
└── WORKFLOW.md                      # Main workflow document (AI follows this)
```

## Quick Start

### Option 1: Copy to Your Project (Recommended)

```bash
# Clone or download this repo
git clone https://github.com/yourusername/workflow.git

# Copy to your project
cp -r workflow/ your-project/
```

### Option 2: Reference Globally

Point your AI assistant to this workflow at the start of each session.

## The 8-Phase Workflow

| Phase | Name | Description |
|-------|------|-------------|
| 0 | **Session Initialization** | Project detection, initial questions, setup |
| 1 | **Project Discovery** | Analyze codebase, identify patterns |
| 2 | **Requirements Gathering** | Understand task, clarify ambiguities |
| 3 | **Task Planning** | Break down into atomic tasks, track progress |
| 4 | **Implementation** | Write code following existing patterns |
| 5 | **Testing & Validation** | Playwright or manual testing |
| 6 | **Documentation** | Component docs, ADRs, updates |
| 7 | **Review & Iteration** | Self-review, task summary, next steps |

## Templates

The `/templates` folder contains ready-to-use documentation templates:

| Template | Purpose |
|----------|---------|
| `PROJECT_OVERVIEW.template.md` | Document project understanding and architecture |
| `COMPONENT_DOC.template.md` | Standardized component documentation |
| `ADR.template.md` | Architectural Decision Records |
| `LESSONS_LEARNED.template.md` | Track failed approaches and anti-patterns |
| `TESTING_STRATEGY.template.md` | Define testing approach for the project |
| `MANUAL_TEST_CHECKLIST.template.md` | Checklists for manual testing |

<!--
NOTE FOR USERS: The /templates folder is INCLUDED in this solution intentionally.
These templates are essential for the workflow to function properly. The AI uses
these templates to create documentation in your project's ./docs/ folder.

You should NOT need to modify these templates unless you want to customize the
documentation format for your organization. If you do customize, consider keeping
backups of the originals.
-->

## Core Principles

### 1. AI Never Commits Code
```
The AI will NEVER run git commit, git push, or git add for commits.
You always review changes and commit manually, maintaining full control
over your version history.
```

### 2. Ask, Don't Assume
When requirements are unclear, the AI asks questions instead of guessing.

### 3. Document Everything
Every decision, failure, and learning is documented for future reference.

### 4. Follow Existing Patterns
The AI matches your project's existing code style and patterns.

### 5. Test Appropriately
Uses Playwright when available, falls back to manual testing with detailed checklists.

## MCP Tools Integration

The workflow supports these MCP (Model Context Protocol) tools:

| Tool | When to Use |
|------|-------------|
| **Perplexity** | Web search, latest practices, error solutions |
| **Playwright** | E2E browser testing and automation |
| **Figma** | Design-to-code implementation |
| **Context7** | Language/framework documentation |

## Example Task Summary

After every task, the AI provides a detailed summary:

```markdown
## Task Summary: Add User Profile Component

### Files Changed
| File | Action | Description |
|------|--------|-------------|
| `src/components/UserProfile.tsx` | Created | New profile component |
| `src/styles/profile.css` | Created | Profile styling |

### Testing Status
- ✅ Component renders correctly
- ⏳ Needs manual testing for accessibility

### Next Steps
- [ ] Add unit tests
- [ ] Integrate with API
```

## Contributing

1. Fork this repository
2. Make your changes to `WORKFLOW.md`
3. Submit a pull request with a clear description

## Version

**Current Version:** 1.2.0

| Version | Changes |
|---------|---------|
| 1.2.0 | Added mandatory detailed task summary requirement |
| 1.1.0 | Added critical rules, server management protocol |
| 1.0.0 | Initial workflow creation |

## Author

<div align="center">

**Mikul Gohil**

Senior Frontend Engineer · Dubai · 15+ Years Experience

[![Website](https://img.shields.io/badge/Website-mikul.in-0A66C2?style=for-the-badge&logo=google-chrome&logoColor=white)](https://www.mikul.in)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/mikulg)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/mikulg)
[![Forem](https://img.shields.io/badge/Forem-Community-5A67D8?style=for-the-badge&logo=forem&logoColor=white)](https://forem.com/mikulg)

</div>

**Expertise:** React.js · Next.js · TypeScript · Tailwind CSS · Sitecore XM Cloud

**Focus Areas:** Agentic AI workflows, Claude Code automation, and no-code web applications

## License

MIT License - feel free to use, modify, and distribute.

---

**Created by [Mikul Gohil](https://www.mikul.in) — Made with AI assistance, reviewed by humans.**
