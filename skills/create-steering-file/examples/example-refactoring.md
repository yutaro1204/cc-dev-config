# Example: Refactoring Request

## User Input
```
/create-steering-file
Refactor: Extract date validation logic from Pydantic schemas into reusable validator functions to reduce code duplication
```

## Skill Processing

### Step 1: Type Detection
- ✓ Explicit prefix: "Refactor:" detected
- **Result**: **Refactoring**

### Step 2: ID Assignment
- Scan: `.steerings/refactoring/*.md`
- Existing files: (none)
- **Result**: **R001**

### Step 3: Generate Short Description
- Input: "Refactor: Extract date validation logic..."
- Remove "Refactor:": "Extract date validation logic"
- Extract key words: "extract date validation"
- Simplify: "extract validators" (3 words, under 5 word limit)
- Kebab-case: **"extract-validators"**

### Step 4: Populate Template
- Read: `.steerings/templates/refactoring-template.md`
- Replace `R###` → `R001`
- Replace `[Refactoring Title]` → "Extract Date Validators"
- Fill sections:

```markdown
# R001: Extract Date Validators

## Objective
Extract date validation logic from Pydantic schemas into reusable validator functions in a dedicated utils module. This will eliminate code duplication, improve maintainability, and make validation logic easier to test independently.

## Motivation
Currently, date validation logic (e.g., ensuring expires_date is after starts_date) is duplicated across multiple Pydantic schema classes (TodoCreate, TodoUpdate). This violates DRY principles and makes the validation logic harder to maintain and test.

**Why this refactoring is needed:**
- **Code Duplication**: Same validation logic exists in multiple schemas
- **Maintainability**: Changes to validation rules require updates in multiple places
- **Testability**: Validation logic is coupled to schemas, harder to unit test
- **Reusability**: Validation logic could be reused in other contexts

**Benefits expected:**
- Single source of truth for date validation
- Easier to test validation logic independently
- Simpler schema definitions
- Reduced risk of inconsistent validation across schemas

## Current State
Date validation is embedded within Pydantic schema field validators.

### Problems with Current Code
1. **Duplication**: `validate_dates` method exists in both `TodoCreate` and `TodoUpdate` schemas
2. **Testing Complexity**: Must test validation through schema instantiation, not directly
3. **Inconsistency Risk**: Easy to update one schema but forget the other
4. **Poor Reusability**: Can't use validation logic outside of schemas

### Files Affected
- `app/schemas/todo.py` - Contains duplicated validation logic
  - TodoCreate class has @field_validator('expires_date')
  - TodoUpdate class has similar @field_validator('expires_date')

### Code Example (Before)
```python
# app/schemas/todo.py (Current implementation)

class TodoCreate(BaseModel):
    title: str = Field(..., min_length=1, max_length=200)
    starts_date: datetime | None = None
    expires_date: datetime | None = None

    @field_validator('expires_date')
    @classmethod
    def validate_dates(cls, v, info):
        if v and info.data.get('starts_date') and v < info.data['starts_date']:
            raise ValueError('expires_date must be after starts_date')
        return v

class TodoUpdate(BaseModel):
    title: str | None = None
    starts_date: datetime | None = None
    expires_date: datetime | None = None

    @field_validator('expires_date')
    @classmethod
    def validate_dates(cls, v, info):
        # Duplicated logic
        if v and info.data.get('starts_date') and v < info.data['starts_date']:
            raise ValueError('expires_date must be after starts_date')
        return v
```

## Proposed Refactoring
Extract validation functions into `app/utils/validators.py` and use them from schemas.

### Design Improvements
1. **Single Validation Function**: One function handles date range validation
2. **Reusable**: Can be used in schemas, services, or anywhere else
3. **Testable**: Pure function, easy to unit test
4. **Clear Naming**: Function name clearly describes what it validates

### Files to Modify
- `app/schemas/todo.py` - Update to use extracted validators
- `app/utils/validators.py` - New file for validation functions

### Code Example (After)
```python
# app/utils/validators.py (New file)

from datetime import datetime

def validate_date_range(
    starts_date: datetime | None,
    expires_date: datetime | None
) -> None:
    """
    Validate that expires_date is after starts_date.

    Args:
        starts_date: Start date (optional)
        expires_date: Expiration date (optional)

    Raises:
        ValueError: If expires_date is before starts_date
    """
    if starts_date and expires_date and expires_date < starts_date:
        raise ValueError('expires_date must be after starts_date')


# app/schemas/todo.py (Refactored)

from app.utils.validators import validate_date_range

class TodoCreate(BaseModel):
    title: str = Field(..., min_length=1, max_length=200)
    starts_date: datetime | None = None
    expires_date: datetime | None = None

    @field_validator('expires_date')
    @classmethod
    def validate_dates(cls, v, info):
        validate_date_range(info.data.get('starts_date'), v)
        return v

class TodoUpdate(BaseModel):
    title: str | None = None
    starts_date: datetime | None = None
    expires_date: datetime | None = None

    @field_validator('expires_date')
    @classmethod
    def validate_dates(cls, v, info):
        validate_date_range(info.data.get('starts_date'), v)
        return v
```

## Refactoring Strategy

### Implementation Steps
1. **Step 1**: Ensure tests exist for current validation behavior
   - Verify test coverage for TodoCreate and TodoUpdate date validation
   - Add tests if missing
2. **Step 2**: Create `app/utils/validators.py`
   - Add `validate_date_range()` function
   - Add unit tests for the function
3. **Step 3**: Update `TodoCreate` to use new validator
   - Replace inline logic with function call
   - Run tests to verify no behavior change
4. **Step 4**: Update `TodoUpdate` to use new validator
   - Replace inline logic with function call
   - Run tests to verify no behavior change
5. **Step 5**: Verify all tests pass
   - Run full test suite
   - Confirm no regressions

### Safety Measures
- [x] Existing tests pass before starting
- [x] Make incremental changes (one schema at a time)
- [x] Run tests after each step
- [x] No behavior changes (pure refactoring)
- [x] Can roll back easily if issues arise

## Behavior Changes
- [x] **No behavior changes** - Pure refactoring
- [ ] Behavior changes - Document below

## Testing Strategy

### Existing Tests
- [x] All existing tests must pass unchanged
- [ ] Tests to modify: None (validation behavior unchanged)

### New Tests to Add
- Unit tests for `validate_date_range()` in `tests/unit/test_validators.py`:
  - Test valid date ranges (starts before expires)
  - Test invalid date ranges (expires before starts)
  - Test None values (both, either, neither)
  - Test same date for both (edge case)

### Regression Testing
- Integration tests for TodoCreate should pass unchanged
- Integration tests for TodoUpdate should pass unchanged
- Manual test: Create TODO with invalid date range via API

## Performance Impact
- [x] No performance impact expected
- [ ] Performance improvement expected
- [ ] Potential performance regression

Function call overhead is negligible (microseconds).

## Breaking Changes
- [x] No breaking changes
- [ ] Breaking changes in internal APIs
- [ ] Breaking changes in public APIs

## Dependencies
- Depends on: None
- Blocks: Future date validation improvements (easier to extend)

## Rollback Plan
Simple git revert of the refactoring commit. No database changes, no API changes.

## Documentation Updates
- Add docstring to `validate_date_range()` function
- Update inline comments in schemas (if any reference validation)

## Success Criteria
- [x] All existing tests pass
- [x] New unit tests for `validate_date_range()` pass
- [x] Code duplication reduced (single validation function)
- [x] No performance regression
- [x] Code review approved

## References
- Design patterns: Pure function pattern
- Documentation: `docs/development-guidelines.md` (DRY principle)

## Risks
- **Risk**: Accidentally changing validation behavior during refactoring
  - **Mitigation**: Comprehensive tests before and after, incremental changes
- **Risk**: Missing edge cases in extracted function
  - **Mitigation**: Unit tests covering all edge cases

## Notes
This is a straightforward refactoring with low risk. The validation logic is simple and well-defined. After this refactoring, additional date validation rules (e.g., preventing past dates) can be easily added to the centralized function.
```

### Step 5: Create File
- Path: `.steerings/refactoring/R001-extract-validators.md`
- Write populated content

### Step 6: Update README
- Read: `.steerings/README.md`
- Find appropriate section (create "Active Refactoring" if needed)
- Add: `- [R001: Extract Date Validators](refactoring/R001-extract-validators.md)`

### Step 7: Output Summary
```
✓ Detected type: Refactoring
✓ Generated ID: R001
✓ Created: .steerings/refactoring/R001-extract-validators.md
✓ Updated: .steerings/README.md

Summary:
- File: .steerings/refactoring/R001-extract-validators.md
- Sections populated:
  - Objective ✓
  - Motivation ✓
  - Current State ✓
  - Problems with Current Code ✓
  - Proposed Refactoring ✓
  - Code Examples (Before/After) ✓
  - Refactoring Strategy ✓
  - Implementation Steps ✓
  - Safety Measures ✓
  - Testing Strategy ✓
  - Success Criteria ✓
- Sections needing attention:
  - (All major sections populated)

Next steps:
1. Review .steerings/refactoring/R001-extract-validators.md
2. Verify existing tests cover current validation behavior
3. Run: Implement R001
4. Follow incremental refactoring steps
5. Verify all tests pass after each step
```

## Result

**File Created**: `.steerings/refactoring/R001-extract-validators.md`

**README.md Updated**:
```markdown
### Active Refactoring Tasks
- [R001: Extract Date Validators](refactoring/R001-extract-validators.md)
```

**User Action Required**:
1. Review the refactoring plan
2. Verify current test coverage is sufficient
3. Run `Implement R001` when ready
4. Follow incremental approach (one schema at a time)
5. Run tests after each step

## Key Differences from Feature/Bug

**Refactoring-Specific Populated Sections**:
- ✓ **Motivation**: Why refactoring is needed (DRY violation)
- ✓ **Current State**: Problems with current code
- ✓ **Code Examples**: Before/After comparison
- ✓ **Safety Measures**: Incremental approach, test-driven
- ✓ **Behavior Changes**: Explicitly marked as "No behavior changes"
- ✓ **Rollback Plan**: Simple git revert
- ✓ **Risks**: With mitigation strategies

**Less Emphasis On**:
- API Design (internal refactoring)
- Security Considerations (no new attack surface)
- New Features (behavior unchanged)
