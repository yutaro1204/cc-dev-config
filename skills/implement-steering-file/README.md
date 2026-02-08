# Implement Steering File Skill

Implement features, bug fixes, or refactoring tasks based on steering files.

## Quick Start

```bash
# After creating a steering file (F001, B001, R001)
/implement-steering-file F001
```

## What It Does

Reads your steering file and implements the feature following:
- ✅ Project's architecture patterns
- ✅ Project coding standards
- ✅ Project test coverage requirements (if specified)
- ✅ All acceptance criteria from steering file

## Usage Examples

### Implement a Feature

```bash
# After creating F001-user-management.md
/implement-steering-file F001
```

**Result**:
- Creates new files (models, controllers, services, API endpoints, etc.)
- Writes comprehensive tests (unit + integration)
- Achieves project's test coverage target
- Verifies all acceptance criteria

### Implement a Bug Fix

```bash
# After creating B001-security-leak.md
/implement-steering-file B001
```

**Result**:
- Fixes authorization check
- Adds test to prevent regression
- Verifies bug is resolved

### Implement Refactoring

```bash
# After creating R001-extract-validators.md
/implement-steering-file R001
```

**Result**:
- Extracts validation logic
- All existing tests still pass
- No behavior changes

## Workflow

1. **Parse ID** → Locate steering file
2. **Read steering file** → Extract requirements
3. **Read project docs** → Understand patterns
4. **Create plan** → Show implementation steps
5. **Implement** → Models → Repos → Services → API → Tests
6. **Verify** → Check acceptance criteria
7. **Update status** → Mark as completed

## Implementation Order

The skill discovers and follows your project's architecture:

```
1. Data Layer               → Models/Entities, database schema
2. Migrations               → Database changes (if applicable)
3. Validation Layer         → Request/response validation
4. Data Access Layer        → Repositories, DAOs, queries
5. Business Logic Layer     → Services, use cases, handlers
6. API/Interface Layer      → Controllers, routes, endpoints
7. Tests                    → Unit + integration
```

The actual order adapts to your project's specific architecture (layered, clean, MVC, hexagonal, etc.)

## What Gets Created

For a typical feature:
- ✅ **Data Models**: Entities/models for database
- ✅ **Migrations**: Database schema changes (if applicable)
- ✅ **Validation**: Request/response validation schemas or DTOs
- ✅ **Data Access**: Repositories, DAOs, or query classes
- ✅ **Business Logic**: Services, use cases, or handlers
- ✅ **API/Interface**: Controllers, routes, or endpoints
- ✅ **Tests**: Comprehensive unit and integration tests
- ✅ **Coverage**: Meets project's coverage standards

## Verification Steps

After implementation, the skill verifies:
1. All acceptance criteria met
2. All tests pass (using project's test command)
3. Coverage meets project standards
4. Code quality checks pass (formatter, linter, type checker if applicable)
5. Database migrations applied (if applicable)

## Example Implementation Plan

When you run `/implement-steering-file F001`, you'll see a plan like:

```
Implementation Plan for F001: User Management

Phase A: Data Layer
- Create User entity/model
- Create related entities if needed
- Create database migrations
- Apply migrations

Phase B: Validation Layer
- Create request validation (CreateUser, UpdateUser)
- Create response schemas (UserResponse)
- Add validation rules

Phase C: Data Access Layer
- Create UserRepository/DAO
- Implement CRUD methods
- Implement query methods

Phase D: Business Logic Layer
- Create UserService/UseCase
- Implement business logic methods
- Add authorization checks

Phase E: API Layer
- Create user endpoints/routes
  - POST /api/users
  - GET /api/users
  - GET /api/users/:id
  - PUT /api/users/:id
  - DELETE /api/users/:id
- Register routes in application

Phase F: Dependencies
- Create authentication helpers (if needed)
- Set up dependency injection (if applicable)

Phase G: Tests
- Unit tests for business logic
- Integration tests for API endpoints

Phase H: Verification
- Run test suite
- Check coverage
- Verify acceptance criteria

Acceptance Criteria: X items to verify
Estimated files: Y new, Z modified
Technology Stack: [Detected from project]

Proceed with implementation? (y/n)
```

You review the plan and approve it, then implementation begins automatically.

## Error Handling

**If steering file not found:**
```
Error: Steering file F001 not found.
Use '/create-steering-file' to create it first.
```

**If steering file incomplete:**
```
Warning: F001 has [TODO] sections.
Complete them before implementing, or proceed anyway?
```

**If tests fail:**
```
Error: Tests failed during verification.
Please fix failing tests before marking as complete.
```

**If coverage is low:**
```
Warning: Test coverage is 68% (target: >80%).
Please add more tests to improve coverage.
```

## Tips

✅ **Complete steering file first**: Fill in [TODO] sections before implementing
✅ **Review plan**: Check the implementation plan before approving
✅ **Test manually**: After implementation, test the feature manually
✅ **Check acceptance criteria**: Verify each criterion is met
✅ **Run quality checks**: Ensure ruff and mypy pass

## Integration with Workflow

```
1. Create steering file
   /create-steering-file
   → Add authentication system

2. Review and edit steering file
   → Complete [TODO] sections
   → Refine acceptance criteria

3. Implement
   /implement-steering-file F001
   → Skill reads F001
   → Creates plan
   → Implements layer by layer
   → Writes tests
   → Verifies

4. Verify manually
   → Test endpoints via Swagger UI
   → Check edge cases

5. Move to next feature
   /implement-steering-file F002
```

## Example Output

```
✓ Implementation Complete: F001 User Management

Files Created (X):
- [models/entities]
- [validation schemas/DTOs]
- [repositories/DAOs]
- [services/use cases]
- [controllers/routes]
- [migrations]
- [unit tests]
- [integration tests]

Files Modified (Y):
- [main application file - registered routes]
- [test configuration - added fixtures]
- .steerings/README.md (moved to Completed)

Tests: X passed, 0 failed
Coverage: Y% (target: Z% if specified)

Acceptance Criteria: X/Y ✓

Next Steps:
1. Manual testing: Test functionality using project's dev environment
2. Review generated code for any improvements
3. Consider next feature: F002 or F003
```

## Detailed Workflow Explanation

### 1. Parse and Locate Steering File

The skill parses the steering file ID (e.g., F001) and locates it:

- **F###** → `.steerings/features/F###-*.md`
- **B###** → `.steerings/bugs/B###-*.md`
- **R###** → `.steerings/refactoring/R###-*.md`

### 2. Read Steering File

Extracts key information:
- **Objective**: What to build
- **Acceptance Criteria**: Requirements checklist
- **Technical Approach**: How to build
- **Files to Change**: Where to write code
- **Database Changes**: Schema modifications
- **Testing Requirements**: What to test

### 3. Read Project Context

Attempts to read available project documentation to understand patterns:
- `CLAUDE.md` or `README.md` - Project overview, domain model, architecture
- `docs/architecture.md` - Architecture patterns and layers
- `docs/api.md` or `docs/functional-design.md` - API specifications
- `docs/repository-structure.md` or `CONTRIBUTING.md` - Directory organization
- `docs/development-guidelines.md` or `docs/coding-standards.md` - Coding standards
- `docs/testing.md` or `docs/test-concepts.md` - Testing patterns

If documentation is not available, the skill explores the codebase to discover patterns.

### 4. Create Implementation Plan

Generates a detailed plan following the project's architecture:
- **Phase A**: Data Layer / Models
- **Phase B**: Validation Layer
- **Phase C**: Data Access Layer
- **Phase D**: Business Logic Layer
- **Phase E**: API/Interface Layer
- **Phase F**: Dependencies/Middleware
- **Phase G**: Tests
- **Phase H**: Verification

### 5. Implement Layer by Layer

**Data Models** (following project's ORM/framework):
```
Entity/Model with:
- Primary key and indexes
- Relationships to other entities
- Timestamps (if standard in project)
- Follows project's naming conventions
```

**Validation Schemas** (following project's validation approach):
```
Request/Response validation with:
- Field types and constraints
- Custom validation rules
- Appropriate defaults
```

**Data Access Layer** (following project's data access pattern):
```
Repository/DAO with:
- CRUD operations
- Query methods
- No business logic
```

**Business Logic Layer** (following project's business logic organization):
```
Service/UseCase with:
- Business rules and validation
- Authorization checks
- Orchestration logic
```

**API/Interface Layer** (following project's API framework):
```
Controller/Route with:
- HTTP endpoints
- Request/response handling
- Authentication/authorization
- Error handling
```

**Tests** (following project's testing patterns):
```
Unit tests:
- Test business logic in isolation
- Mock dependencies

Integration tests:
- Test full API flow
- Use test database/environment
```

### 6. Verify Acceptance Criteria

Checks each acceptance criterion from steering file:
- ✓ Core functionality works as specified
- ✓ Data validation works correctly
- ✓ Authorization checks prevent unauthorized access
- ✓ Error handling works as expected
- ✓ All tests pass
- ✓ Coverage meets project standards

### 7. Update Status

Updates `.steerings/README.md`:
```markdown
## Completed Features

- **[F001](features/F001-user-management.md)**: User Management
  - Status: ✅ Completed (2024-02-08)
  - Coverage: X%
  - Tests: Y passed
```

## FAQ

### Q: Can I pause and resume implementation?

Yes! The skill executes in phases. You can stop at any phase and continue later. For example:
- Complete Phase A (Models), then review
- Continue with Phase B-H later

### Q: What if I disagree with the plan?

The skill presents the plan for your approval first. You can:
- Request modifications to the plan
- Add or remove phases
- Change the implementation approach

### Q: What if tests fail?

The skill will report test failures and pause. You can:
- Review the failing test
- Fix the issue manually or ask the skill to fix it
- Continue verification after fixing

### Q: Can I add custom code after implementation?

Yes! The generated code follows project patterns, so you can:
- Add additional methods to services
- Create new endpoints
- Extend models with new fields
- The code is yours to modify

### Q: What if acceptance criteria are incomplete?

The skill will warn you if the steering file has `[TODO]` sections. You can:
- Complete the sections first (recommended)
- Proceed anyway (skill will do its best)
- Skip certain criteria (document in steering file)

### Q: How does it handle database changes?

The skill:
1. Creates data models/entities using project's ORM or database layer
2. Generates migrations using project's migration tool (if applicable)
3. Reviews migrations for correctness
4. Applies migrations using project's migration command
5. Verifies schema matches models

### Q: What about code quality?

The skill automatically:
- Formats code using project's formatter (if applicable)
- Checks linting using project's linter (if applicable)
- Verifies types using project's type checker (if applicable)
- Runs tests using project's test command
- Measures coverage using project's coverage tool

## Best Practices

1. **Complete Steering File First**
   - Fill in all [TODO] sections
   - Define clear acceptance criteria
   - Specify testing requirements

2. **Review the Plan**
   - Check the implementation order
   - Verify files to be created/modified
   - Confirm approach matches your expectations

3. **Test Incrementally**
   - Review generated code after each phase
   - Run tests frequently
   - Fix issues early

4. **Manual Testing**
   - Test functionality using project's development environment
   - Test API endpoints via API client or documentation interface
   - Test edge cases and error scenarios
   - Verify error handling works correctly

5. **Code Review**
   - Review generated code for improvements
   - Check for security issues
   - Verify performance considerations
   - Ensure code follows project conventions

## Troubleshooting

### Database Connection Issues

**Problem**: "Could not connect to database"

**Solution**:
- Check if database is running
- Verify database connection configuration
- Check environment variables or config files
- Ensure database credentials are correct

### Migration Conflicts

**Problem**: "Database migration failed" or "Target database is not up to date"

**Solution**:
- Check current migration status using project's migration tool
- Apply pending migrations
- Review migration files for conflicts
- Verify database schema matches expected state

### Import/Module Errors

**Problem**: Module or import not found errors

**Solution**:
- Verify all necessary files are created
- Check module initialization files (if applicable to language)
- Ensure dependencies are installed
- Verify environment is properly configured
- Check import paths match project structure

### Test Failures

**Problem**: Tests fail with missing fixtures, setup errors, or unexpected results

**Solution**:
- Check test configuration files exist
- Verify test fixtures are properly defined
- Ensure test database/environment is set up
- Review error messages for specific issues
- Run tests in verbose mode for more details

## Related Skills

- **[create-steering-file](../create-steering-file/README.md)**: Create steering files for this skill to implement
- **[review-steering-file](../review-steering-file/README.md)**: Review steering files before implementation (if available)

## Support

If you encounter issues:
1. Check the steering file is complete (no [TODO] sections)
2. Verify database is running
3. Check `.env` configuration
4. Review error messages carefully
5. Ask for help: describe the issue and show error output

## Version History

- **v1.0** (2024-02-08): Initial release
  - Supports features (F###), bugs (B###), refactoring (R###)
  - Clean Architecture implementation
  - Unit + integration testing
  - Acceptance criteria verification
