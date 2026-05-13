```markdown
# ManGaAI Development Patterns

> Auto-generated skill from repository analysis

## Overview

This skill provides a comprehensive guide to the development patterns, coding conventions, and common workflows used in the ManGaAI codebase. Built with TypeScript and Vite, ManGaAI emphasizes code consistency, reusability, and maintainability through shared utilities, standardized component patterns, and robust CI/CD practices. This guide will help you contribute effectively by following established conventions and leveraging automated workflows.

## Coding Conventions

### File Naming

- Use **camelCase** for file and folder names.
  - Example: `formatTime.ts`, `novelHelpers.tsx`

### Import Style

- Prefer **alias imports** for clarity and maintainability.
  - Example:
    ```typescript
    import { formatTime } from '@/shared/utils';
    ```

### Export Style

- Mixed usage of **named** and **default exports**.
  - Named export example:
    ```typescript
    export function generateId() { /* ... */ }
    ```
  - Default export example:
    ```typescript
    export default MyComponent;
    ```

### Commit Message Patterns

- Use **conventional commit** prefixes: `fix`, `refactor`, `chore`, `feat`, `ci`, `docs`.
- Average commit message length: ~58 characters.
  - Example: `feat: add emotion constants for manga pipeline`

## Workflows

### Deduplicate and Unify Utility Functions

**Trigger:** When utility functions (like `formatTime`, `generateId`, etc.) are duplicated across multiple files and need to be unified.  
**Command:** `/deduplicate-utils`

1. Identify duplicate utility functions in feature, service, or component files.
2. Move or implement the unified version in `src/shared/utils/index.ts`.
3. Remove local duplicates from all affected files.
4. Update all call sites to use the shared utility.
5. Clean up imports and remove dead code.

**Example:**
```typescript
// Before (in multiple files)
function formatTime(ts: number) { /* ... */ }

// After (in src/shared/utils/index.ts)
export function formatTime(ts: number) { /* ... */ }

// Usage
import { formatTime } from '@/shared/utils';
```

---

### React FC to Function Component Migration

**Trigger:** When standardizing React components to use function declarations instead of `React.FC`.  
**Command:** `/migrate-fc-to-fn`

1. Identify components using `React.FC`.
2. Convert each to a function declaration.
3. Update any related imports/exports.
4. Batch similar changes together for related components.
5. Commit with a `refactor` message.

**Example:**
```typescript
// Before
const MyComponent: React.FC<Props> = (props) => { /* ... */ };

// After
function MyComponent(props: Props) { /* ... */ }
```

---

### Dead Code and Unused Import Removal

**Trigger:** When dead code, unused imports, or deprecated files are identified during refactoring or code review.  
**Command:** `/remove-dead-code`

1. Scan for dead code blocks, commented-out code, and unused imports.
2. Remove these from the relevant files.
3. Delete deprecated or pure forwarding files if all consumers have migrated.
4. Commit with a `refactor` message.

**Example:**
```typescript
// Before
// const unused = 42;
import { unusedFn } from './unused';

// After
// (Removed unused code and imports)
```

---

### Extract and Share Utility or Constants

**Trigger:** When utility functions or constants are used in multiple places or need to be reused across features.  
**Command:** `/extract-shared-utils`

1. Identify reusable utility functions or constants.
2. Extract them into a new or existing shared file (e.g., `novel-helpers.ts`, `emotion-constants.ts`).
3. Update imports in all consumers to use the shared version.
4. Remove old definitions from original files.

**Example:**
```typescript
// src/core/services/novel-helpers.ts
export const EMOTION_CONSTANTS = { /* ... */ };

// Usage
import { EMOTION_CONSTANTS } from '@/core/services/novel-helpers';
```

---

### Refactor Feature Workflow Migration

**Trigger:** When a feature's local implementation can be replaced with a shared or improved version for consistency and maintainability.  
**Command:** `/migrate-feature-to-shared`

1. Identify local implementations in feature files (e.g., `formatTime`, `generateId`, etc.).
2. Replace with calls to shared or unified services/utilities.
3. Remove old code and update all relevant call sites.
4. Test to ensure feature parity.

**Example:**
```typescript
// Replace local formatTime with shared version
import { formatTime } from '@/shared/utils';
```

---

### CI Workflow YML Adjustment

**Trigger:** When release automation fails or needs improvement in the CI/CD pipeline.  
**Command:** `/fix-release-ci`

1. Edit `.github/workflows/release.yml` to adjust parameters, outputs, or steps.
2. Test the workflow in CI.
3. Repeat as needed until the workflow passes.

**Example:**
```yaml
# .github/workflows/release.yml
jobs:
  release:
    steps:
      - name: Checkout code
        uses: actions/checkout@v3
      # ...other steps
```

---

## Testing Patterns

- **Framework:** Jest
- **Test file pattern:** `*.test.ts`
- **Test example:**
  ```typescript
  // src/shared/utils/formatTime.test.ts
  import { formatTime } from './index';

  test('formats timestamp correctly', () => {
    expect(formatTime(1234567890)).toBe('...expected output...');
  });
  ```

## Commands

| Command                | Purpose                                                        |
|------------------------|----------------------------------------------------------------|
| /deduplicate-utils     | Deduplicate and unify utility functions in shared utils        |
| /migrate-fc-to-fn      | Migrate React.FC components to function declarations           |
| /remove-dead-code      | Remove dead code, unused imports, and deprecated files         |
| /extract-shared-utils  | Extract and share utility functions or constants               |
| /migrate-feature-to-shared | Refactor feature logic to use shared services/utilities    |
| /fix-release-ci        | Adjust CI workflow YAML for release automation                 |
```