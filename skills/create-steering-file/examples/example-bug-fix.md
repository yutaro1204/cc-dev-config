# Example: Bug Fix Request

## User Input
```
/create-steering-file
Fix: Users can see other users' TODOs in the GET /api/todos endpoint response
```

## Skill Processing

### Step 1: Type Detection
- ✓ Explicit prefix: "Fix:" detected
- **Result**: **Bug**

### Step 2: ID Assignment
- Scan: `.steerings/bugs/*.md`
- Existing files: (none)
- **Result**: **B001**

### Step 3: Generate Short Description
- Input: "Fix: Users can see other users' TODOs..."
- Remove "Fix:": "Users can see other users' TODOs"
- Extract key words: "users see other users TODOs"
- Simplify: "security leak" (semantic understanding)
- Kebab-case: **"security-leak"**

### Step 4: Determine Severity
- Keywords detected: "users can see other users" (authorization issue)
- Context: Sensitive data exposure
- **Result**: **Critical** (security vulnerability)

### Step 5: Populate Template
- Read: `.steerings/templates/bug-template.md`
- Replace `B###` → `B001`
- Replace `[Bug Title]` → "Security Leak - Unauthorized TODO Access"
- Fill sections:

```markdown
# B001: Security Leak - Unauthorized TODO Access

## Summary
Users can see other users' TODO items when accessing GET /api/todos endpoint, violating authorization requirements.

## Severity
- [x] Critical - Data exposure and authorization bypass
- [ ] High - Major feature broken
- [ ] Medium - Feature partially broken
- [ ] Low - Minor issue or cosmetic

## Current Behavior
When a user requests GET /api/todos, the endpoint returns TODO items from all users in the database, not just the authenticated user's items.

### Steps to Reproduce
1. Create user A with email "usera@example.com"
2. Create user B with email "userb@example.com"
3. Create TODO "User A Task" for user A
4. Create TODO "User B Task" for user B
5. Authenticate as user A
6. Call GET /api/todos
7. Observe that both "User A Task" and "User B Task" are returned

### Actual Result
All TODO items from all users are returned in the response, regardless of which user is authenticated.

### Expected Result
Only TODO items belonging to the authenticated user should be returned.

## Error Messages / Logs
```
[No error message - this is a logic bug, not an exception]
```

## Environment
[TODO: Fill in - Development environment details]

## Impact
- **All users affected**: Every user can view every other user's private tasks
- **Severity**: Critical security vulnerability
- **Frequency**: 100% - happens on every request
- **Workaround**: None available

## Root Cause Analysis
Missing authorization filter in the TODO list query.

### Affected Code
- `app/api/todos.py` - GET /api/todos endpoint (likely line ~20-30)
- `app/services/todo_service.py` - get_todos method missing user_id filter
- `app/repositories/todo_repository.py` - get_all query returns all records

### Why It Happens
The repository query likely looks like:
```python
# Current (broken)
def get_all(self):
    return self.db.query(Todo).all()  # Returns ALL todos
```

Should be:
```python
# Fixed
def get_all_for_user(self, user_id: int):
    return self.db.query(Todo).filter(Todo.user_id == user_id).all()
```

## Proposed Solution
Add user_id filter to all TODO queries to ensure users can only access their own data.

### Changes Required
1. Update `TodoRepository.get_all()` to accept and filter by user_id
2. Update `TodoService.get_todos()` to pass authenticated user_id
3. Update API endpoint to extract user_id from authenticated user
4. Add integration test to verify authorization

### Code Example
```python
# app/repositories/todo_repository.py
class TodoRepository:
    def get_all_for_user(self, user_id: int) -> list[Todo]:
        return self.db.query(Todo)\
            .filter(Todo.user_id == user_id)\
            .options(joinedload(Todo.tags))\
            .all()

# app/services/todo_service.py
class TodoService:
    def get_todos(self, user_id: int, status: str | None = None) -> list[Todo]:
        todos = self.todo_repo.get_all_for_user(user_id)
        if status:
            todos = [t for t in todos if t.status == status]
        return todos

# app/api/todos.py
@router.get("/", response_model=list[TodoResponse])
async def get_todos(
    current_user: User = Depends(get_current_user),
    todo_service: TodoService = Depends(get_todo_service)
):
    return await todo_service.get_todos(current_user.id)
```

## Testing Strategy

### Verification Steps
1. Create two test users with different TODO items
2. Authenticate as user A
3. Call GET /api/todos
4. Verify only user A's TODOs are returned (not user B's)
5. Authenticate as user B
6. Call GET /api/todos
7. Verify only user B's TODOs are returned (not user A's)

### Unit Tests to Add/Modify
- `test_todo_repository_filters_by_user()` - Verify repository filters correctly
- `test_todo_service_returns_user_todos()` - Verify service uses user_id

### Integration Tests to Add/Modify
- `test_get_todos_returns_only_authenticated_users_todos()` - Full endpoint test
- `test_get_todos_with_different_users()` - Multi-user isolation test
- `test_unauthorized_access_prevented()` - Negative test

## Security Implications
**Critical**: This bug exposes all user data. Must be fixed immediately before any production deployment.

## Breaking Changes
- [ ] This fix introduces breaking changes
- [ ] This fix requires database migration
- [ ] This fix requires configuration changes
- [x] No breaking changes

## Related Issues
[TODO: Fill in - Any related bugs or features]

## References
- Documentation: `docs/architecture.md` (Authorization patterns)
- Security guidelines: `docs/development-guidelines.md`

## Notes
This is a critical security bug that must be addressed before any production deployment. All TODO-related endpoints should be audited for similar authorization issues.
```

### Step 6: Create File
- Path: `.steerings/bugs/B001-security-leak.md`
- Write populated content

### Step 7: Update README
- Read: `.steerings/README.md`
- Find appropriate section (create "Active Bugs" if needed)
- Add: `- [B001: Security Leak - Unauthorized TODO Access](bugs/B001-security-leak.md) ⚠️ CRITICAL`

### Step 8: Output Summary
```
✓ Detected type: Bug
✓ Generated ID: B001
✓ Detected severity: Critical (security issue)
✓ Created: .steerings/bugs/B001-security-leak.md
✓ Updated: .steerings/README.md

⚠️  CRITICAL SECURITY BUG ⚠️

Summary:
- File: .steerings/bugs/B001-security-leak.md
- Severity: Critical - Data exposure
- Sections populated:
  - Summary ✓
  - Severity ✓ (Critical auto-detected)
  - Current Behavior ✓
  - Expected Result ✓
  - Steps to Reproduce ✓
  - Root Cause Analysis ✓
  - Proposed Solution ✓
  - Code Examples ✓
- Sections needing attention:
  - Environment [TODO: Fill in]
  - Related Issues [TODO: Fill in]

Next steps:
1. Review .steerings/bugs/B001-security-leak.md
2. Verify root cause analysis is correct
3. THIS IS CRITICAL - Fix immediately
4. Run: Implement B001
5. Verify fix with integration tests
```

## Result

**File Created**: `.steerings/bugs/B001-security-leak.md`

**README.md Updated**:
```markdown
### Active Bugs (Needs Immediate Fix)
- [B001: Security Leak - Unauthorized TODO Access](bugs/B001-security-leak.md) ⚠️ CRITICAL
```

**User Action Required**:
1. Review the bug analysis immediately (CRITICAL severity)
2. Verify environment details
3. Run `Implement B001` to fix
4. Verify fix with all suggested tests
5. Consider security audit of other endpoints
