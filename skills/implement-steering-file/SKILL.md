---
name: implement-steering-file
description: Implement features, bug fixes, or refactoring tasks based on steering files
allowed-tools: Read, Write, Edit, Glob, Grep, Bash, mcp__serena__get_symbols_overview, mcp__serena__find_symbol, mcp__serena__replace_symbol_body, mcp__serena__insert_after_symbol, mcp__serena__insert_before_symbol
---

# Implement Steering File Skill

This skill implements features, bug fixes, or refactoring tasks by reading steering files from `.steerings/` directory and executing the implementation following the project's architecture patterns.

## What This Skill Does

1. **Reads** the specified steering file (F###, B###, or R###)
2. **Parses** requirements, acceptance criteria, and technical approach
3. **Reads** project documentation (if available) for context and patterns
4. **Creates** implementation plan following the project's architecture
5. **Implements** following discovered or standard patterns
6. **Writes tests** according to project testing conventions
7. **Verifies** against acceptance criteria
8. **Updates** steering file status

## Usage

The user invokes this skill with a steering file ID:

```bash
# Implement feature F001
/implement-steering-file F001
# or use args parameter:
# args: "F001"

# Implement bug fix B001
/implement-steering-file B001

# Implement refactoring R001
/implement-steering-file R001
```

The skill expects the steering file ID as an argument. If not provided, ask the user for it.

## Workflow

### Step 1: Parse and Locate Steering File

**Input**: Steering file ID (e.g., F001, B001, R001)

**Actions**:
1. Extract type (F/B/R) and number from ID
2. Determine directory:
   - F### → `.steerings/features/`
   - B### → `.steerings/bugs/`
   - R### → `.steerings/refactoring/`
3. Use Glob to find matching file: `{directory}/{ID}-*.md`
4. Validate file exists

**Error Handling**:
- **File not found**: "Error: Steering file {ID} not found in {directory}. Use '/create-steering-file' to create it first."
- **Invalid ID format**: "Error: Invalid ID format '{ID}'. Use F###, B###, or R### format (e.g., F001)."
- **Multiple matches**: List all matches and ask user to specify

### Step 2: Read and Parse Steering File

**Actions**:
1. Read the full steering file content
2. Extract key sections:
   - **Objective**: What needs to be implemented
   - **Context**: Background and current state
   - **Constraints**: Project requirements
   - **Acceptance Criteria**: Checklist of requirements
   - **API Design**: Endpoints, request/response formats
   - **Technical Approach**: Suggested implementation steps
   - **Files to Change**: New and modified files
   - **Database Changes**: Schema modifications
   - **Code Examples**: Patterns to follow
   - **Security Considerations**: Safety requirements
   - **Testing Requirements**: Unit and integration tests
   - **References**: Related documentation

3. Check for incomplete sections:
   - Look for `[TODO: Fill in]` markers
   - If found, warn user: "Warning: Steering file has incomplete sections: [...]. Complete them before implementing, or proceed anyway? (y/n)"

### Step 3: Read Project Documentation Context (Optional)

**Actions**:
Before implementing, attempt to discover and read project patterns from available documentation:

**Check and read if available:**
1. **CLAUDE.md** or **README.md** - Project overview, domain model, architecture patterns, naming conventions
2. **docs/architecture.md** - Architecture patterns and layers
3. **docs/functional-design.md** or **docs/api.md** - API specs, data models
4. **docs/repository-structure.md** or **CONTRIBUTING.md** - Directory organization, file naming
5. **docs/development-guidelines.md** or **docs/coding-standards.md** - Coding standards
6. **docs/test-concepts.md** or **docs/testing.md** - Testing patterns
7. **docs/ubiquitous-language.md** - Domain terminology (if applicable)

**If documentation not found:**
- Explore existing codebase structure to discover patterns
- Look for similar files to understand conventions
- Use common industry-standard patterns for the detected technology stack
- Ask user for guidance on critical architectural decisions

**Goal**: Understand existing patterns to maintain consistency

### Step 4: Create Implementation Plan

**Actions**:
1. Analyze steering file requirements
2. Discover project structure and patterns from codebase
3. Create step-by-step plan following project's architecture:

```
Implementation Plan for {ID}: {Title}

Phase A: Data Layer / Models
- Identify where models/entities are defined in the project
- Create/modify necessary data models
- Create database migrations (if project uses migrations)
- Apply schema changes

Phase B: Data Validation / Schemas
- Identify where request/response validation is handled
- Create validation schemas or DTOs
- Add validation rules per steering file requirements

Phase C: Data Access Layer
- Identify where database access is organized
- Create/modify data access layer (repositories, DAOs, queries, etc.)
- Implement CRUD and query methods as needed

Phase D: Business Logic Layer
- Identify where business logic resides (services, use cases, handlers, etc.)
- Create/modify business logic components
- Implement validation, authorization, and orchestration

Phase E: API/Interface Layer
- Identify where API endpoints/routes/controllers are defined
- Create/modify endpoints per steering file specifications
- Wire up to business logic layer
- Register routes/endpoints in application

Phase F: Dependencies/Middleware
- Create/update dependency injection or middleware as needed
- Implement authentication/authorization helpers if required

Phase G: Testing
- Identify project's testing structure and conventions
- Write unit tests for business logic
- Write integration/API tests for endpoints
- Follow project's testing patterns and coverage requirements

Phase H: Verification
- Run test suite using project's test command
- Check coverage against project standards (if specified)
- Verify all acceptance criteria from steering file
- Run code quality checks (linting, formatting, type checking)

Acceptance Criteria: X items to verify
Estimated files: Y new, Z modified
Technology Stack: [Detected from project]
Architecture Pattern: [Detected from project]
```

2. Present plan to user
3. Wait for approval before proceeding

### Step 5: Implement Layer by Layer

**Implementation Order**:
Follow the architecture pattern discovered in the project (e.g., layered, clean architecture, MVC, etc.)

**Common patterns:**
- Data Layer → Validation → Data Access → Business Logic → API/Interface → Tests
- Models → Views → Controllers → Tests
- Entities → Use Cases → Controllers → Tests

For each phase, follow the project's conventions and patterns:

#### Phase A: Data Layer / Models

**Discover project's data model location:**
- Look for existing models/entities (common locations: `models/`, `src/models/`, `entities/`, `domain/`)
- Check framework conventions (e.g., Django models, SQLAlchemy, TypeORM, Mongoose, etc.)

**Create Data Models** following project patterns:
```
# Pseudocode pattern
Entity {
    - id: identifier (primary key, indexed)
    - foreign_keys: references to related entities (indexed)
    - attributes: entity-specific fields
    - status/state: if applicable (enum/string)
    - timestamps: created_at, updated_at (if project uses them)
    - relationships: to related entities
}
```

**Key considerations:**
- Follow project's naming conventions (camelCase, snake_case, PascalCase)
- Use project's field types and validation
- Index foreign keys and frequently queried fields
- Add timestamps if standard in the project
- Define bidirectional relationships if needed

**Create Migrations** (if project uses them):
```bash
# Use project's migration tool
# Examples:
# - Alembic: alembic revision --autogenerate -m "Create entities"
# - Django: python manage.py makemigrations
# - TypeORM: npm run migration:generate
# - Rails: rails generate migration CreateEntities
# - Sequelize: npx sequelize-cli migration:generate --name create-entities

# Review generated migration
# Apply migration using project's command
```

#### Phase B: Data Validation / Schemas

**Discover project's validation approach:**
- Look for existing validation patterns (common: Pydantic, Zod, Joi, class-validator, Django forms, etc.)
- Check where request/response DTOs or schemas are defined

**Create Validation Schemas** following project patterns:
```
# Pseudocode pattern

# Create Request Schema (for creating new entities)
EntityCreate {
    - required_fields: with validation rules (length, format, range)
    - optional_fields: with appropriate defaults
    - enums/choices: for status or category fields
    - custom_validators: for complex validation logic
}

# Update Request Schema (for updating entities)
EntityUpdate {
    - all_fields_optional: allow partial updates
    - same_validation_rules: as create schema
}

# Response Schema (for returning entities)
EntityResponse {
    - id: identifier
    - all_entity_fields: for API response
    - timestamps: if applicable
    - related_entities: if needed
    - exclude_sensitive: password hashes, internal flags
}
```

**Key considerations:**
- Separate Create, Update, and Response schemas/DTOs
- Add field-level validation (length, format, required/optional)
- Implement custom validators for business rules
- Match field names to steering file API design
- Add documentation/descriptions to fields

#### Phase C: Data Access Layer

**Discover project's data access pattern:**
- Look for existing data access patterns (repositories, DAOs, queries, ORM models with methods)
- Identify where database operations are organized

**Create Data Access Layer** following project patterns:
```
# Pseudocode pattern

EntityRepository/DAO {
    constructor(database_connection/session)

    # CRUD operations
    get_by_id(id) -> Entity | None
        - Query by primary key
        - Eager load relationships if needed (prevent N+1)

    get_all(filters?) -> List[Entity]
        - Query with optional filters
        - Apply pagination if needed
        - Order by appropriate field

    get_for_user(user_id, filters?) -> List[Entity]
        - Query with user authorization
        - Apply filters per steering file

    create(data) -> Entity
        - Insert new entity
        - Persist to database
        - Return created entity with ID

    update(entity, data) -> Entity
        - Update entity fields
        - Persist changes
        - Return updated entity

    delete(entity) -> void
        - Remove entity from database
}
```

**Key considerations:**
- No business logic in data access layer (pure database operations)
- Use eager loading for relationships to avoid N+1 queries
- Return None/null for not found (not exceptions at this layer)
- Use transactions appropriately
- Apply indexes for frequently filtered fields

#### Phase D: Business Logic Layer

**Discover project's business logic organization:**
- Look for existing services, use cases, handlers, or business logic layer
- Identify where business rules and authorization are implemented

**Create Business Logic Layer** following project patterns:
```
# Pseudocode pattern

EntityService/UseCase {
    constructor(entity_repository, other_dependencies)

    create_entity(user_id, create_data) -> Entity
        - Validate business rules
        - Check authorization if needed
        - Delegate to repository
        - Handle related entities
        - Return created entity
        - Throw appropriate exceptions

    get_entity(entity_id, user_id) -> Entity
        - Fetch from repository
        - Check not found -> throw NotFoundError
        - Check authorization -> throw UnauthorizedError
        - Return entity

    get_entities(user_id, filters) -> List[Entity]
        - Apply user-specific filtering
        - Delegate to repository
        - Return filtered list

    update_entity(entity_id, user_id, update_data) -> Entity
        - Get entity with authorization check
        - Validate update data
        - Apply business rules
        - Delegate update to repository
        - Return updated entity

    delete_entity(entity_id, user_id) -> void
        - Get entity with authorization check
        - Check if deletion allowed (business rules)
        - Delegate to repository
}
```

**Key considerations:**
- Business logic and validation belong here (not in repository)
- Authorization checks for user data isolation
- Proper error handling with domain-appropriate exceptions
- Orchestrate multiple repository calls if needed
- Add documentation for complex business rules

#### Phase E: API/Interface Layer

**Discover project's API/routing structure:**
- Look for existing API endpoints, routes, controllers, or handlers
- Identify framework (Express, FastAPI, Rails, Django, Spring, etc.)
- Check routing/endpoint registration patterns

**Create API Endpoints** following project patterns:
```
# Pseudocode pattern

# Define routes/endpoints per steering file API design
EntityController/Router {

    POST /api/entities
        - Accept: CreateRequest (validated)
        - Authenticate: get current user
        - Call: service.create_entity(user_id, data)
        - Return: 201 Created with EntityResponse
        - Error: 400 Bad Request for validation errors

    GET /api/entities
        - Query params: filters (status, search, etc.)
        - Authenticate: get current user
        - Call: service.get_entities(user_id, filters)
        - Return: 200 OK with List[EntityResponse]

    GET /api/entities/:id
        - Path param: entity_id
        - Authenticate: get current user
        - Call: service.get_entity(entity_id, user_id)
        - Return: 200 OK with EntityResponse
        - Error: 404 Not Found, 403 Forbidden

    PUT/PATCH /api/entities/:id
        - Path param: entity_id
        - Accept: UpdateRequest (validated)
        - Authenticate: get current user
        - Call: service.update_entity(entity_id, user_id, data)
        - Return: 200 OK with EntityResponse
        - Error: 404 Not Found, 403 Forbidden

    DELETE /api/entities/:id
        - Path param: entity_id
        - Authenticate: get current user
        - Call: service.delete_entity(entity_id, user_id)
        - Return: 204 No Content
        - Error: 404 Not Found, 403 Forbidden
}

# Register routes in main application file
```

**Key considerations:**
- Use appropriate HTTP methods (POST, GET, PUT/PATCH, DELETE)
- Return correct HTTP status codes (201, 200, 204, 400, 401, 403, 404)
- Apply authentication/authorization middleware
- Validate input using schemas/DTOs
- Handle exceptions and convert to HTTP errors
- Delegate all logic to service layer
- Add API documentation (Swagger, JSDoc, etc.)

#### Phase F: Dependencies/Middleware

**Discover project's dependency injection or middleware patterns:**
- Look for existing authentication/authorization helpers
- Identify dependency injection patterns (if applicable)
- Check middleware organization

**Create/Update Dependencies** following project patterns:
```
# Pseudocode pattern

# Authentication helper
get_current_user(request/context) -> User
    - Extract authentication token (header, cookie, session)
    - Validate token (JWT, session, API key)
    - Fetch user from database
    - Return authenticated user
    - Throw 401 Unauthorized if invalid

# Database connection helper (if needed)
get_database_connection() -> Connection
    - Provide database connection/session
    - Handle connection pooling
    - Ensure proper cleanup

# Service factory helpers (if using dependency injection)
get_entity_service(dependencies) -> EntityService
    - Instantiate service with required dependencies
    - Wire up repository and other dependencies

# Permission checkers (if needed)
require_permission(permission_name)
    - Check if current user has permission
    - Throw 403 Forbidden if not authorized
```

**Key considerations:**
- Follow project's authentication pattern (JWT, sessions, OAuth, API keys)
- Reuse existing authentication helpers if available
- Add authorization helpers if steering file requires permissions
- Use dependency injection framework if project uses one
- Ensure proper error responses (401 for auth, 403 for permissions)

#### Phase G: Testing

**Discover project's testing structure:**
- Look for existing test files and patterns
- Identify test framework (Jest, pytest, RSpec, JUnit, Mocha, etc.)
- Check test organization (unit vs integration, file naming conventions)
- Find test coverage tool and requirements

**Write Unit Tests** (test business logic in isolation):
```
# Pseudocode pattern

test_entity_service:
    setup:
        - Create mock repository
        - Instantiate service with mocked dependencies

    test_create_entity_success:
        - Arrange: prepare test data, mock repository responses
        - Act: call service.create_entity()
        - Assert: verify result, verify repository called correctly

    test_create_entity_validation_error:
        - Arrange: prepare invalid data
        - Act & Assert: expect validation error thrown

    test_get_entity_not_found:
        - Arrange: mock repository returns None
        - Act & Assert: expect NotFoundError thrown

    test_get_entity_unauthorized:
        - Arrange: mock entity owned by different user
        - Act & Assert: expect PermissionError thrown

    test_update_entity_success:
        - Arrange: prepare entity and update data
        - Act: call service.update_entity()
        - Assert: verify update applied correctly

    test_delete_entity_success:
        - Arrange: prepare entity
        - Act: call service.delete_entity()
        - Assert: verify repository.delete called
```

**Write Integration Tests** (test full API flow):
```
# Pseudocode pattern

test_entity_api:
    setup:
        - Start test database
        - Create authenticated test client
        - Seed test data if needed

    test_create_entity_success:
        - Send: POST /api/entities with valid data
        - Assert: status 201, response has id and data

    test_create_entity_unauthenticated:
        - Send: POST /api/entities without auth
        - Assert: status 401

    test_get_entities_list:
        - Setup: create multiple entities
        - Send: GET /api/entities
        - Assert: status 200, list contains created entities

    test_get_entity_by_id:
        - Setup: create entity
        - Send: GET /api/entities/:id
        - Assert: status 200, correct entity returned

    test_update_entity:
        - Setup: create entity
        - Send: PUT /api/entities/:id with changes
        - Assert: status 200, entity updated

    test_delete_entity:
        - Setup: create entity
        - Send: DELETE /api/entities/:id
        - Assert: status 204
        - Verify: GET returns 404

    test_authorization:
        - Setup: create entity for user A
        - Send: GET as user B
        - Assert: status 403 or 404 (per steering file)
```

**Run Tests** using project's test command:
```bash
# Examples based on common frameworks:
# - Python/pytest: pytest
# - Node/Jest: npm test
# - Ruby/RSpec: rspec
# - Java/JUnit: mvn test
# - .NET: dotnet test

# Coverage check (examples):
# - pytest --cov=src --cov-report=term
# - npm run test:coverage
# - coverage run && coverage report
```

**Key considerations:**
- Follow project's test file naming conventions
- Use project's test fixtures/factories
- Mock external dependencies in unit tests
- Use test database for integration tests
- Test both success and error cases
- Verify authorization checks work correctly
- Aim for project's coverage target (if specified)

### Step 6: Verify Acceptance Criteria

**Actions**:
1. Read acceptance criteria from steering file
2. For each criterion:
   - Check if implemented
   - Verify with tests if applicable
   - Mark as ✓ or ✗
3. Run full test suite using project's test command
4. Check coverage using project's coverage tool (if applicable)
5. Verify coverage meets project standards (if specified in steering file or docs)
6. Run code quality checks using project's tools:
   - Code formatting (if project uses formatter)
   - Linting (if project uses linter)
   - Type checking (if project uses type checker)
   - Any other quality checks defined in project

**Report**:
```
Acceptance Criteria Verification:

✓ Users can create entities with required fields
✓ Users can list their entities
✓ Users can update entities
✓ Users can delete entities
✓ Entities have timestamps (if required)
✓ Authorization checks prevent access to other users' data
✓ API returns appropriate HTTP status codes
✓ Input validation prevents invalid data
✗ Advanced filtering not implemented (deferred to future)

Passed: 8/9 criteria
```

### Step 7: Update Steering File Status

**Actions**:
1. Read `.steerings/README.md`
2. Find entry for implemented steering file (e.g., F001)
3. Move from "Active Features" section to "Completed Features" section
4. Update steering file itself:
   - Add implementation notes
   - Check off completed acceptance criteria
   - Add completion date

**Example**:
```markdown
<!-- In .steerings/README.md -->

## Completed Features

- **[F001](features/F001-todo-crud.md)**: TODO CRUD Operations
  - Status: ✅ Completed (2024-02-08)
  - Coverage: 87%
  - Tests: 36 passed
```

### Step 8: Provide Summary

**Output to user**:
```
✓ Implementation Complete: {ID} {Feature Name}

Files Created ({count}):
- [List of created files with paths]
- [Models, schemas/DTOs, repositories, services, controllers, etc.]
- [Migration files if applicable]
- [Test files]

Files Modified ({count}):
- [Main application file with route registration]
- [Test configuration or fixtures]
- [.steerings/README.md moved to Completed]

Tests: {passed} passed, {failed} failed
Coverage: {percentage}% [target: {project_target}% if specified]

Acceptance Criteria: {met}/{total} ✓
- ✓ Core CRUD operations
- ✓ Authorization checks
- ✓ Input validation
- ✓ Required fields and constraints
- ✗ Advanced features (deferred if applicable)

Next Steps:
1. Manual testing: Test functionality using project's dev environment
2. Review generated code for improvements or optimizations
3. Consider implementing deferred items (or create new steering files)
4. Move to next feature: {NextID}
```

## Error Handling

### Steering File Not Found
```
Error: Steering file F001 not found in .steerings/features/

Available steering files:
- F002: Tag Management
- F003: User Profile

Use '/create-steering-file' to create a new steering file.
```

### Invalid ID Format
```
Error: Invalid steering file ID format: "Feature1"

Valid formats:
- F### (features): F001, F002, etc.
- B### (bugs): B001, B002, etc.
- R### (refactoring): R001, R002, etc.

Example: /implement-steering-file F001
```

### Incomplete Steering File
```
Warning: Steering file F001 has incomplete sections:
- [TODO: Fill in] Technical Approach
- [TODO: Fill in] Testing Requirements

These sections should be completed for best results.

Proceed anyway? (y/n)
```

### Migration Failure
```
Error: Database migration failed.

Please check:
1. Database is running and accessible
2. Connection configuration is correct
3. Previous migrations succeeded
4. Migration file is valid

Run project's migration command to apply pending migrations.
```

### Test Failure
```
Error: Tests failed during verification:

[test file path]::[test name] FAILED
  [Error details]

Please fix the failing test before marking as complete.
Run project's test command with specific test to see details.
```

### Low Coverage
```
Warning: Test coverage is below target:
  Current: {percentage}%
  Target: {project_target}%

Missing coverage:
- [List of files with low coverage]

Please add more tests to improve coverage.
```

## Key Principles

1. **Discover Project Architecture**: Explore codebase to understand structure and patterns before implementing
2. **Read Steering File Carefully**: Don't deviate from requirements without user approval
3. **Use Project Patterns**: Apply patterns discovered from codebase and documentation
4. **Follow Layer Order**: Implement in the project's architecture order (data → logic → interface)
5. **Test Coverage**: Meet project's coverage standards (if specified)
6. **Verify Criteria**: Check all acceptance criteria before marking complete
7. **Update Status**: Mark steering file as completed in README.md
8. **Incremental Execution**: Can pause and resume between phases
9. **Present Plan First**: Always show plan to user for approval before implementing
10. **Adapt to Technology**: Use the project's frameworks, tools, and conventions

## Smart Features

### Context-Aware Implementation
- Discovers project structure by exploring existing code
- Reads available documentation (CLAUDE.md, README.md, docs/) for patterns
- Identifies technology stack automatically (framework, ORM, language)
- Uses correct terminology from project documentation
- Applies coding standards from project guidelines (if available)

### Adaptive Layer-by-Layer Execution
- Follows project's architecture pattern (layered, clean, MVC, hexagonal, etc.)
- Implements in dependency order (data layer before business logic)
- Writes tests alongside implementation
- Verifies incrementally (run tests after each phase)

### Intelligent Code Generation
- Examines existing similar files for style consistency
- Matches project's code conventions (formatting, naming, structure)
- Uses project's patterns for error handling and validation
- Follows framework-specific best practices
- Adapts to language idioms (snake_case vs camelCase, etc.)

## Implementation Checklist

Before marking as complete, verify:

- [ ] All data models/entities created with proper relationships
- [ ] Migrations created and applied successfully (if project uses migrations)
- [ ] All validation schemas/DTOs have proper validation rules
- [ ] Data access layer follows project pattern (no business logic)
- [ ] Business logic layer has proper validation and authorization
- [ ] API endpoints/routes return correct status codes
- [ ] Authentication/authorization works correctly
- [ ] Unit tests written (with mocked dependencies)
- [ ] Integration tests written (with test database/environment)
- [ ] All tests pass (using project's test command)
- [ ] Coverage meets project standards (if specified)
- [ ] Code formatted (if project uses formatter)
- [ ] Linting passes (if project uses linter)
- [ ] Type checking passes (if project uses type checker)
- [ ] All acceptance criteria from steering file met
- [ ] Steering file status updated
- [ ] .steerings/README.md updated (moved to Completed)

## Success Criteria

The skill is successful when:
- ✓ Steering file parsed correctly
- ✓ Implementation plan created and approved
- ✓ All layers implemented in correct order
- ✓ Tests written (unit + integration)
- ✓ Test coverage >80%
- ✓ All tests pass
- ✓ Code quality checks pass
- ✓ Acceptance criteria met
- ✓ Steering file updated
- ✓ Summary provided to user
