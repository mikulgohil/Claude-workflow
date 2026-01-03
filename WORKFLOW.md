# AI-Assisted Frontend Development Workflow

> A comprehensive workflow guide for AI (Claude) to follow when assisting with frontend development projects. This document serves as a ruleset to ensure consistent, high-quality, and error-free development.

---

## CRITICAL RULES (NEVER BREAK)

```
╔══════════════════════════════════════════════════════════════════════════════╗
║                                                                              ║
║   🚫 NEVER COMMIT CODE                                                       ║
║                                                                              ║
║   - NEVER run `git commit` under any circumstances                           ║
║   - NEVER run `git push` under any circumstances                             ║
║   - NEVER stage files with `git add` for committing                          ║
║   - If user asks to commit, remind them: "I don't commit code.               ║
║     Please review the changes and commit manually when ready."               ║
║   - User must ALWAYS review and commit code themselves                       ║
║   - This ensures user maintains full control over version history            ║
║                                                                              ║
╚══════════════════════════════════════════════════════════════════════════════╝
```

**Why this matters:**
- User must review all changes before they become permanent
- Prevents accidental commits of incomplete or broken code
- Maintains clean git history under user's control
- Allows user to write meaningful commit messages
- Protects against committing sensitive data accidentally

```
╔══════════════════════════════════════════════════════════════════════════════╗
║                                                                              ║
║   📋 ALWAYS PROVIDE DETAILED TASK SUMMARY                                    ║
║                                                                              ║
║   After completing EVERY task, provide a comprehensive summary including:    ║
║                                                                              ║
║   1. FILES MODIFIED                                                          ║
║      - List every file that was created, modified, or deleted               ║
║      - Include the full file path                                           ║
║      - Note the type of change (created/modified/deleted)                   ║
║                                                                              ║
║   2. CHANGES MADE                                                            ║
║      - Describe each change in detail                                       ║
║      - Explain what was added, removed, or modified                         ║
║      - Include code snippets for significant changes                        ║
║                                                                              ║
║   3. WHY CHANGES WERE MADE                                                   ║
║      - Explain the reasoning behind each change                             ║
║      - Connect changes to the original requirement                          ║
║                                                                              ║
║   4. TESTING STATUS                                                          ║
║      - What was tested                                                       ║
║      - What needs manual testing                                            ║
║      - Any known issues or limitations                                      ║
║                                                                              ║
║   5. NEXT STEPS (if any)                                                     ║
║      - What remains to be done                                              ║
║      - Dependencies or blockers                                             ║
║                                                                              ║
╚══════════════════════════════════════════════════════════════════════════════╝
```

---

## Response & Communication Style

### Response Verbosity Control

```
VERBOSITY MODES:

CONCISE MODE (Default for simple tasks)
- One-word or one-line answers when possible
- No preamble ("Here is...", "I will...")
- No postamble ("Let me know if...", "Hope this helps...")
- Code output without explanation unless asked
- Examples:
  user: "2 + 2"
  assistant: "4"

  user: "what command lists files?"
  assistant: "ls"

DETAILED MODE (For complex explanations)
- Use when user asks "explain", "why", "how does this work"
- Use for architectural decisions
- Use when presenting options
- Include reasoning and trade-offs

AUTO-DETECT:
- Questions → Answer first, THEN offer to take action
- Commands → Execute with minimal commentary
- "Help me with X" → Brief plan, then execute
- "Explain X" → Detailed explanation
```

### Answer First Protocol

**CRITICAL: Always answer the user's question before taking action.**

```
ANSWER FIRST PROTOCOL:

WRONG APPROACH:
user: "How should I approach adding authentication?"
assistant: [immediately starts writing auth code]

CORRECT APPROACH:
user: "How should I approach adding authentication?"
assistant: "I recommend using JWT with refresh tokens because [reasons].
            Here are the steps:
            1. Set up auth middleware
            2. Create login/register endpoints
            3. Add protected route wrapper

            Would you like me to implement this?"

WHEN TO ANSWER FIRST:
□ "How should I..." → Explain approach, then offer to implement
□ "What's the best way to..." → Compare options, then recommend
□ "Can you help me..." → Clarify scope, then proceed
□ "Why is this..." → Explain cause, then offer fix if applicable

WHEN TO ACT IMMEDIATELY:
□ "Fix this bug" → Fix it
□ "Add a button that..." → Add it
□ "Run the tests" → Run them
□ "Create a component for..." → Create it
```

---

## Table of Contents

1. [Response & Communication Style](#response--communication-style)
   - [Response Verbosity Control](#response-verbosity-control)
   - [Answer First Protocol](#answer-first-protocol)
2. [Phase 0: Session Initialization](#phase-0-session-initialization)
   - [CLAUDE.md Setup](#step-04-initialize-claudemd-claude-code-context-file)
   - [Hooks & Automation](#phase-05-hooks--automation-setup)
3. [Phase 1: Project Discovery & Understanding](#phase-1-project-discovery--understanding)
4. [Phase 2: Requirements Gathering](#phase-2-requirements-gathering)
5. [Phase 3: Task Planning & Management](#phase-3-task-planning--management)
6. [Phase 4: Implementation](#phase-4-implementation)
   - [Library & Dependency Verification](#library--dependency-verification)
7. [Phase 5: Testing & Validation](#phase-5-testing--validation)
8. [Phase 6: Documentation](#phase-6-documentation)
9. [Phase 7: Review & Iteration](#phase-7-review--iteration)
10. [Knowledge Management](#knowledge-management)
11. [Context Management](#context-management)
    - [Context Rot Prevention](#context-rot-prevention)
    - [Multi-Worktree Collaboration](#multi-worktree-collaboration)
    - [Session State Management](#session-state-management)
12. [MCP Tools Reference](#mcp-tools-reference)
    - [MCP Integration Workflows](#mcp-integration-workflows)
    - [CLI Flags for Automation](#cli-flags-for-automation)
13. [Recovery & Debugging Protocols](#recovery--debugging-protocols)
14. [Background Process Management](#background-process-management)
15. [Agent Delegation Patterns](#agent-delegation-patterns)
16. [Decision Framework](#decision-framework)
17. [Anti-Patterns & Lessons Learned](#anti-patterns--lessons-learned)

---

## Phase 0: Session Initialization

### First-Time Project Setup

When starting with a new project for the first time, complete these initialization steps:

#### Step 0.1: Project Type Detection
```
DETECT:
- [ ] Is this a new project or existing codebase?
- [ ] What is the primary framework? (React/Vue/Angular/Svelte/Next.js/Nuxt/etc.)
- [ ] Is this a monorepo or single package?
- [ ] What package manager is used? (npm/yarn/pnpm/bun)
- [ ] What is the TypeScript configuration?
```

#### Step 0.2: Initial Questions to Ask User
```
MANDATORY QUESTIONS:
1. "What is the primary purpose of this project?"
2. "Who is the target audience?"
3. "Are there any specific coding standards or style guides to follow?"
4. "What is the deployment target?" (Vercel/AWS/Azure/On-premise/etc.)
5. "Are there any existing design systems or component libraries in use?"
6. "What is your preferred testing strategy?" (TDD/Test-after/Manual)
7. "Are there any accessibility requirements?" (WCAG level)
8. "What browsers/devices must be supported?"
```

#### Step 0.3: Create Project Documentation Structure
```
CREATE in ./docs/ or ./documentation/:
├── PROJECT_OVERVIEW.md      # Project understanding document
├── ARCHITECTURE.md          # Technical architecture decisions
├── COMPONENTS.md            # Component documentation index
├── DECISIONS.md             # Architectural Decision Records (ADR)
├── LESSONS_LEARNED.md       # Failed approaches and anti-patterns
├── TESTING_STRATEGY.md      # Testing approach documentation
└── SETUP.md                 # Development environment setup
```

#### Step 0.4: Initialize CLAUDE.md (Claude Code Context File)

**CRITICAL: CLAUDE.md is automatically loaded by Claude Code for every conversation.**

```
CLAUDE.MD INITIALIZATION:

1. AUTO-GENERATE with /init command
   - Run `/init` in Claude Code CLI
   - Scans entire codebase automatically
   - Detects technologies, structure, dependencies
   - Creates initial CLAUDE.md at project root

2. FILE HIERARCHY (loaded in order)
   ~/.claude/CLAUDE.md          # Global (all projects)
   ./CLAUDE.md                  # Project root (team-shared)
   ./.claude/settings.json      # Project settings (committed)
   ./.claude/settings.local.json # Personal settings (git-ignored)
   ./.claude/local.md           # Personal notes (git-ignored)
   ./subdir/CLAUDE.md           # Subdirectory context (monorepos)

3. WHAT TO INCLUDE
   ✓ Project purpose and goals
   ✓ Technology stack with versions
   ✓ Repository structure overview
   ✓ Code style guidelines
   ✓ Common bash commands (build, test, lint)
   ✓ Testing instructions
   ✓ Branch naming conventions
   ✓ Environment setup requirements
   ✓ Project-specific warnings

4. WHAT TO AVOID
   ✗ Lengthy inline documentation (reference file paths instead)
   ✗ Task-specific instructions (use separate files)
   ✗ Bloated content (affects token usage)

5. RECOMMENDED STRUCTURE FOR LARGE PROJECTS
   agent_docs/
   ├── building_the_project.md
   ├── running_tests.md
   ├── code_conventions.md
   ├── service_architecture.md
   └── database_schema.md

   Then in CLAUDE.md, list these files with brief descriptions
   and instruct Claude to read relevant ones before starting work.
```

**CLAUDE.md Template:**
```markdown
# Project Name

## Overview
Brief description of the project and its purpose.

## Tech Stack
- Framework: Next.js 14
- Language: TypeScript 5.x
- Styling: Tailwind CSS
- State: Zustand
- Testing: Jest + Playwright

## Project Structure
src/
├── components/    # Reusable UI components
├── pages/         # Next.js pages
├── hooks/         # Custom React hooks
├── utils/         # Utility functions
└── types/         # TypeScript definitions

## Commands
- `npm run dev` - Start development server
- `npm run build` - Production build
- `npm run test` - Run unit tests
- `npm run lint` - Run ESLint

## Code Conventions
- Use functional components with hooks
- Prefer named exports
- Use TypeScript strict mode
- Follow ESLint + Prettier configuration

## Important Notes
- [Add project-specific warnings here]
- [Add unexpected behaviors here]

## Related Documentation
- See `agent_docs/` for detailed guides
```

---

## Phase 0.5: Hooks & Automation Setup

### Configure Claude Code Hooks

Hooks automate actions in response to Claude Code events. Configure in `.claude/settings.json`:

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write(*.ts)",
        "hooks": [
          {
            "type": "command",
            "command": "npx prettier --write \"$file\""
          }
        ]
      },
      {
        "matcher": "Write(*.tsx)",
        "hooks": [
          {
            "type": "command",
            "command": "npx eslint --fix \"$file\""
          }
        ]
      },
      {
        "matcher": "Write(*.css)",
        "hooks": [
          {
            "type": "command",
            "command": "npx prettier --write \"$file\""
          }
        ]
      }
    ]
  }
}
```

### Available Hook Events

```
HOOK EVENTS:

1. PreToolUse
   - Runs BEFORE a tool executes
   - Can block or modify the action
   - Use for: validation, confirmation prompts

2. PostToolUse
   - Runs AFTER a tool completes
   - Use for: formatting, linting, notifications

3. UserPromptSubmit
   - Runs when user submits a prompt
   - Use for: input preprocessing, logging

4. SessionStart
   - Runs when Claude Code session begins
   - Use for: environment setup, context loading
```

### Common Hook Patterns

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write(*.py)",
        "hooks": [{ "type": "command", "command": "python -m black \"$file\"" }]
      },
      {
        "matcher": "Write(*.go)",
        "hooks": [{ "type": "command", "command": "gofmt -w \"$file\"" }]
      },
      {
        "matcher": "Write(package.json)",
        "hooks": [{ "type": "command", "command": "npm install" }]
      }
    ],
    "SessionStart": [
      {
        "hooks": [{ "type": "command", "command": "git fetch origin" }]
      }
    ]
  }
}
```

---

## Phase 1: Project Discovery & Understanding

### 1.1 Codebase Analysis

Before any development work, thoroughly understand the project:

```
ANALYZE AND DOCUMENT:

1. PROJECT STRUCTURE
   - Directory organization
   - Entry points
   - Build configuration
   - Environment variables

2. TECHNOLOGY STACK
   - Framework version
   - State management solution
   - Styling approach (CSS Modules/Tailwind/Styled-components/etc.)
   - API integration patterns
   - Authentication method

3. EXISTING PATTERNS
   - Component structure
   - Naming conventions
   - Import/export patterns
   - Error handling approach
   - Logging strategy

4. DEPENDENCIES
   - Key packages and their purposes
   - Outdated or vulnerable packages
   - Dev vs production dependencies
```

### 1.2 Pattern Recognition

Identify and document existing patterns:

```markdown
## Existing Patterns Found

### Component Pattern
- [Describe the component structure used]
- [Props interface conventions]
- [State management within components]

### Styling Pattern
- [CSS approach: Modules/Tailwind/CSS-in-JS]
- [Theme structure]
- [Responsive design approach]

### Data Fetching Pattern
- [API client setup]
- [Caching strategy]
- [Error handling]

### File Naming Convention
- [Component files: PascalCase/kebab-case]
- [Utility files: camelCase]
- [Test files: *.test.ts/*.spec.ts]
```

---

## Phase 2: Requirements Gathering

### 2.1 Understanding the Task

For each new task or feature request:

```
REQUIREMENTS CHECKLIST:
□ What is the user trying to achieve?
□ What is the expected behavior?
□ What are the edge cases?
□ Are there any constraints (performance/accessibility/browser support)?
□ Is there a design/mockup to reference?
□ What data is required?
□ Are there dependencies on other features?
```

### 2.2 Clarification Protocol

**RULE: Never assume. Always ask when unclear.**

```
WHEN TO ASK USER:

1. MULTIPLE APPROACHES EXIST
   "I see two approaches for this:
   Option A: [Description] - Pros: [list] Cons: [list]
   Option B: [Description] - Pros: [list] Cons: [list]
   Which approach do you prefer?"

2. REQUIREMENTS ARE AMBIGUOUS
   "To clarify the requirement:
   - Did you mean [interpretation A] or [interpretation B]?
   - What should happen when [edge case]?"

3. DESIGN DECISIONS NEEDED
   "This requires a design decision:
   - Should this be [option 1] or [option 2]?
   - What is the priority: [performance/readability/flexibility]?"

4. BREAKING CHANGES POSSIBLE
   "This change may affect [components/features].
   Should I proceed with the breaking change or maintain backward compatibility?"
```

### 2.3 Requirements Documentation

Create a requirements document for significant features:

```markdown
## Feature: [Feature Name]

### User Story
As a [user type], I want [goal] so that [benefit].

### Acceptance Criteria
- [ ] Criteria 1
- [ ] Criteria 2
- [ ] Criteria 3

### Technical Requirements
- Performance: [targets]
- Accessibility: [requirements]
- Browser Support: [list]

### Dependencies
- [List dependencies]

### Questions/Clarifications
- [Resolved questions]
- [Pending questions]
```

---

## Phase 3: Task Planning & Management

### 3.1 Task Breakdown

Break down every feature into atomic, trackable tasks:

```
TASK BREAKDOWN RULES:

1. Each task should be completable in a single session
2. Tasks should have clear acceptance criteria
3. Dependencies between tasks must be explicit
4. Estimate complexity (Low/Medium/High)

TASK FORMAT:
- [ ] [Task Name] | Priority: [High/Medium/Low] | Complexity: [L/M/H]
      Dependencies: [list or "none"]
      Acceptance: [criteria]
```

### 3.2 Progress Tracking

Use TODO list for every development session:

```
TODO LIST PROTOCOL:

1. CREATE at session start
2. UPDATE as work progresses
3. MARK completed immediately after finishing
4. ADD discovered tasks during implementation
5. NEVER leave incomplete without documenting state
```

### 3.3 Task Status Flow

```
PENDING → IN_PROGRESS → COMPLETED
              ↓
          BLOCKED → [Document blocker] → Resolve → IN_PROGRESS
              ↓
          FAILED → [Document in LESSONS_LEARNED.md] → Alternative approach
```

---

## Phase 4: Implementation

### 4.1 Pre-Implementation Checklist

Before writing any code:

```
PRE-IMPLEMENTATION CHECKLIST:
□ Understood the requirement completely
□ Identified affected files/components
□ Checked for existing similar implementations
□ Reviewed LESSONS_LEARNED.md for related anti-patterns
□ Planned the implementation approach
□ Identified test scenarios
```

### 4.2 Implementation Guidelines

#### Code Quality Rules

```
IMPLEMENTATION RULES:

1. MINIMAL CHANGES
   - Only modify what's necessary
   - Don't refactor unrelated code
   - Don't add "nice to have" features

2. FOLLOW EXISTING PATTERNS
   - Match the project's code style
   - Use existing utilities/helpers
   - Follow established naming conventions

3. SECURITY FIRST
   - Sanitize user inputs
   - Avoid XSS vulnerabilities
   - Never hardcode secrets
   - Use proper authentication/authorization

4. PERFORMANCE CONSCIOUS
   - Avoid unnecessary re-renders
   - Use proper memoization
   - Lazy load when appropriate
   - Optimize bundle size

5. ACCESSIBILITY (A11Y)
   - Use semantic HTML
   - Include proper ARIA attributes
   - Ensure keyboard navigation
   - Test with screen readers

6. NO COMMENTS UNLESS ASKED
   - Do not add comments to code unless explicitly requested
   - Code should be self-documenting
   - Use descriptive variable/function names instead
```

#### Library & Dependency Verification

**CRITICAL: NEVER assume a library is available, even if it's well-known.**

```
LIBRARY VERIFICATION PROTOCOL:

BEFORE USING ANY LIBRARY:
1. CHECK package.json (or cargo.toml, requirements.txt, etc.)
   - Is the library already a dependency?
   - What version is installed?

2. IF LIBRARY EXISTS:
   ✓ Use it following existing patterns in codebase
   ✓ Check how it's imported in other files
   ✓ Match the existing usage style

3. IF LIBRARY DOESN'T EXIST:
   ⚠️ ASK USER before adding new dependency
   "This feature would benefit from [library].
    Should I add it to the project, or use an alternative approach?"

4. CHECK NEIGHBORING FILES
   - How do similar components handle this?
   - Are there existing utilities that do this?
   - Is there a project-specific wrapper?

VERIFICATION COMMANDS:
# Check if package exists
grep "library-name" package.json

# Check how it's used
grep -r "from 'library-name'" src/

# Check for existing utilities
ls src/utils/ src/helpers/ src/lib/

COMMON MISTAKES TO AVOID:
✗ Assuming lodash is available (check first)
✗ Assuming axios when fetch might be used
✗ Adding moment.js when date-fns is already installed
✗ Using a UI library not in the project
```

#### Component Development Pattern

```
FOR EACH COMPONENT:

1. CREATE component file with proper structure
2. ADD TypeScript interfaces for props
3. IMPLEMENT core functionality
4. ADD error handling
5. INCLUDE loading states
6. ADD debug logging (removable in production)
7. DOCUMENT the component
8. WRITE tests or prepare manual test plan
```

### 4.3 Error Handling Standard

```typescript
// Standard error handling pattern
try {
  // Operation
} catch (error) {
  // 1. Log for debugging
  console.error('[ComponentName] Operation failed:', error);

  // 2. User-friendly error state
  setError('A user-friendly message');

  // 3. Optional: Report to error tracking service
  errorTracker.capture(error);
}
```

### 4.4 Debug Logging Standard

```typescript
// Debug logging pattern (for development)
const DEBUG = process.env.NODE_ENV === 'development';

function debugLog(component: string, action: string, data?: any) {
  if (DEBUG) {
    console.log(`[${component}] ${action}`, data ? JSON.stringify(data, null, 2) : '');
  }
}

// Usage
debugLog('UserProfile', 'Fetching user data', { userId });
debugLog('UserProfile', 'User data received', userData);
```

---

## Phase 5: Testing & Validation

### 5.1 Testing Strategy Decision Tree

```
TESTING DECISION TREE:

IS PLAYWRIGHT AVAILABLE AND CONFIGURED?
├── YES → Use Playwright for E2E testing
│         ├── Create Page Object Model
│         ├── Write test scenarios
│         ├── Run in CI/CD
│         └── Document test coverage
│
└── NO → Use Manual Testing Protocol
          ├── Add comprehensive debug logs
          ├── Create test checklist
          ├── Ask user to test manually
          ├── Request logs for verification
          └── Document test results
```

### 5.2 Development Server Management

**CRITICAL: Always check for running servers before starting a new one.**

```
SERVER MANAGEMENT PROTOCOL:

BEFORE STARTING ANY SERVER:
1. CHECK if server is already running
   - Check common ports: 3000, 3001, 5173, 8080, 4200
   - Use: `lsof -i :[PORT]` or `netstat -an | grep [PORT]`
   - Check for running npm/node processes: `ps aux | grep -E "(node|npm|next|vite)"`

2. IF SERVER IS RUNNING:
   ✓ DO NOT start another server
   ✓ Use the existing server for testing
   ✓ Note: "Server already running on port [PORT], using existing instance"

3. IF SERVER HAS ISSUES (not responding, errors, wrong state):
   ⚠️ ALWAYS INFORM USER FIRST:
   "The development server on port [PORT] is not responding properly.
    I need to kill the current server and start a fresh one.
    Proceeding to restart the server..."

   Then:
   - Kill the problematic server: `kill -9 [PID]` or `npx kill-port [PORT]`
   - Wait 2-3 seconds for port to be released
   - Start fresh server
   - Verify server is healthy before proceeding

4. IF NO SERVER RUNNING:
   - Start the development server
   - Wait for server to be ready (check for "ready" or "compiled" message)
   - Verify by hitting the health endpoint or main page

SERVER CHECK COMMANDS:
```bash
# Check if port is in use
lsof -i :3000

# Find process using port
lsof -t -i :3000

# Kill process on port
kill -9 $(lsof -t -i :3000)
# OR
npx kill-port 3000

# Check running node processes
ps aux | grep node
```

COMMON SERVER START COMMANDS:
- Next.js: `npm run dev` (port 3000)
- Vite: `npm run dev` (port 5173)
- Create React App: `npm start` (port 3000)
- Angular: `ng serve` (port 4200)

HEALTH CHECK PATTERN:
```typescript
// Wait for server to be ready
async function waitForServer(url: string, maxAttempts = 30): Promise<boolean> {
  for (let i = 0; i < maxAttempts; i++) {
    try {
      const response = await fetch(url);
      if (response.ok) return true;
    } catch {
      await new Promise(r => setTimeout(r, 1000));
    }
  }
  return false;
}
```
```

---

### 5.3 Playwright Testing Protocol

When Playwright is available:

```
PLAYWRIGHT TESTING STEPS:

0. SERVER CHECK (MANDATORY FIRST STEP)
   - Run server management protocol above
   - Ensure server is running and healthy
   - Do NOT proceed until server is confirmed ready

1. SETUP
   - Verify playwright.config.ts exists
   - Check test directory structure
   - Identify existing test patterns

2. PAGE OBJECT MODEL
   Create for each page/component:
   ```typescript
   // pages/ComponentPage.ts
   export class ComponentPage {
     constructor(private page: Page) {}

     // Locators
     get submitButton() { return this.page.getByRole('button', { name: 'Submit' }); }

     // Actions
     async performAction() { /* ... */ }

     // Assertions
     async verifyState() { /* ... */ }
   }
   ```

3. TEST STRUCTURE
   ```typescript
   test.describe('Feature Name', () => {
     test('should perform expected behavior', async ({ page }) => {
       // Arrange
       // Act
       // Assert
     });
   });
   ```

4. RUN AND VERIFY
   - Run tests locally first
   - Check for flaky tests
   - Ensure CI passes
```

### 5.4 Manual Testing Protocol

When automated testing isn't available:

```
MANUAL TESTING PROTOCOL:

1. ADD DEBUG LOGS
   - Entry/exit of key functions
   - State changes
   - API calls and responses
   - User interactions

2. CREATE TEST CHECKLIST
   ```markdown
   ## Manual Test Checklist: [Feature Name]

   ### Happy Path
   - [ ] Step 1: [Action] → Expected: [Result]
   - [ ] Step 2: [Action] → Expected: [Result]

   ### Edge Cases
   - [ ] Empty state
   - [ ] Maximum values
   - [ ] Special characters
   - [ ] Slow network

   ### Error Scenarios
   - [ ] Invalid input
   - [ ] Network failure
   - [ ] Unauthorized access
   ```

3. REQUEST USER TESTING
   "Please test the following and share the console logs:
   1. [Test scenario 1]
   2. [Test scenario 2]
   3. [Test scenario 3]

   Copy the browser console output and share with me."

4. VERIFY FROM LOGS
   - Check debug log sequence
   - Verify expected states
   - Identify any errors
   - Confirm feature works
```

---

## Phase 6: Documentation

### 6.1 Component Documentation Standard

Every component must have attached documentation:

```markdown
# ComponentName

## Overview
Brief description of what this component does.

## Props

| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| prop1 | string | Yes | - | Description |
| prop2 | number | No | 0 | Description |

## Usage

```tsx
import { ComponentName } from './ComponentName';

<ComponentName prop1="value" />
```

## States

### Loading
[Description of loading state]

### Error
[Description of error state]

### Empty
[Description of empty state]

## Events

| Event | Payload | Description |
|-------|---------|-------------|
| onClick | void | Triggered when... |

## Accessibility
- Keyboard navigation: [description]
- Screen reader: [description]
- ARIA attributes: [list]

## Testing
- Automated: [Yes/No] - [test file location]
- Manual: [test checklist location]

## Dependencies
- [List internal dependencies]
- [List external dependencies]

## Changelog
| Date | Change | Author |
|------|--------|--------|
| YYYY-MM-DD | Initial implementation | AI |
```

### 6.2 Decision Documentation (ADR)

For significant decisions, create an Architectural Decision Record:

```markdown
# ADR-[NUMBER]: [Title]

## Status
[Proposed | Accepted | Deprecated | Superseded]

## Context
What is the issue that we're seeing that is motivating this decision?

## Options Considered

### Option 1: [Name]
- Pros: [list]
- Cons: [list]

### Option 2: [Name]
- Pros: [list]
- Cons: [list]

## Decision
We will use [chosen option] because [reasoning].

## Consequences

### Positive
- [list]

### Negative
- [list]

### Neutral
- [list]

## Related
- [Links to related ADRs or documentation]
```

---

## Phase 7: Review & Iteration

### 7.1 Self-Review Checklist

Before considering any task complete:

```
SELF-REVIEW CHECKLIST:

CODE QUALITY
□ Follows project coding standards
□ No console.log statements (except debug utility)
□ No commented-out code
□ Proper error handling
□ No hardcoded values that should be configurable

FUNCTIONALITY
□ Meets all acceptance criteria
□ Edge cases handled
□ Error states implemented
□ Loading states implemented

PERFORMANCE
□ No unnecessary re-renders
□ Proper memoization where needed
□ No memory leaks
□ Bundle size considered

ACCESSIBILITY
□ Semantic HTML used
□ ARIA attributes where needed
□ Keyboard navigation works
□ Color contrast sufficient

SECURITY
□ No XSS vulnerabilities
□ Input validation present
□ No sensitive data exposed

DOCUMENTATION
□ Component documentation updated
□ README updated if needed
□ Inline comments for complex logic
□ ADR created for significant decisions
```

### 7.2 Task Completion Summary (MANDATORY)

After completing ANY task, provide this summary:

```markdown
## Task Summary: [Task Name]

### Files Changed
| File | Action | Description |
|------|--------|-------------|
| `src/components/Button.tsx` | Modified | Added loading state prop |
| `src/styles/button.css` | Created | New styles for loading spinner |
| `src/utils/helpers.ts` | Modified | Added formatDate utility |

### Changes Made

#### 1. [Component/Feature Name]
**What:** [Detailed description of the change]
**Why:** [Reason for this change]
**Code:**
```[language]
// Key code snippet showing the change
```

#### 2. [Next Change]
...

### Testing Status
- ✅ [What was tested and passed]
- ⏳ [What needs manual testing]
- ⚠️ [Known issues or limitations]

### Manual Testing Required
Please test the following:
1. [Test scenario 1] → Expected: [result]
2. [Test scenario 2] → Expected: [result]

### Next Steps
- [ ] [Remaining task 1]
- [ ] [Remaining task 2]
- [x] [Completed in this session]

### Notes
[Any additional context, warnings, or important information]
```

**IMPORTANT:** This summary must be provided after EVERY task completion, no exceptions.

---

### 7.3 Iteration Protocol

When changes are requested:

```
ITERATION STEPS:

1. UNDERSTAND the feedback
   - What specifically needs to change?
   - Why is the change needed?
   - Are there new requirements?

2. UPDATE task list
   - Add new tasks
   - Re-prioritize if needed

3. CHECK lessons learned
   - Is this a repeated issue?
   - Update LESSONS_LEARNED.md if applicable

4. IMPLEMENT changes
   - Follow same quality standards
   - Don't rush to fix

5. VERIFY
   - Test changes
   - Ensure no regressions
```

---

## Knowledge Management

### Failed Approaches Tracking

**CRITICAL: Document every failed approach to prevent repetition.**

```markdown
# LESSONS_LEARNED.md

## [Date] - [Feature/Component Name]

### Approach That Failed
[Describe the approach]

### Why It Failed
[Explain the failure reason]

### Error/Issue Encountered
```
[Error message or description]
```

### Better Alternative
[What worked instead]

### Tags
#[framework] #[pattern] #[error-type]

---
```

### Knowledge Base Query Protocol

Before attempting any implementation:

```
KNOWLEDGE CHECK:

1. SEARCH LESSONS_LEARNED.md for related patterns
2. CHECK DECISIONS.md for related decisions
3. REVIEW component documentation for similar components
4. IF similar failure found → Use alternative approach
```

---

## Context Management

### Context Window Optimization

Effective context management is critical for AI-assisted development on large codebases.

```
CONTEXT MANAGEMENT STRATEGIES:

1. TOKEN BUDGET MANAGEMENT
   - Keep CLAUDE.md under 500 lines
   - Use file references instead of inline content
   - Define maximum token budget for context
   - Respect latency when fetching context

2. WRITE-SELECT-COMPRESS-ISOLATE FRAMEWORK
   ┌─────────────────────────────────────────────────┐
   │ WRITE    → Document context at session end      │
   │ SELECT   → Choose only relevant snippets        │
   │ COMPRESS → Summarize verbose documentation      │
   │ ISOLATE  → Separate concerns into dedicated files│
   └─────────────────────────────────────────────────┘

3. FILE REFERENCE PATTERNS
   - Use `@file.ts` to reference specific files in prompts
   - Use `!bash-command` to include command output in prompts
   - Use `--add-dir ../path` for additional context directories

4. SESSION DOCUMENTATION
   At end of each session, document:
   - High-level progress summary
   - Key decisions made
   - Specific dependency versions used
   - Learnings and gotchas discovered
```

### Context Rot Prevention

**Context rot occurs when AI output degrades due to accumulated irrelevant or conflicting context.**

```
SYMPTOMS OF CONTEXT ROT:
- Output degrades with more context
- Code becomes bloated or off-target
- Prompt drift occurs (losing focus on original task)
- Style inconsistencies emerge
- Repeated suggestions of already-rejected approaches

PREVENTION STRATEGIES:

1. REGULAR CONTEXT CLEANUP
   □ Use /clear periodically to reset context
   □ Use /compact to summarize long sessions
   □ Split large tasks into focused sub-sessions
   □ Remove completed tasks from active discussion

2. CONTEXT HEALTH CHECKLIST
   □ Is CLAUDE.md still accurate?
   □ Are referenced files still current?
   □ Has the project structure changed?
   □ Are there conflicting instructions?

3. SESSION SEGMENTATION
   For long tasks, segment into focused sessions:

   Session 1: Research & Planning
   ↓ Document findings, clear context
   Session 2: Core Implementation
   ↓ Document progress, clear context
   Session 3: Testing & Refinement
   ↓ Document results, clear context
   Session 4: Documentation & Cleanup

4. CONTEXT REFRESH PROTOCOL
   When context feels stale:
   a. Run /clear to reset
   b. Re-read CLAUDE.md with /init
   c. Provide fresh, focused context
   d. Resume with clear task definition
```

### Multi-Worktree Collaboration

For parallel development across multiple branches:

```
MULTI-WORKTREE SETUP:

1. CREATE WORKTREE FOR FEATURE BRANCH
   git worktree add ../feature-branch-name feature-branch

2. WORK IN SEPARATE CLAUDE SESSIONS
   # Terminal 1 - Main branch
   cd /project/main && claude

   # Terminal 2 - Feature branch
   cd /project/feature-branch-name && claude

3. CONTEXT ISOLATION
   - Each worktree has its own Claude session
   - Changes don't pollute other sessions
   - Easy A/B comparisons between approaches

4. CLEANUP AFTER MERGE
   git worktree remove ../feature-branch-name
   git branch -d feature-branch

BENEFITS:
✓ Parallel feature development
✓ Isolated contexts per branch
✓ Easy context switching
✓ No git stash juggling
✓ Compare implementations side-by-side
```

### Session State Management

```
SESSION STATE PROTOCOL:

AT SESSION START:
1. Check for existing context files
2. Review previous session notes
3. Load relevant CLAUDE.md
4. Set clear session objectives

DURING SESSION:
1. Track progress in TODO list
2. Document decisions as they're made
3. Note any blockers or questions
4. Keep focused on current objective

AT SESSION END:
1. Summarize what was accomplished
2. Document incomplete work
3. Note next steps clearly
4. Update CLAUDE.md if needed
5. Clear or compact context for next session

RESUMING INTERRUPTED SESSION:
1. Use `claude -c` to continue previous session
2. Or use /status to check current state
3. Review what was in progress
4. Re-establish context before continuing
```

---

## MCP Tools Reference

### When to Use Each Tool

```
MCP TOOL SELECTION:

WEB SEARCH / RESEARCH
├── Perplexity (perplexity_ask)
│   └── Use for: Current best practices, library updates, error solutions
│
└── Context7 (when configured)
    └── Use for: Latest language/framework documentation

FIGMA INTEGRATION
├── show_frameworks → First step: identify target framework
├── get_figma_data → Get design data for implementation
├── process_design_comments → Read designer notes
├── download_design_assets → Export images/icons
└── check_reference → Analyze reference image

BROWSER TESTING (Playwright)
├── browser_navigate → Open page for testing
├── browser_snapshot → Capture page state
├── browser_click → Interact with elements
├── browser_type → Fill form fields
└── browser_take_screenshot → Visual verification

FILE OPERATIONS
├── Read/Glob/Grep → Search and read code
├── Edit → Modify existing files
└── Write → Create new files
```

### Research Protocol

```
RESEARCH BEFORE IMPLEMENTING:

FOR NEW LIBRARY/API:
1. Use Perplexity to search: "[library] best practices [year]"
2. Verify compatibility with project stack
3. Check for known issues
4. Document findings

FOR ERROR RESOLUTION:
1. Search exact error message
2. Look for framework-specific solutions
3. Check for version-specific fixes
4. Try solutions in order of relevance
```

### MCP Integration Workflows

```
MCP WORKFLOW PATTERNS:

1. FIGMA-TO-CODE WORKFLOW
   ┌─────────────────────────────────────────────────────────────┐
   │ show_frameworks      → Select target framework              │
   │         ↓                                                   │
   │ get_figma_data       → Extract design structure             │
   │         ↓                                                   │
   │ download_design_assets → Get images/icons                   │
   │         ↓                                                   │
   │ process_design_comments → Read designer annotations         │
   │         ↓                                                   │
   │ check_reference      → Analyze visual reference             │
   │         ↓                                                   │
   │ Implement components → Write code matching design           │
   └─────────────────────────────────────────────────────────────┘

2. RESEARCH-IMPLEMENT-VALIDATE WORKFLOW
   ┌─────────────────────────────────────────────────────────────┐
   │ perplexity_ask       → Research best practices              │
   │         ↓                                                   │
   │ Read existing code   → Understand current patterns          │
   │         ↓                                                   │
   │ Write/Edit           → Implement changes                    │
   │         ↓                                                   │
   │ browser_navigate     → Open for testing                     │
   │         ↓                                                   │
   │ browser_snapshot     → Verify functionality                 │
   │         ↓                                                   │
   │ browser_take_screenshot → Visual verification               │
   └─────────────────────────────────────────────────────────────┘

3. DEBUGGING WORKFLOW
   ┌─────────────────────────────────────────────────────────────┐
   │ Read error logs      → Understand the issue                 │
   │         ↓                                                   │
   │ perplexity_ask       → Search for solutions                 │
   │         ↓                                                   │
   │ Read relevant files  → Find affected code                   │
   │         ↓                                                   │
   │ Edit                 → Apply fix                            │
   │         ↓                                                   │
   │ browser_snapshot     → Verify fix works                     │
   │         ↓                                                   │
   │ Document in LESSONS_LEARNED.md                              │
   └─────────────────────────────────────────────────────────────┘

4. EXTERNAL SERVICE INTEGRATION (when configured)
   - Google Docs → Pull specifications
   - Jira/Linear → Update tickets with PR links
   - Slack → Send notifications
   - GitHub → Issue/PR management
```

### CLI Flags for Automation

```
CLAUDE CODE CLI FLAGS:

SESSION MANAGEMENT:
  claude -c                    # Continue previous session
  claude -p "prompt"           # Run single prompt, then exit
  claude --resume SESSION_ID   # Resume specific session

OUTPUT CONTROL:
  --output-format json         # JSON output for scripting
  --output-format text         # Plain text output
  --output-format markdown     # Markdown formatted output

CONTEXT CONTROL:
  --add-dir ../path            # Add additional directories
  --model sonnet               # Use specific model
  --allowedTools "Tool1" "Tool2"  # Pre-approve tools

EXAMPLES:

# Pipe input for analysis
cat error.log | claude -p "explain these errors" --output-format json

# Automated code review
claude -p "review this PR for bugs" --allowedTools "Read" "Grep"

# Generate and exit
claude -p "create unit tests for auth module" --output-format text > tests.md
```

---

## Recovery & Debugging Protocols

### Debugging with AI

```
AI-ASSISTED DEBUGGING WORKFLOW:

1. STREAM LOGS FOR MONITORING
   tail -f logs/dev.log | claude -p "notify on new error patterns"

2. TDD DEBUGGING CYCLE
   Step 1: Write failing test that reproduces bug
   Step 2: Ask AI to analyze and fix
   Step 3: Validate with test
   Step 4: Document fix

3. ERROR RESOLUTION PATTERN
   a. Capture full error message + stack trace
   b. Include relevant file contents
   c. Ask: "debug this error: [paste error]"
   d. AI reads code, applies patches, validates

4. STACK TRACE ANALYSIS
   Provide:
   - Full stack trace
   - Relevant source files
   - Recent changes
   Ask for root cause analysis
```

### Session Recovery

```
SESSION RECOVERY PROTOCOL:

AFTER UNEXPECTED INTERRUPTION:
1. Check git status for uncommitted changes
   git status
   git diff

2. Review what was in progress
   - Check TODO list state
   - Review recent file modifications
   - Check for partial implementations

3. Resume or restart session
   Option A: claude -c (continue previous)
   Option B: Start fresh with clear context

4. Re-establish context
   - Summarize what was done
   - State what remains
   - Continue from last known good state

PREVENTING DATA LOSS:
□ Commit frequently (user responsibility)
□ Document progress in session notes
□ Use /compact before complex operations
□ Keep LESSONS_LEARNED.md updated
```

### Error Recovery Patterns

```
COMMON ERROR RECOVERY:

1. BUILD FAILURES
   - Read full error output
   - Check for missing dependencies
   - Verify TypeScript/lint configuration
   - Check for circular dependencies

2. RUNTIME ERRORS
   - Check browser console
   - Review network requests
   - Verify API responses
   - Check state management

3. TEST FAILURES
   - Run single test in isolation
   - Check test setup/teardown
   - Verify mocks and stubs
   - Review async handling

4. DEPLOYMENT FAILURES
   - Check environment variables
   - Verify build output
   - Review deployment logs
   - Check resource limits

ESCALATION PATH:
Try fix → Document attempt → Research solution →
Ask for clarification → Try alternative approach →
Document in LESSONS_LEARNED.md
```

---

## Background Process Management

### Long-Running Tasks

For development servers, build watchers, and other long-running processes:

```
BACKGROUND PROCESS PROTOCOL:

1. STARTING BACKGROUND PROCESSES
   - Use `run_in_background` parameter for long-running commands
   - Do NOT use '&' at end of command (handled automatically)
   - Never use `run_in_background` for 'sleep' (returns immediately)

2. MONITORING BACKGROUND PROCESSES
   - Use BashOutput tool to check process output
   - Check periodically for errors or completion
   - Use filter parameter to find specific log patterns

3. MANAGING MULTIPLE PROCESSES
   - Use /bashes command to list all running shells
   - Track shell IDs for each process
   - Clean up unused processes

4. TERMINATING PROCESSES
   - Use KillBash tool with shell_id
   - Verify termination was successful
   - Check for orphaned child processes
```

### Common Background Tasks

```
BACKGROUND TASK EXAMPLES:

DEV SERVER:
- Start: npm run dev (with run_in_background: true)
- Monitor: BashOutput with shell_id
- Kill: KillBash when done

BUILD WATCHER:
- Start: npm run build:watch
- Monitor: Look for "compiled successfully" or errors
- Restart: Kill and restart on config changes

TEST WATCHER:
- Start: npm run test:watch
- Monitor: Filter for "PASS" or "FAIL"
- Check: Review failing tests in output

LOG MONITORING:
- Start: tail -f logs/app.log
- Filter: BashOutput with regex pattern
- Alert: Check for ERROR or WARN patterns
```

### Process Cleanup Checklist

```
BEFORE ENDING SESSION:
□ List all running background shells (/bashes)
□ Kill unnecessary processes
□ Verify dev servers are stopped
□ Check for orphaned node processes
□ Confirm ports are freed (lsof -i :PORT)
```

---

## Agent Delegation Patterns

### When to Use Sub-Agents

Use the Task tool to spawn specialized agents for complex operations:

```
AGENT DELEGATION DECISION TREE:

IS THE TASK COMPLEX AND MULTI-STEP?
├── YES → Consider agent delegation
│   │
│   ├── CODE REVIEW NEEDED?
│   │   └── Spawn code-reviewer agent after significant code changes
│   │
│   ├── RESEARCH REQUIRED?
│   │   └── Spawn general-purpose agent for codebase exploration
│   │
│   ├── MULTI-FILE SEARCH?
│   │   └── Spawn agent instead of multiple Glob/Grep calls
│   │
│   └── CONFIGURATION TASK?
│       └── Spawn specialized agent (statusline-setup, etc.)
│
└── NO → Handle directly with standard tools
```

### Agent Communication Best Practices

```
AGENT PROMPT GUIDELINES:

1. BE SPECIFIC
   ✗ "Review the code"
   ✓ "Review src/auth/login.ts for security vulnerabilities,
      focusing on input validation and SQL injection risks"

2. DEFINE OUTPUT FORMAT
   ✗ "Check for issues"
   ✓ "Return a JSON object with: {issues: [], suggestions: [],
      severity: 'low'|'medium'|'high'}"

3. SPECIFY SCOPE
   ✗ "Fix the bugs"
   ✓ "Fix the type errors in src/components/*.tsx files only.
      Do not modify test files or configuration."

4. CLARIFY READ vs WRITE
   ✗ "Help with authentication"
   ✓ "Research authentication patterns in codebase.
      Do NOT write any code, only report findings."
```

### Parallel Agent Execution

```
PARALLEL AGENTS:

When tasks are independent, launch multiple agents simultaneously:

EXAMPLE - Full Project Review:
1. Agent 1: Security review of auth modules
2. Agent 2: Performance analysis of data fetching
3. Agent 3: Accessibility audit of UI components

Launch all three in ONE message with multiple Task tool calls.

RESULTS:
- Faster completion
- Independent context for each
- Combine findings in summary
```

---

## Decision Framework

### Option Presentation Format

When multiple valid approaches exist:

```
OPTION PRESENTATION FORMAT:

"I've identified [N] approaches for [task]:

**Option 1: [Name]** (Recommended)
- Description: [Brief explanation]
- Pros: [List benefits]
- Cons: [List drawbacks]
- Effort: [Low/Medium/High]
- Risk: [Low/Medium/High]

**Option 2: [Name]**
- Description: [Brief explanation]
- Pros: [List benefits]
- Cons: [List drawbacks]
- Effort: [Low/Medium/High]
- Risk: [Low/Medium/High]

My recommendation is Option [X] because [reasoning].

Which approach would you like to proceed with?"
```

### Decision Matrix

For complex decisions:

```
| Criteria | Weight | Option 1 | Option 2 | Option 3 |
|----------|--------|----------|----------|----------|
| Performance | 30% | 8 | 6 | 9 |
| Maintainability | 25% | 7 | 9 | 6 |
| Time to Implement | 20% | 9 | 5 | 7 |
| Risk | 15% | 8 | 7 | 5 |
| Future Flexibility | 10% | 6 | 9 | 8 |
| **Weighted Score** | | **7.5** | **7.0** | **7.2** |
```

---

## Anti-Patterns & Lessons Learned

### Common Anti-Patterns to Avoid

```
ANTI-PATTERNS:

0. COMMITTING CODE (CRITICAL)
   ❌ Running git commit, git push, or git add for commits
   ❌ Committing even when user asks (politely decline)
   ✓ Let user review and commit manually
   ✓ Remind user: "Please review changes and commit when ready"

1. ASSUMING INSTEAD OF ASKING
   ❌ Implementing based on assumptions
   ✓ Asking for clarification when unclear

2. OVER-ENGINEERING
   ❌ Adding features "just in case"
   ✓ Implementing exactly what's requested

3. IGNORING EXISTING PATTERNS
   ❌ Introducing new patterns inconsistently
   ✓ Following established project patterns

4. SKIPPING DOCUMENTATION
   ❌ Implementing without documenting
   ✓ Documenting as part of implementation

5. NOT TRACKING FAILURES
   ❌ Repeating failed approaches
   ✓ Recording and learning from failures

6. INCOMPLETE TESTING
   ❌ Only testing happy path
   ✓ Testing edge cases and error scenarios

7. HARDCODING VALUES
   ❌ Magic numbers and strings
   ✓ Configuration and constants

8. IGNORING ACCESSIBILITY
   ❌ Building inaccessible UIs
   ✓ Following WCAG guidelines

9. STARTING DUPLICATE SERVERS
   ❌ Running `npm run dev` without checking existing servers
   ❌ Killing servers without informing user
   ✓ Check if server is already running first
   ✓ Inform user before killing/restarting servers
   ✓ Use existing server instance when available
```

### Recovery Protocols

```
WHEN STUCK:

1. STEP BACK
   - Re-read the requirement
   - Check if approach matches requirement

2. DOCUMENT THE ISSUE
   - What was attempted
   - What went wrong
   - What error occurred

3. SEARCH FOR SOLUTIONS
   - Use Perplexity for research
   - Check existing patterns
   - Review documentation

4. ASK FOR HELP
   - Present the issue clearly
   - Show what was attempted
   - Ask specific questions

5. TRY ALTERNATIVE
   - Don't repeat failed approach
   - Document why switching
```

---

## Session Checklist

### Session Start
```
□ Review previous session state
□ Check pending tasks
□ Review any user feedback
□ Load context from documentation
```

### During Session
```
□ Keep TODO list updated
□ Document decisions made
□ Record any failures/learnings
□ Ask questions when unclear
```

### Session End
```
□ Update all documentation
□ Mark completed tasks
□ Document incomplete work
□ Summarize progress for user
□ List next steps
```

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0.0 | 2025-01-02 | Initial workflow creation |
| 1.1.0 | 2025-01-02 | Added CRITICAL RULES section (never commit), Server management protocol for Playwright testing |
| 1.2.0 | 2025-01-02 | Added mandatory detailed task summary requirement with template |
| 1.3.0 | 2025-01-03 | Added CLAUDE.md setup guide with /init command, Hooks & Automation section, Context Management strategies, Context Rot Prevention, Multi-Worktree Collaboration, Enhanced MCP Integration Workflows, CLI Flags for Automation, Recovery & Debugging Protocols |
| 1.4.0 | 2025-01-03 | Added Response Verbosity Control, Answer First Protocol, Library Verification Rule, Background Process Management, Agent Delegation Patterns |

---

*This workflow is a living document. Update it as new patterns, tools, and learnings emerge.*
