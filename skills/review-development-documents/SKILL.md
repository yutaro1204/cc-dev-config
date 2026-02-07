---
name: new-review-development-documents
description: Review development documents against implementation (technology and domain agnostic)
allowed-tools: Read, Write, Edit, Grep, Glob
---

# Generic Development Documents Review

This skill provides a comprehensive framework for reviewing development documentation against actual implementation. It is designed to be technology-agnostic and domain-agnostic, adaptable to any software project.

## How to Use This Skill

1. **Configure Project Context**: Before review, identify your project's specifics (see Configuration section)
2. **Select Review Perspectives**: Choose which document perspectives are relevant to your project
3. **Execute Review**: Follow the checklists adapted to your technology stack and domain
4. **Report Findings**: Use the standardized output format for each category
5. **Generate Review Report**: Write the comprehensive review results to `docs/DOCUMENTATION_REVIEW_REPORT.md`

## Review Report Format

The final review report (`docs/DOCUMENTATION_REVIEW_REPORT.md`) must include an **Overall Summary Table** at the beginning with the following columns:

| Document/Section       | DocumentationQuality                                          | ImplementationStatus                                          |
| ---------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- |
| Product Requirements   | ✅ Excellent / 👍 Good / ⚠️ Partial / ❌ Missing / ❓ Unclear | ✅ Excellent / 👍 Good / ⚠️ Partial / ❌ Missing / ❓ Unclear |
| Functional Design      | ...                                                           | ...                                                           |
| Architecture           | ...                                                           | ...                                                           |
| Ubiquitous Language    | ...                                                           | ...                                                           |
| Test Concepts          | ...                                                           | ...                                                           |
| Repository Structure   | ...                                                           | ...                                                           |
| Development Guidelines | ...                                                           | ...                                                           |
| Environments           | ...                                                           | ...                                                           |

**Column Definitions**:

- **DocumentationQuality**: Evaluates the quality, completeness, and clarity of the documentation itself
  - ✅ **Excellent**: Documentation is comprehensive, clear, and well-structured
  - 👍 **Good**: Documentation is adequate with minor gaps or unclear areas
  - ⚠️ **Partial**: Documentation exists but has significant gaps or unclear sections
  - ❌ **Missing**: Documentation is absent or severely incomplete
  - ❓ **Unclear**: Cannot assess documentation quality

- **ImplementationStatus**: Evaluates how well the actual implementation matches the documentation
  - ✅ **Excellent**: Implementation fully matches documentation, no discrepancies
  - 👍 **Good**: Implementation mostly matches with minor deviations
  - ⚠️ **Partial**: Significant gaps between documentation and implementation
  - ❌ **Missing**: Documentation describes features/patterns that are not implemented
  - ❓ **Unclear**: Cannot determine implementation status

After the summary table, provide detailed findings for each section as specified in the review output formats below.

## Project Configuration

Before starting the review, identify the following about your project:

### Technology Stack

- **Frontend Framework**: [e.g., React, Vue, Angular, Svelte, vanilla JS]
- **Backend Framework**: [e.g., Express, FastAPI, Django, Spring Boot, Ruby on Rails]
- **Data Layer**: [e.g., Prisma, TypeORM, Sequelize, raw SQL, MongoDB]
- **Routing System**: [e.g., React Router, Next.js App Router, Express routes]
- **State Management**: [e.g., Redux, Zustand, Context API, Pinia, none]
- **Type System**: [e.g., TypeScript, Flow, JSDoc, none]

### Domain Context

- **Core Domain**: [e.g., e-commerce, healthcare, education, finance]
- **Primary Entities**: [list 3-5 main business entities, e.g., User, Product, Order]
- **Key Workflows**: [list 2-4 main business processes, e.g., checkout, appointment booking]

### Documentation Structure

- **Product Requirements**: Path to business requirements document
- **Functional Design**: Path to functional specifications document
- **Architecture**: Path to technical architecture document
- **Ubiquitous Language**: Path to domain terminology document (if exists)
- **Other Docs**: List any additional relevant documentation

---

# 1. Product Requirements Review

Review product requirements document against technical architecture to ensure business needs are technically supported.

## 1.1. Business Goals Alignment

**Objective**: Verify that technical architecture enables business objectives

- [ ] Architecture supports all stated business objectives
- [ ] Technical decisions enable business value delivery
- [ ] Revenue/monetization model (if any) is technically feasible
- [ ] Market positioning is supported by technology choices
- [ ] Time-to-market requirements are achievable with chosen stack
- [ ] Competitive advantages are technically enabled

**Generic Patterns to Check**:

- Business metrics are measurable with current technical design
- Technology choices align with business constraints (budget, team skills, time)
- Technical debt strategy balances speed with quality

## 1.2. Feature Requirements Support

**Objective**: Ensure all required features are architecturally possible

- [ ] All core features listed in requirements have architectural support
- [ ] Feature scalability matches business growth expectations
- [ ] Technology stack enables required development velocity
- [ ] Third-party integrations are properly planned
- [ ] Feature dependencies are clearly defined in architecture
- [ ] Feature priorities align with technical implementation order

**Generic Patterns to Check**:

- Each feature in requirements has corresponding technical component/module
- External dependencies (APIs, services) are identified
- Feature interactions and data flows are documented

## 1.3. User Experience Requirements

**Objective**: Validate that UX requirements are achievable with technical stack

- [ ] Performance requirements are architecturally achievable (load times, response times)
- [ ] Responsive design is supported by frontend technology
- [ ] Accessibility requirements can be met with chosen frameworks
- [ ] Target device support (mobile, tablet, desktop) is addressed
- [ ] Progressive enhancement strategy exists (if applicable)
- [ ] Offline capabilities (if required) are architected

**Generic Patterns to Check**:

- Performance budgets are defined and measurable
- Accessibility standards (WCAG, ARIA) are technically supported
- Client-side/server-side rendering strategy matches UX needs

## 1.4. Functional Requirements Coverage

**Objective**: Verify all functional capabilities are architecturally defined

- [ ] User authentication/authorization architecture is defined
- [ ] Core CRUD operations for main entities are supported
- [ ] Business workflow processing is architecturally sound
- [ ] Data validation and business rules can be enforced
- [ ] Search and filtering requirements are met
- [ ] User management capabilities exist (if applicable)
- [ ] Notification/communication mechanisms are defined

**Generic Patterns to Check**:

- For each functional requirement, verify corresponding architectural component
- Data flow diagrams support functional requirements
- API contracts or service interfaces are defined

## 1.5. Non-Functional Requirements

**Objective**: Ensure quality attributes are addressed in architecture

### Performance

- [ ] Response time targets match architecture capabilities
- [ ] Throughput requirements (requests/second) are addressed
- [ ] Resource usage constraints (CPU, memory) are considered
- [ ] Database query performance strategy exists
- [ ] Caching strategy (if needed) is defined

### Scalability

- [ ] Horizontal/vertical scaling strategies address growth projections
- [ ] Load balancing approach is defined (if needed)
- [ ] Database scaling strategy exists
- [ ] Stateless/stateful component separation is clear

### Availability

- [ ] Uptime requirements (SLA) are addressed
- [ ] Redundancy and failover strategies exist
- [ ] Disaster recovery plan is defined
- [ ] Health monitoring and alerting are planned

### Reliability

- [ ] Backup and recovery strategies exist
- [ ] Data durability requirements are met
- [ ] Error handling and recovery mechanisms are defined
- [ ] Transaction integrity is ensured (ACID properties where needed)

### Security

- [ ] Authentication mechanisms meet security standards
- [ ] Authorization and access control are defined
- [ ] Data encryption (at rest, in transit) is addressed
- [ ] Input validation and sanitization are planned
- [ ] Security vulnerability scanning is included
- [ ] Secrets management strategy exists

### Maintainability

- [ ] Code organization supports long-term maintenance
- [ ] Testing strategy is comprehensive
- [ ] Documentation standards are defined
- [ ] Dependency management approach is clear
- [ ] Versioning strategy exists

### Observability

- [ ] Logging strategy meets operational needs
- [ ] Monitoring and metrics collection is defined
- [ ] Distributed tracing (if needed) is planned
- [ ] Alerting thresholds and escalation are defined
- [ ] Debugging capabilities are built in

## 1.6. Data Requirements

**Objective**: Validate data modeling supports all business needs

- [ ] Data model includes all entities from requirements
- [ ] Data relationships and cardinality are properly modeled
- [ ] Data validation rules are enforceable
- [ ] Data retention and archival policies are architecturally supported
- [ ] Reporting and analytics data needs are addressed
- [ ] Data migration and seeding strategies exist
- [ ] Data privacy and compliance requirements are met

**Generic Patterns to Check**:

- Entity-relationship diagram matches requirements
- Data integrity constraints are defined
- Data access patterns support use cases

## 1.7. Integration Requirements

**Objective**: Ensure all external integrations are planned

- [ ] Third-party service integrations are documented
- [ ] API contracts for external systems are defined
- [ ] Authentication methods for integrations are specified
- [ ] Error handling for external failures is planned
- [ ] Rate limiting and quota management are addressed
- [ ] Data synchronization strategies exist (if needed)
- [ ] Webhook/callback mechanisms are defined (if needed)

**Generic Patterns to Check**:

- Each external dependency is listed with purpose
- Fallback strategies for integration failures exist
- Integration testing approach is defined

## 1.8. User Roles and Permissions

**Objective**: Verify all user roles are architecturally supported

- [ ] All user roles from requirements are in data model
- [ ] Role-based access control (RBAC) is architecturally defined
- [ ] Permission hierarchies and inheritance are implemented
- [ ] Privilege escalation controls are secured
- [ ] Multi-tenancy (if required) is architecturally supported
- [ ] Role management workflows are defined

**Generic Patterns to Check**:

- Permission model covers all protected resources
- Authorization checks are consistently applied
- Role changes and auditing are supported

## 1.9. Platform and Device Support

**Objective**: Validate platform requirements are met

- [ ] Target platform compatibility requirements are addressed
- [ ] Browser/client compatibility is defined
- [ ] Mobile responsiveness is built into frontend architecture
- [ ] Native app support (if required) is planned
- [ ] Cross-platform testing strategy is defined
- [ ] Platform-specific optimizations are documented

## 1.10. Compliance and Legal Requirements

**Objective**: Ensure regulatory compliance is architecturally addressed

- [ ] Data privacy regulations (GDPR, CCPA, etc.) are addressed
- [ ] Industry-specific compliance (PCI-DSS, HIPAA, etc.) is considered
- [ ] Terms of service and privacy policy mechanisms exist
- [ ] Consent management (cookies, tracking) is supported
- [ ] Data export and deletion capabilities exist
- [ ] Audit logging for compliance is defined
- [ ] Age/jurisdiction verification (if required) is architected

**Generic Patterns to Check**:

- Personally Identifiable Information (PII) is identified and protected
- Data retention policies are enforceable
- Compliance auditing mechanisms exist

## 1.11. Communication Requirements

**Objective**: Verify notification and communication capabilities

- [ ] Email notification system is architected (if needed)
- [ ] SMS notifications (if required) are planned
- [ ] In-app notifications are supported (if needed)
- [ ] Push notifications (if required) are defined
- [ ] Real-time communication (chat, websockets) is architected (if needed)
- [ ] Notification preferences and opt-out mechanisms exist
- [ ] Communication templates and localization are planned

## 1.12. Localization and Internationalization

**Objective**: Validate multi-language and regional support

- [ ] Multi-language support (if required) is architected
- [ ] Currency handling and conversion is defined (if applicable)
- [ ] Timezone handling is addressed
- [ ] Regional variations are supported (if needed)
- [ ] Date/time formatting follows locale conventions
- [ ] Content translation workflows are defined
- [ ] Right-to-left (RTL) languages supported (if needed)

## 1.13. Analytics and Reporting

**Objective**: Ensure data collection and reporting capabilities exist

- [ ] User behavior tracking is architecturally supported (if needed)
- [ ] Business intelligence requirements are met
- [ ] Admin dashboards and reporting are planned
- [ ] Custom reports and data export are possible
- [ ] Real-time vs. batch analytics strategy is defined
- [ ] A/B testing capabilities (if required) exist
- [ ] Analytics privacy and consent are addressed

## Review Output Format

For each category above, provide:

1. **Status**:
   - ✅ **Excellent**: Requirement is completely and properly addressed in architecture
   - 👍 **Good**: Requirement is adequately addressed with minor areas for improvement
   - ⚠️ **Partial**: Some aspects addressed, but significant gaps exist
   - ❌ **Missing**: Requirement is not addressed in architecture
   - ❓ **Unclear**: Cannot determine support from documentation

2. **Findings**: Specific gaps, concerns, or observations

3. **Evidence**: References to specific sections in architecture document

4. **Recommendations**: Concrete actions to address gaps

5. **Priority**:
   - **Critical**: Must be addressed before launch
   - **High**: Should be addressed soon
   - **Medium**: Should be planned
   - **Low**: Nice to have

---

# 2. Functional Design Review

Review functional design document against actual implementation to ensure specifications match reality.

## 2.1. Routing System Implementation

**Objective**: Verify all documented routes exist and are correctly configured

### Route Existence

- [ ] All routes documented in functional design exist in codebase
- [ ] Route paths match documentation exactly
- [ ] Route hierarchy and nesting are correctly implemented
- [ ] Dynamic route segments match documentation (e.g., `:id`, `[slug]`)
- [ ] Catch-all/wildcard routes (if any) are implemented
- [ ] Redirects and aliases are correctly configured

**Generic Patterns to Check**:

- Find routing configuration file(s) based on framework:
  - React Router: `routes.ts`, route files in `routes/` directory
  - Next.js: `app/` or `pages/` directory structure
  - Express: route definitions in server files
  - Vue Router: `router/index.ts`
  - Other frameworks: consult framework documentation
- Compare documented routes against actual route definitions
- Verify route parameters and query string handling

### Route Configuration

- [ ] Loaders/data fetchers match documentation
- [ ] Actions/mutations match documentation
- [ ] Middleware/guards match documentation (auth, validation)
- [ ] Route metadata (titles, meta tags) match documentation
- [ ] Error boundaries are correctly configured
- [ ] Loading states are implemented as designed

**Generic Patterns to Check**:

- Each route has necessary data fetching logic
- Protected routes have appropriate access control
- Form submissions are handled by documented actions

### Route Type Safety

- [ ] Routes use framework's type-safe patterns (if applicable)
- [ ] Route parameters are properly typed
- [ ] Data fetcher return types match component expectations
- [ ] Action input/output types are defined

**Framework-Specific Checks**:

- TypeScript projects: Verify type definitions exist for all routes
- Dynamic routing: Check type guards for route parameters

## 2.2. Component Architecture

**Objective**: Ensure UI component structure matches functional design

### Component Existence

- [ ] All documented components exist in codebase
- [ ] Component file locations match documented structure
- [ ] Component naming follows documented conventions
- [ ] All sub-components are implemented

**Generic Patterns to Check**:

- Search for component files by name
- Verify component exports match documentation
- Check component file organization (flat vs. nested)

### Layout Components

- [ ] Root layout component exists
- [ ] Shared layouts (if any) are implemented
- [ ] Layout composition matches documentation:
  - Header/navigation
  - Main content area
  - Footer
  - Sidebars (if applicable)
  - Modal/overlay areas (if applicable)

### Feature Components

- [ ] All feature-specific components are implemented
- [ ] Component hierarchy matches documentation
- [ ] Component responsibilities match documented scope
- [ ] Shared components are properly reused

### UI/Design System Components

- [ ] Button components with documented variants
- [ ] Form components (inputs, selects, checkboxes, etc.)
- [ ] Card/panel components
- [ ] Modal/dialog components
- [ ] Navigation components (tabs, menus, breadcrumbs)
- [ ] Feedback components (toasts, alerts, loading indicators)
- [ ] Data display components (tables, lists, grids)

**Generic Patterns to Check**:

- Component props match documented interfaces
- Component variants/modes are implemented
- Accessibility attributes are present

### Component Hierarchy

- [ ] Parent-child relationships match documentation
- [ ] Component composition follows documented patterns
- [ ] Props drilling vs. context usage matches design
- [ ] State management integration is correct

## 2.3. Data Model Implementation

**Objective**: Verify data models match functional design specifications

### Entity Models

- [ ] All documented entities have corresponding models/schemas
- [ ] Entity fields match documentation (names, types, constraints)
- [ ] Required vs. optional fields match specifications
- [ ] Default values are correctly set
- [ ] Field validation rules are implemented

**Generic Patterns to Check**:

- Locate data model definitions:
  - ORM models (Prisma schema, TypeORM entities, Sequelize models)
  - Database schema files (migrations, SQL)
  - TypeScript interfaces/types
  - GraphQL schema (if applicable)
- Compare each field against functional design
- Verify field types are correct (string, number, date, boolean, etc.)

### Relationships

- [ ] One-to-many relationships are correctly defined
- [ ] Many-to-many relationships have proper join tables
- [ ] One-to-one relationships are correctly constrained
- [ ] Foreign key constraints match documentation
- [ ] Cascade behaviors (delete, update) are correct
- [ ] Inverse relationships are defined (if applicable)

### Enums and Constants

- [ ] All documented enums exist in code
- [ ] Enum values match documentation exactly
- [ ] Enum naming follows conventions
- [ ] Type-safe enum usage (TypeScript enums, union types, etc.)

**Generic Patterns to Check**:

- Search for enum definitions in codebase
- Verify enum values used in models
- Check database-level enum constraints (if applicable)

### Indexes and Performance

- [ ] Documented indexes are created
- [ ] Unique constraints are applied where specified
- [ ] Composite indexes match documentation
- [ ] Full-text search indexes (if applicable) are configured

### Timestamps and Metadata

- [ ] Created timestamp exists (createdAt, created_at)
- [ ] Updated timestamp exists (updatedAt, updated_at)
- [ ] Soft delete timestamp (deletedAt) if required
- [ ] Version fields if optimistic locking is used
- [ ] Audit fields (createdBy, updatedBy) if required

## 2.4. API Implementation

**Objective**: Ensure all API endpoints match functional design specifications

### Endpoint Existence

- [ ] All documented API endpoints exist
- [ ] HTTP methods match documentation (GET, POST, PUT, PATCH, DELETE)
- [ ] Endpoint paths match exactly
- [ ] Path parameters are correctly defined
- [ ] Query parameters are supported

**Generic Patterns to Check**:

- Locate API route definitions:
  - Express: `app.get()`, `router.post()`, etc.
  - Next.js: API routes in `app/api/` or `pages/api/`
  - FastAPI: `@app.get()`, `@app.post()`, etc.
  - Framework-specific routing files
- Search codebase for route definitions
- Create list of all endpoints and compare to documentation

### Request Handling

- [ ] Request body schemas match documentation
- [ ] Request validation is implemented
- [ ] Authentication/authorization checks are present
- [ ] Content-Type handling is correct (JSON, multipart/form-data, etc.)
- [ ] Rate limiting is applied where specified

### Response Format

- [ ] Response structure matches documentation
- [ ] HTTP status codes match specifications
- [ ] Response headers are correct (Content-Type, Cache-Control, etc.)
- [ ] Pagination format matches documentation (if applicable)
- [ ] Error responses follow documented format

**Generic Patterns to Check**:

- Verify response shape for success cases
- Verify error response format
- Check status codes: 200, 201, 400, 401, 403, 404, 500, etc.

### Data Serialization

- [ ] Dates are formatted as documented (ISO 8601, timestamps, etc.)
- [ ] Numeric precision matches specifications
- [ ] Null vs. undefined handling is consistent
- [ ] Nested objects/arrays match documentation
- [ ] Sensitive data is excluded from responses

### Authentication & Authorization

- [ ] Protected endpoints require authentication
- [ ] Role-based access control is enforced
- [ ] Token validation is implemented
- [ ] Session management matches design
- [ ] OAuth/SSO flows (if any) are correct

## 2.5. Business Logic Services

**Objective**: Verify business logic implementation matches functional design

### Service Layer Organization

- [ ] Service modules exist for each domain area
- [ ] Service responsibilities match documentation
- [ ] Service methods match documented business operations
- [ ] Service dependencies are correctly injected

**Generic Patterns to Check**:

- Locate service/business logic files:
  - Service classes
  - Use case files
  - Domain logic modules
- Verify separation of concerns (controllers vs. services vs. data access)

### Business Rules Enforcement

- [ ] All documented business rules are implemented
- [ ] Validation logic matches specifications
- [ ] Calculations and formulas are correct
- [ ] State transitions follow documented workflows
- [ ] Constraints are enforced (min/max, required combinations, etc.)

**Examples of Business Rules to Check**:

- Monetary calculations (discounts, tax, totals)
- Inventory/availability rules
- User permission rules
- Workflow state machines
- Quota/limit enforcement

### Transaction Management

- [ ] Database transactions are used where needed
- [ ] ACID properties are maintained for critical operations
- [ ] Rollback logic is implemented for failures
- [ ] Distributed transactions (if needed) are handled
- [ ] Idempotency is ensured where required

### External Service Integration

- [ ] Third-party API calls are implemented as documented
- [ ] Error handling for external failures is robust
- [ ] Retry logic is implemented where specified
- [ ] Circuit breakers (if needed) are configured
- [ ] Fallback behaviors are defined

## 2.6. State Management

**Objective**: Ensure client-side state management matches design

### State Structure

- [ ] Global state shape matches documentation
- [ ] Local component state is used appropriately
- [ ] State normalization follows documented approach
- [ ] State persistence (localStorage, sessionStorage) matches design

**Generic Patterns to Check**:

- Identify state management solution:
  - Redux: store, slices, reducers, actions
  - Zustand: stores
  - Context API: context providers
  - MobX: observables
  - Component state: useState, useReducer
- Verify state shape and organization

### State Updates

- [ ] State update logic matches functional specifications
- [ ] Optimistic updates are implemented where designed
- [ ] State synchronization with backend is correct
- [ ] Derived state is computed as documented

### Side Effects

- [ ] Async operations (API calls) are handled correctly
- [ ] Side effect management matches design (useEffect, middleware, etc.)
- [ ] Error handling for async operations is robust
- [ ] Loading states are properly managed

## 2.7. Type Definitions

**Objective**: Verify type safety matches functional design (for typed languages)

### Interface and Type Definitions

- [ ] All documented interfaces exist in code
- [ ] Interface properties match documentation
- [ ] Type constraints are correctly applied
- [ ] Generic types are properly used
- [ ] Union and intersection types match specifications

**Generic Patterns to Check** (TypeScript/Flow):

- Search for `interface` and `type` definitions
- Verify types are exported and reused
- Check type imports across modules

### Component Prop Types

- [ ] Component props are properly typed
- [ ] Required vs. optional props match design
- [ ] Prop validation is implemented (TypeScript, PropTypes, etc.)
- [ ] Default props are correctly typed

### API Contract Types

- [ ] Request types match API documentation
- [ ] Response types match API documentation
- [ ] Shared types between frontend/backend exist
- [ ] API client is fully typed

### Type Generation

- [ ] Generated types (from GraphQL, OpenAPI, etc.) are up to date
- [ ] Generated types match functional design
- [ ] Type generation scripts are documented

## 2.8. User Flow Validation

**Objective**: Verify user workflows are correctly implemented

### Core User Flows

For each documented user flow:

- [ ] All steps in the flow are implemented
- [ ] Navigation between steps is correct
- [ ] Data persistence across steps is correct
- [ ] Validation occurs at documented checkpoints
- [ ] Error states and recovery paths exist
- [ ] Success paths lead to documented outcomes

**Generic Flow Validation Process**:

1. Identify all documented user flows (e.g., signup, checkout, booking)
2. For each flow, trace through code from start to finish
3. Verify each step exists and functions correctly
4. Check edge cases and error handling

### User Flow Examples to Check

- **Authentication flows**: Signup, login, logout, password reset
- **Core workflows**: Create/edit/delete primary entities
- **Multi-step processes**: Checkout, onboarding, booking, application submission
- **Profile management**: View/edit profile, change settings
- **Data browsing**: List, filter, sort, search, detail view

## 2.9. UI/UX Implementation

**Objective**: Ensure user interface matches functional design specifications

### Visual Design Fidelity

- [ ] Wireframes/mockups are accurately implemented
- [ ] Spacing and layout match design specifications
- [ ] Color scheme matches design system
- [ ] Typography (fonts, sizes, weights) matches design
- [ ] Icons and imagery match specifications

### Responsive Design

- [ ] Mobile breakpoints are correctly implemented
- [ ] Tablet breakpoints are correctly implemented
- [ ] Desktop layouts match design
- [ ] Touch targets are appropriately sized for mobile
- [ ] Responsive images are optimized

### Interactive Elements

- [ ] Button states (hover, active, disabled) are implemented
- [ ] Form field states (focus, error, success) are styled
- [ ] Loading indicators appear as designed
- [ ] Animations and transitions match specifications
- [ ] Modal/overlay behaviors are correct

### Accessibility

- [ ] Semantic HTML is used correctly
- [ ] ARIA attributes are present where needed
- [ ] Keyboard navigation is supported
- [ ] Focus indicators are visible
- [ ] Color contrast meets standards (WCAG)
- [ ] Screen reader compatibility is ensured

## 2.10. Validation and Error Handling

**Objective**: Verify input validation and error handling match specifications

### Client-Side Validation

- [ ] All form validations are implemented
- [ ] Validation rules match documentation (required, min/max, pattern, etc.)
- [ ] Validation timing matches design (onBlur, onChange, onSubmit)
- [ ] Validation error messages match specifications
- [ ] Multi-field validation (e.g., password confirmation) works correctly

### Server-Side Validation

- [ ] All inputs are validated on server
- [ ] Validation rules match documentation
- [ ] Validation errors are returned in documented format
- [ ] Security validations are in place (XSS, SQL injection prevention)

### Error Handling

- [ ] All error scenarios are handled
- [ ] Error messages are user-friendly and match design
- [ ] Technical errors are logged appropriately
- [ ] Error boundaries prevent app crashes (React/Vue)
- [ ] Network errors are handled gracefully
- [ ] Retry mechanisms are implemented where specified

## 2.11. API Response Format Consistency

**Objective**: Ensure API responses follow documented standards

### Standard Response Structure

- [ ] Success responses have consistent structure
- [ ] Error responses have consistent structure
- [ ] Response envelope matches documentation
- [ ] Metadata fields are consistent (timestamp, version, etc.)

### Data Serialization

- [ ] Date formats are consistent across all endpoints
- [ ] Number formats match specifications (decimals, integers)
- [ ] Boolean representations are consistent
- [ ] Null handling is consistent
- [ ] Array responses are consistently formatted

### Pagination

- [ ] Pagination parameters match documentation (limit, offset, page)
- [ ] Pagination metadata is included (total, hasNext, etc.)
- [ ] Pagination format is consistent across all list endpoints

### Filtering and Sorting

- [ ] Query parameter format matches documentation
- [ ] Supported filters match specifications
- [ ] Sorting parameters work as documented
- [ ] Filter combinations are supported

## 2.12. Security Implementation

**Objective**: Verify security measures match functional design

### Authentication Security

- [ ] Password storage uses proper hashing (bcrypt, argon2, etc.)
- [ ] Token generation is secure (JWT, sessions, etc.)
- [ ] Token expiration is configured as documented
- [ ] Password reset flows are secure
- [ ] Account lockout after failed attempts (if specified)

### Authorization

- [ ] Permission checks are consistently applied
- [ ] Role-based access control is enforced
- [ ] Resource ownership is verified before access
- [ ] Privilege escalation is prevented

### Input Sanitization

- [ ] User inputs are sanitized
- [ ] XSS prevention is implemented
- [ ] SQL injection prevention is implemented
- [ ] Path traversal prevention is implemented
- [ ] File upload restrictions are enforced

### Data Protection

- [ ] Sensitive data is encrypted in transit (HTTPS)
- [ ] Sensitive data is encrypted at rest (if specified)
- [ ] PII is protected and audited
- [ ] Secrets are not exposed in responses
- [ ] CORS configuration is correct

## 2.13. Database Constraints and Business Rules

**Objective**: Ensure database-level enforcement matches design

### Database Constraints

- [ ] NOT NULL constraints are applied where required
- [ ] UNIQUE constraints match specifications
- [ ] CHECK constraints enforce business rules (if applicable)
- [ ] Foreign key constraints are properly defined
- [ ] Default values are set correctly

### Business Rules Enforcement

- [ ] Immutable fields cannot be changed
- [ ] Calculated fields are computed correctly
- [ ] Triggers (if used) implement documented logic
- [ ] Stored procedures (if used) match specifications

### Transaction Integrity

- [ ] Critical operations use transactions
- [ ] Isolation levels are appropriately set
- [ ] Deadlock prevention strategies are implemented
- [ ] Data consistency is maintained

## 2.14. Cross-Document Consistency

**Objective**: Ensure functional design aligns with other documentation

### Product Requirements Alignment

- [ ] All features in product requirements are in functional design
- [ ] Feature priorities match
- [ ] User roles and permissions are consistent

### Architecture Alignment

- [ ] Component structure matches architectural diagram
- [ ] Data flow matches architecture
- [ ] Technology stack usage is consistent

### API Documentation Alignment

- [ ] API endpoints in functional design match API docs (OpenAPI, etc.)
- [ ] Request/response formats are consistent
- [ ] Authentication methods are consistent

## Review Output Format

For each section, provide:

1. **Status**: ✅ Excellent | 👍 Good | ⚠️ Partial | ❌ Missing | ❓ Unclear

2. **Findings**: Specific discrepancies or issues

3. **Code References**: File paths and line numbers demonstrating findings

4. **Recommendations**: Actions to resolve discrepancies

5. **Priority**: Critical | High | Medium | Low

---

# 3. Architecture Review

Review technical architecture document for completeness, consistency, and best practices.

## 3.1. Architecture Overview

**Objective**: Verify high-level architecture is clearly documented

- [ ] System architecture diagram exists and is clear
- [ ] Architecture style is clearly stated (monolith, microservices, serverless, etc.)
- [ ] Technology stack is fully documented
- [ ] Deployment architecture is described
- [ ] Key architectural decisions are documented (ADRs if available)

## 3.2. Component Architecture

**Objective**: Ensure component structure is well-defined

- [ ] All major components/modules are identified
- [ ] Component responsibilities are clearly defined
- [ ] Component interactions are documented
- [ ] Layer separation is clear (presentation, business, data)
- [ ] Dependency directions follow best practices
- [ ] Component reusability is addressed

## 3.3. Data Architecture

**Objective**: Verify data layer design is comprehensive

- [ ] Database technology is specified and justified
- [ ] Data model is documented (ERD or similar)
- [ ] Data access patterns are described
- [ ] Caching strategy is defined (if applicable)
- [ ] Data migration strategy exists
- [ ] Backup and recovery are addressed

### Database Design

- [ ] Normalization strategy is clear
- [ ] Denormalization decisions are justified
- [ ] Index strategy is documented
- [ ] Partitioning/sharding strategy exists (if needed)

### Data Flow

- [ ] Data flow diagrams exist for key processes
- [ ] Data transformations are documented
- [ ] Data consistency strategies are defined
- [ ] Event sourcing or CQRS patterns (if used) are explained

## 3.4. API Architecture

**Objective**: Ensure API design is comprehensive

- [ ] API style is defined (REST, GraphQL, gRPC, etc.)
- [ ] API versioning strategy is documented
- [ ] Authentication mechanism is specified
- [ ] Authorization model is defined
- [ ] Rate limiting strategy is documented
- [ ] API documentation approach is specified (OpenAPI, etc.)

### API Design Patterns

- [ ] Endpoint naming conventions are consistent
- [ ] HTTP methods are used correctly
- [ ] Status codes are used appropriately
- [ ] Error response format is standardized
- [ ] Pagination strategy is defined

## 3.5. Security Architecture

**Objective**: Verify security measures are comprehensive

- [ ] Authentication methods are documented
- [ ] Authorization model is clearly defined
- [ ] Data encryption strategy is specified (at rest and in transit)
- [ ] Secret management approach is documented
- [ ] Security headers are configured
- [ ] Input validation strategy is defined
- [ ] OWASP Top 10 vulnerabilities are addressed

### Security Checklist

- [ ] XSS prevention
- [ ] CSRF protection
- [ ] SQL injection prevention
- [ ] Secure session management
- [ ] Secure password handling
- [ ] API authentication
- [ ] Rate limiting and DDoS protection

## 3.6. Performance Architecture

**Objective**: Ensure performance considerations are addressed

- [ ] Performance requirements are stated (latency, throughput)
- [ ] Caching strategy is comprehensive (client, CDN, application, database)
- [ ] Database query optimization is addressed
- [ ] Asset optimization is described (minification, compression, etc.)
- [ ] Lazy loading strategies are defined
- [ ] Code splitting is planned (if applicable)

### Performance Monitoring

- [ ] Performance metrics are defined
- [ ] Monitoring tools are specified
- [ ] Performance testing strategy exists
- [ ] Performance budgets are set

## 3.7. Scalability Architecture

**Objective**: Verify scalability strategy is clear

- [ ] Scaling strategy is defined (vertical, horizontal, auto-scaling)
- [ ] Stateless vs. stateful components are identified
- [ ] Load balancing approach is documented
- [ ] Database scaling strategy exists
- [ ] Message queue/async processing is architected (if needed)
- [ ] Microservices decomposition (if applicable) is justified

## 3.8. Reliability and Resilience

**Objective**: Ensure system reliability is addressed

- [ ] Error handling strategy is comprehensive
- [ ] Retry mechanisms are defined
- [ ] Circuit breaker patterns (if needed) are documented
- [ ] Graceful degradation is planned
- [ ] Health check endpoints exist
- [ ] Disaster recovery plan is documented
- [ ] Backup strategy is defined

### High Availability

- [ ] Redundancy strategy is documented
- [ ] Failover mechanisms are defined
- [ ] Data replication is addressed
- [ ] Zero-downtime deployment is planned

## 3.9. Observability Architecture

**Objective**: Verify monitoring and debugging capabilities

- [ ] Logging strategy is comprehensive
  - Log levels are defined
  - Log aggregation is specified
  - Structured logging is used
- [ ] Monitoring strategy is clear
  - Metrics collection is defined
  - Alerting rules are specified
  - Dashboards are planned
- [ ] Tracing strategy exists (for distributed systems)
- [ ] Error tracking is configured

## 3.10. Development and Build Architecture

**Objective**: Ensure development workflow is clear

- [ ] Development environment setup is documented
- [ ] Build process is automated
- [ ] Dependency management is clear
- [ ] Version control strategy is defined
- [ ] Code review process is documented
- [ ] Testing strategy is comprehensive

### CI/CD Pipeline

- [ ] Continuous Integration is configured
- [ ] Continuous Deployment pipeline is documented
- [ ] Environment promotion strategy is clear
- [ ] Rollback procedures are defined
- [ ] Deployment strategies are specified (blue-green, canary, etc.)

## 3.11. Testing Architecture

**Objective**: Verify testing strategy is comprehensive

- [ ] Testing pyramid is followed (unit, integration, e2e)
- [ ] Unit testing approach is documented
- [ ] Integration testing strategy is defined
- [ ] End-to-end testing approach is specified
- [ ] Performance testing is planned
- [ ] Security testing is included
- [ ] Test data management strategy exists

## 3.12. Third-Party Services and Dependencies

**Objective**: Ensure external dependencies are documented

- [ ] All third-party services are listed
- [ ] Service purposes are documented
- [ ] Alternatives are considered
- [ ] Vendor lock-in risks are assessed
- [ ] Service-level agreements (SLAs) are documented
- [ ] Cost implications are noted
- [ ] Fallback strategies exist for service failures

## 3.13. Infrastructure Architecture

**Objective**: Verify infrastructure is well-planned

- [ ] Hosting platform is specified (cloud, on-premise, hybrid)
- [ ] Infrastructure as Code (IaC) approach is documented
- [ ] Network architecture is diagrammed
- [ ] Security groups/firewall rules are defined
- [ ] CDN strategy is documented (if applicable)
- [ ] DNS configuration is specified

### Cloud Architecture (if applicable)

- [ ] Cloud provider is specified and justified
- [ ] Service choices are documented (compute, storage, database, etc.)
- [ ] Multi-region strategy is defined (if needed)
- [ ] Cost optimization strategies are noted

## 3.14. Documentation and Knowledge Management

**Objective**: Ensure documentation strategy is clear

- [ ] Code documentation standards are defined
- [ ] API documentation approach is specified
- [ ] Architecture Decision Records (ADRs) process exists
- [ ] Runbooks for operational tasks are planned
- [ ] Onboarding documentation exists

## Review Output Format

For each section, provide:

1. **Status**: ✅ Excellent | 👍 Good | ⚠️ Partial | ❌ Missing | ❓ Unclear

2. **Findings**: Gaps or areas needing clarification

3. **Best Practices**: Industry standards that should be considered

4. **Recommendations**: Specific improvements to documentation or architecture

5. **Priority**: Critical | High | Medium | Low

---

# 4. Ubiquitous Language Review

Review domain terminology document (ubiquitous language) for consistency across codebase.

## 4.1. Terminology Definition

**Objective**: Ensure domain terms are clearly defined

- [ ] All core domain concepts are defined
- [ ] Definitions are clear and unambiguous
- [ ] Terms are organized logically
- [ ] Synonyms and aliases are documented
- [ ] Terms to avoid are listed
- [ ] Glossary format is easy to reference

## 4.2. Terminology Usage in Code

**Objective**: Verify code uses domain terminology consistently

### Naming Conventions

- [ ] Variable names use documented domain terms
- [ ] Function names follow domain language
- [ ] Class/interface names match domain concepts
- [ ] Database tables/columns use consistent terminology
- [ ] API endpoint paths follow domain language
- [ ] Constants and enums use domain terms

**Generic Patterns to Check**:

- Search codebase for domain terms
- Verify terminology is used consistently
- Flag deviations from documented terms
- Check for deprecated or discouraged terms

### Code Examples

- [ ] Code examples in documentation use correct terminology
- [ ] TypeScript/type definitions use domain terms
- [ ] Comments and documentation use consistent language

## 4.3. Business Rules Documentation

**Objective**: Ensure business rules align with domain language

- [ ] Business rules are expressed using domain terminology
- [ ] Rule names are clear and follow conventions
- [ ] Calculations use documented domain concepts
- [ ] State transitions use domain language
- [ ] Constraints are named appropriately

## 4.4. API and Data Model Consistency

**Objective**: Verify external contracts use domain language

### API Terminology

- [ ] API request/response fields use domain terms
- [ ] API error messages use correct terminology
- [ ] API documentation uses consistent language
- [ ] GraphQL types/fields (if applicable) use domain terms

### Data Model Terminology

- [ ] Database tables are named using domain language
- [ ] Column names follow documented terminology
- [ ] Enums match documented domain concepts
- [ ] Relationships use appropriate domain terms

## 4.5. UI/UX Terminology

**Objective**: Ensure user interface uses domain language appropriately

- [ ] Button labels use domain terminology
- [ ] Form field labels are consistent
- [ ] Page titles use correct terms
- [ ] Help text and tooltips use domain language
- [ ] Error messages use appropriate terminology
- [ ] Validation messages follow domain language

**User-Facing vs. Technical Terms**:

- [ ] User-facing terms are appropriate for audience
- [ ] Technical terms are used only where appropriate
- [ ] Domain jargon is explained when necessary

## 4.6. Cross-Document Consistency

**Objective**: Verify terminology is consistent across all documentation

- [ ] Product requirements use documented domain terms
- [ ] Functional design follows domain language
- [ ] Architecture documents use consistent terminology
- [ ] Test documentation uses domain language
- [ ] Development guidelines reference domain terms
- [ ] README and setup guides use consistent language

## 4.7. Evolution and Maintenance

**Objective**: Ensure domain language evolves appropriately

- [ ] Process for adding new terms is defined
- [ ] Deprecated terms are clearly marked
- [ ] Change history is tracked
- [ ] Terminology updates trigger code review
- [ ] Living document approach is documented

## 4.8. Domain-Specific Patterns

**Objective**: Verify domain patterns are consistently applied

### Entity Naming

- [ ] Primary entities follow naming conventions
- [ ] Entity relationships use consistent terminology
- [ ] Entity states/statuses use domain language

### Action/Operation Naming

- [ ] CRUD operations follow conventions
- [ ] Business operations use domain verbs
- [ ] Event names follow domain language

### Value Objects and Enums

- [ ] Value object names are consistent
- [ ] Enum values use domain terminology
- [ ] Type aliases follow conventions

## Review Output Format

For each section, provide:

1. **Status**: ✅ Excellent | 👍 Good | ⚠️ Partial | ❌ Missing | ❓ Unclear

2. **Findings**: Specific inconsistencies or deviations

3. **Examples**: Code references showing terminology usage

4. **Recommendations**: Actions to improve consistency

5. **Priority**: Critical | High | Medium | Low

---

# 5. Test Concepts Review

Review test concepts document against actual testing implementation.

## 5.1. Testing Strategy

**Objective**: Ensure overall testing approach is documented and followed

- [ ] Testing philosophy is clearly stated
- [ ] Testing pyramid is defined (unit, integration, e2e ratios)
- [ ] Testing priorities are documented
- [ ] Test coverage goals are specified
- [ ] Testing tools and frameworks are listed
- [ ] Continuous testing approach is defined

## 5.2. Unit Testing

**Objective**: Verify unit testing practices match documentation

### Unit Test Coverage

- [ ] Unit tests exist for business logic
- [ ] Unit tests exist for utility functions
- [ ] Unit tests exist for data models/validators
- [ ] Test coverage meets documented goals
- [ ] Critical paths have comprehensive tests

### Unit Test Quality

- [ ] Tests follow AAA pattern (Arrange, Act, Assert)
- [ ] Tests are isolated and independent
- [ ] Tests use appropriate mocking/stubbing
- [ ] Tests have clear, descriptive names
- [ ] Tests are fast and reliable
- [ ] Edge cases are tested

**Generic Patterns to Check**:

- Locate unit test files (`.test.ts`, `.spec.ts`, `_test.py`, etc.)
- Verify test organization mirrors source code structure
- Check test naming conventions

## 5.3. Integration Testing

**Objective**: Ensure integration tests match documented approach

### Integration Test Coverage

- [ ] API endpoints have integration tests
- [ ] Database interactions are tested
- [ ] Third-party integrations are tested
- [ ] Authentication/authorization flows are tested
- [ ] Multi-component workflows are tested

### Integration Test Quality

- [ ] Tests use test databases or containers
- [ ] Tests clean up after themselves
- [ ] Tests are idempotent
- [ ] Tests cover happy paths and error cases
- [ ] Tests verify data integrity

**Generic Patterns to Check**:

- Locate integration test files
- Verify test setup and teardown
- Check database seeding for tests

## 5.4. End-to-End (E2E) Testing

**Objective**: Verify E2E testing matches documented strategy

### E2E Test Coverage

- [ ] Critical user flows have E2E tests
- [ ] Cross-browser testing is implemented (if specified)
- [ ] Mobile/responsive tests exist (if specified)
- [ ] Accessibility tests are included (if specified)

### E2E Test Quality

- [ ] Tests use documented E2E framework (Cypress, Playwright, Selenium, etc.)
- [ ] Tests are stable and not flaky
- [ ] Tests have appropriate wait strategies
- [ ] Tests use page object pattern (if specified)
- [ ] Tests clean up test data

**Generic Patterns to Check**:

- Locate E2E test files
- Verify E2E test configuration
- Check CI/CD integration for E2E tests

## 5.5. Test Data Management

**Objective**: Ensure test data strategy is implemented

- [ ] Test data generation approach matches documentation
- [ ] Fixtures/seeds exist for tests
- [ ] Test data isolation is maintained
- [ ] Sensitive data is not used in tests
- [ ] Test database setup is automated

## 5.6. Testing Best Practices

**Objective**: Verify tests follow documented best practices

- [ ] Test code quality meets standards
- [ ] Tests are maintainable and readable
- [ ] Tests avoid duplication (DRY principle)
- [ ] Tests use appropriate assertions
- [ ] Tests have proper error messages
- [ ] Tests are documented where necessary

## 5.7. Performance Testing

**Objective**: Ensure performance testing matches documentation (if applicable)

- [ ] Load testing strategy is implemented
- [ ] Performance benchmarks are defined
- [ ] Performance tests are automated
- [ ] Performance regression tests exist

## 5.8. Security Testing

**Objective**: Verify security testing is implemented (if applicable)

- [ ] Authentication/authorization tests exist
- [ ] Input validation tests cover security
- [ ] Vulnerability scanning is configured
- [ ] Penetration testing approach is documented

## 5.9. Test Automation

**Objective**: Ensure test automation matches CI/CD strategy

- [ ] Tests run automatically on commits/PRs
- [ ] Test failures block merges (if specified)
- [ ] Test reports are generated
- [ ] Code coverage reports are generated
- [ ] Flaky test handling is implemented

## 5.10. Test Documentation

**Objective**: Verify tests are properly documented

- [ ] Test naming clearly describes what is being tested
- [ ] Complex test logic is commented
- [ ] Test setup/teardown is documented
- [ ] Known limitations are documented

## Review Output Format

For each section, provide:

1. **Status**: ✅ Excellent | 👍 Good | ⚠️ Partial | ❌ Missing | ❓ Unclear

2. **Findings**: Gaps in test coverage or quality

3. **Examples**: References to test files demonstrating findings

4. **Recommendations**: Specific improvements to testing

5. **Priority**: Critical | High | Medium | Low

---

# 6. Repository Structure Review

Review repository structure document against actual codebase organization.

## 6.1. Directory Structure

**Objective**: Verify directory organization matches documentation

- [ ] All documented directories exist
- [ ] Directory purposes match documentation
- [ ] Naming conventions are followed
- [ ] Directory hierarchy is logical
- [ ] No undocumented major directories exist

**Generic Patterns to Check**:

- Compare actual directory structure to documented structure
- Verify separation of concerns (source code, tests, config, docs)
- Check for common patterns (src/, lib/, app/, components/, services/, etc.)

## 6.2. File Organization

**Objective**: Ensure file organization follows documented patterns

- [ ] File naming conventions are consistent
- [ ] Files are in correct directories
- [ ] File grouping strategy is followed (feature-based, type-based, etc.)
- [ ] Co-location patterns are followed (components with styles/tests)
- [ ] File size guidelines are followed

## 6.3. Source Code Structure

**Objective**: Verify source code organization matches documentation

### Application Code

- [ ] Entry point file matches documentation
- [ ] Core application files are in documented locations
- [ ] Feature modules are organized as documented
- [ ] Shared/common code is in documented location
- [ ] Utilities and helpers are properly organized

### Component Structure (Frontend)

- [ ] Component directory structure matches documentation
- [ ] Component files follow documented patterns
- [ ] Shared components are in correct location
- [ ] Component styles are organized as documented

### Backend Structure

- [ ] Routes/controllers are organized as documented
- [ ] Service/business logic location matches documentation
- [ ] Data access layer is in correct location
- [ ] Middleware is properly organized

## 6.4. Configuration Files

**Objective**: Ensure configuration files match documentation

- [ ] All documented config files exist
- [ ] Config file locations are correct
- [ ] Environment-specific configs are organized as documented
- [ ] Config file purposes are clear

**Common Config Files to Check**:

- Package manager: `package.json`, `requirements.txt`, `pom.xml`, `Cargo.toml`
- TypeScript: `tsconfig.json`
- Build tools: `vite.config.ts`, `webpack.config.js`, `rollup.config.js`
- Linters: `.eslintrc`, `.prettierrc`, `pylint.rc`
- Test frameworks: `jest.config.js`, `vitest.config.ts`, `pytest.ini`
- Environment: `.env.example`, `config/`
- Docker: `Dockerfile`, `docker-compose.yml`
- CI/CD: `.github/workflows/`, `.gitlab-ci.yml`, `circle.yml`

## 6.5. Test Structure

**Objective**: Verify test organization matches documentation

- [ ] Test directory structure matches documentation
- [ ] Test file naming follows conventions
- [ ] Test files are co-located with source (if specified)
- [ ] Test fixtures/data are properly organized
- [ ] Test utilities are in documented location

## 6.6. Documentation Structure

**Objective**: Ensure documentation is organized as specified

- [ ] README exists and contains documented sections
- [ ] Documentation directory matches structure
- [ ] API documentation location is correct
- [ ] Architecture diagrams are in documented location
- [ ] ADRs are organized as documented (if applicable)

## 6.7. Build and Output Directories

**Objective**: Verify build artifacts are organized correctly

- [ ] Build output directory matches documentation
- [ ] Generated code location is documented and correct
- [ ] Temporary directories are properly configured
- [ ] Distribution files are in correct location

## 6.8. Version Control Patterns

**Objective**: Ensure version control setup matches documentation

- [ ] `.gitignore` includes documented patterns
- [ ] Git hooks (if any) are in documented location
- [ ] Submodules (if any) are documented and present
- [ ] Branch strategy matches documentation

## 6.9. Dependency Management

**Objective**: Verify dependencies are managed as documented

- [ ] Lock files are present and committed (if specified)
- [ ] Dependency versions follow documented strategy
- [ ] Peer dependencies are correctly specified
- [ ] Dev vs. production dependencies are correctly categorized

## 6.10. Special Directories

**Objective**: Ensure special-purpose directories match documentation

- [ ] Public/static assets are in documented location
- [ ] Scripts directory matches documentation
- [ ] Tools/utilities are properly organized
- [ ] Database migrations are in documented location
- [ ] Seeds/fixtures are properly organized

## Review Output Format

For each section, provide:

1. **Status**: ✅ Excellent | 👍 Good | ⚠️ Partial | ❌ Missing | ❓ Unclear

2. **Findings**: Discrepancies in structure or organization

3. **Examples**: Specific files/directories demonstrating issues

4. **Recommendations**: Restructuring or documentation updates needed

5. **Priority**: Critical | High | Medium | Low

---

# 7. Development Guidelines Review

Review development guidelines document for clarity and ensure code follows documented practices.

## 7.1. Coding Standards

**Objective**: Verify code follows documented standards

### Code Style

- [ ] Code formatting follows documented rules
- [ ] Linter configuration matches guidelines
- [ ] Naming conventions are consistently applied
- [ ] Code organization follows patterns
- [ ] Comments and documentation follow standards

**Generic Patterns to Check**:

- Run linter and check for violations
- Sample random files to verify consistency
- Check for linter/formatter config files

### Language-Specific Standards

- [ ] Language-specific best practices are documented
- [ ] Framework conventions are followed
- [ ] Type safety practices are documented (if applicable)
- [ ] Async/await patterns follow guidelines
- [ ] Error handling patterns are consistent

## 7.2. Git Workflow

**Objective**: Ensure version control practices match documentation

- [ ] Branch naming conventions are documented and followed
- [ ] Commit message format is documented and followed
- [ ] Pull request process is documented
- [ ] Code review checklist is documented
- [ ] Merge strategy is documented (squash, merge commit, rebase)

**Generic Patterns to Check**:

- Review recent commit messages
- Check branch naming in repository
- Verify PR templates exist (if documented)

## 7.3. Code Review Process

**Objective**: Verify code review practices are documented

- [ ] Code review requirements are clear
- [ ] Reviewer responsibilities are documented
- [ ] Approval process is defined
- [ ] Review checklist exists
- [ ] Feedback guidelines are provided

## 7.4. Testing Requirements

**Objective**: Ensure testing requirements are clear and followed

- [ ] Test coverage requirements are documented
- [ ] Test writing guidelines are provided
- [ ] Test organization is specified
- [ ] Test data management is documented
- [ ] Definition of done includes testing

## 7.5. Documentation Requirements

**Objective**: Verify documentation practices are clear

- [ ] Code documentation requirements are specified
- [ ] API documentation requirements are clear
- [ ] README requirements are documented
- [ ] Inline comment guidelines are provided
- [ ] Documentation update process is defined

## 7.6. Security Practices

**Objective**: Ensure security guidelines are documented and followed

- [ ] Secure coding practices are documented
- [ ] Authentication/authorization patterns are specified
- [ ] Input validation requirements are clear
- [ ] Secret management practices are documented
- [ ] Security review process is defined

## 7.7. Performance Guidelines

**Objective**: Verify performance best practices are documented

- [ ] Performance optimization guidelines exist
- [ ] Performance testing requirements are clear
- [ ] Performance budgets are documented
- [ ] Profiling tools are specified
- [ ] Database query optimization is addressed

## 7.8. Error Handling and Logging

**Objective**: Ensure error handling practices are consistent

- [ ] Error handling patterns are documented
- [ ] Logging guidelines are provided
- [ ] Log levels are defined
- [ ] Error reporting process is clear
- [ ] User-facing error messages follow guidelines

## 7.9. Dependency Management

**Objective**: Verify dependency practices are clear

- [ ] Dependency addition process is documented
- [ ] Dependency update strategy is defined
- [ ] License compatibility is addressed
- [ ] Security vulnerability scanning is mentioned
- [ ] Dependency versioning strategy is clear

## 7.10. CI/CD Practices

**Objective**: Ensure CI/CD guidelines are documented

- [ ] Build process is documented
- [ ] Deployment process is clear
- [ ] Environment configuration is specified
- [ ] Rollback procedures are documented
- [ ] Release process is defined

## 7.11. Onboarding and Setup

**Objective**: Verify developer onboarding is clear

- [ ] Setup instructions are comprehensive
- [ ] Development environment requirements are listed
- [ ] First-time setup is automated (if specified)
- [ ] Common issues and troubleshooting are documented
- [ ] Team contacts and resources are provided

## 7.12. Code Organization Principles

**Objective**: Ensure architectural principles are documented

- [ ] Separation of concerns is addressed
- [ ] DRY (Don't Repeat Yourself) principle is mentioned
- [ ] SOLID principles are referenced (if applicable)
- [ ] Dependency injection patterns are documented
- [ ] Modularity guidelines are provided

## Review Output Format

For each section, provide:

1. **Status**: ✅ Excellent | 👍 Good | ⚠️ Partial | ❌ Missing | ❓ Unclear

2. **Findings**: Gaps in guidelines or deviations in practice

3. **Examples**: Code references demonstrating adherence or violations

4. **Recommendations**: Guideline improvements or enforcement suggestions

5. **Priority**: Critical | High | Medium | Low

---

# 8. Environments Documentation Review

Review environments documentation against actual environment configuration.

## 8.1. Environment Definitions

**Objective**: Ensure all environments are clearly defined

- [ ] All environments are listed (dev, staging, production, etc.)
- [ ] Purpose of each environment is clear
- [ ] Environment differences are documented
- [ ] Environment promotion flow is defined
- [ ] Access controls for each environment are documented

## 8.2. Development Environment

**Objective**: Verify development setup is comprehensive

- [ ] Prerequisites are listed (Node.js version, databases, etc.)
- [ ] Installation steps are clear and complete
- [ ] Environment variables are documented
- [ ] Local development tools are specified
- [ ] Docker/containerization setup (if applicable) is documented
- [ ] Database setup and seeding is explained

**Generic Patterns to Check**:

- Verify `.env.example` or similar exists
- Check if setup scripts exist
- Verify Docker Compose configuration (if applicable)

## 8.3. Environment Variables

**Objective**: Ensure environment configuration is clear

- [ ] All environment variables are documented
- [ ] Variable purposes are explained
- [ ] Required vs. optional variables are specified
- [ ] Default values are documented
- [ ] Sensitive variables are clearly marked
- [ ] Variable validation is implemented

**Generic Patterns to Check**:

- Compare `.env.example` to documentation
- Search code for `process.env`, `os.environ`, etc.
- Verify all used variables are documented

## 8.4. Configuration Management

**Objective**: Verify configuration approach is clear

- [ ] Configuration loading mechanism is documented
- [ ] Configuration validation is implemented
- [ ] Environment-specific config files are organized
- [ ] Configuration precedence is clear
- [ ] Secrets management approach is documented

## 8.5. Database Configuration

**Objective**: Ensure database setup is comprehensive

- [ ] Database system is specified
- [ ] Database connection configuration is documented
- [ ] Migration strategy is explained
- [ ] Seeding/fixtures approach is documented
- [ ] Database backup strategy is mentioned (production)
- [ ] Connection pooling configuration is documented

## 8.6. External Services Configuration

**Objective**: Verify third-party service setup is clear

- [ ] All external services are listed
- [ ] Service account setup is documented
- [ ] API keys and credentials management is explained
- [ ] Service endpoints for each environment are specified
- [ ] Service-specific configuration is documented

## 8.7. Build and Deployment

**Objective**: Ensure build and deployment process is clear

- [ ] Build process is documented
- [ ] Build configuration for each environment is explained
- [ ] Asset compilation is addressed
- [ ] Deployment steps are clear
- [ ] Deployment automation is documented
- [ ] Rollback procedures are provided

## 8.8. Testing Environments

**Objective**: Verify test environment setup is documented

- [ ] Test environment configuration is specified
- [ ] Test database setup is explained
- [ ] Test data management is documented
- [ ] CI/CD test environment is configured
- [ ] Integration test environment is documented

## 8.9. Staging/Pre-Production Environment

**Objective**: Ensure staging environment matches production

- [ ] Staging environment mirrors production
- [ ] Staging-specific configuration is documented
- [ ] Data synchronization strategy is explained
- [ ] Access controls are defined
- [ ] Testing procedures for staging are documented

## 8.10. Production Environment

**Objective**: Verify production setup is comprehensive

- [ ] Infrastructure is clearly documented
- [ ] Scaling configuration is explained
- [ ] Monitoring and alerting are configured
- [ ] Backup and disaster recovery are addressed
- [ ] Security hardening is documented
- [ ] Performance optimization is applied

## 8.11. Environment Parity

**Objective**: Ensure environments are sufficiently similar

- [ ] Environment differences are minimized
- [ ] Known differences are documented and justified
- [ ] Configuration parity is maintained
- [ ] Version parity is maintained (dependencies, databases)

## 8.12. Troubleshooting

**Objective**: Verify troubleshooting information is provided

- [ ] Common issues are documented
- [ ] Debug procedures are provided
- [ ] Log locations are specified
- [ ] Health check endpoints are documented
- [ ] Support contacts are listed

## Review Output Format

For each section, provide:

1. **Status**: ✅ Excellent | 👍 Good | ⚠️ Partial | ❌ Missing | ❓ Unclear

2. **Findings**: Gaps or inaccuracies in environment documentation

3. **Verification**: Actual configuration vs. documented configuration

4. **Recommendations**: Documentation or configuration improvements

5. **Priority**: Critical | High | Medium | Low

---

# General Review Guidelines

## Review Process

1. **Preparation**
   - Read project configuration section
   - Identify relevant documentation files
   - Set up local development environment
   - Clone repository and checkout latest code

2. **Systematic Review**
   - Go through each review section systematically
   - Use checklist items as guide, adapt to project needs
   - Document findings as you go
   - Reference specific files and line numbers

3. **Cross-Document Validation**
   - Compare findings across different document reviews
   - Identify inconsistencies between documents
   - Verify alignment between requirements, design, and implementation

4. **Prioritization**
   - Categorize findings by priority
   - Focus on critical issues first
   - Group related findings together

5. **Reporting**
   - Start with the Overall Summary Table showing DocumentationQuality and ImplementationStatus for each document/section
   - Use consistent output format for detailed findings
   - Provide actionable recommendations
   - Include code references and examples
   - Summarize key findings at the end

## Output Format Standards

### Status Indicators

- ✅ **Excellent**: Requirement is fully met, implementation matches documentation perfectly, follows best practices
- 👍 **Good**: Requirement is adequately met with only minor areas for improvement
- ⚠️ **Partial**: Partial compliance, some aspects addressed but significant gaps exist
- ❌ **Missing**: Requirement not met, not addressed in documentation or implementation
- ❓ **Unclear**: Cannot determine status from available information, needs investigation

### Findings Structure

For each finding, include:

```markdown
## [Section Name]

**Status**: [✅ Excellent / 👍 Good / ⚠️ Partial / ❌ Missing / ❓ Unclear]

**Summary**: Brief description of the finding

**Details**:

- Specific observation or gap
- Another observation

**Evidence**:

- File: `path/to/file.ts:123`
- Documentation: `docs/document.md` section X

**Impact**: [Critical / High / Medium / Low]

**Recommendation**:

1. Concrete action to take
2. Another action

**Priority**: [Critical / High / Medium / Low]
```

## Tips for Effective Review

1. **Be Specific**: Always reference exact file paths and line numbers
2. **Be Objective**: Focus on facts, not opinions
3. **Be Constructive**: Provide actionable recommendations, not just criticism
4. **Be Thorough**: Check edge cases and error scenarios
5. **Be Consistent**: Use the same criteria across all reviews
6. **Be Practical**: Prioritize issues that matter for project success

## Adapting This Framework

This framework is designed to be generic. Adapt it to your project by:

1. **Adding Project-Specific Sections**: Include checks specific to your domain or technology
2. **Removing Irrelevant Sections**: Skip sections that don't apply to your project
3. **Adjusting Checklists**: Modify checklist items to match your requirements
4. **Customizing Output Format**: Adjust reporting format to your team's needs
5. **Defining Custom Priorities**: Create priority definitions that fit your context

## Common Pitfalls to Avoid

1. **Over-Generalization**: Don't assume all projects follow the same patterns
2. **Technology Bias**: Don't favor one technology over another without justification
3. **Perfectionism**: Focus on important issues, not every minor inconsistency
4. **Scope Creep**: Stay focused on review objectives, don't redesign the system
5. **Lack of Context**: Consider project constraints (timeline, budget, team skills)

---

# Conclusion

This generic development documents review framework provides a comprehensive approach to verifying that:

1. **Product requirements** are technically supported
2. **Functional design** matches implementation
3. **Architecture** is complete and sound
4. **Ubiquitous language** is consistently applied
5. **Test concepts** are properly implemented
6. **Repository structure** is well-organized
7. **Development guidelines** are clear and followed
8. **Environments** are properly configured

By adapting this framework to your specific project, you can ensure high-quality documentation that accurately reflects your codebase and serves as a reliable reference for your development team.
