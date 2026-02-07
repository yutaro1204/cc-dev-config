# Ubiquitous Language

> **Note**: This is a template document based on Domain-Driven Design principles. The concept of ubiquitous language and its structure should be preserved, while the specific domain terms should be replaced with your project's actual business terminology. Replace all placeholders in [brackets] with your domain-specific entities, concepts, and rules.

## Purpose

This document defines the domain-specific terminology and concepts used throughout the [Project Name] codebase. All team members, code, documentation, and conversations should use these terms consistently to maintain a shared understanding of the domain.

## Core Entities

### [Platform/Product Name]

**Definition**: [Brief description of what the platform/product is and what it does].

**Context**: [When and how this term is used - in branding, business discussions, etc.].

**Examples**:

- "[Example sentence using the platform name]"
- "[Another example in a business context]"

**Code References**:

- [Where this appears in code - configuration, UI, API responses]
- [Other code locations where this term is used]

### [Primary Entity 1]

**Definition**: [Clear, precise definition of what this entity represents in your domain].

**Aliases**: [Alternative terms that mean the same thing, if any]

**Context**: [When and how this entity is used. How it relates to other entities].

**Properties**:

- [Property 1 with brief description]
- [Property 2 with brief description]
- [Property 3 with brief description]
- [Property 4 with brief description]
- [Property 5 with brief description]

**Examples**:

- "[Example sentence showing how this entity is used]"
- "[Another example demonstrating a key characteristic]"
- "[Example showing relationship to other entities]"

**Code References**:

```[language]
interface [EntityName] {
  [field]: [type]
  [field]: [type]
  [field]: [type]
  [field]: [type]
  [field]: [type] | null
}
```

### [Primary Entity 2]

**Definition**: [Clear definition distinguishing this entity from related entities].

**Context**: [How this entity fits into your business model and relates to other entities].

**Properties**:

- [Property 1 with description]
- [Property 2 with description]
- [Property 3 with description]
- [Property 4 with description]
- [Property 5 with description]

**Examples**:

- "[Example showing typical usage]"
- "[Example showing business rules]"
- "[Example showing relationships]"

**Code References**:

```[language]
interface [RelatedEntity] {
  [foreignKey]: [type] // References the [Entity]
  // ...
}

interface [ItemEntity] {
  [foreignKey]: [type]
  [calculatedField]: [type] // [Description of calculation]
}
```

## Core Concepts

### [Core Concept 1]

**Definition**: [What this concept represents in your domain].

**Properties**:

- [Property/characteristic 1]
- [Property/characteristic 2]
- [Property/characteristic 3]
- [Property/characteristic 4]
- [Property/characteristic 5]

**Examples**:

- "[Example of how this concept is used]"
- "[Example showing a key attribute]"
- "[Example showing relationships]"

**Code References**:

```[language]
interface [ConceptName] {
  [field]: [type]
  [field]: [type]
  [field]: [EnumType]
  [field]: [type] // [Important note about this field]
  [field]: [type]
}
```

### [Core Concept 2]

**Definition**: [Definition emphasizing the temporary or persistent nature, purpose, etc.].

**Context**: [How this concept is used in your workflows].

**Properties**:

- [Property 1]
- [Property 2]
- [Property 3]
- [Property 4]

**Examples**:

- "[Action example with this concept]"
- "[State example]"
- "[Calculation example]"

**Code References**:

```[language]
interface [ItemType] {
  [field]: [type]
  [field]: [type]
  [field]: [type]
  [field]: [type]
}

interface [ConceptName] {
  [collection]: [ItemType][]
  [calculatedField]: [type]
}
```

### [Core Concept 3]

**Definition**: [Definition describing the purpose and lifecycle of this concept].

**Context**: [When this is created, how it's used, what it tracks].

**Properties**:

- [Property 1]
- [Property 2]
- [Property 3]
- [Property 4]

**Examples**:

- "[Example of viewing/accessing]"
- "[Example of status change]"
- "[Example of calculation]"

**Code References**:

```[language]
interface [ConceptName] {
  [field]: [type]
  [field]: [type]
  [field]: [StatusEnumType]
  [field]: [type]
  [collection]: [ItemType][]
  [field]: [AddressType]
}

enum [StatusEnumType] {
  [STATE1] = '[STATE1]',
  [STATE2] = '[STATE2]',
  [STATE3] = '[STATE3]',
  [STATE4] = '[STATE4]',
  [STATE5] = '[STATE5]',
}
```

### [Core Concept 4 - Line Item/Detail]

**Definition**: [Definition of what a line item or detail record represents].

**Context**: [How this captures snapshots, references, or calculations].

**Properties**:

- [Property 1]
- [Property 2]
- [Property 3]
- [Property 4]

**Examples**:

- "[Example showing quantity/count]"
- "[Example showing snapshot behavior]"
- "[Example showing calculation]"

**Code References**:

```[language]
interface [ItemName] {
  [field]: [type]
  [foreignKey]: [type]
  [foreignKey]: [type]
  [foreignKey]: [type]
  [field]: [type]
  [snapshotField]: [type]
  [calculatedField]: [type] // [Percentage/split description]
  [calculatedField]: [type] // [Percentage/split description]
}
```

## Business Concepts

### [Financial Concept 1]

**Definition**: [Definition of the financial value, balance, or amount].

**Context**: [When this is used, how it's validated, how it's updated].

**Properties**:

- [Storage format]
- [Constraints]
- [Update behavior]

**Examples**:

- "[Example showing current state]"
- "[Example showing validation]"
- "[Example showing calculation]"

**Code References**:

```[language]
interface [Entity] {
  [field]: [type] // [Note about storage format]
}

// In [business logic]
if ([entity].[field] < [threshold]) {
  throw new Error('[Error message]')
}
```

### [Financial Concept 2]

**Definition**: [Definition of fee, commission, or revenue split].

**Context**: [Your business model's revenue/fee structure].

**Examples**:

- "[Example showing fee percentage]"
- "[Example showing calculation with real numbers]"

**Code References**:

```[language]
const [fee] = [amount] * [percentage]
const [remainder] = [amount] * [percentage]
```

### [Inventory/Resource Concept]

**Definition**: [Definition of quantity, availability, or capacity].

**Context**: [How this is updated, constraints, validation].

**Examples**:

- "[Example showing available quantity]"
- "[Example showing unavailable state]"
- "[Example showing update]"

**Code References**:

```[language]
interface [Entity] {
  [field]: [type]
}

// Cannot [action] if [condition]
if ([entity].[field] === [threshold]) {
  throw new Error('[Error message]')
}
```

### [Status/State Concept]

**Definition**: [Definition of state, status, or condition that affects behavior or pricing].

**Values**:

- **[VALUE1]**: [Description of this state]
- **[VALUE2]**: [Description of this state]
- **[VALUE3]**: [Description of this state]
- **[VALUE4]**: [Description of this state]

**Examples**:

- "[Example showing specific state]"
- "[Example showing filtering by state]"
- "[Example showing impact on other properties]"

**Code References**:

```[language]
enum [EnumName] {
  [VALUE1] = '[VALUE1]',
  [VALUE2] = '[VALUE2]',
  [VALUE3] = '[VALUE3]',
  [VALUE4] = '[VALUE4]',
}
```

## Transaction Concepts

### [Transaction Process 1]

**Definition**: [Definition of the key transaction or conversion process].

**Context**: [Multi-step process description].

**Process**:

1. [Step 1]
2. [Step 2]
3. [Step 3]
4. [Step 4]
5. [Step 5]
6. [Step 6]
7. [Step 7]
8. [Step 8]

**Examples**:

- "[Example of initiating]"
- "[Example of failure]"
- "[Example of success]"

**Code References**:

```[language]
export async function [actionHandler]({ [params] }: [Type]) {
  // Validation and transaction logic
  const [result] = await [createFunction]([param], [param])
  return redirect(`[path]/${[result].[field]}`)
}
```

### [Transaction Process 2]

**Definition**: [Definition of fulfillment, processing, or delivery workflow].

**Context**: [Who handles what, what the stages are].

**Stages**:

1. [STAGE1]: [Description]
2. [STAGE2]: [Description]
3. [STAGE3]: [Description]
4. [STAGE4]: [Description]

**Examples**:

- "[Example showing ownership/responsibility]"
- "[Example showing tracking]"
- "[Example showing delegation]"

### [Atomic Operation]

**Definition**: [Definition of the atomic database operation].

**Context**: [Why atomicity matters, what must be consistent].

**Properties**:

- [Operation 1]
- [Operation 2]
- [Operation 3]
- [Operation 4]
- [All-or-nothing behavior]

**Examples**:

- "[Example of failure]"
- "[Example of success]"
- "[Example emphasizing atomicity]"

**Code References**:

```[language]
// Pseudo-code for transaction
await db.[transactionMethod](async (tx) => {
  const [record1] = await tx.[model].create([data])
  await tx.[model].update([id], { [field]: [newValue] })
  await tx.[model].updateMany([updates])
})
```

## Authentication Concepts

### [Auth Session Concept]

**Definition**: [Definition of session, token, or authentication state].

**Context**: [When created, how stored, how validated].

**Properties**:

- [Property 1]
- [Property 2]
- [Property 3]
- [Property 4]

**Examples**:

- "[Example of expiration]"
- "[Example of storage]"
- "[Example of validation]"

**Code References**:

```[language]
interface [SessionType] {
  [field]: [type]
  [field]: [type]
  [field]: [type]
  [field]: [type]
}
```

### [Authentication Process]

**Definition**: [Definition of the verification process].

**Context**: [When required, what it enables].

**Examples**:

- "[Example of requirement]"
- "[Example of failure]"
- "[Example of success]"

### [Authorization Concept]

**Definition**: [Definition of access control or permissions].

**Context**: [What rules apply, what constraints exist].

**Examples**:

- "[Example of access control]"
- "[Example of permission check]"

## UI/UX Concepts

### [Pagination Concept]

**Definition**: [Definition of how large datasets are divided].

**Context**: [Default page size, navigation behavior].

**Examples**:

- "[Example showing page indicator]"
- "[Example showing controls]"
- "[Example showing navigation]"

**Code References**:

```[language]
interface [PaginationType] {
  [field]: [type]
  [field]: [type]
  [field]: [type]
  [field]: [type]
}
```

### [Filter Concept]

**Definition**: [Definition of filtering mechanism].

**Context**: [What can be filtered, why it's useful].

**Examples**:

- "[Example of filtering by category]"
- "[Example of filtering by range]"
- "[Example of clearing]"

### [Search Concept]

**Definition**: [Definition of search functionality].

**Context**: [What is searched, how it works].

**Examples**:

- "[Example of search query]"
- "[Example of results]"
- "[Example of no results]"

## Price and Currency Concepts

### [Price Concept]

**Definition**: [Definition of price/cost and storage format].

**Context**: [Why stored this way, calculation implications].

**Examples**:

- "[Example showing storage format]"
- "[Example showing display format]"
- "[Example showing who sets it]"

**Code References**:

```[language]
// Always store as [storage format]
interface [Entity] {
  [field]: [type] // [conversion note]
}

// Format for display
function [formatFunction]([param]: [type]): [returnType] {
  return [formatting logic]
}
```

### [Revenue Concept]

**Definition**: [Definition of revenue and how it's split].

**Examples**:

- "[Example showing split calculation for party 1]"
- "[Example showing split calculation for party 2]"
- "[Example showing total]"

**Code References**:

```[language]
const [revenue1] = [calculation]
const [revenue2] = [total] - [revenue1]
```

## Platform Concepts

### [Platform/System Concept]

**Definition**: [Definition of platform, system, or category].

**Values**: [Value1], [Value2], [Value3], [Value4], [Value5], [Value6], etc.

**Context**: [How users interact with this concept].

**Examples**:

- "[Example showing specific platform]"
- "[Example showing filtering]"
- "[Example showing availability]"

**Code References**:

```[language]
interface [Entity] {
  [field]: [type] // [examples of values]
}
```

### [Category/Type Concept]

**Definition**: [Definition of category, type, or genre].

**Context**: [How this helps users or organizes data].

**Examples**:

- "[Example showing category]"
- "[Example showing browsing]"
- "[Example showing popular categories]"

## Technical Terms

### [Framework Concept 1]

**Definition**: [Definition of framework-specific concept like Loader, Controller, etc.].

**Context**: [When it runs, what it does].

**Examples**:

- "[Example of specific usage]"
- "[Example of execution context]"

**Code References**:

```[language]
export async function [functionName]({ [params] }: [Type]) {
  const [data] = await [fetchFunction]()
  return { [data] }
}
```

### [Framework Concept 2]

**Definition**: [Definition of another framework concept like Action, Mutation, etc.].

**Context**: [What operations it handles].

**Examples**:

- "[Example of specific usage]"
- "[Example of operation type]"

**Code References**:

```[language]
export async function [functionName]({ [params] }: [Type]) {
  const [data] = await [params].formData()
  // Process [data]
  return redirect('[path]')
}
```

### [Rendering Concept]

**Definition**: [Definition of rendering approach (SSR, CSR, etc.)].

**Context**: [Why it's used, what benefits it provides].

**Examples**:

- "[Example of feature benefit]"
- "[Example of configuration]"

## Anti-Patterns (Terms to Avoid)

### ❌ [Ambiguous Term 1]

**Use Instead**: [Preferred Term]

**Reason**: [Why the preferred term is better].

### ❌ [Ambiguous Term 2]

**Use Instead**: [Preferred Term]

**Reason**: [Why this is more specific or accurate].

### ❌ [Ambiguous Term 3]

**Use Instead**: [Preferred Term] for [use case 1], [Different Term] for [use case 2]

**Reason**: [Why disambiguation is important].

### ❌ [Vague Financial Term]

**Use Instead**: Be specific - "[Specific Term 1]" ([context]), "[Specific Term 2]" ([context]), "[Specific Term 3]" ([context])

**Reason**: [Why clarity prevents confusion].

### ❌ [Role/Entity Not In Domain]

**Use Instead**: [Current terms or note about future addition]

**Reason**: [Why this isn't part of current domain].

## Usage Guidelines

### In Code

- Use exact terminology from this document
- Variable names should match domain terms
- Comments should use domain language

```[language]
// Good
const [entity]: [EntityType] = await [fetchFunction]([id])
const [property] = [entity].[field]
const [calculated] = [calculateFunction]([collection].[items])

// Avoid
const [wrongTerm] = await [getFunction]([id])
const [wrongProperty] = [wrongEntity].[wrongField]
const [wrongCalculation] = [getTotal]([items])
```

### In Documentation

- Always capitalize domain terms ([Entity1], [Entity2], [Concept1], [Concept2])
- Use consistent terminology across all docs
- Define terms on first use

### In Conversations

- Use domain language in discussions
- Correct misuse of terms politely
- Refer to this document for clarification

### In Tests

- Test names should use domain language
- Mock objects should follow domain models

```[language]
// Good
describe('[Entity] [process name]', () => {
  it('creates [Result] when [Entity] has sufficient [Resource]', () => {
    // ...
  })
})

// Avoid
describe('[wrong term] [wrong process]', () => {
  it('makes [wrong term] when [wrong entity] has [wrong resource]', () => {
    // ...
  })
})
```

## Glossary Quick Reference

| Term               | Definition         | Code Type                 |
| ------------------ | ------------------ | ------------------------- |
| [Platform Name]    | [Short definition] | -                         |
| [Entity 1]         | [Short definition] | `[TypeName]`              |
| [Entity 2]         | [Short definition] | (ref in `[Type].[field]`) |
| [Concept 1]        | [Short definition] | `[TypeName]`              |
| [Concept 2]        | [Short definition] | `[TypeName]`              |
| [Concept 3]        | [Short definition] | `[TypeName]`              |
| [Concept 4]        | [Short definition] | `[TypeName]`              |
| [Financial 1]      | [Short definition] | `[primitiveType]`         |
| [Financial 2]      | [Short definition] | `[primitiveType]`         |
| [Resource Concept] | [Short definition] | `[primitiveType]`         |
| [Status Concept]   | [Short definition] | `[EnumType]`              |
| [Process 1]        | [Short definition] | [function type]           |
| [Process 2]        | [Short definition] | `[StatusEnumType]`        |
| [Auth Concept]     | [Short definition] | `[TypeName]`              |
| [Price]            | [Short definition] | `[primitiveType]`         |
| [Category 1]       | [Short definition] | `[primitiveType]`         |
| [Category 2]       | [Short definition] | `[primitiveType]`         |

## Domain Rules

### Business Rules (Always True)

1. [Rule about primary entity relationships]
2. [Rule about revenue/fee split]
3. [Rule about financial value storage and constraints]
4. [Rule about price storage and constraints]
5. [Rule about resource quantity constraints]
6. [Rule about total calculation]
7. [Rule about immutability of specific entities]
8. [Rule about temporary vs permanent data]
9. [Rule about authentication requirements]
10. [Rule about resource availability requirements]

### Technical Rules (Always True)

1. [Rule about monetary value storage format]
2. [Rule about ID format]
3. [Rule about date/timestamp storage]
4. [Rule about database transaction usage]
5. [Rule about password/credential storage]
6. [Rule about token/session properties]
7. [Rule about rendering approach]
8. [Rule about type safety or language features]

## Evolution of Language

This document is a living document. When new concepts are introduced:

1. **Discuss** the term with the team
2. **Define** it clearly with examples
3. **Document** it in this file
4. **Use** it consistently in code and conversation
5. **Refactor** old code to use new terminology when appropriate

### Change Log

**[YYYY-MM-DD]**: Initial version created

- Defined core entities: [Entity1], [Entity2], [Entity3]
- Defined business concepts: [Concept1], [Concept2], [Concept3]
- Established naming conventions
- Documented domain rules
