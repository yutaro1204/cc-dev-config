# Test Concepts

This document explains the core principles of software testing that apply universally across all frameworks and languages.

## Testing Types Overview

### 🔬 Unit Tests

**Scope**: Test individual units of code in isolation (functions, methods, components)

**Characteristics**:

- **Fastest** to run (milliseconds)
- **Cheapest** to maintain
- **Most isolated** - mock all dependencies
- **Most granular** - test specific logic
- **Easy to debug** - failure points to exact issue

**What to test**:

- Pure functions (formatting, calculations)
- Validation logic
- Data transformations
- Utility functions

---

### 🔗 Integration Tests

**Scope**: Test how multiple units work together with real dependencies in a controlled environment

**Characteristics**:

- **Moderate speed** (seconds to minutes)
- **Moderate cost** to maintain
- **Real dependencies** - use actual database, cache, message queues, etc.
- **Containerized environment** - typically using containers for consistency
- **Isolated from external services** - runs on one machine/container network
- **Tests full stack** - from HTTP request to database and back
- **More realistic** than unit tests, more controlled than E2E tests

**What to test**:

- Database queries and mutations (CRUD operations)
- API endpoints with real database interactions
- Form submissions that persist to database
- Authentication flows with session storage
- Cache invalidation and updates
- Search functionality
- File uploads to storage
- File download and deletion
- Background job processing

---

### 🌐 E2E (End-to-End) Tests

**Scope**: Test complete user flows through the entire application in a deployed environment

**Characteristics**:

- **Slowest** to run (minutes to hours)
- **Most expensive** to maintain
- **No mocking of internal services** - use real database, cache, storage, and application
- **Tests user journeys** - complete workflows from user's perspective
- **Real browser automation**
- **Cross-browser testing**
- **Production-like environment** - built application with real infrastructure services
- **Catches deployment and configuration issues**

**What to test**:

- **Critical business flows** - purchase, signup, subscription
- **Payment processing** - successful payments, failures, refunds
- **Email notifications** - order confirmations, password resets
- **Third-party integrations** - payment gateways, shipping APIs, analytics
- **Cross-browser compatibility**
- **Mobile responsiveness** - different screen sizes and orientations
- **Performance** - page load times, time to interactive
- **Security** - HTTPS, authentication, authorization
- **Error scenarios** - network failures, timeout handling, error messages

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

Let's walk through a simple TDD cycle for a password validation function:

**Step 1: RED - Write a failing test**

```
// Test the requirement first
test('password must be at least 8 characters', () => {
  const result = validatePassword('short')
  expect(result.isValid).toBe(false)
  expect(result.error).toBe('Password must be at least 8 characters')
})

// Run test → ❌ FAILS (validatePassword doesn't exist yet)
```

**Step 2: GREEN - Write minimal code to pass**

```
// Simplest implementation that makes the test pass
function validatePassword(password) {
  if (password.length < 8) {
    return {
      isValid: false,
      error: 'Password must be at least 8 characters'
    }
  }
  return { isValid: true }
}

// Run test → ✅ PASSES
```

**Step 3: REFACTOR - Improve the code**

```
// Refactor if needed (in this case, code is already clean)
// Run test → ✅ PASSES (no changes broke anything)
```

**Step 4: Add next test (RED again)**

```
test('password must contain a number', () => {
  const result = validatePassword('password')
  expect(result.isValid).toBe(false)
  expect(result.error).toBe('Password must contain a number')
})

// Run test → ❌ FAILS (new requirement not implemented)
```

**Step 5: Implement to pass (GREEN)**

```
function validatePassword(password) {
  if (password.length < 8) {
    return {
      isValid: false,
      error: 'Password must be at least 8 characters'
    }
  }

  if (!/\d/.test(password)) {
    return {
      isValid: false,
      error: 'Password must contain a number'
    }
  }

  return { isValid: true }
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

**Classical School approach is recommended** for better integration and fewer brittle tests.

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
| Database                                 | ✅ Yes       | ❌ Never            | ❌ Never            | I/O in unit; real in integration/E2E      |
| Cache                                    | ✅ Yes       | ❌ Never            | ❌ Never            | I/O in unit; real in integration/E2E      |
| Storage                                  | ✅ Yes       | ❌ Never            | ❌ Never            | I/O in unit; real (emulation) in others   |
| Session storage                          | ✅ Yes       | ❌ Never            | ❌ Never            | I/O in unit; real in integration/E2E      |
|                                          |              |                     |                     |                                           |
| **External Services (Not Your Control)** |              |                     |                     |                                           |
| Payment gateway                          | ✅ Yes       | ⚠️ Test mode        | ⚠️ Test mode        | Use service test mode, not mocks          |
| Email service                            | ✅ Yes       | ⚠️ Test mode        | ⚠️ Test mode        | Use mail catcher or test mode             |
| SMS service                              | ✅ Yes       | ⚠️ Test mode        | ⚠️ Test mode        | Use service test mode                     |
| External HTTP APIs                       | ✅ Yes       | ⚠️ Mock at boundary | ⚠️ Mock at boundary | Avoid costs/rate limits                   |
| Analytics/tracking                       | ✅ Yes       | ⚠️ Disable          | ⚠️ Disable          | Avoid polluting analytics                 |
|                                          |              |                     |                     |                                           |
| **System Resources**                     |              |                     |                     |                                           |
| File system                              | ✅ Yes       | ❌ Never            | ❌ Never            | I/O in unit; real in integration/E2E      |
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

- Database operations
- External HTTP APIs
- File system operations
- Any I/O operations

#### ❌ DON'T Mock in Unit Tests

- Internal business logic
- Pure utility functions
- Validators
- Formatters

### Integration Test Mocking Guidelines

#### ✅ Use Real Services

- All internal code
- Database (via containers)
- Cache (via containers)
- Storage (via emulation or containers)
- Internal APIs

#### ⚠️ Mock Only External Services

- External payment APIs (or use test mode)
- External email services (or use test mode)
- Third-party APIs with costs/rate limits

### E2E Test Mocking Guidelines

**General Rule: NO Mocking**

E2E tests should use real services to test the complete system as users experience it.

**✅ Use Real Services (Never Mock)**:

- Internal application code
- Database (test instance)
- Cache (test instance)
- Storage (test instance or emulation)
- Internal APIs
- Authentication
- Business logic

**⚠️ Exceptions: When to Mock (External 3rd Party Only)**

Only mock **external services you don't control** to avoid costs, rate limits, or external dependencies:

1. **Payment Gateways** - Use payment provider's test mode (not mocking your code)
2. **Email/SMS Services** - Use email service test mode or mail catcher
3. **External APIs with Costs/Limits** - Mock only at HTTP boundary
4. **Third-Party Analytics/Tracking** - Disable or mock in test environment

**When NOT to Mock (Keep Real)**:

- ❌ Never mock your own application code
- ❌ Never mock your database
- ❌ Never mock your cache
- ❌ Never mock your internal APIs
- ❌ Never mock authentication logic
- ❌ Never mock file storage
- ❌ Never mock business logic

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

---

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

| Aspect            | Unit                  | Integration                       | E2E                     |
| ----------------- | --------------------- | --------------------------------- | ----------------------- |
| **Speed**         | ⚡️ Fast (~ms)         | ⚡ Medium (~sec to min)           | 🐌 Slow (~min to hours) |
| **Cost**          | 💰 Cheap              | 💰💰 Medium                       | 💰💰💰 Expensive        |
| **Environment**   | In-memory             | Containers (local)                | Staging/Production-like |
| **Dependencies**  | All mocked            | Real (in containers)              | Real deployed services  |
| **External APIs** | Mocked                | Mocked or containerized           | Real (test mode)        |
| **Database**      | Mocked or in-memory   | Real database in container        | Real staging database   |
| **Cache**         | Mocked                | Real cache in container           | Real staging cache      |
| **Storage**       | Mocked                | Real emulation in container       | Real staging storage    |
| **Confidence**    | Low                   | Medium-High                       | Highest                 |
| **Debugging**     | Easy                  | Medium                            | Hard                    |
| **Flakiness**     | Rare                  | Occasional                        | Common                  |
| **When to run**   | Every save            | Every commit                      | Pre-deploy              |
| **Scope**         | Single function/class | Multiple modules + infrastructure | Full user journey       |

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

- Use real database, cache, and storage (via containers)
- Verify response status codes and data structure
- Test error handling and validation
- Test authentication and authorization logic
- Verify side effects (database writes, cache updates, storage uploads)

### E2E Test Best Practices

- Focus on critical user journeys only
- Use Page Object Model for maintainability
- Run against staging/test environments
- Handle async operations properly with proper waiting
- Use stable selectors
- Keep tests independent with proper setup/teardown
- Run in CI/CD pipeline before deployment

---

## Common Misconceptions

❌ **"E2E tests replace other tests"** - No, you need all three types for comprehensive coverage

❌ **"More tests = better"** - Quality > Quantity, focus on high-value tests

❌ **"100% coverage"** - Aim for ~80%, diminishing returns after that

❌ **"Only test happy paths"** - Error cases are often more important

❌ **"Integration tests are just slow unit tests"** - No, they test real interactions with infrastructure

❌ **"Integration tests should mock the database"** - No, use real database in containers for true integration testing

❌ **"Containers are too slow for tests"** - Not with optimized settings, tests run fast

❌ **"E2E tests can only run against deployed environments"** - They should, for realistic testing

❌ **"TDD slows down development"** - Initially slower, but faster overall due to fewer bugs and easier maintenance

❌ **"TDD means no bugs"** - TDD reduces bugs but doesn't eliminate them

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

- You're implementing API endpoints or handlers
- You're building forms with multiple fields
- You're creating features that interact with infrastructure
- You're implementing search/filter functionality
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

## Key Questions for Testing Strategy

1. **What's your risk tolerance?** - More E2E = more confidence but slower feedback
2. **What's most critical?** - Payment flow? Authentication? Inventory?
3. **What breaks most often?** - Focus more tests there
4. **What's your deployment frequency?** - Fast deploys need fast tests
5. **Do you have staging environment?** - E2E tests need somewhere to run
6. **Is the team comfortable with TDD?** - TDD requires practice and discipline

---

## Metrics to Track

- **Test execution time** - Keep unit tests under 10 seconds total
- **Test coverage** - Aim for 80%+ on critical paths
- **Test reliability** - Track flaky test rates
- **Test maintenance cost** - Time spent fixing broken tests
- **Bug escape rate** - Bugs found in production vs caught by tests
- **TDD cycle time** - Time from red to green (target: < 1 minute for unit tests)
