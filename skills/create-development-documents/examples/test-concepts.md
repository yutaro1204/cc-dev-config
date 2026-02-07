# Test Concepts

> **Note**: This is a template document. The core concepts of testing (unit, integration, E2E, testing pyramid, mocking philosophy) are universal and should be preserved. Adapt the technology-specific examples, tools, and setup instructions based on your project's testing framework, language, and infrastructure. Replace all placeholders in [brackets] with your actual testing tools and configurations.

This document explains the differences between unit tests, integration tests, and E2E tests, and provides guidance on building a comprehensive testing strategy.

## Testing Types Overview

### 🔬 Unit Tests

**Scope**: Test individual units of code in isolation (functions, methods, components)

**Characteristics**:

- **Fastest** to run (milliseconds)
- **Cheapest** to maintain
- **Most isolated** - mock all dependencies
- **Most granular** - test specific logic
- **Easy to debug** - failure points to exact issue

**Example for your project**:

```[language]
// [test file path]
describe('[module name]', () => {
  it('[test description]', () => {
    expect([functionCall]([input])).toBe([expected])
  })
})
```

**What to test**:

- Pure functions (formatting, calculations)
- Validation logic
- Data transformations
- Custom hooks/utilities (in isolation)
- Helper functions

---

### 🔗 Integration Tests

**Scope**: Test how multiple units work together with real dependencies in a controlled environment

**Characteristics**:

- **Moderate speed** (seconds to minutes)
- **Moderate cost** to maintain
- **Real dependencies** - use actual database, cache, message queues, etc.
- **Containerized environment** - typically using [Container Tool] for consistency
- **Isolated from external services** - runs on one machine/container network
- **Tests full stack** - from HTTP request to database and back
- **More realistic** than unit tests, more controlled than E2E tests

**[Framework] Testing Approach**:

In [Framework Name], integration tests take two forms:

1. **[Handler/Controller] Tests** - Test [server-side handlers] directly as functions:
   - Tests the actual server-side code that runs in production
   - Works with real database connections and services
   - Validates request/response handling
   - Verifies data transformations and business logic
   - Tests error handling and edge cases
   - Call [handlers/controllers] directly with Request objects

2. **Component Integration Tests** - Test [UI components] with [Testing Library]:
   - Tests component rendering and user interactions
   - Validates form behavior and validation
   - Tests component composition and prop passing
   - Uses [testing library] for rendering and queries
   - Mocks [handlers/data] or provides test data via props

**Environment Setup**:

```yaml
# [container-config-file].yml
services:
  app:
    build: .
    ports:
      - '[port]:[port]'
    depends_on:
      - [service1]
      - [service2]
    environment:
      [DATABASE_URL]: [connection-string]
      [CACHE_URL]: [connection-string]

  [service1]:
    image: [image-name]:[version]
    environment:
      [CONFIG_KEY]: [value]
    tmpfs:
      - [path-for-in-memory-storage]

  [service2]:
    image: [image-name]:[version]
    command: [command-for-testing-mode]
```

**Example for your project**:

```[language]
// [test file path]
import { describe, it, expect, beforeAll, afterAll } from '[test-framework]'
import { [handler] } from '[module-path]'
import { db } from '[db-client-path]'

// These tests run against real [database/services] in [container-tool]
describe('[Feature Name] Integration', () => {
  beforeAll(async () => {
    // [Database/Services] already running in [Container Tool]
    await seedTestData()
  })

  afterAll(async () => {
    await cleanupTestData()
  })

  it('[handler] fetches data from real database', async () => {
    // Create test request
    const request = new Request('[url]')
    const context = { [context-properties] } as any

    // Call [handler] directly - no mocks, talks to real [Database] in [Container]
    const response = await [handler]({ request, [parameters], context })
    const data = await response.json()

    expect(data.[property]).toHaveLength([number])
    expect(data.[property][0].[field]).toBe('[value]')
    expect(data.[property][0].[field]).toBe([value])
  })

  it('[handler] filters data using database query', async () => {
    // Create request with query params
    const request = new Request('[url]?[param]=[value]')
    const context = { [context-properties] } as any

    const response = await [handler]({ request, [parameters], context })
    const data = await response.json()

    // Verifies database query filtering works
    expect(data.[collection].every((item: any) => item.[field] === '[value]')).toBe(true)
  })

  it('[action] creates record in database', async () => {
    // Create form data
    const formData = new FormData()
    formData.append('[field]', '[value]')
    formData.append('[field]', '[value]')
    formData.append('[field]', '[value]')

    // Create request with form data
    const request = new Request('[url]', {
      method: 'POST',
      body: formData,
    })
    const context = { [context-properties] } as any

    // Call [action] directly - tests validation → database insert → redirect
    const response = await [actionHandler]({ request, [parameters], context })

    // Verify redirect response
    expect(response.status).toBe([statusCode])

    // Verify record was created in real database
    const record = await db.[model].findFirst({
      where: { [field]: '[value]' },
    })
    expect(record).toBeTruthy()
    expect(record?.[field]).toBe([value])
  })

  it('[action] uploads file to storage', async () => {
    const { [StorageClient], [Command] } = await import('[storage-sdk]')

    const client = new [StorageClient]({
      endpoint: '[local-endpoint]',
      region: '[region]',
      [config-options],
      credentials: {
        accessKeyId: '[test-key]',
        secretAccessKey: '[test-secret]',
      },
    })

    // Create form data with file
    const fileContent = Buffer.from('[test content]')
    const file = new Blob([fileContent], { type: '[mime-type]' })
    const formData = new FormData()
    formData.append('[field]', '[value]')
    formData.append('[field]', '[value]')
    formData.append('[fileField]', file, '[filename]')

    const request = new Request('[url]', {
      method: 'POST',
      body: formData,
    })
    const context = { [context-properties] } as any

    // Call [action] - uploads to [Local Storage Service]
    const response = await [actionHandler]({ request, [parameters], context })
    expect(response.status).toBe([statusCode])

    // Verify file was uploaded to [Local Storage]
    const record = await db.[model].findFirst({
      where: { [field]: '[value]' },
    })
    expect(record?.[urlField]).toMatch(/[pattern]/)

    // Verify file exists in storage
    const key = record?.[urlField].split('/').pop()!
    const storageResponse = await client.send(
      new [Command]({
        [Bucket]: '[test-bucket]',
        [Key]: key,
      })
    )
    expect(storageResponse.$metadata.httpStatusCode).toBe(200)
  })
})

// Component Integration Test Example
describe('[Component Name] Integration', () => {
  it('displays data correctly', () => {
    const [data] = {
      [field]: [value],
      [field]: '[value]',
      [field]: [value],
      [field]: '[value]',
      [field]: '[url]',
    }

    render(<[Component] [data]={[data]} />)

    expect(screen.getByText('[value]')).toBeInTheDocument()
    expect(screen.getByText('[formatted-value]')).toBeInTheDocument()
    expect(screen.getByText('[value]')).toBeInTheDocument()
    expect(screen.getByRole('[role]')).toHaveAttribute('[attribute]', [data].[field])
  })

  it('handles user interaction', async () => {
    const user = [userEventSetup]()
    const [mockHandler] = [mockFunction]()

    const [data] = {
      [field]: [value],
      [field]: '[value]',
      [field]: [value],
      [field]: '[value]',
    }

    render(<[Component] [data]={[data]} [onAction]={[mockHandler]} />)

    await user.click(screen.getByRole('[role]', { name: /[text]/i }))

    expect([mockHandler]).toHaveBeenCalledWith([data].[field])
  })
})
```

**What to test**:

- Database queries and mutations (CRUD operations with [ORM])
- API endpoints with real [Database] database interactions
- Form submissions that persist to database
- Authentication flows with session storage in [Cache Service]
- Cache invalidation and updates ([Cache Service])
- Search functionality with [Database] full-text search
- File uploads to storage (using [Local Storage Service])
- File download and deletion from storage
- Background job processing

**Running Integration Tests**:

```bash
# Start test environment
[container-tool] -f [test-config] up -d

# Run integration tests
[test-command]

# Teardown
[container-tool] -f [test-config] down -v
```

---

### 🌐 E2E (End-to-End) Tests

**Scope**: Test complete user flows through the entire application in a deployed environment

**Characteristics**:

- **Slowest** to run (minutes to hours)
- **Most expensive** to maintain
- **No mocking of internal services** - use real database, cache, storage, and application
- **Tests user journeys** - complete workflows from user's perspective
- **Real browser automation** - [E2E Framework] with [browsers]
- **Cross-browser testing** - [browser1], [browser2], [browser3], mobile browsers
- **Production-like environment** - built application with real infrastructure services
- **Catches deployment and configuration issues**

**Environment**:

E2E tests run with real services (no mocking):

- **Application** - Built production application ([framework])
- **Database** - Real [Database] database (test instance)
- **Cache** - Real [Cache Service] cache (test instance)
- **Storage** - Real storage (emulation for local/CI)
- **Browser** - Real browser automation via [E2E Framework]
- **All services on one machine** - Container services for local/CI testing

**Example for your project**:

```[language]
// [e2e test path]
import { test, expect } from '[e2e-framework]'

// Runs against [staging-url]
test('[complete user flow description]', async ({ page }) => {
  // Navigate to deployed environment
  await page.goto('[path]')

  // Browse and select item
  await page.getByTestId('[test-id]').first().click()
  await expect(page).toHaveURL(/[pattern]/)

  // Perform action
  await page.getByRole('[role]', { name: /[text]/i }).click()
  await expect(page.getByText(/[text]/i)).toBeVisible()

  // View result
  await page.getByRole('[role]', { name: /[text]/i }).click()
  await expect(page).toHaveURL('[path]')

  // Proceed to next step
  await page.getByRole('[role]', { name: /[text]/i }).click()
  await expect(page).toHaveURL('[path]')

  // Fill form
  await page.getByLabel(/[label]/i).fill('[value]')
  await page.getByLabel(/[label]/i).fill('[value]')
  await page.getByLabel(/[label]/i).fill('[value]')
  await page.getByLabel(/[label]/i).fill('[value]')

  // Fill payment with real payment processor ([Provider] test mode)
  await page.getByLabel(/[label]/i).fill('[test-card-number]')
  await page.getByLabel(/[label]/i).fill('[expiry]')
  await page.getByLabel(/[label]/i).fill('[cvc]')

  // Submit - this hits real payment API in test mode
  await page.getByRole('[role]', { name: /[text]/i }).click()

  // Verify confirmation - real database entry created
  await expect(page).toHaveURL(/[pattern]/)
  await expect(page.getByText(/[text]/i)).toBeVisible()
  await expect(page.getByText(/[text]/i)).toBeVisible()

  // Verify email was sent (check email service dashboard or inbox)
  // Verify payment was processed (check [Payment Provider] dashboard)
})

test('handles [error scenario] gracefully', async ({ page }) => {
  await page.goto('[path]')

  // Fill valid information
  await page.getByLabel(/[label]/i).fill('[value]')
  // ... fill other fields ...

  // Use [Provider] test card/data that triggers [error]
  await page.getByLabel(/[label]/i).fill('[error-test-data]')
  await page.getByLabel(/[label]/i).fill('[expiry]')
  await page.getByLabel(/[label]/i).fill('[cvc]')

  await page.getByRole('[role]', { name: /[text]/i }).click()

  // Verify error handling
  await expect(page.getByText(/[error-message]/i)).toBeVisible()
  await expect(page).toHaveURL('[path]') // Should stay on same page
})
```

**What to test**:

- **Critical business flows** - [flow1], [flow2], [flow3]
- **Payment processing** - successful payments, failures, refunds
- **Email notifications** - confirmations, password resets
- **Third-party integrations** - payment gateways, shipping APIs, analytics
- **Cross-browser compatibility** - [browser1], [browser2], [browser3], mobile
- **Mobile responsiveness** - different screen sizes and orientations
- **Performance** - page load times, time to interactive
- **Security** - HTTPS, authentication, authorization
- **Error scenarios** - network failures, timeout handling, error messages

**Running E2E Tests**:

```bash
# Run against staging environment
[E2E_BASE_URL]=[staging-url] [test-command]

# Run against production (smoke tests only)
[E2E_BASE_URL]=[production-url] [test-command-smoke]

# Run with specific browser
[test-command] -- --project=[browser-name]

# Run in headed mode to watch
[test-command-headed]
```

---

## Test-Driven Development (TDD)

### What is TDD?

Test-Driven Development is a software development approach where you write tests **before** writing the implementation code. The cycle is short and iterative: write a failing test, write just enough code to make it pass, then refactor.

### The Red-Green-Refactor Cycle

```
┌─────────────────────────────────────┐
│                                     │
│  1. RED                             │
│  Write a failing test               │
│  (Test what you want to implement)  │
│                                     │
└──────────────┬──────────────────────┘
               │
               ↓
┌─────────────────────────────────────┐
│                                     │
│  2. GREEN                           │
│  Write minimal code to pass         │
│  (Make the test pass)               │
│                                     │
└──────────────┬──────────────────────┘
               │
               ↓
┌─────────────────────────────────────┐
│                                     │
│  3. REFACTOR                        │
│  Improve the code                   │
│  (Tests still pass)                 │
│                                     │
└──────────────┬──────────────────────┘
               │
               │
               └──────→ Repeat
```

### The Three Laws of TDD

1. **You are not allowed to write any production code** unless it is to make a failing unit test pass
2. **You are not allowed to write any more of a unit test** than is sufficient to fail (compilation failures are failures)
3. **You are not allowed to write any more production code** than is sufficient to pass the one failing unit test

### Benefits of TDD

**1. Better Design**

- Forces you to think about the interface before implementation
- Encourages smaller, focused functions
- Leads to more modular, decoupled code
- Naturally promotes dependency injection

**2. Higher Test Coverage**

- Tests are written as part of development, not as an afterthought
- Every line of production code is written to pass a test
- Less likely to skip testing "just this once"

**3. Confidence in Changes**

- Comprehensive test suite catches regressions immediately
- Safe to refactor knowing tests will catch breaks
- Makes maintenance easier

**4. Living Documentation**

- Tests serve as examples of how to use the code
- Tests document expected behavior
- Tests clarify intent and edge cases

**5. Faster Debugging**

- Failures are caught immediately, not hours/days later
- Smaller code changes between test runs
- Easier to identify what broke and why

**6. Reduced Debugging Time**

- Bugs are caught during development, not in QA or production
- Tests pinpoint exact failure location
- Less time spent in debugger

### When TDD Works Best

✅ **Ideal for:**

- Business logic with clear requirements
- Algorithms and calculations
- Utility functions and helpers
- API endpoints with defined contracts
- Data transformations
- Validation logic

⚠️ **Challenging for:**

- UI/UX explorations where requirements are unclear
- Prototypes and experiments
- Learning new technologies/frameworks
- Complex visual layouts
- Third-party API integration exploration

### TDD Workflow Example

Let's walk through a simple TDD cycle for a validation function:

**Step 1: RED - Write a failing test**

```[language]
// Test the requirement first
test('[requirement description]', () => {
  const result = [functionToTest]('[invalid-input]')
  expect(result.[property]).toBe([expected])
  expect(result.[property]).toBe('[expected-message]')
})

// Run test → ❌ FAILS ([functionToTest] doesn't exist yet)
```

**Step 2: GREEN - Write minimal code to pass**

```[language]
// Simplest implementation that makes the test pass
function [functionToTest]([parameter]) {
  if ([condition]) {
    return {
      [property]: [value],
      [property]: '[message]'
    }
  }
  return { [property]: [value] }
}

// Run test → ✅ PASSES
```

**Step 3: REFACTOR - Improve the code**

```[language]
// Refactor if needed (in this case, code is already clean)
// Run test → ✅ PASSES (no changes broke anything)
```

**Step 4: Add next test (RED again)**

```[language]
test('[next requirement description]', () => {
  const result = [functionToTest]('[different-invalid-input]')
  expect(result.[property]).toBe([expected])
  expect(result.[property]).toBe('[expected-message]')
})

// Run test → ❌ FAILS (new requirement not implemented)
```

**Step 5: Implement to pass (GREEN)**

```[language]
function [functionToTest]([parameter]) {
  if ([condition1]) {
    return {
      [property]: [value],
      [property]: '[message1]'
    }
  }

  if ([condition2]) {
    return {
      [property]: [value],
      [property]: '[message2]'
    }
  }

  return { [property]: [value] }
}

// Run test → ✅ PASSES (both tests pass)
```

**Continue the cycle** for each new requirement...

### TDD Best Practices

**1. Keep Tests Small and Focused**

- One test should verify one behavior
- Test names should clearly describe what is being tested
- Each test should be independent

**2. Write the Simplest Test First**

- Start with the happy path
- Then add edge cases
- Then add error cases

**3. Test Behavior, Not Implementation**

- Focus on what the code does, not how it does it
- Tests should survive refactoring
- Don't test private methods directly

**4. Keep the Red Phase Short**

- Don't write multiple failing tests at once
- Write one test, make it pass, then write the next
- Keeps feedback loop tight

**5. Keep the Green Phase Minimal**

- Write just enough code to pass the test
- Don't anticipate future requirements
- Resist the urge to add "nice to have" features

**6. Refactor with Confidence**

- Only refactor when tests are green
- Make small, incremental improvements
- Run tests frequently during refactoring

**7. Treat Test Code as Production Code**

- Keep tests clean and maintainable
- Refactor tests when needed
- Remove duplicate test code

### Common TDD Mistakes

❌ **Writing too much test at once**

- Write the smallest test that fails
- Add complexity incrementally

❌ **Writing production code without a failing test**

- Always write the test first
- No production code without a failing test

❌ **Not refactoring**

- Don't skip the refactor step
- Clean code is as important as working code

❌ **Testing implementation details**

- Test the interface, not the implementation
- Tests should survive refactoring

❌ **Having tests depend on each other**

- Each test should be independent
- Tests should pass in any order

❌ **Making tests too complex**

- Keep tests simple and readable
- Complex tests are hard to maintain

❌ **Not running tests frequently**

- Run tests after every small change
- Fast feedback is key to TDD

### TDD vs. Test-After Development

| Aspect                     | TDD (Test First)                 | Test After                       |
| -------------------------- | -------------------------------- | -------------------------------- |
| **When tests written**     | Before implementation            | After implementation             |
| **Design influence**       | Tests drive design               | Tests adapt to design            |
| **Coverage**               | High (every line has a test)     | Variable (easy to skip)          |
| **Debugging**              | Immediate feedback               | Delayed feedback                 |
| **Refactoring confidence** | High (tests catch breaks)        | Lower (incomplete tests)         |
| **Development speed**      | Slower initially, faster overall | Faster initially, slower overall |
| **Code quality**           | Generally higher                 | Variable                         |
| **Learning curve**         | Steeper                          | Gentler                          |

### TDD Variants

**1. Classic TDD (Detroit School)**

- Use real collaborators where possible
- Only mock external dependencies
- Tests verify overall behavior
- More integration-focused

**2. Mockist TDD (London School)**

- Mock all dependencies
- Test in complete isolation
- Tests verify interactions
- More unit-focused

**3. Outside-In TDD**

- Start with acceptance tests (E2E)
- Work inward to implementation
- Build features end-to-end
- Ensures user value

**4. Inside-Out TDD**

- Start with domain logic (units)
- Build up to integration
- Focus on core algorithms first
- Then connect pieces

### TDD and Different Test Types

**Unit Tests with TDD:**

- Perfect fit for TDD
- Fast feedback loop
- Clear pass/fail criteria
- Easy to practice

**Integration Tests with TDD:**

- Slower feedback loop
- Still valuable for TDD
- Write integration test first
- Then implement handler/endpoint

**E2E Tests with TDD:**

- Too slow for tight TDD loop
- Better as specification/acceptance tests
- Write E2E test to define acceptance criteria
- Use unit/integration TDD to implement

### Getting Started with TDD

**For Beginners:**

1. **Start small** - Practice with simple functions (e.g., calculator, string utilities)
2. **Focus on the cycle** - Get comfortable with Red-Green-Refactor
3. **Use katas** - Practice exercises designed for TDD (e.g., FizzBuzz, Roman Numerals)
4. **Pair program** - Learn from someone experienced with TDD
5. **Be patient** - TDD feels unnatural at first, stick with it

**Practice Exercises (Katas):**

- **FizzBuzz** - Classic beginner kata
- **String Calculator** - Roy Osherove's kata
- **Roman Numerals** - Convert numbers to Roman numerals
- **Bowling Game** - Calculate bowling scores
- **Prime Factors** - Decompose numbers into prime factors
- **Gilded Rose** - Refactoring kata

### TDD Anti-Patterns

**1. The Liar**

- Test passes but doesn't actually test anything
- Solution: Verify test actually fails when it should

**2. Excessive Setup**

- Test requires too much setup/teardown
- Solution: Refactor code to be more testable

**3. The Giant**

- Test tries to verify too much
- Solution: Split into smaller, focused tests

**4. The Mockery**

- Over-mocking leads to brittle tests
- Solution: Use real collaborators where practical

**5. The Inspector**

- Test knows too much about implementation
- Solution: Test behavior, not implementation

**6. The Slow Poke**

- Tests take too long to run
- Solution: Mock slow dependencies, optimize setup

### TDD Metrics

**Cycle Time:**

- Time from writing test to green
- Target: < 1 minute for unit tests
- Longer cycles indicate design problems

**Test Coverage:**

- TDD naturally achieves high coverage
- Aim for 80%+ on business logic
- Don't aim for 100% (diminishing returns)

**Test Maintenance:**

- Tests should be easy to maintain
- Brittle tests indicate poor design
- Refactor tests as you refactor code

### Resources for Learning TDD

**Books:**

- "Test Driven Development: By Example" by Kent Beck (the classic)
- "Growing Object-Oriented Software, Guided by Tests" by Steve Freeman & Nat Pryce
- "Modern C++ Programming with Test-Driven Development" by Jeff Langr

**Online:**

- Coding Dojos and Katas
- TDD screencasts and tutorials
- Open source projects practicing TDD

**Key Takeaways:**

1. **Write the test first** - Always red before green
2. **Take small steps** - One test, one implementation, one refactor
3. **Keep it simple** - Write minimal code to pass
4. **Refactor fearlessly** - Tests give you confidence
5. **Practice regularly** - TDD is a skill that improves with practice

---

## Mocking Philosophy Across Test Types

### General Principle: Mock at Boundaries, Not Inside

The key principle of mocking is to **mock at external boundaries** while using **real implementations for internal code**.

```
Your Application
┌─────────────────────────────────────┐
│                                     │
│  ┌──────────┐    ┌──────────┐      │
│  │ Function │───→│ Function │      │
│  │    A     │    │    B     │      │
│  └──────────┘    └──────────┘      │
│       │               │             │
│       │  Real calls   │             │
│       │  (no mocks)   │             │
│       ↓               ↓             │
│  ┌─────────────────────────┐       │
│  │   Internal Logic        │       │
│  │   (Use Real)            │       │
│  └─────────┬───────────────┘       │
│            │                        │
└────────────┼────────────────────────┘
             │ ← Mock HERE (at boundary)
             ↓
    ┌────────────────┐
    │ External APIs  │
    │ Database       │
    │ File System    │
    │ HTTP Requests  │
    └────────────────┘
```

**Two Schools of Thought:**

1. **London School** - Mock all dependencies, test in isolation
2. **Classical School** - Use real collaborators, mock only external boundaries

**This project follows the Classical School approach** for better integration and fewer brittle tests.

### Mocking Decision Matrix

Comprehensive guide for when to mock across all three test types:

| Dependency Type                          | Unit Test    | Integration Test    | E2E Test            | Reason                                    |
| ---------------------------------------- | ------------ | ------------------- | ------------------- | ----------------------------------------- |
| **Internal Code You Control**            |              |                     |                     |                                           |
| Business logic functions                 | ❌ Never     | ❌ Never            | ❌ Never            | Need to test real behavior                |
| Utility functions                        | ❌ Never     | ❌ Never            | ❌ Never            | Pure, fast, deterministic                 |
| Validators                               | ❌ Never     | ❌ Never            | ❌ Never            | No side effects, fast                     |
| Formatters                               | ❌ Never     | ❌ Never            | ❌ Never            | Pure transformations                      |
| Internal APIs                            | ❌ Never     | ❌ Never            | ❌ Never            | Need to test integration                  |
| Authentication logic                     | ❌ Never     | ❌ Never            | ❌ Never            | Critical business logic                   |
|                                          |              |                     |                     |                                           |
| **Infrastructure (Your Control)**        |              |                     |                     |                                           |
| Database ([Database])                    | ✅ Yes       | ❌ Never            | ❌ Never            | I/O in unit; real in integration/E2E      |
| Cache ([Cache Service])                  | ✅ Yes       | ❌ Never            | ❌ Never            | I/O in unit; real in integration/E2E      |
| Storage ([Storage Service])              | ✅ Yes       | ❌ Never            | ❌ Never            | I/O in unit; real (emulation) in others   |
| Session storage                          | ✅ Yes       | ❌ Never            | ❌ Never            | I/O in unit; real in integration/E2E      |
|                                          |              |                     |                     |                                           |
| **External Services (Not Your Control)** |              |                     |                     |                                           |
| Payment gateway ([Provider])             | ✅ Yes       | ⚠️ Test mode        | ⚠️ Test mode        | Use [Provider] test mode, not mocks       |
| Email service (SMTP)                     | ✅ Yes       | ⚠️ Test mode        | ⚠️ Test mode        | Use mail catcher or test mode             |
| SMS service                              | ✅ Yes       | ⚠️ Test mode        | ⚠️ Test mode        | Use service test mode                     |
| External HTTP APIs                       | ✅ Yes       | ⚠️ Mock at boundary | ⚠️ Mock at boundary | Avoid costs/rate limits                   |
| Analytics/tracking                       | ✅ Yes       | ⚠️ Disable          | ⚠️ Disable          | Avoid polluting analytics                 |
|                                          |              |                     |                     |                                           |
| **System Resources**                     |              |                     |                     |                                           |
| File system (fs)                         | ✅ Yes       | ❌ Never            | ❌ Never            | I/O in unit; real in integration/E2E      |
| Environment variables                    | ⚠️ Maybe     | ⚠️ Maybe            | ⚠️ Maybe            | Mock if testing different configs         |
| Date/Time                                | ⚠️ If needed | ❌ Never            | ❌ Never            | Mock only if testing time-dependent logic |
| Random generation                        | ⚠️ If needed | ❌ Never            | ❌ Never            | Mock for deterministic tests              |
| Network requests                         | ✅ Yes       | ❌ Never            | ❌ Never            | Mock in unit; real in integration/E2E     |

**Legend:**

- ❌ Never mock - Use real implementation
- ✅ Yes - Mock this dependency
- ⚠️ Test mode - Use service's test/sandbox mode (not mocking your code)
- ⚠️ Mock at boundary - Mock only the HTTP call, not your code
- ⚠️ Disable - Disable or no-op in tests
- ⚠️ Maybe - Context-dependent

### Unit Test Mocking Guidelines

#### ✅ DO Mock in Unit Tests

**1. Database Operations**

```[language]
// ✅ GOOD: Mock database in unit test
// [test file path]
import { describe, it, expect, [mockFunction] } from '[test-framework]'
import { [functionToTest] } from '[module-path]'

describe('[function name]', () => {
  it('queries database for data', async () => {
    // Mock [ORM] client (external I/O)
    const mockDb = {
      [model]: {
        [method]: [mockFunction]().mockResolvedValue({
          [field]: '[value]',
          [field]: '[value]',
          [field]: '[value]',
        }),
      },
    }

    const result = await [functionToTest](mockDb, '[parameter]')

    expect(result.[field]).toBe('[value]')
    expect(mockDb.[model].[method]).toHaveBeenCalledWith({
      where: { [field]: '[value]' },
    })
  })
})
```

**2. External HTTP APIs**

```[language]
// ✅ GOOD: Mock external API client
// [test file path]
import { describe, it, expect, [mockFunction] } from '[test-framework]'
import { [functionToTest] } from '[module-path]'

describe('[function name]', () => {
  it('fetches data from external API', async () => {
    // Mock HTTP client (external service)
    const mockHttp = {
      [method]: [mockFunction]().mockResolvedValue({
        data: { [field]: [value], [field]: '[value]' },
      }),
    }

    const result = await [functionToTest](mockHttp, {
      [param]: [value],
      [param]: '[value]',
    })

    expect(result).toBe([value])
    expect(mockHttp.[method]).toHaveBeenCalled()
  })
})
```

**3. File System Operations**

```[language]
// ✅ GOOD: Mock file system
// [test file path]
import { describe, it, expect, [mockFunction] } from '[test-framework]'
import { [functionToTest] } from '[module-path]'

describe('[function name]', () => {
  it('writes file to disk', async () => {
    // Mock fs module (I/O operation)
    const mockFs = {
      [method]: [mockFunction]().mockResolvedValue(undefined),
    }

    await [functionToTest](mockFs, '[filename]', '[content]')

    expect(mockFs.[method]).toHaveBeenCalledWith('[filename]', '[content]')
  })
})
```

#### ❌ DON'T Mock in Unit Tests

**1. Internal Business Logic**

```[language]
// ❌ BAD: Over-mocking internal functions
describe('[function name]', () => {
  it('[test description]', () => {
    const [mockFunction1] = [mockFunction]().mockReturnValue([value])
    const [mockFunction2] = [mockFunction]().mockReturnValue([value])

    // Too much mocking! Testing mocks, not real behavior
    [functionToTest]([param], [mockFunction1], [mockFunction2])
  })
})

// ✅ GOOD: Use real internal functions
describe('[function name]', () => {
  it('[test description with real behavior]', () => {
    const [data] = [
      { [field]: [value], [field]: [value] }, // [Comment explaining data]
      { [field]: [value], [field]: [value] }, // [Comment explaining data]
    ]

    // Uses REAL internal functions
    const result = [functionToTest]([mockDb], [data])

    expect(result.[field]).toBe([expected]) // Real calculation
    expect(result.[collection]).toHaveLength([number])
  })
})
```

**2. Pure Utility Functions**

```[language]
// ❌ BAD: Mocking pure functions
describe('[function name]', () => {
  it('[test description]', () => {
    const [mockFunction] = [mockFunction]().mockReturnValue('[value]')

    // Why mock a pure function?
    [functionToTest]({ [function]: [mockFunction] })
  })
})

// ✅ GOOD: Use real pure functions
describe('[function name]', () => {
  it('[test description with real behavior]', () => {
    const result = [functionToTest]({
      [param]: [value],
      [param]: '[value]',
    })

    // Real utility function
    expect(result.[field]).toBe('[expected]')
  })
})
```

**3. Validators**

```[language]
// ❌ BAD: Mocking validators
describe('[function name]', () => {
  it('[test description]', () => {
    const [mockValidator] = [mockFunction]().mockReturnValue(true)

    // Mocking validation logic defeats the purpose!
    [functionToTest]({ [field]: '[invalid]' }, [mockValidator])
  })
})

// ✅ GOOD: Use real validators
describe('[function name]', () => {
  it('rejects invalid input', () => {
    // Real validation logic
    expect(() => [functionToTest]({ [field]: '[invalid]' })).toThrow(
      '[error message]'
    )
  })

  it('accepts valid input', () => {
    // Real validation logic
    expect(() => [functionToTest]({ [field]: '[valid]' })).not.toThrow()
  })
})
```

### Integration Test Mocking Guidelines

#### ✅ Use Real Services

```[language]
// ✅ GOOD: Integration test with real services
// [test file path]
import { describe, it, expect, beforeEach } from '[test-framework]'
import { db } from '[db-client-path]' // Real [ORM] client
import { cache } from '[cache-client-path]' // Real [Cache Service]
import { [functionToTest] } from '[module-path]'

describe('[Feature Name] (Integration)', () => {
  beforeEach(async () => {
    // Clean real database
    await db.[model].deleteMany()
    await db.[relatedModel].deleteMany()

    // Seed real data
    await db.[model].create({
      data: {
        [field]: '[value]',
        [field]: '[value]',
        [field]: [value],
      },
    })
  })

  it('[test description with real services]', async () => {
    // Uses REAL database, REAL cache, REAL business logic
    const result = await [functionToTest]({
      [param]: '[value]',
      [param]: [{ [field]: '[value]', [field]: [value] }],
    })

    // Verify in real database
    const dbRecord = await db.[model].findUnique({
      where: { [field]: result.[field] },
    })
    expect(dbRecord).toBeTruthy()
    expect(dbRecord.[field]).toBe([expected])

    // Verify in real cache
    const cachedData = await cache.get(`[key-pattern]:${result.[field]}`)
    expect(cachedData).toBeTruthy()
  })
})
```

#### ⚠️ Mock Only External Services

```[language]
// ⚠️ ACCEPTABLE: Mock external payment API in integration test
// [test file path]
import { [setupServer] } from '[http-mock-library]'
import { [httpMethod] } from '[http-mock-library]'

// Mock external [Provider] API at HTTP boundary
const server = [setupServer](
  [httpMethod]('[external-api-url]', (req, res, ctx) => {
    return res(
      ctx.json({
        [field]: '[value]',
        [field]: '[value]',
      })
    )
  })
)

describe('[Feature Name] (Integration)', () => {
  beforeAll(() => server.listen())
  afterAll(() => server.close())

  it('[test description with mocked external service]', async () => {
    // Real database, real cache, real business logic
    // Only [External Provider] HTTP calls are mocked
    const result = await [functionToTest]({
      [param]: [value],
      [param]: '[value]',
    })

    // Verify in real database
    const dbRecord = await db.[model].findUnique({
      where: { [field]: result.[field] },
    })
    expect(dbRecord.[status]).toBe('[expected-status]')
  })
})
```

### E2E Test Mocking Guidelines

**Summary for E2E:**

- ❌ Never mock internal services
- ❌ Never mock database, cache, storage
- ⚠️ Use test mode for payment gateways ([Provider] test mode)
- ⚠️ Use test mode or catcher for email services
- ⚠️ Mock only external APIs at HTTP boundary if necessary

### Key Takeaways

**Unit Tests:**

- ✅ Mock: Database, external APIs, file system, I/O operations
- ❌ Don't mock: Business logic, utilities, validators, formatters
- 🎯 Goal: Test logic in isolation from I/O

**Integration Tests:**

- ✅ Use real: Database, cache, storage, all internal code
- ❌ Don't mock: Any internal services
- ⚠️ Exception: Mock external 3rd party APIs if necessary
- 🎯 Goal: Test services working together

**E2E Tests:**

- ✅ Use real: Everything internal + infrastructure
- ❌ Don't mock: Any internal services or infrastructure
- ⚠️ Exception: Use test mode for payment/email (not mocking your code)
- 🎯 Goal: Test complete system as users experience it

**The Golden Rule:**

> Mock at the boundaries of your system, not inside it.

## The Testing Pyramid 🔺

```
        /\
       /E2E\      ← Few tests, high value, slow, expensive
      /------\
     /  INTG  \   ← More tests, medium speed/cost
    /----------\
   /   UNIT     \ ← Many tests, fast, cheap, focused
  /--------------\
```

**Recommended distribution**:

- **70%** Unit tests
- **20%** Integration tests
- **10%** E2E tests

---

## Comparison Table

| Aspect            | Unit                      | Integration                             | E2E                             |
| ----------------- | ------------------------- | --------------------------------------- | ------------------------------- |
| **Speed**         | ⚡️ Fast (~ms)             | ⚡ Medium (~sec to min)                 | 🐌 Slow (~min to hours)         |
| **Cost**          | 💰 Cheap                  | 💰💰 Medium                             | 💰💰💰 Expensive                |
| **Environment**   | In-memory                 | [Container Tool] (local containers)     | Staging/Production-like         |
| **Dependencies**  | All mocked                | Real (DB, cache, etc. in containers)    | Real deployed services          |
| **External APIs** | Mocked                    | Mocked or containerized                 | Real (test mode)                |
| **Database**      | Mocked or in-memory       | Real [Database] in [Container]          | Real staging [Database]         |
| **Cache**         | Mocked                    | Real [Cache] in [Container]             | Real staging [Cache]            |
| **Storage**       | Mocked                    | Real [Storage Emulation] in [Container] | Real staging [Storage]          |
| **Confidence**    | Low                       | Medium-High                             | Highest                         |
| **Debugging**     | Easy                      | Medium                                  | Hard                            |
| **Flakiness**     | Rare                      | Occasional                              | Common                          |
| **When to run**   | Every save (watch mode)   | Every commit (CI pipeline)              | Pre-deploy (staging validation) |
| **Scope**         | Single function/component | Multiple modules + infrastructure       | Full user journey               |

---

## For Your [Project Type] Project

### Unit Tests Priority

1. **Validation schemas** ([Validation library] schemas)
2. **[Business logic calculations]** ([examples])
3. **[Core feature] logic** ([operations])
4. **[Utility category]** ([utility examples])
5. **Custom hooks/utilities** ([hook examples])

### Integration Tests Priority

1. **Database operations** (CRUD for [entities])
2. **[Feature] with filters** (database queries with WHERE clauses)
3. **[Flow] creation** (validation → database insert → updates)
4. **Authentication** (user registration, login with session storage)
5. **[Feature] operations** (add/remove items, persist to database/cache)
6. **Search functionality** (full-text search in database)
7. **[Resource] management** ([tracking operations])
8. **Form submissions** ([validation library] → database persistence)

### E2E Tests Priority

1. **[Critical flow 1]** ([steps])
2. **User authentication** ([steps])
3. **Search and filter** ([steps])
4. **Error handling** ([error scenarios])

---

## Setting Up [Container Tool] for Integration Tests

Integration tests should run against real dependencies (database, cache, etc.) in an isolated, reproducible environment. [Container Tool] is perfect for this.

### Complete [Container Tool] Setup

**[container-config].yml**:

```yaml
version: '[version]'

services:
  # Your application
  app:
    build:
      context: .
      dockerfile: [Dockerfile]
    ports:
      - '[port]:[port]'
    depends_on:
      [service1]:
        condition: service_healthy
      [service2]:
        condition: service_started
      [service3]:
        condition: service_healthy
    environment:
      [ENV_VAR]: [value]
      [DATABASE_URL]: [connection-string]
      [CACHE_URL]: [connection-string]
      [STORAGE_ENDPOINT]: [url]
      [CONFIG_KEY]: [value]
    volumes:
      - ./[source-dir]:/app/[source-dir]
      - ./[tests-dir]:/app/[tests-dir]

  # [Database Service]
  [service1]:
    image: [image]:[tag]
    ports:
      - '[host-port]:[container-port]'
    environment:
      [CONFIG_KEY]: [value]
      [CONFIG_KEY]: [value]
      [CONFIG_KEY]: [value]
    healthcheck:
      test: ['[health-check-command]']
      interval: 5s
      timeout: 5s
      retries: 5
    tmpfs:
      # Use tmpfs for faster test database (in-memory)
      - [data-path]
    command:
      - [command]
      - [performance-option-1]
      - [performance-option-2]
      - [performance-option-3]

  # [Cache Service]
  [service2]:
    image: [image]:[tag]
    ports:
      - '[host-port]:[container-port]'
    command: [command] [test-mode-options] # Disable persistence for tests

  # [Storage Service] for storage testing
  [service3]:
    image: [image]:[tag]
    ports:
      - '[host-port]:[container-port]'
    environment:
      [CONFIG_KEY]: [value]
      [CONFIG_KEY]: [value]
    volumes:
      - ./[init-script]:[container-path]
    tmpfs:
      - [temp-path]
    healthcheck:
      test: ['[health-check-command]']
      interval: 10s
      timeout: 5s
      retries: 5
```

**[Dockerfile]**:

```dockerfile
FROM [base-image]:[tag]

WORKDIR /app

# Install dependencies
COPY [package-file] ./
RUN [install-command]

# Copy [ORM] schema
COPY [orm-dir] ./[orm-dir]

# Generate [ORM] Client
RUN [generate-command]

# Copy application code
COPY . .

# Build application
RUN [build-command]

# Expose port
EXPOSE [port]

# Run migrations and start server
CMD ["sh", "-c", "[migration-command] && [start-command]"]
```

### Database Migration Script

**[scripts-dir]/[migration-script]**:

```bash
#!/bin/bash
set -e

echo "Waiting for [Database]..."
until [health-check-command]; do
  sleep 1
done

echo "Running [ORM] migrations..."
[migration-command]

echo "Generating [ORM] Client..."
[generate-command]

echo "Seeding test database..."
[seed-command]

echo "Database ready!"
```

### [Storage Service] Initialization Script

**[scripts-dir]/[init-script]**:

```bash
#!/bin/bash
# Initialize [Storage] in [Storage Service] for testing

echo "Waiting for [Storage Service] to be ready..."
sleep 5

# Create [Storage] bucket
[create-bucket-command]

# Enable public access for testing
[configure-access-command]

echo "[Storage Service] [Storage] test bucket created successfully"
```

Make the script executable:

```bash
chmod +x [scripts-dir]/[init-script]
```

### Package.json Scripts

```json
{
  "scripts": {
    "test:integration": "[test:integration:setup command] && [test-command]",
    "test:integration:watch": "[test:integration:setup command] && [test-command-watch]",
    "test:integration:setup": "[container-up-command] && [wait-command]",
    "test:integration:wait": "[wait-script]",
    "test:integration:teardown": "[container-down-command]",

    "[migration-command-name]": "[migration-command]",
    "[migration-dev-command-name]": "[migration-dev-command]",
    "[generate-command-name]": "[generate-command]",
    "[seed-command-name]": "[seed-command]",
    "[studio-command-name]": "[studio-command]",
    "[reset-command-name]": "[reset-command]"
  },
  "[orm-config-key]": {
    "seed": "[seed-script-runner] [seed-script]"
  }
}
```

### Database Seed Script

**[seed-script-path]**:

```[language]
import { [ORMClient] } from '[orm-package]'

const [client] = new [ORMClient]()

async function main() {
  console.log('Seeding database...')

  // Create test [entities]
  const [entity1] = await [client].[model].upsert({
    where: { [field]: '[value]' },
    update: {},
    create: {
      [field]: '[value]',
      [field]: '[value]',
      [field]: '[hashed-value]', // Use proper hashing in real code
      [field]: '[value]',
    },
  })

  // Create test [related entities]
  await [client].[relatedModel].createMany({
    data: [
      {
        [field]: '[value]',
        [field]: '[description]',
        [field]: [value],
        [field]: '[value]',
        [field]: '[value]',
        [field]: [value],
        [field]: '[url]',
      },
      {
        [field]: '[value]',
        [field]: '[description]',
        [field]: [value],
        [field]: '[value]',
        [field]: '[value]',
        [field]: [value],
        [field]: '[url]',
      },
      {
        [field]: '[value]',
        [field]: '[description]',
        [field]: [value],
        [field]: '[value]',
        [field]: '[value]',
        [field]: [value],
        [field]: '[url]',
      },
    ],
    skipDuplicates: true,
  })

  console.log('Database seeded successfully!')
}

main()
  .catch((e) => {
    console.error('Error seeding database:', e)
    process.exit(1)
  })
  .finally(async () => {
    await [client].$disconnect()
  })
```

**Note**: To run the seed script, install required dependencies.

### Wait for Services Script

**[scripts-dir]/[wait-script]**:

```[language]
const [netModule] = require('[network-module]')
const { [execSync] } = require('[child-process-module]')

async function waitForService(host, port, serviceName) {
  const maxRetries = 30
  const retryDelay = 1000

  for (let i = 0; i < maxRetries; i++) {
    try {
      await new Promise((resolve, reject) => {
        const socket = [netModule].createConnection(port, host, () => {
          socket.end()
          resolve()
        })
        socket.on('error', reject)
      })
      console.log(`✓ ${serviceName} is ready`)
      return
    } catch (error) {
      if (i === maxRetries - 1) {
        throw new Error(`${serviceName} failed to start`)
      }
      await new Promise((resolve) => setTimeout(resolve, retryDelay))
    }
  }
}

async function main() {
  console.log('Waiting for services to be ready...')

  await waitForService('[host]', [port], '[Service1]')
  await waitForService('[host]', [port], '[Service2]')
  await waitForService('[host]', [port], '[Service3]')

  // Run database migrations
  console.log('Running [ORM] migrations...')
  [execSync]('[migration-command]', { stdio: 'inherit' })

  // Generate [ORM] Client
  console.log('Generating [ORM] Client...')
  [execSync]('[generate-command]', { stdio: 'inherit' })

  // Seed test data
  console.log('Seeding test database...')
  [execSync]('[seed-command]', { stdio: 'inherit' })

  console.log('✓ All services ready!')
}

main().catch((error) => {
  console.error('Failed to start services:', error)
  process.exit(1)
})
```

### [Test Framework] Integration Test Config

**[test-config].ts**:

```[language]
import { defineConfig } from '[test-framework]'
import [plugin] from '[plugin-package]'
import [pathsPlugin] from '[paths-plugin]'

export default defineConfig({
  plugins: [[plugin](), [pathsPlugin]()],
  test: {
    name: 'integration',
    include: ['**/*.[integration-pattern].{[ext1],[ext2]}'],
    environment: '[environment]',
    setupFiles: ['./[tests-dir]/[setup-file]'],
    globalSetup: ['./[tests-dir]/[global-setup-file]'],
    testTimeout: 30000, // Longer timeout for integration tests
    hookTimeout: 30000,
    pool: '[pool-type]',
    poolOptions: {
      [poolType]: {
        [option]: [value], // Share database connection
      },
    },
  },
})
```

### Integration Test Setup

**[tests-dir]/[setup-file]**:

```[language]
import { beforeAll, afterAll, beforeEach, afterEach } from '[test-framework]'
import { [ORMClient] } from '[orm-package]'

export const db = new [ORMClient]({
  [datasourceUrl]: '[test-connection-string]',
})

beforeAll(async () => {
  // Connect to database
  await db.$connect()
})

afterAll(async () => {
  // Disconnect from database
  await db.$disconnect()
})

beforeEach(async () => {
  // Clear data before each test (or use transactions)
  await db.$executeRaw`[truncate-command]`
})

afterEach(async () => {
  // Cleanup after each test
})
```

### Example Integration Test

**[test-file-path]**:

```[language]
import { describe, it, expect, beforeEach } from '[test-framework]'
import { db } from '[setup-file-path]'
import { [handler] } from '[handler-path]'
import { [action] } from '[action-path]'

describe('[Feature Name] Integration Tests', () => {
  beforeEach(async () => {
    // Insert test data
    await db.[model].createMany({
      data: [
        {
          [field]: '[value]',
          [field]: [value],
          [field]: '[value]',
          [field]: '[value]',
          [field]: [value],
        },
        {
          [field]: '[value]',
          [field]: [value],
          [field]: '[value]',
          [field]: '[value]',
          [field]: [value],
        },
      ],
    })
  })

  it('[handler] fetches data from database', async () => {
    const request = new Request('[url]')
    const context = { [param]: {}, request } as any

    const response = await [handler]({ request, [param]: {}, context })
    const data = await response.json()

    expect(data.[collection]).toHaveLength([number])
    expect(data.[collection][0].[field]).toBe('[value]')
    expect(data.[collection][1].[field]).toBe('[value]')
  })

  it('[handler] filters data by [parameter]', async () => {
    await db.[model].create({
      data: {
        [field]: '[value]',
        [field]: [value],
        [field]: '[different-value]',
        [field]: '[value]',
        [field]: [value],
      },
    })

    const request = new Request('[url]?[param]=[filter-value]')
    const context = { [param]: {}, request } as any

    const response = await [handler]({ request, [param]: {}, context })
    const data = await response.json()

    expect(data.[collection]).toHaveLength([number])
    expect(data.[collection].every((item: any) => item.[field] === '[filter-value]')).toBe(true)
  })

  it('[action] creates record in database', async () => {
    const formData = new FormData()
    formData.append('[field]', '[value]')
    formData.append('[field]', '[value]')
    formData.append('[field]', '[value]')
    formData.append('[field]', '[value]')

    const request = new Request('[url]', {
      method: 'POST',
      body: formData,
    })
    const context = { [param]: {}, request } as any

    const response = await [action]({ request, [param]: {}, context })
    expect(response.status).toBe([statusCode])

    // Verify it's in the database
    const recordInDb = await db.[model].findFirst({ where: { [field]: '[value]' } })
    expect(recordInDb).toBeTruthy()
    expect(recordInDb?.[field]).toBe('[value]')
    expect(recordInDb?.[field]).toBe([value])
  })

  it('[action] updates [resource] when [operation] occurs', async () => {
    const [entity] = await db.[model].findFirst({ where: { [field]: '[value]' } })

    const formData = new FormData()
    formData.append('[field]', '[value]')
    formData.append('[field]', [entity]!.[field].toString())
    formData.append('[field]', '[value]')

    const request = new Request('[url]', {
      method: 'POST',
      body: formData,
    })
    const context = { [param]: {}, request } as any

    await [action]({ request, [param]: {}, context })

    // Verify [resource] was updated
    const [updatedEntity] = await db.[model].findUnique({ where: { [field]: [entity]!.[field] } })
    expect([updatedEntity]?.[field]).toBe([expectedValue])
  })

  it('uploads and retrieves file from [Storage]', async () => {
    const { [StorageClient], [PutCommand], [GetCommand] } =
      await import('[storage-sdk]')

    const client = new [StorageClient]({
      endpoint: '[local-endpoint]',
      region: '[region]',
      [option]: [value],
      credentials: {
        accessKeyId: '[test-key]',
        secretAccessKey: '[test-secret]',
      },
    })

    // Upload file to [Storage Service]
    const fileContent = Buffer.from('[test content]')
    const key = `[path]/[filename]-${Date.now()}.[ext]`

    await client.send(
      new [PutCommand]({
        [Bucket]: '[test-bucket]',
        [Key]: key,
        [Body]: fileContent,
        [ContentType]: '[mime-type]',
      })
    )

    // Retrieve file from [Storage]
    const response = await client.send(
      new [GetCommand]({
        [Bucket]: '[test-bucket]',
        [Key]: key,
      })
    )

    expect(response.[ContentType]).toBe('[mime-type]')
    expect(response.$metadata.httpStatusCode).toBe(200)
  })
})
```

### CI/CD Integration

**[ci-config-file]**:

```yaml
name: Integration Tests

on: [push, pull_request]

jobs:
  integration:
    runs-on: [runner-type]

    steps:
      - uses: [checkout-action]@[version]

      - uses: [setup-action]@[version]
        with:
          [runtime]-version: [version]
          cache: '[package-manager]'

      - name: Install dependencies
        run: [install-command]

      - name: Generate [ORM] Client
        run: [generate-command]

      - name: Start test environment
        run: [container-up-command]

      - name: Wait for services
        run: [wait-command]

      - name: Run integration tests
        run: [test-command]

      - name: Teardown test environment
        if: always()
        run: [container-down-command]
```

### Benefits of This Approach

1. **Reproducible** - Same environment every time
2. **Isolated** - No conflicts with local development
3. **Fast** - tmpfs for database, no disk I/O
4. **Realistic** - Tests against real services, not mocks
5. **CI-friendly** - Runs the same locally and in CI
6. **Disposable** - Tear down and recreate easily

---

## Key Questions for Testing Strategy

1. **What's your risk tolerance?** - More E2E = more confidence but slower feedback
2. **What's most critical?** - Payment flow? Authentication? Core feature?
3. **What breaks most often?** - Focus more tests there
4. **What's your deployment frequency?** - Fast deploys need fast tests
5. **Do you have staging environment?** - E2E tests need somewhere to run
6. **Is the team comfortable with TDD?** - TDD requires practice and discipline

## Common Misconceptions

❌ **"E2E tests replace other tests"** - No, you need all three types for comprehensive coverage

❌ **"More tests = better"** - Quality > Quantity, focus on high-value tests

❌ **"100% coverage"** - Aim for ~80%, diminishing returns after that

❌ **"Only test happy paths"** - Error cases are often more important

❌ **"Integration tests are just slow unit tests"** - No, they test real interactions with infrastructure

❌ **"Integration tests should mock the database"** - No, use real database in containers for true integration testing

❌ **"[Container Tool] is too slow for tests"** - Not with tmpfs and optimized settings, tests run fast

❌ **"E2E tests can run locally"** - They can, but should target deployed environments for realistic testing

❌ **"TDD slows down development"** - Initially slower, but faster overall due to fewer bugs and easier maintenance

❌ **"TDD means no bugs"** - TDD reduces bugs but doesn't eliminate them

---

## Testing Best Practices

### General Principles

1. **Test behavior, not implementation** - Focus on what the code does, not how it does it
2. **Write tests first when fixing bugs** - Reproduce the bug, then fix it
3. **Keep tests independent** - Each test should run in isolation
4. **Use descriptive test names** - Test names should describe the scenario and expected outcome
5. **Arrange-Act-Assert pattern** - Structure tests clearly

### Unit Test Best Practices

- Mock all external dependencies
- Test edge cases and error conditions
- Keep tests focused on a single behavior
- Use test data builders for complex objects
- Test pure functions extensively

### Integration Test Best Practices

**For [Handler/Controller] Tests**:

- Test [handlers] as pure functions with Request objects
- Use real database, cache, and storage (via [Container Tool])
- Verify response status codes and data structure
- Test error handling and validation
- Test authentication and authorization logic
- Verify side effects (database writes, cache updates, storage uploads)

**For Component Integration Tests**:

- Use [testing library] for rendering and queries
- Test user interactions and form submissions
- Verify component behavior with different props
- Test error states and loading states
- Use [testing library]'s user event for realistic interactions
- Prefer user-facing queries (getByRole, getByLabelText) over test IDs

### E2E Test Best Practices

- Focus on critical user journeys only
- Use Page Object Model for maintainability
- Run against staging/test environments
- Handle async operations properly with waitFor
- Use data-testid for stable selectors
- Keep tests independent with proper setup/teardown
- Run in CI/CD pipeline before deployment

---

## Test Organization

### File Structure

```
[source-dir]/
├── [components-dir]/
│   ├── [feature]/
│   │   ├── [Component].[ext]
│   │   └── [Component].[test-pattern].[ext]          # Component unit/integration tests
├── [routes-dir]/
│   ├── [route].[ext]
│   └── [route].[test-pattern].[ext]                  # [Handler] integration tests
├── [utils-dir]/
│   ├── [utility].[ext]
│   └── [utility].[test-pattern].[ext]                # Utility unit tests
├── [lib-dir]/
│   ├── [validation-dir]/
│   │   ├── [schema].[ext]
│   │   └── [schema].[test-pattern].[ext]            # Validation unit tests

[tests-dir]/
├── [integration-dir]/                                 # Integration tests
│   └── [feature].[integration-pattern].[ext]         # Integration test specs
└── [e2e-dir]/                                         # E2E tests
    ├── [fixtures-dir]/                                # Test data and fixtures
    ├── [page-objects-dir]/                            # Page Object Models
    └── [feature].[e2e-pattern].[ext]                  # E2E test specs
```

### Naming Conventions

- Unit/Integration tests: `*.[test-pattern].[ext]` or `*.[test-pattern].[ext]`
- E2E tests: `*.[e2e-pattern].[ext]`
- Test utilities: `[test-utils].[ext]`, `[test-helpers].[ext]`
- Mock data: `[fixtures-dir]/`, `[mocks-dir]/`

---

## When to Write Each Type

### Write Unit Tests When:

- You have pure functions with complex logic
- You're implementing algorithms or calculations
- You're writing validation rules
- You're creating utility functions
- You need fast feedback during development
- **You're practicing TDD** - Unit tests are ideal for TDD

### Write Integration Tests When:

- You're implementing [framework] [handlers/controllers] (test as functions with real DB)
- You're building forms with multiple fields (test with [Testing Library])
- You're creating components that interact with hooks
- You're implementing search/filter functionality (test [handler] with query params)
- You need to test component composition
- You're integrating with infrastructure (database, cache, storage)
- You're implementing file upload/download functionality

### Write E2E Tests When:

- You're implementing critical business flows
- You need to test cross-page navigation
- You're integrating with external services
- You want to verify the entire user experience
- You need confidence before deployment

---

## Test Execution Strategy

### Development

```bash
# Run unit/integration tests in watch mode
[test-command-watch]

# Run specific test file
[test-command] -- [test-file]

# Run with coverage
[test-command] -- --coverage
```

### CI/CD Pipeline

```yaml
# Run in sequence for fast feedback
1. Lint & Format Check (seconds)
2. Type Check (seconds)
3. Unit Tests (seconds)
4. Integration Tests (seconds to minutes)
5. Build (minutes)
6. E2E Tests (minutes)
```

### Pre-deployment

- Run full test suite including E2E
- Run E2E tests against staging environment
- Check coverage reports
- Review failed test reports

---

## Metrics to Track

- **Test execution time** - Keep unit tests under 10 seconds total
- **Test coverage** - Aim for 80%+ on critical paths
- **Test reliability** - Track flaky test rates
- **Test maintenance cost** - Time spent fixing broken tests
- **Bug escape rate** - Bugs found in production vs caught by tests
- **TDD cycle time** - Time from red to green (target: < 1 minute for unit tests)

---

## Resources

- [[Framework] Testing Documentation]([url])
- [[Test Framework] Documentation]([url])
- [[E2E Framework] Best Practices]([url])
- [[Testing Library] Guiding Principles]([url])
