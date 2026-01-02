# Testing Strategy

> **Project:** [Project Name]
> **Created:** [Date]
> **Last Updated:** [Date]

---

## Testing Philosophy

[Describe the overall approach to testing in this project]

---

## Testing Pyramid

```
                    ┌─────────────┐
                    │    E2E      │  ← Few, critical user flows
                    │  (Slowest)  │
                    └──────┬──────┘
                           │
              ┌────────────┴────────────┐
              │      Integration        │  ← Component interactions
              │       (Medium)          │
              └────────────┬────────────┘
                           │
    ┌──────────────────────┴──────────────────────┐
    │                Unit Tests                    │  ← Most tests here
    │                 (Fast)                       │
    └──────────────────────────────────────────────┘
```

| Level | Coverage Target | Focus |
|-------|-----------------|-------|
| Unit | 80%+ | Individual functions, hooks, utilities |
| Integration | Key paths | Component interactions, API mocking |
| E2E | Critical flows | User journeys, cross-browser |

---

## Testing Tools

### Unit & Integration Testing

| Tool | Purpose | Configuration |
|------|---------|---------------|
| [Jest/Vitest] | Test runner | [config file] |
| [React Testing Library] | Component testing | [setup file] |
| [MSW] | API mocking | [handlers location] |

### E2E Testing

| Tool | Purpose | Configuration |
|------|---------|---------------|
| [Playwright/Cypress] | Browser testing | [config file] |
| [Visual regression tool] | Visual testing | [config] |

### Code Quality

| Tool | Purpose |
|------|---------|
| ESLint | Static analysis |
| TypeScript | Type checking |
| [Coverage tool] | Coverage reports |

---

## Test Organization

### Directory Structure

```
[project]/
├── src/
│   └── components/
│       └── ComponentName/
│           ├── ComponentName.tsx
│           ├── ComponentName.test.tsx    ← Unit tests
│           └── index.ts
├── __tests__/
│   └── integration/
│       └── [feature].test.tsx            ← Integration tests
├── e2e/
│   ├── pages/                            ← Page objects
│   │   └── LoginPage.ts
│   ├── fixtures/                         ← Test data
│   └── tests/
│       └── [feature].spec.ts             ← E2E tests
└── test-utils/
    ├── render.tsx                        ← Custom render
    └── mocks/                            ← Mock data
```

### Naming Conventions

| Type | Pattern | Example |
|------|---------|---------|
| Unit test | `[Component].test.tsx` | `Button.test.tsx` |
| Integration | `[feature].integration.test.tsx` | `checkout.integration.test.tsx` |
| E2E | `[feature].spec.ts` | `login.spec.ts` |
| Page objects | `[Page]Page.ts` | `LoginPage.ts` |

---

## Unit Testing Standards

### What to Test

- Pure functions and utilities
- Custom hooks
- Component rendering
- User interactions
- State changes
- Edge cases

### What NOT to Test

- Third-party library internals
- CSS styling (use visual testing)
- Implementation details
- Trivial code (simple getters)

### Test Template

```typescript
import { render, screen, fireEvent } from '@testing-library/react';
import { ComponentName } from './ComponentName';

describe('ComponentName', () => {
  describe('rendering', () => {
    it('renders with default props', () => {
      render(<ComponentName />);
      expect(screen.getByRole('button')).toBeInTheDocument();
    });

    it('renders with custom children', () => {
      render(<ComponentName>Custom Text</ComponentName>);
      expect(screen.getByText('Custom Text')).toBeInTheDocument();
    });
  });

  describe('interactions', () => {
    it('calls onClick when clicked', () => {
      const handleClick = jest.fn();
      render(<ComponentName onClick={handleClick} />);
      fireEvent.click(screen.getByRole('button'));
      expect(handleClick).toHaveBeenCalledTimes(1);
    });
  });

  describe('edge cases', () => {
    it('handles empty state', () => {
      render(<ComponentName items={[]} />);
      expect(screen.getByText('No items')).toBeInTheDocument();
    });
  });
});
```

---

## Integration Testing Standards

### What to Test

- Component compositions
- Context providers
- Router interactions
- API integration (with mocking)
- Form submissions

### API Mocking Setup

```typescript
// mocks/handlers.ts
import { rest } from 'msw';

export const handlers = [
  rest.get('/api/users', (req, res, ctx) => {
    return res(
      ctx.json([
        { id: 1, name: 'User 1' },
        { id: 2, name: 'User 2' },
      ])
    );
  }),

  rest.post('/api/login', async (req, res, ctx) => {
    const { email, password } = await req.json();
    if (email === 'test@example.com') {
      return res(ctx.json({ token: 'fake-token' }));
    }
    return res(ctx.status(401), ctx.json({ error: 'Invalid credentials' }));
  }),
];
```

---

## E2E Testing Standards

### Playwright Configuration

```typescript
// playwright.config.ts
import { defineConfig } from '@playwright/test';

export default defineConfig({
  testDir: './e2e/tests',
  fullyParallel: true,
  retries: process.env.CI ? 2 : 0,
  workers: process.env.CI ? 1 : undefined,
  reporter: 'html',
  use: {
    baseURL: 'http://localhost:3000',
    trace: 'on-first-retry',
    screenshot: 'only-on-failure',
  },
  projects: [
    { name: 'chromium', use: { browserName: 'chromium' } },
    { name: 'firefox', use: { browserName: 'firefox' } },
    { name: 'webkit', use: { browserName: 'webkit' } },
  ],
});
```

### Page Object Template

```typescript
// e2e/pages/LoginPage.ts
import { Page, Locator, expect } from '@playwright/test';

export class LoginPage {
  readonly page: Page;
  readonly emailInput: Locator;
  readonly passwordInput: Locator;
  readonly submitButton: Locator;
  readonly errorMessage: Locator;

  constructor(page: Page) {
    this.page = page;
    this.emailInput = page.getByLabel('Email');
    this.passwordInput = page.getByLabel('Password');
    this.submitButton = page.getByRole('button', { name: 'Sign in' });
    this.errorMessage = page.getByRole('alert');
  }

  async goto() {
    await this.page.goto('/login');
  }

  async login(email: string, password: string) {
    await this.emailInput.fill(email);
    await this.passwordInput.fill(password);
    await this.submitButton.click();
  }

  async expectError(message: string) {
    await expect(this.errorMessage).toContainText(message);
  }

  async expectLoggedIn() {
    await expect(this.page).toHaveURL('/dashboard');
  }
}
```

### E2E Test Template

```typescript
// e2e/tests/login.spec.ts
import { test, expect } from '@playwright/test';
import { LoginPage } from '../pages/LoginPage';

test.describe('Login Flow', () => {
  let loginPage: LoginPage;

  test.beforeEach(async ({ page }) => {
    loginPage = new LoginPage(page);
    await loginPage.goto();
  });

  test('successful login redirects to dashboard', async () => {
    await loginPage.login('test@example.com', 'password123');
    await loginPage.expectLoggedIn();
  });

  test('invalid credentials shows error message', async () => {
    await loginPage.login('wrong@example.com', 'wrongpassword');
    await loginPage.expectError('Invalid credentials');
  });

  test('empty form shows validation errors', async ({ page }) => {
    await loginPage.submitButton.click();
    await expect(page.getByText('Email is required')).toBeVisible();
    await expect(page.getByText('Password is required')).toBeVisible();
  });
});
```

---

## Manual Testing Checklist Template

When automated testing is not available:

```markdown
## Manual Test Checklist: [Feature Name]

**Tester:** [Name]
**Date:** [Date]
**Environment:** [Browser/Device]
**Build:** [Version/Commit]

### Prerequisites
- [ ] [Setup step 1]
- [ ] [Setup step 2]

### Happy Path Tests
| # | Step | Expected Result | Actual Result | Pass/Fail |
|---|------|-----------------|---------------|-----------|
| 1 | [Action] | [Expected] | | [ ] |
| 2 | [Action] | [Expected] | | [ ] |

### Edge Cases
| # | Scenario | Expected Result | Actual Result | Pass/Fail |
|---|----------|-----------------|---------------|-----------|
| 1 | Empty input | [Expected] | | [ ] |
| 2 | Maximum length | [Expected] | | [ ] |

### Error Scenarios
| # | Trigger | Expected Error | Actual Error | Pass/Fail |
|---|---------|----------------|--------------|-----------|
| 1 | [Trigger] | [Expected] | | [ ] |

### Cross-Browser (if applicable)
| Browser | Version | Pass/Fail | Notes |
|---------|---------|-----------|-------|
| Chrome | | | |
| Firefox | | | |
| Safari | | | |
| Edge | | | |

### Console Logs
```
[Paste relevant console output]
```

### Issues Found
- [ ] Issue 1: [Description]
- [ ] Issue 2: [Description]

### Sign-off
- [ ] All tests passed
- [ ] Issues documented
- [ ] Ready for deployment
```

---

## Debug Logging for Manual Testing

When adding debug logs for manual testing:

```typescript
// utils/debug.ts
const DEBUG = process.env.NODE_ENV === 'development';

export const debugLog = {
  info: (component: string, action: string, data?: unknown) => {
    if (DEBUG) {
      console.log(`[${component}] ${action}`, data ?? '');
    }
  },
  warn: (component: string, action: string, data?: unknown) => {
    if (DEBUG) {
      console.warn(`[${component}] WARNING: ${action}`, data ?? '');
    }
  },
  error: (component: string, action: string, error: unknown) => {
    if (DEBUG) {
      console.error(`[${component}] ERROR: ${action}`, error);
    }
  },
  state: (component: string, stateName: string, value: unknown) => {
    if (DEBUG) {
      console.log(`[${component}] State ${stateName}:`, value);
    }
  },
};

// Usage
debugLog.info('UserProfile', 'Fetching user data', { userId: 123 });
debugLog.state('UserProfile', 'userData', userData);
debugLog.error('UserProfile', 'Failed to fetch user', error);
```

---

## CI/CD Integration

### GitHub Actions Workflow

```yaml
# .github/workflows/test.yml
name: Tests

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

jobs:
  unit-tests:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '20'
          cache: 'npm'
      - run: npm ci
      - run: npm run test:unit -- --coverage
      - uses: codecov/codecov-action@v3

  e2e-tests:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '20'
          cache: 'npm'
      - run: npm ci
      - run: npx playwright install --with-deps
      - run: npm run build
      - run: npm run test:e2e
      - uses: actions/upload-artifact@v3
        if: failure()
        with:
          name: playwright-report
          path: playwright-report/
```

---

## Test Coverage Requirements

| Area | Minimum Coverage | Target Coverage |
|------|------------------|-----------------|
| Utilities/Helpers | 90% | 100% |
| Hooks | 85% | 95% |
| Components | 75% | 85% |
| Pages | 70% | 80% |
| Overall | 75% | 85% |

---

## Flaky Test Protocol

When a test is flaky:

1. **Document** the flaky behavior
2. **Investigate** root cause
3. **Fix** or add retry logic
4. **Monitor** for recurrence

```typescript
// Retry pattern for flaky tests
test('flaky test with retry', async ({ page }) => {
  await expect(async () => {
    await page.getByRole('button').click();
    await expect(page.getByText('Success')).toBeVisible();
  }).toPass({ timeout: 10000 });
});
```

---

## Review Checklist

Before merging code:

- [ ] All unit tests pass
- [ ] All integration tests pass
- [ ] E2E tests pass (if applicable)
- [ ] No flaky tests introduced
- [ ] Coverage thresholds met
- [ ] New code has appropriate tests
- [ ] Test descriptions are clear

---

*Last Updated: [Date]*
