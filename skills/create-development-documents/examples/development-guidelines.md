# Development Guidelines

> **Note**: This is a template document. Adapt, modify, or remove sections based on your project's specific technology stack and requirements. Some sections (e.g., TypeScript, specific testing frameworks, styling solutions) may not apply to your environment. Replace all placeholders in [brackets] with your actual technology choices, tools, and conventions.

## Coding Manner

### [Framework Name] Patterns

This project follows [Framework Name] conventions and best practices. Key patterns to follow:

#### [Primary Pattern: e.g., Route Components]

```[language]
// Good - [description of good pattern]
[code example showing recommended approach]

// Include [error handling pattern]
[code example showing error handling]
```

#### [Secondary Pattern: e.g., Form Handling]

```[language]
// [Description of pattern]
[code example demonstrating pattern]
```

#### [Tertiary Pattern: e.g., Data Loading]

```[language]
// [Pattern description]
[code example showing implementation]
```

### Component Design Principles

#### Composition Over Inheritance

```[language]
// Good - composable components
[code example demonstrating composition]

// Usage
[usage example]
```

#### Controlled vs Uncontrolled Components

```[language]
// Controlled - for [use case]
[controlled component example]

// Uncontrolled - for [use case]
[uncontrolled component example]
```

#### Custom Hooks for Reusable Logic

```[language]
// Good - extract reusable logic into hooks
[custom hook example with documentation]

// Usage in component
[usage example]
```

### TypeScript Best Practices

#### Prefer Interfaces for Objects

```typescript
// Good - interface for object shapes
interface [EntityName] {
  [property]: [type]
  [property]: [type]
  [property]: [type]
}

// Good - type for unions and complex types
type [TypeName] = [type definition]
type [GenericType]<T> = [complex type definition]
```

#### Avoid `any`, Use `unknown` When Needed

```typescript
// Bad
function processData(data: any) {
  return data.value // No type safety
}

// Good - use proper types
function processData(data: [Type]) {
  return data.[property]
}

// Good - when type is truly unknown
function parseJSON(text: string): unknown {
  return JSON.parse(text)
}

// Validate before use
const data = parseJSON(response)
if (is[Type](data)) {
  // Now TypeScript knows data is [Type]
  console.log(data.[property])
}
```

#### Use Type Guards

```typescript
// Type guard function
function is[Type](value: unknown): value is [Type] {
  return (
    typeof value === 'object' &&
    value !== null &&
    '[property]' in value &&
    '[property]' in value &&
    '[property]' in value
  )
}

// Usage
const data: unknown = await response.json()
if (is[Type](data)) {
  // TypeScript knows data is [Type] here
  console.log(data.[property])
}
```

#### Discriminated Unions for API Responses

```typescript
// Good - discriminated union
type ApiResponse<T> =
  | { success: true; data: T }
  | { success: false; error: string }

function handleResponse<T>(response: ApiResponse<T>) {
  if (response.success) {
    // TypeScript knows response.data exists
    return response.data
  } else {
    // TypeScript knows response.error exists
    throw new Error(response.error)
  }
}
```

### Form Validation with [Validation Library]

This project uses [Validation Library] with [Schema Library] for type-safe form validation and management.

#### Installing Dependencies

```bash
[package manager install command]
```

#### Defining Schemas

```[language]
// [path to validation schemas]
import { [validation imports] } from '[library]'

// Simple schema
export const [entityName]Schema = [schema definition]

// Infer TypeScript type from schema
export type [EntityName] = [type inference from schema]

// Schema for [specific use case]
export const [specificSchema] = [schema definition]
```

#### Form Validation with [Form Library]

##### Basic Form with Server-Side Validation

```[language]
// [route path]
[import statements]

export async function [actionHandler]([parameters]) {
  [request handling logic]

  // Parse and validate
  const submission = [validation logic]

  // Return errors if validation fails
  if ([error condition]) {
    return { [error response] }
  }

  // Use validated data
  [success logic]
}

export default function [ComponentName]([props]) {
  [form setup logic]

  return (
    [form JSX with validation]
  )
}
```

##### Form with Default Values

```[language]
export async function [loaderHandler]([parameters]) {
  [data loading logic]
  return { [data] }
}

export default function [ComponentName]([props]) {
  [form setup with default values]

  return (
    [form JSX]
  )
}
```

##### Nested Objects and Arrays

```[language]
// Schema with nested structure
const [schemaName] = [nested schema definition]

export default function [ComponentName]([props]) {
  [form setup logic]

  [nested field handling]

  return (
    [form JSX with nested fields]
  )
}
```

##### Custom Validation

```[language]
// Schema with custom refinement
const [schemaName] = [schema with custom validation]

export async function [actionHandler]([parameters]) {
  [validation logic including custom rules]
}
```

#### Reusable Form Components

```[language]
// [path to form components]
[import statements]

interface [PropsInterface] {
  [field definitions]
}

export function [ComponentName]([props]: [PropsInterface]) {
  return (
    [reusable form field JSX]
  )
}

// Usage
[usage example]
```

#### Validating URL and Query Parameters

```[language]
// Validate URL params
const paramsSchema = [schema definition]

export async function [loaderHandler]([parameters]) {
  [validation logic]
}

// Validate search params
const searchParamsSchema = [schema definition]

export async function [loaderHandler]([parameters]) {
  [search param validation logic]
}
```

#### API Response Validation

```[language]
// [path to API utilities]
import { [validation imports] } from '[library]'

const [apiSchema] = [API response schema]

export async function [apiFunctionName](): Promise<[ReturnType]> {
  [API call logic]

  // Validate API response
  const result = [validation logic]

  if (!result.success) {
    [error handling]
  }

  return result.data
}
```

#### Reusable Validation Schemas

```[language]
// [path to common validation]
import { [validation imports] } from '[library]'

// Reusable field validators
export const [fieldName] = [field validator]

// Reusable schemas
export const [schemaName] = [common schema]
```

#### Intent-Based Form Actions

```[language]
// Handle multiple intents in one action
const [intent1Schema] = [schema definition]

const [intent2Schema] = [schema definition]

const [combinedSchema] = [discriminated union schema]

export async function [actionHandler]([parameters]) {
  [intent-based action handling]
}

// In component
[form with intent field]
```

#### Validation Best Practices

1. **Always validate on the server**: [Explanation]
2. **Use [Form Library] for forms**: [Explanation]
3. **Infer types from schemas**: [Explanation]
4. **Create reusable schemas**: [Explanation]
5. **Provide clear error messages**: [Explanation]
6. **Validate at boundaries**: [Explanation]
7. **Use progressive enhancement**: [Explanation]
8. **Handle validation errors gracefully**: [Explanation]
9. **Use intent-based actions**: [Explanation]
10. **Test validation logic**: [Explanation]

### Error Handling

#### [Level]-Level Error Boundaries

```[language]
// Export ErrorBoundary from [location]
[error boundary implementation]
```

#### Try-Catch in [Handlers]

```[language]
export async function [handlerName]([parameters]) {
  try {
    [main logic]
  } catch (error) {
    [error handling]
  }
}
```

#### Client-Side Error Handling

```[language]
function [ComponentName]([props]) {
  [error state management]

  async function [handleFunction]() {
    try {
      [main logic]
    } catch (err) {
      [error handling]
    }
  }

  [error display logic]
}
```

## Naming Rules

### Variables and Functions

```[language]
// camelCase for variables and functions
const [variableName] = [value]
const [totalValue] = [value]

function [functionName]([parameters]): [returnType] {
  [implementation]
}

// Boolean variables should be prefixed with is/has/can/should
const [isCondition] = [boolean]
const [hasProperty] = [boolean]
const [canPerform] = [boolean]
const [shouldExecute] = [boolean]
```

### Constants

```[language]
// UPPER_CASE for true constants
const [CONSTANT_NAME] = [value]
const [API_ENDPOINT] = [value]

// camelCase for configuration objects
const config = {
  [property]: [value],
  [property]: [value],
}
```

### Components

```[language]
// PascalCase for components
function [ComponentName]() {}
function [AnotherComponent]() {}

// Use descriptive names that indicate purpose
// Good
function [DescriptiveComponentName]() {}

// Avoid
function [GenericName]() {} // Too generic
```

### Hooks

```[language]
// Prefix with 'use'
function use[HookName]() {}

// Name should describe what it does
function use[DescriptiveHookName]<T>([parameters]) {}
```

### Types and Interfaces

```[language]
// PascalCase for type names
interface [EntityName] {}
type [TypeName] = [definition]

// Avoid prefixing with 'I' or 'T'
// Good
interface [Name] {}
type [Type] = {}

// Avoid
interface I[Name] {}
type T[Name] = {}

// Props interfaces can have 'Props' suffix
interface [ComponentName]Props {
  [property]: [type]
  [optionalHandler]?: ([parameters]) => [returnType]
}
```

### Files and Directories

```[language]
// Components: PascalCase
[ComponentName].[extension]

// Hooks: camelCase with 'use' prefix
use[HookName].[extension]

// Utilities: camelCase
[utilityName].[extension]

// Types: camelCase (singular or plural based on content)
[typeName].[extension]

// Routes: [naming convention]
[route-name].[extension]
```

### Event Handlers

```[language]
// Prefix with 'handle' for event handlers
function handle[EventName]() {}

// Props for event handlers use 'on' prefix
interface [ComponentName]Props {
  on[EventName]?: () => void
  on[Action]?: ([parameters]) => [returnType]
}
```

### API and Database

```[language]
// API functions: verb + noun
async function fetch[Resource]() {}
async function create[Resource]() {}
async function update[Resource]() {}
async function delete[Resource]() {}

// Database models: PascalCase singular
class [ModelName] {}

// Database tables: [naming convention]
[table_name]
```

## Styling with [CSS Framework]

### [CSS Framework] Usage

This project uses [CSS Framework] with [build tool] integration. Styles are applied using [styling approach].

#### Basic Component Styling

```[language]
// Good - using [CSS framework] utilities
[component example with styling]
```

#### Responsive Design

```[language]
// [Responsive approach description]
[responsive component example]
```

#### Conditional Styling

```[language]
// Using [conditional styling approach]
[conditional styling example]
```

#### Using [Utility Library] for Complex Conditionals

```[language]
import [utilityFunction] from '[library]'

function [ComponentName]([props]) {
  return (
    [complex conditional styling example]
  )
}
```

#### Custom Styles (When Necessary)

```[language]
// For unique styles not covered by [framework]
[custom styling examples]
```

#### Layout Patterns

```[language]
// Container
[container pattern]

// Flexbox layout
[flexbox pattern]

// Grid layout
[grid pattern]

// Stack (vertical spacing)
[stack pattern]
```

#### Common Utility Patterns

```[language]
// [Pattern 1] styling
const [patternName]Classes = [class string]

// [Pattern 2] base
const [patternName] = [class string]

// [Pattern 3] styling
const [patternName]Classes = [class string]

// [Pattern 4] styling
const [patternName]Classes = [class string]
```

#### Accessibility with [CSS Framework]

```[language]
// Focus states
[focus state example]

// Screen reader only text
[sr-only example]

// Disabled states
[disabled state example]
```

## Testing

This project uses [Testing Framework] as the test framework.

### Running Tests

```bash
[test command]              # [Description]
[test command with flag]    # [Description]
[test command with flag]    # [Description]
[test command with flag]    # [Description]
```

### Test File Conventions

**Unit tests:** [Location and naming convention]

```
[directory structure showing unit test locations]
```

**Integration tests:** [Location and naming convention]

```
[directory structure showing integration test locations]
```

**E2E tests:** [Location and naming convention]

```
[directory structure showing E2E test locations]
```

### Unit Testing

#### Testing Utilities

```[language]
// [test file path]
import { [test imports] } from '[testing framework]'
import { [functions to test] } from '[module path]'

describe('[module name]', () => {
  describe('[function name]', () => {
    it('[test description]', () => {
      [test implementation]
    })

    it('[another test description]', () => {
      [test implementation]
    })
  })
})
```

#### Testing Hooks

```[language]
// [test file path]
import { [test imports] } from '[testing framework]'
import { [hook imports] } from '[testing utilities]'
import { [hook to test] } from '[module path]'

describe('[hook name]', () => {
  it('[test description]', async () => {
    [hook test implementation]
  })
})
```

### Component Testing

```[language]
// [test file path]
import { [test imports] } from '[testing framework]'
import { [render imports] } from '[testing library]'
import { [component to test] } from '[module path]'

describe('[ComponentName]', () => {
  const [mockData] = {
    [mock data definition]
  }

  it('[test description]', () => {
    [component test implementation]
  })

  it('[interaction test description]', () => {
    [interaction test implementation]
  })

  it('[conditional test description]', () => {
    [conditional rendering test]
  })
})
```

### Integration Testing

```[language]
// [test file path]
import { [test imports] } from '[testing framework]'
import { [integration test imports] } from '[testing utilities]'

describe('[Feature Name]', () => {
  it('[integration test description]', async () => {
    [integration test implementation]
  })
})
```

### Mocking

#### Mocking API Calls

```[language]
import { [mock utility] } from '[testing framework]'
import * as api from '[api module]'

// Mock the entire module
[mock setup]

// Use in test
it('[test description]', async () => {
  [mock implementation and assertions]
})
```

#### Mocking [Framework] Hooks

```[language]
import { [mock utility] } from '[testing framework]'
import { [hook to mock] } from '[framework]'

[mock setup]

it('[test description]', () => {
  [hook mock implementation]
})
```

### Test Coverage Goals

- **Statements**: > [percentage]%
- **Branches**: > [percentage]%
- **Functions**: > [percentage]%
- **Lines**: > [percentage]%

### Testing Best Practices

1. **Write tests alongside code**: [Explanation]
2. **Test user behavior, not implementation**: [Explanation]
3. **Use descriptive test names**: [Explanation]
4. **Arrange-Act-Assert pattern**: [Explanation]
5. **Mock external dependencies**: [Explanation]
6. **Avoid testing implementation details**: [Explanation]
7. **Keep tests simple**: [Explanation]

## End-to-End Testing with [E2E Framework]

This project uses [E2E Framework] for end-to-end testing to verify complete user flows and interactions.

### Installing [E2E Framework]

```bash
[installation commands]
```

### Configuration

Create a `[config file name]` file in the project root:

```[language]
[E2E framework configuration]
```

### Test File Structure

E2E tests should be placed in the `[e2e directory]/` directory:

```
[E2E test directory structure]
```

### Basic E2E Test

```[language]
// [test file path]
import { [test imports] } from '[e2e framework]'

[test suite description](() => {
  [test case]('[test description]', async ([test context]) => {
    [test implementation]
  })

  [test case]('[another test description]', async ([test context]) => {
    [test implementation]
  })
})
```

### Page Object Model

Use the Page Object Model pattern for maintainable tests:

```[language]
// [page object path]
import { [imports] } from '[e2e framework]'

export class [PageObjectName] {
  [property definitions]

  constructor([parameters]) {
    [initialization]
  }

  async [methodName]([parameters]) {
    [method implementation]
  }

  async [assertionMethod]([parameters]) {
    [assertion implementation]
  }
}
```

Using the Page Object:

```[language]
// [test file path]
import { [test imports] } from '[e2e framework]'
import { [PageObject] } from '[page object path]'

[test suite](() => {
  [test case]('[test description]', async ([context]) => {
    [page object usage]
  })
})
```

### Testing Forms

```[language]
// [test file path]
import { [test imports] } from '[e2e framework]'

[test suite]('[Feature Name]', () => {
  [test case]('[success case]', async ([context]) => {
    [form interaction and assertions]
  })

  [test case]('[validation case]', async ([context]) => {
    [validation testing]
  })

  [test case]('[error case]', async ([context]) => {
    [error handling testing]
  })
})
```

### Testing User Flows

```[language]
// [test file path]
import { [test imports] } from '[e2e framework]'

[test suite]('[Flow Name]', () => {
  [test case]('[complete flow description]', async ([context]) => {
    [step-by-step flow testing]
  })
})
```

### Authentication Setup

Create reusable authentication for tests that require logged-in users:

```[language]
// [auth setup file path]
import { [setup imports] } from '[e2e framework]'

const authFile = '[auth state file path]'

[setup]('[setup name]', async ([context]) => {
  [authentication logic]

  // Save authentication state
  [save state]
})
```

Configure in `[config file]`:

```[language]
[authentication configuration]
```

### API Mocking

Mock API responses for consistent testing:

```[language]
// [test file path]
import { [test imports] } from '[e2e framework]'

[test case]('[test description]', async ([context]) => {
  // Mock API response
  [API mocking setup]

  [test assertions]
})

[test case]('[error handling test]', async ([context]) => {
  // Mock API error
  [error mocking setup]

  [error assertions]
})
```

### Visual Regression Testing

```[language]
// [test file path]
import { [test imports] } from '[e2e framework]'

[test suite]('Visual Regression', () => {
  [test case]('[visual test description]', async ([context]) => {
    [screenshot assertions]
  })
})
```

### Running Tests

```bash
# Run all tests
[run command]

# Run tests in [mode]
[run command with flag]

# Run specific test file
[run command with file]

# Run tests in specific [configuration]
[run command with config]

# Run tests in debug mode
[debug command]

# Run tests with UI
[ui command]

# Generate test report
[report command]
```

### Test Fixtures

Create reusable test fixtures:

```[language]
// [fixtures file path]
import { [fixture imports] } from '[e2e framework]'

type [FixturesType] = {
  [fixture definitions]
}

export const [testName] = [fixture extension]

export { [exports] } from '[e2e framework]'
```

Using fixtures:

```[language]
// [test file path]
import { [test imports] } from '[fixtures path]'

[test case]('[test description]', async ([fixtures]) => {
  [test implementation using fixtures]
})
```

### E2E Testing Best Practices

1. **Test critical user journeys**: [Explanation]
2. **Use data-testid attributes**: [Explanation]
3. **Avoid brittle selectors**: [Explanation]
4. **Use Page Object Model**: [Explanation]
5. **Mock external services**: [Explanation]
6. **Run in CI/CD**: [Explanation]
7. **Keep tests independent**: [Explanation]
8. **Use fixtures for setup**: [Explanation]
9. **Handle loading states**: [Explanation]
10. **Test across browsers**: [Explanation]
11. **Take screenshots on failure**: [Explanation]
12. **Use traces for debugging**: [Explanation]

## Code Style

[Formatter Name] is configured with:

- [Configuration setting 1]
- [Configuration setting 2]
- [Configuration setting 3]
- [Configuration setting 4]
- [Configuration setting 5]

Format code: `[format command]`

### [Linter Name] Configuration

[Linter Name] is configured to enforce code quality and consistency. The configuration is designed to work seamlessly with [Formatter Name] without conflicts.

#### Installing [Linter Name]

```bash
# Install [linter] and plugins
[installation commands]

# Install [formatter] integration (disables conflicting rules)
[integration installation]
```

#### [Linter Name] Configuration File

Create `[config file name]` in the project root:

```[language]
[linter configuration]
```

#### Alternative: Legacy [Linter Name] Configuration

If you prefer the legacy `[legacy config file]` format:

```[format]
[legacy configuration]
```

#### Package.json Scripts

Add these scripts to your `package.json`:

```json
{
  "scripts": {
    "[lint command]": "[linter command]",
    "[lint:fix command]": "[linter fix command]",
    "[format command]": "[formatter command]",
    "[format:check command]": "[formatter check command]",
    "[type-check command]": "[type checker command]",
    "[validate command]": "[validation commands]"
  }
}
```

#### [IDE Name] Integration

Create `[IDE config path]` for automatic formatting and linting:

```json
[IDE configuration for linting and formatting]
```

#### Pre-commit Hook with [Git Hook Tool]

Install [Git Hook Tool] and [Staged Files Tool] for automatic linting on commit:

```bash
[installation commands]
[initialization command]
```

Update `[hook file path]`:

```bash
[pre-commit hook configuration]
```

Add to `package.json`:

```json
{
  "[staged files config]": {
    [file patterns and commands]
  }
}
```

#### CI/CD Integration

Add linting to your [CI Platform] workflow:

```yaml
# [CI config file path]
[CI configuration for linting]
```

#### Common [Linter Name] Rules Explained

**[Language] Rules:**

- [Rule 1]: [Explanation]
- [Rule 2]: [Explanation]
- [Rule 3]: [Explanation]

**JavaScript Rules:**

- [Rule 1]: [Explanation]
- [Rule 2]: [Explanation]
- [Rule 3]: [Explanation]

**[Framework] Rules:**

- [Rule 1]: [Explanation]
- [Rule 2]: [Explanation]
- [Rule 3]: [Explanation]

**[Feature] Rules:**

- [Rule 1]: [Explanation]
- [Rule 2]: [Explanation]

**Accessibility Rules:**

- [Rule 1]: [Explanation]
- [Rule 2]: [Explanation]
- [Rule 3]: [Explanation]

#### [Formatter] and [Linter] Integration

The `[integration package]` package disables all [linter] rules that conflict with [formatter]. This means:

1. **[Linter] handles code quality rules** ([list examples])
2. **[Formatter] handles code formatting** ([list examples])
3. **No conflicts between the two tools**

Run [formatter] first, then [linter]:

```bash
[formatter command]  # [Description]
[linter command]     # [Description]
```

Or use the validate script to run all checks:

```bash
[validate command]
```

#### Disabling Rules

When necessary, disable rules with comments:

```[language]
// Disable for next line
[disable comment]

// Disable for entire file
[disable file comment]

// Disable specific rule for entire file
[disable specific rule comment]
```

Use sparingly and document why the rule is disabled.

## Process Management with [Process Manager]

### Overview

[Process Manager] is used as the process manager for [environments]. It provides [key features].

### [Process Manager] in Development vs Production

#### Development Usage

[Process Manager] can be used in development to [use cases]:

**When to use [process manager] in development:**

- [Use case 1]
- [Use case 2]
- [Use case 3]
- [Use case 4]

**Development command:**

```bash
[development commands with descriptions]
```

**When to use [dev server] in development:**

- [Use case 1]
- [Use case 2]
- [Use case 3]

**Development command:**

```bash
[dev server command]
```

#### Production Usage

[Process Manager] is **required** in production for:

- [Benefit 1]
- [Benefit 2]
- [Benefit 3]
- [Benefit 4]
- [Benefit 5]

**Production command:**

```bash
[production command]
```

### [Process Manager] Configuration

The application includes `[config file]` which configures:

- **[Feature 1]**: [Description]
- **[Feature 2]**: [Description]
- **[Feature 3]**: [Description]
- **[Feature 4]**: [Description]
- **[Feature 5]**: [Description]

### [Process Manager] Commands

#### Development Commands

```bash
[command] # [Description]
[command] # [Description]
[command] # [Description]
[command] # [Description]
```

#### Production Commands

```bash
[command] # [Description]
[command] # [Description]
[command] # [Description]
[command] # [Description]
```

### [Process Manager] Best Practices

#### 1. [Best Practice 1]

```bash
[commands demonstrating best practice]
```

[Explanation]

#### 2. [Best Practice 2]

```bash
[monitoring commands]
```

#### 3. [Best Practice 3]

[Implementation example with code]

#### 4. [Best Practice 4]

[Log management configuration]

#### 5. [Best Practice 5]

[Startup script configuration]

#### 6. [Best Practice 6]

[Health check implementation example]

#### 7. [Best Practice 7 - Optional Feature]

[Optional integration details]

### Debugging [Process Manager] Issues

#### Check [Process Manager] Logs

```bash
[log viewing commands]
```

#### Inspect Process Details

```bash
[inspection commands]
```

#### Reset [Process Manager]

If [process manager] is misbehaving:

```bash
[reset commands]
```

### [Process Manager] in [Container Platform]

When running [process manager] in [container platform], use [specific mode]:

```dockerfile
# [Container config file]
[container configuration]
```

[Explanation of why this mode is needed]

### Choosing the Right Development Server

| Scenario     | Recommended Command | Reason   |
| ------------ | ------------------- | -------- |
| [Scenario 1] | [command]           | [Reason] |
| [Scenario 2] | [command]           | [Reason] |
| [Scenario 3] | [command]           | [Reason] |
| [Scenario 4] | [command]           | [Reason] |

### [Process Manager] vs [Dev Server] vs [Production Server]

- **[Dev Server]** ([command]):
  - [Feature 1]
  - [Feature 2]
  - [Feature 3]
  - [Best for description]

- **[Process Manager] in development** ([command]):
  - [Feature 1]
  - [Feature 2]
  - [Feature 3]
  - [Best for description]

- **[Production Server]** ([command]):
  - [Feature 1]
  - [Feature 2]
  - [Feature 3]
  - [Best for description]

- **[Process Manager] in production** ([command]):
  - [Feature 1]
  - [Feature 2]
  - [Feature 3]
  - [Feature 4]
  - [Best for description]

## Code Review Checklist

### Before Submitting PR

- [ ] Code follows naming conventions
- [ ] Components are properly typed with [type system]
- [ ] Tests are written and passing
- [ ] Code is formatted with [formatter]
- [ ] No console.log or debug code
- [ ] Error handling is implemented
- [ ] Accessibility considerations addressed
- [ ] Responsive design verified
- [ ] Performance considerations reviewed

### Reviewing Others' Code

- Check for type safety and proper [type system] usage
- Verify test coverage for new functionality
- Ensure error handling is comprehensive
- Look for potential performance issues
- Verify accessibility with [accessibility approach]
- Check for code duplication
- Ensure consistent naming conventions
- Verify documentation for complex logic
