# Manual Test Checklist: [Feature/Component Name]

> **Version:** [Version/Build]
> **Tester:** [Name]
> **Date:** [Date]
> **Environment:** [Browser/OS/Device]

---

## Pre-Test Setup

### Environment
- [ ] Clear browser cache and cookies
- [ ] Use correct environment: [Development/Staging/Production]
- [ ] Open browser console (F12)
- [ ] Enable "Preserve log" in console

### Test Data
- [ ] [Required test data setup]
- [ ] [User accounts if needed]
- [ ] [Any required state setup]

---

## Test Scenarios

### Scenario 1: [Primary Happy Path]

**Objective:** [What this test verifies]

| Step | Action | Expected Result | Actual Result | Status |
|------|--------|-----------------|---------------|--------|
| 1 | Navigate to [URL/page] | Page loads successfully | | [ ] Pass [ ] Fail |
| 2 | [Action description] | [Expected behavior] | | [ ] Pass [ ] Fail |
| 3 | [Action description] | [Expected behavior] | | [ ] Pass [ ] Fail |
| 4 | [Action description] | [Expected behavior] | | [ ] Pass [ ] Fail |

**Console Logs:**
```
[Paste relevant console output here]
```

**Notes:**
[Any observations]

---

### Scenario 2: [Secondary Path / Alternative Flow]

**Objective:** [What this test verifies]

| Step | Action | Expected Result | Actual Result | Status |
|------|--------|-----------------|---------------|--------|
| 1 | [Action description] | [Expected behavior] | | [ ] Pass [ ] Fail |
| 2 | [Action description] | [Expected behavior] | | [ ] Pass [ ] Fail |

**Console Logs:**
```
[Paste relevant console output here]
```

---

### Scenario 3: [Error Handling]

**Objective:** Verify error states are handled correctly

| Step | Action | Expected Result | Actual Result | Status |
|------|--------|-----------------|---------------|--------|
| 1 | [Trigger error condition] | [Error message displayed] | | [ ] Pass [ ] Fail |
| 2 | [Invalid input] | [Validation message] | | [ ] Pass [ ] Fail |
| 3 | [Network failure simulation] | [Graceful degradation] | | [ ] Pass [ ] Fail |

**Console Logs:**
```
[Paste relevant console output here]
```

---

## Edge Cases

| # | Scenario | Expected Behavior | Actual Result | Status |
|---|----------|-------------------|---------------|--------|
| 1 | Empty state (no data) | [Expected] | | [ ] Pass [ ] Fail |
| 2 | Maximum length input | [Expected] | | [ ] Pass [ ] Fail |
| 3 | Special characters | [Expected] | | [ ] Pass [ ] Fail |
| 4 | Rapid repeated clicks | [Expected] | | [ ] Pass [ ] Fail |
| 5 | Page refresh during operation | [Expected] | | [ ] Pass [ ] Fail |
| 6 | Back button behavior | [Expected] | | [ ] Pass [ ] Fail |

---

## Accessibility Checks

| # | Check | Requirement | Result | Status |
|---|-------|-------------|--------|--------|
| 1 | Keyboard navigation | Tab through all interactive elements | | [ ] Pass [ ] Fail |
| 2 | Focus visibility | Focus indicator visible | | [ ] Pass [ ] Fail |
| 3 | Screen reader | [Test with VoiceOver/NVDA] | | [ ] Pass [ ] Fail |
| 4 | Color contrast | Meets WCAG AA | | [ ] Pass [ ] Fail |

---

## Responsive Design

| Device/Viewport | Expected | Actual Result | Status |
|-----------------|----------|---------------|--------|
| Mobile (375px) | [Expected layout] | | [ ] Pass [ ] Fail |
| Tablet (768px) | [Expected layout] | | [ ] Pass [ ] Fail |
| Desktop (1024px) | [Expected layout] | | [ ] Pass [ ] Fail |
| Large (1440px+) | [Expected layout] | | [ ] Pass [ ] Fail |

---

## Cross-Browser Testing

| Browser | Version | OS | Status | Notes |
|---------|---------|-----|--------|-------|
| Chrome | Latest | [OS] | [ ] Pass [ ] Fail | |
| Firefox | Latest | [OS] | [ ] Pass [ ] Fail | |
| Safari | Latest | macOS | [ ] Pass [ ] Fail | |
| Edge | Latest | [OS] | [ ] Pass [ ] Fail | |
| Mobile Safari | Latest | iOS | [ ] Pass [ ] Fail | |
| Chrome Mobile | Latest | Android | [ ] Pass [ ] Fail | |

---

## Performance Observations

| Metric | Acceptable | Observed | Status |
|--------|------------|----------|--------|
| Initial load time | <3s | | [ ] Pass [ ] Fail |
| Interaction response | <100ms | | [ ] Pass [ ] Fail |
| No jank/stuttering | Yes | | [ ] Pass [ ] Fail |
| Memory leaks | None | | [ ] Pass [ ] Fail |

---

## Network Conditions

| Condition | Behavior | Status |
|-----------|----------|--------|
| Slow 3G | [Expected - loading states, etc.] | [ ] Pass [ ] Fail |
| Offline | [Expected - offline message, cached data] | [ ] Pass [ ] Fail |
| Reconnection | [Expected - resync, retry] | [ ] Pass [ ] Fail |

---

## Issues Found

### Issue 1
- **Severity:** [Critical/High/Medium/Low]
- **Description:** [Detailed description]
- **Steps to Reproduce:**
  1. [Step 1]
  2. [Step 2]
- **Expected:** [What should happen]
- **Actual:** [What actually happened]
- **Screenshot/Video:** [Link if available]
- **Console Error:**
```
[Error message]
```

### Issue 2
[Same format as above]

---

## Full Console Log

```
[Paste complete console log from the testing session]
```

---

## Summary

| Category | Passed | Failed | Blocked |
|----------|--------|--------|---------|
| Happy Path | /  | /  | /  |
| Error Handling | /  | /  | /  |
| Edge Cases | /  | /  | /  |
| Accessibility | /  | /  | /  |
| Responsive | /  | /  | /  |
| Cross-browser | /  | /  | /  |
| **Total** | **/** | **/** | **/** |

---

## Sign-off

- [ ] All critical tests passed
- [ ] All issues documented
- [ ] Screenshots captured for failures
- [ ] Console logs collected

**Tester Sign-off:** _________________ Date: _________

**Developer Review:** _________________ Date: _________

---

## Attachments

- [ ] Screenshots
- [ ] Screen recordings
- [ ] Console logs
- [ ] Network HAR file

---

*Template Version: 1.0*
