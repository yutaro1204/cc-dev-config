# Workflow Example: Implementing a Feature

This example demonstrates the complete workflow of implementing a feature using the `implement-steering-file` skill. This example uses generic concepts that adapt to your project's technology stack.

## Prerequisites

1. Steering file created: `.steerings/features/F001-user-management.md`
2. Database running (if applicable)
3. Development environment set up and dependencies installed

## Step 1: Invoke the Skill

```bash
/implement-steering-file F001
```

## Step 2: Skill Locates and Reads Steering File

```
🔍 Locating steering file F001...
✓ Found: .steerings/features/F001-user-management.md

📖 Reading steering file...
✓ Objective: Implement user management with CRUD operations
✓ Acceptance Criteria: X items
✓ Technical Approach: [As specified in steering file]
✓ Database Changes: User entity/table with required fields
✓ Testing Requirements: As specified in steering file
```

## Step 3: Skill Reads Project Context

```
📚 Discovering project structure and reading available documentation...
✓ Detected technology stack: [Framework, ORM, Language]
✓ Detected architecture pattern: [Layered/Clean/MVC/etc.]
✓ CLAUDE.md or README.md - Project overview (if available)
✓ docs/architecture.md - Architecture patterns (if available)
✓ docs/ files - Additional documentation (if available)
✓ Explored existing code to understand patterns
```

## Step 4: Skill Creates Implementation Plan

```
📋 Implementation Plan for F001: User Management

Technology Stack: [Detected from project]
Architecture: [Detected pattern - e.g., Layered, Clean, MVC]

Phase A: Data Layer
───────────────────
1. Create User entity/model
   - id, required fields per steering file
   - timestamps (if project convention)
   - relationships (if applicable)

2. Create database migrations (if project uses migrations)
   - Generate migration using project's tool
   - Review generated migration
   - Apply migration

Phase B: Validation Layer
─────────────────────────
3. Create validation schemas/DTOs
   - CreateUserRequest (input validation)
   - UpdateUserRequest (input validation)
   - UserResponse (output format)

Phase C: Data Access Layer
──────────────────────────
4. Create UserRepository/DAO
   - create(data)
   - get_by_id(id)
   - get_all(filters)
   - update(id, data)
   - delete(id)

Phase D: Business Logic Layer
─────────────────────────────
5. Create UserService/UseCase
   - create_user(data) - with validation
   - get_user(id, requesting_user) - with authorization
   - get_users(filters, requesting_user)
   - update_user(id, data, requesting_user)
   - delete_user(id, requesting_user)

Phase E: API/Interface Layer
────────────
6. Create API endpoints/routes
    - POST /api/users (create)
    - GET /api/users (list)
    - GET /api/users/:id (get one)
    - PUT /api/users/:id (update)
    - DELETE /api/users/:id (delete)

7. Register routes in main application file

Phase F: Dependencies/Middleware
────────────────────────────────
8. Create/update authentication helpers (if needed)
    - get_current_user
    - Authentication middleware

Phase G: Tests
──────────────
9. Unit tests
    - Test business logic in isolation
    - Mock repository dependencies
    - Test validation rules
    - Test authorization checks

10. Integration tests
    - Test full API endpoints
    - Test with real database
    - Test authentication flow
    - Test error scenarios

11. Update test fixtures/configuration
    - Test client setup
    - Test user fixtures

Phase H: Verification
─────────────────────
12. Run test suite
13. Check coverage against project standards
14. Verify all acceptance criteria
15. Update steering file status

Estimated Changes:
- Files to create: X
- Files to modify: Y
- Tests to write: ~Z
- Target coverage: [project standard]

Proceed with implementation? (y/n)
```

## Step 5: User Approves Plan

```
User: y

✓ Plan approved. Starting implementation...
```

## Step 6: Phase A - Data Layer

```
Phase A: Data Layer
═══════════════════

[1/3] Creating User entity/model...
✓ Created User entity following project patterns
  - Required fields per steering file
  - Timestamps (per project convention)
  - Relationships (if applicable)

[2/3] Creating migrations (if applicable)...
✓ Generated migration using project's migration tool
  - Reviewed generated migration
  - Applied migration successfully

[3/3] Verifying database schema...
✓ Database schema matches entity definitions

Phase A complete ✓
```

## Step 7: Phase B - Validation Layer

```
Phase B: Validation Layer
═════════════════════════

[1/1] Creating validation schemas/DTOs...
✓ Created validation layer following project patterns
  - CreateUserRequest (input validation)
  - UpdateUserRequest (partial update validation)
  - UserResponse (output formatting)

Phase B complete ✓
```

## Step 8: Phase C - Repositories

```
Phase C: Repositories
═════════════════════

[1/2] Creating UserRepository...
✓ Created app/repositories/user_repository.py
  - create_user() method
  - get_user_by_email() method
  - get_user_by_id() method

[2/2] Creating SessionRepository...
✓ Created app/repositories/session_repository.py
  - create_session() method
  - get_session_by_token() method
  - deactivate_session() method

Phase C complete ✓
```

## Step 9: Phase D - Business Logic Layer

```
Phase D: Business Logic Layer
══════════════════════════════

[1/1] Creating UserService/UseCase...
✓ Created business logic layer following project patterns
  - create_user() with validation
  - get_user() with authorization check
  - get_users() with filtering
  - update_user() with authorization
  - delete_user() with authorization
  - Proper error handling

Phase D complete ✓
```

## Step 10: Phase E - API/Interface Layer

```
Phase E: API/Interface Layer
════════════════════════════

[1/2] Creating API endpoints...
✓ Created endpoints following project patterns
  - POST /api/users (201 on success)
  - GET /api/users (200 with list)
  - GET /api/users/:id (200 with entity)
  - PUT /api/users/:id (200 on update)
  - DELETE /api/users/:id (204 on delete)
  - Error handling (400, 401, 403, 404)

[2/2] Registering routes...
✓ Modified main application file
  - Registered new routes

Phase E complete ✓
```

## Step 11: Phase F - Dependencies/Middleware

```
Phase F: Dependencies/Middleware
═════════════════════════════════

[1/1] Creating authentication helpers...
✓ Created/updated authentication helpers
  - get_current_user() for authentication
  - Validates authentication token
  - Returns authenticated user

Phase F complete ✓
```

## Step 12: Phase G - Tests

```
Phase G: Tests
══════════════

[1/3] Writing unit tests...
✓ Created unit tests (X tests)
  - Test business logic in isolation
  - Test validation rules
  - Test authorization checks
  - Test error handling

[2/3] Writing integration tests...
✓ Created integration tests (Y tests)
  - Test create endpoint
  - Test list endpoint
  - Test get by id endpoint
  - Test update endpoint
  - Test delete endpoint
  - Test authentication flow
  - Test authorization checks
  - Test error scenarios

[3/3] Updating test fixtures...
✓ Modified tests/conftest.py
  - Added: test_user fixture
  - Added: authenticated_client fixture

Phase G complete ✓

Running tests...
$ pytest
================================ test session starts =================================
collected 36 items

tests/unit/test_security.py ...                                            [  8%]
tests/unit/test_auth_service.py ............                              [ 41%]
tests/integration/test_auth_api.py .....................                  [100%]

================================= 36 passed in 2.34s =================================

✓ All tests pass!
```

## Step 13: Phase H - Verification

```
Phase H: Verification
═════════════════════

[1/4] Running tests...
$ pytest
✓ 36 tests passed, 0 failed

[2/4] Checking coverage...
$ pytest --cov=app --cov-report=term
Name                                  Stmts   Miss  Cover
---------------------------------------------------------
app/__init__.py                           0      0   100%
app/api/__init__.py                       0      0   100%
app/api/auth.py                          45      3    93%
app/api/deps.py                          18      1    94%
app/core/__init__.py                      0      0   100%
app/core/security.py                     12      0   100%
app/models/__init__.py                    0      0   100%
app/models/user.py                       10      0   100%
app/models/session.py                     8      0   100%
app/repositories/__init__.py              0      0   100%
app/repositories/user_repository.py      22      1    95%
app/repositories/session_repository.py   18      2    89%
app/services/__init__.py                  0      0   100%
app/services/auth_service.py             38      2    95%
---------------------------------------------------------
TOTAL                                   171     9    87%

✓ Coverage: 87% (target: >80%)

[3/4] Running code quality checks...
$ ruff format .
✓ 14 files formatted

$ ruff check .
✓ No linting errors

$ mypy app/
✓ No type errors

[4/4] Verifying acceptance criteria...

Acceptance Criteria Verification:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Authentication
─────────────
✓ Users can sign up with email, name, and password
✓ Email is validated and must be unique
✓ Passwords are hashed using bcrypt (12 rounds)
✓ Users can sign in with email and password
✓ Sign in returns a session token
✓ Users can sign out (token is invalidated)

Authorization
────────────
✓ Protected endpoints require valid session token
✓ Unauthorized requests return 401
✓ Invalid tokens return 401
✓ Expired sessions return 401

Data Model
──────────
✓ User model has id, email, name, password_hash, timestamps
✓ Session model has id, user_id, token, is_active, expires_at
✓ Foreign key constraint: sessions.user_id -> users.id
✓ Unique constraint: users.email
✓ Index on users.email for fast lookups

API Endpoints
─────────────
✓ POST /api/auth/signup returns 201 on success
✓ POST /api/auth/signup returns 409 if email exists
✓ POST /api/auth/signup validates email format
✓ POST /api/auth/signin returns 200 with token
✓ POST /api/auth/signin returns 401 for wrong password
✓ POST /api/auth/signout returns 204 on success
✓ POST /api/auth/signout returns 401 without token

Testing
───────
✓ Unit tests for security utilities (100% coverage)
✓ Unit tests for AuthService (95% coverage)
✓ Integration tests for all endpoints (93% coverage)
✓ Total coverage >80% (achieved: 87%)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Result: 26/26 criteria met ✓
```

## Step 14: Update Steering File Status

```
[1/2] Updating steering file...
✓ Marked acceptance criteria as completed in F001-user-management.md
✓ Added implementation notes
✓ Added completion date: [date]

[2/2] Updating README...
✓ Moved F001 from "Active Features" to "Completed Features" in .steerings/README.md
```

## Step 15: Final Summary

```
═══════════════════════════════════════════════════════════════
✓ Implementation Complete: F001 User Management
═══════════════════════════════════════════════════════════════

Files Created (X):
━━━━━━━━━━━━━━━━━━
Data Layer:
  ✓ [entity models]
  ✓ [migration files if applicable]

Validation Layer:
  ✓ [validation schemas/DTOs]

Data Access Layer:
  ✓ [repositories/DAOs]

Business Logic Layer:
  ✓ [services/use cases]

API/Interface Layer:
  ✓ [controllers/routes]
  ✓ [authentication helpers]

Tests:
  ✓ [unit test files]
  ✓ [integration test files]

Files Modified (Y):
━━━━━━━━━━━━━━━━━
  ✓ [main application file - registered routes]
  ✓ [test configuration - added fixtures]
  ✓ .steerings/README.md (moved to Completed)

Test Results:
━━━━━━━━━━━━
  ✓ Tests: X passed, 0 failed
  ✓ Coverage: Y% (target: Z% if specified)

Code Quality:
━━━━━━━━━━━━
  ✓ Formatting: Passed (if applicable)
  ✓ Linting: Passed (if applicable)
  ✓ Type checking: Passed (if applicable)

Acceptance Criteria:
━━━━━━━━━━━━━━━━━━━
  ✓ X/Y criteria met

Next Steps:
━━━━━━━━━━━
1. Manual testing:
   → Start development server
   → Test API endpoints using project's API client/documentation
   → Test create, list, get, update, delete operations
   → Verify authentication and authorization

2. Review generated code:
   → Check business logic implementation
   → Verify error handling
   → Review test coverage

3. Consider improvements (optional):
   → [Feature-specific enhancements]
   → [Performance optimizations]
   → [Additional validation]

4. Move to next feature:
   → /implement-steering-file F002
   → /implement-steering-file F003

═══════════════════════════════════════════════════════════════
```

## Conclusion

User can now manually test the implementation:

```bash
# Start the server
$ uvicorn app.main:app --reload

# In another terminal, test with curl

# 1. Sign up
$ curl -X POST http://localhost:8000/api/auth/signup \
  -H "Content-Type: application/json" \
  -d '{"email":"test@example.com","name":"Test User","password":"password123"}'

# Response:
{
  "id": 1,
  "email": "test@example.com",
  "name": "Test User",
  "created_at": "2024-02-08T10:30:00Z",
  "updated_at": "2024-02-08T10:30:00Z"
}

# 2. Sign in
$ curl -X POST http://localhost:8000/api/auth/signin \
  -H "Content-Type: application/json" \
  -d '{"email":"test@example.com","password":"password123"}'

# Response:
{
  "user": {
    "id": 1,
    "email": "test@example.com",
    "name": "Test User",
    "created_at": "2024-02-08T10:30:00Z",
    "updated_at": "2024-02-08T10:30:00Z"
  },
  "token": "abc123xyz789..."
}

# 3. Access protected endpoint
$ curl -X GET http://localhost:8000/api/todos \
  -H "Authorization: Bearer abc123xyz789..."

# Response: (will work after implementing F002)
[]

# 4. Sign out
$ curl -X POST http://localhost:8000/api/auth/signout \
  -H "Authorization: Bearer abc123xyz789..."

# Response: 204 No Content
```

## Summary

This example demonstrated:
1. **Invocation**: Simple command `/implement-steering-file F001`
2. **Plan Review**: Detailed implementation plan with all phases
3. **Incremental Execution**: Phase-by-phase implementation with progress indicators
4. **Testing**: Automatic test generation and execution
5. **Verification**: Coverage check, code quality, acceptance criteria
6. **Status Update**: Automatic steering file and README updates
7. **Summary**: Comprehensive output with next steps

The entire process took approximately 5 minutes, created 14 files, wrote 36 tests, and achieved 87% coverage, meeting all 26 acceptance criteria.
