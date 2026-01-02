# [ComponentName]

> **Location:** `src/components/[path]/[ComponentName].tsx`
> **Created:** [Date]
> **Last Updated:** [Date]
> **Status:** [Draft | In Development | Complete | Deprecated]

---

## Overview

[Brief description of what this component does and when to use it]

---

## Visual Reference

<!-- Include screenshot or Figma link if available -->
![Component Screenshot](./screenshots/[component-name].png)

**Figma Design:** [Link if available]

---

## Props

| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `children` | `ReactNode` | No | - | Content to render inside |
| `variant` | `'primary' \| 'secondary'` | No | `'primary'` | Visual variant |
| `disabled` | `boolean` | No | `false` | Disables interaction |
| `onClick` | `() => void` | No | - | Click handler |

### Props Interface

```typescript
interface [ComponentName]Props {
  children?: React.ReactNode;
  variant?: 'primary' | 'secondary';
  disabled?: boolean;
  onClick?: () => void;
  className?: string;
}
```

---

## Usage Examples

### Basic Usage

```tsx
import { [ComponentName] } from '@/components/[path]/[ComponentName]';

function Example() {
  return (
    <[ComponentName]>
      Basic content
    </[ComponentName]>
  );
}
```

### With All Props

```tsx
<[ComponentName]
  variant="secondary"
  disabled={isLoading}
  onClick={handleClick}
  className="custom-class"
>
  Full example
</[ComponentName]>
```

### Common Patterns

```tsx
// Pattern 1: [Description]
<[ComponentName] variant="primary">
  Pattern 1 content
</[ComponentName]>

// Pattern 2: [Description]
<[ComponentName] variant="secondary">
  Pattern 2 content
</[ComponentName]>
```

---

## States

### Default State
[Description of default appearance/behavior]

### Loading State
```tsx
<[ComponentName] isLoading>
  Loading content...
</[ComponentName]>
```

### Error State
```tsx
<[ComponentName] error="Error message">
  Error content
</[ComponentName]>
```

### Empty State
```tsx
<[ComponentName] isEmpty>
  No data available
</[ComponentName]>
```

### Disabled State
```tsx
<[ComponentName] disabled>
  Disabled content
</[ComponentName]>
```

---

## Events

| Event | Payload | Description |
|-------|---------|-------------|
| `onClick` | `void` | Triggered when component is clicked |
| `onChange` | `(value: T) => void` | Triggered when value changes |
| `onError` | `(error: Error) => void` | Triggered on error |

---

## Styling

### CSS Classes

| Class | Description |
|-------|-------------|
| `.component-base` | Base styles |
| `.component-primary` | Primary variant |
| `.component-secondary` | Secondary variant |

### Customization

```tsx
// Using className prop
<[ComponentName] className="my-custom-styles">
  Custom styled content
</[ComponentName]>

// Using Tailwind (if applicable)
<[ComponentName] className="bg-blue-500 hover:bg-blue-600">
  Tailwind styled
</[ComponentName]>
```

### Theme Integration

[Description of how component integrates with theme system]

---

## Accessibility

### Keyboard Navigation

| Key | Action |
|-----|--------|
| `Tab` | Focus component |
| `Enter` | Activate component |
| `Space` | Activate component |
| `Escape` | Close/dismiss |

### ARIA Attributes

```tsx
<[ComponentName]
  aria-label="Descriptive label"
  aria-describedby="description-id"
  role="button"
/>
```

### Screen Reader Support
- [Announce state changes]
- [Read label and description]
- [Provide context for actions]

### WCAG Compliance
- [x] Color contrast: AA compliant
- [x] Focus indicators visible
- [x] Interactive elements focusable
- [x] Labels provided for form elements

---

## Testing

### Automated Tests

**Location:** `__tests__/[ComponentName].test.tsx`

```typescript
describe('[ComponentName]', () => {
  it('renders correctly', () => {
    render(<[ComponentName]>Test</[ComponentName]>);
    expect(screen.getByText('Test')).toBeInTheDocument();
  });

  it('handles click events', () => {
    const handleClick = jest.fn();
    render(<[ComponentName] onClick={handleClick}>Click me</[ComponentName]>);
    fireEvent.click(screen.getByText('Click me'));
    expect(handleClick).toHaveBeenCalled();
  });
});
```

### Manual Test Checklist

- [ ] Component renders correctly in all variants
- [ ] Keyboard navigation works
- [ ] Click/interaction works as expected
- [ ] Loading state displays correctly
- [ ] Error state displays correctly
- [ ] Responsive on all breakpoints
- [ ] Works in dark/light mode (if applicable)

### E2E Tests (Playwright)

**Location:** `e2e/[component-name].spec.ts`

```typescript
test('[ComponentName] functionality', async ({ page }) => {
  await page.goto('/page-with-component');
  const component = page.getByTestId('[component-name]');
  await expect(component).toBeVisible();
  await component.click();
  // Assert expected behavior
});
```

---

## Dependencies

### Internal Dependencies
- `@/components/[Dependency1]` - [Why needed]
- `@/hooks/[useHook]` - [Why needed]

### External Dependencies
- `[package-name]` - [Why needed]

---

## Related Components

| Component | Relationship |
|-----------|--------------|
| `[ParentComponent]` | Parent container |
| `[SiblingComponent]` | Often used together |
| `[ChildComponent]` | Used internally |

---

## Performance Considerations

### Memoization
```tsx
// Component is memoized to prevent unnecessary re-renders
export const [ComponentName] = memo(function [ComponentName](props) {
  // ...
});
```

### Code Splitting
```tsx
// Lazy load if component is heavy
const [ComponentName] = lazy(() => import('./[ComponentName]'));
```

### Bundle Impact
- Estimated size: [X]kb (gzipped)
- [Any optimization notes]

---

## Known Issues

| Issue | Status | Workaround |
|-------|--------|------------|
| [Issue description] | [Open/Closed] | [Workaround if any] |

---

## Changelog

| Version | Date | Changes | Author |
|---------|------|---------|--------|
| 1.0.0 | [Date] | Initial implementation | [Author] |
| 1.1.0 | [Date] | Added [feature] | [Author] |

---

## Decision Log

### Why [Specific Implementation Choice]
**Date:** [Date]
**Context:** [Why this decision was needed]
**Decision:** [What was decided]
**Alternatives Considered:** [Other options]
**Rationale:** [Why this choice was made]

---

## Notes

[Any additional notes, tips, or gotchas]
