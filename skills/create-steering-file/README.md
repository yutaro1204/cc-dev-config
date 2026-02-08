# Create Steering File Skill

Generate well-structured steering files from natural language descriptions.

## Quick Start

```bash
/create-steering-file
Add full-text search with ranking
```

## What It Does

Converts your feature ideas, bug reports, or refactoring plans into structured steering files that guide implementation.

**The skill:**
1. ✅ Parses your natural language description
2. ✅ Detects type automatically (Feature/Bug/Refactoring)
3. ✅ Assigns the next available ID (F001, B001, R001...)
4. ✅ Populates the appropriate template with your content
5. ✅ Creates the steering file in the correct directory
6. ✅ Updates `.steerings/README.md` index
7. ✅ Provides clear next steps

## Usage Examples

### Example 1: Create a Feature
```
/create-steering-file
Add pagination to the data list with configurable page size
```

**Result:**
- ✓ Creates: `.steerings/features/F001-data-pagination.md`
- ✓ Populates Objective with pagination description
- ✓ Adds acceptance criteria (can paginate, configurable size, etc.)
- ✓ Updates `.steerings/README.md`

### Example 2: Report a Bug
```
/create-steering-file
Fix: Authentication tokens expire after 5 minutes instead of 24 hours
```

**Result:**
- ✓ Detects "Fix:" prefix → identifies as bug
- ✓ Creates: `.steerings/bugs/B001-auth-token-expiry.md`
- ✓ Populates Summary, Current Behavior, Expected Result
- ✓ Sets severity: Medium (pre-filled based on description)

### Example 3: Plan Refactoring
```
/create-steering-file
Refactor: Extract date validation logic into reusable functions
```

**Result:**
- ✓ Detects "Refactor:" prefix
- ✓ Creates: `.steerings/refactoring/R001-extract-validators.md`
- ✓ Populates Objective, Motivation
- ✓ Suggests likely files based on project structure

### Example 4: Use Explicit ID
```
/create-steering-file
F042: Add WebSocket support for real-time updates
```

**Result:**
- ✓ Uses explicit ID: F042 (not next sequential)
- ✓ Creates: `.steerings/features/F042-websocket-support.md`

## Type Detection

The skill automatically detects the type using these rules:

| Input Pattern | Detected Type | Example |
|---------------|---------------|---------|
| Starts with "Feature:" | Feature | "Feature: Add CSV export" |
| Starts with "Bug:" or "Fix:" | Bug | "Fix: Token expires too fast" |
| Starts with "Refactor:" | Refactoring | "Refactor: Extract validators" |
| Starts with F### | Feature | "F042: Add WebSocket" |
| Starts with B### | Bug | "B007: Fix security leak" |
| Starts with R### | Refactoring | "R003: Simplify auth" |
| Contains "Fix", "Error", "Bug" | Bug | "Users can't log in" |
| Contains "Refactor", "Extract" | Refactoring | "Extract common logic" |
| Default | Feature | "Add search functionality" |

## What Gets Populated

The skill fills in these sections automatically:

### ✅ Always Populated
- **ID**: F###, B###, or R###
- **Title/Objective**: From your description
- **Basic Context**: Extracted from your input

### ✅ Smart Generation
- **Acceptance Criteria**: Generated based on feature type
  - Features: Functional requirements, authorization, error handling
  - Bugs: Reproduction steps, expected behavior, verification
  - Refactoring: No behavior changes, tests pass, quality improved

### 📝 You Complete
- **Technical Approach**: [TODO: Fill in]
- **Detailed Acceptance Criteria**: Refine generated ones
- **Testing Requirements**: Specific test cases
- **Security Considerations**: Detailed analysis
- **Files to Change**: Specific file paths and changes

## Filename Format

Generated filenames follow this pattern:

```
{Type}{Number}-{short-description}.md

Examples:
- F001-data-pagination.md
- B001-auth-token-expiry.md
- R001-extract-validators.md
```

**Short Description Rules:**
- Max 5 words
- Kebab-case (lowercase-with-hyphens)
- No articles (a, an, the)
- Action verbs preferred

## ID Assignment

The skill automatically assigns the next available ID:

```
Existing files:               Next ID assigned:
(none)                    →   F001 (first feature)
F001                      →   F002
F001, F002                →   F003
F001, F003 (gap)          →   F004 (doesn't fill gaps)
```

**With Explicit ID:**
```
/create-steering-file F050
Add export feature
```
→ Uses F050 (regardless of existing sequence)

## Next Steps After Creation

After the skill creates your steering file:

1. **Review the File**: Check the generated content
   ```bash
   cat .steerings/features/F001-data-pagination.md
   ```

2. **Complete [TODO] Sections**:
   - Technical Approach
   - Detailed Testing Requirements
   - Security Considerations
   - Files to Change

3. **Refine Acceptance Criteria**: Add specific edge cases and requirements

4. **Implement the Feature**:
   ```bash
   Implement F001
   ```

## Tips for Best Results

### ✅ Good Descriptions
Be specific and include key details:
```
✓ "Add full-text search using PostgreSQL full-text search with relevance ranking"
✓ "Fix: Date validation allows end_date before start_date, causing query errors"
✓ "Refactor: Extract password hashing into security module to reduce duplication"
```

### ❌ Avoid Vague Descriptions
```
✗ "Make it better" (too vague)
✗ "Fix the bug" (no details)
✗ "Add feature" (not specific)
✗ "Improve performance" (no target)
```

### 🎯 Include Context
- Mention relevant entities and data models
- Specify constraints: pagination, authentication, performance
- Note related features: "Add X to existing Y endpoint"

### 📋 Natural Language Works
You don't need special syntax - just describe what you want:
```
"I need to add a way for users to search their data by keywords in the title or description,
with results ranked by relevance and paginated"
```

## Common Use Cases

### Use Case 1: New API Endpoint
```
/create-steering-file
Add GET /api/search endpoint with query parameter and pagination
```

### Use Case 2: Data Model Change
```
/create-steering-file
Add priority field to data model with values: low, medium, high
```

### Use Case 3: Security Fix
```
/create-steering-file
Fix: Authorization check missing in DELETE endpoint
```

### Use Case 4: Code Quality
```
/create-steering-file
Refactor: Split large service class into focused service classes
```

### Use Case 5: Performance Improvement
```
/create-steering-file
Fix: N+1 query problem when loading related data
```

## Advanced Usage

### Specify Severity for Bugs
Include severity keywords in your description:
```
"Fix: Critical security issue - users can delete other users' data"
→ Severity: Critical (auto-detected)

"Fix: Minor UI issue with date formatting"
→ Severity: Low (auto-detected)
```

### Suggest Files to Change
Mention specific components:
```
"Add filtering to the data list endpoint (DataService and DataRepository)"
→ Suggests files based on mentioned components and project structure
```

### Include Acceptance Criteria
Natural language criteria get converted:
```
"Add search where users can search by keyword, results are ranked by relevance,
and only their own data is returned"

→ Generated Acceptance Criteria:
- [ ] User can search by keyword
- [ ] Results ranked by relevance
- [ ] Only authenticated user's data returned
- [ ] Handles empty search query
- [ ] Performance meets project standards
```

## Integration with Workflow

### Full Workflow
```
1. Create Steering File
   /create-steering-file
   Add pagination to data list

2. Review & Edit Generated File
   → .steerings/features/F001-data-pagination.md
   → Complete [TODO] sections
   → Refine acceptance criteria

3. Implement Feature
   Implement F001
   → Claude Code reads F001 and implements

4. Test & Verify
   Run tests
   → Verify acceptance criteria met

5. Mark Complete
   → Update .steerings/README.md
   → Move to "Completed" section
```

## Troubleshooting

### Issue: Wrong Type Detected
**Solution**: Use explicit prefix
```
Instead of: "Add fix for authentication"
Use:        "Fix: Authentication token validation error"
```

### Issue: Description Too Short
**Solution**: Provide more context
```
Instead of: "Add search"
Use:        "Add full-text search with pagination"
```

### Issue: Duplicate ID
**Solution**: Skill will warn and suggest next available
```
If F042 exists and you specify:
/create-steering-file F042
→ Warning: F042 already exists. Suggested: F043
```

### Issue: Unclear Next Steps
**Solution**: Check the summary output
```
The skill provides:
- File path created
- Sections that need completion
- Explicit "Implement F###" command
```

## File Structure Created

```
.steerings/
├── features/
│   └── F001-data-pagination.md        ← Created here
├── bugs/
│   └── B001-auth-token-expiry.md      ← Or here
├── refactoring/
│   └── R001-extract-validators.md     ← Or here
└── README.md                           ← Updated with link
```

## Example Output

```
/create-steering-file
Add date range filtering to the data endpoint

✓ Detected type: Feature
✓ Generated ID: F001
✓ Created: .steerings/features/F001-date-range-filtering.md
✓ Updated: .steerings/README.md

Summary:
- File: .steerings/features/F001-date-range-filtering.md
- Sections populated:
  - Objective ✓
  - Basic context ✓
  - Acceptance criteria ✓ (5 criteria generated)
- Sections needing attention:
  - Technical Approach [TODO: Fill in]
  - API Design [TODO: Fill in]
  - Testing Requirements [TODO: Fill in]
  - Security Considerations [TODO: Fill in]

Next steps:
1. Review and edit .steerings/features/F001-date-range-filtering.md
2. Complete [TODO] sections with specific implementation details
3. Run: Implement F001
```

## Benefits

✅ **Consistent Structure**: All steering files follow the same template
✅ **Quick Creation**: Generate in seconds from natural language
✅ **Smart Defaults**: Auto-generated acceptance criteria based on type
✅ **Automatic Tracking**: README.md updated automatically
✅ **Clear Guidance**: [TODO] markers show what you need to complete
✅ **Type Safety**: Enforced F###/B###/R### naming convention
✅ **Sequential IDs**: Never worry about ID conflicts

## Questions?

If the skill behavior is unclear:
- Check the generated file to see what was populated
- Look for [TODO: Fill in] markers for sections needing attention
- Review the summary output for next steps
- Edit the steering file directly to add missing details

## Related Skills

- **Implement Feature**: Use after creating and completing a steering file
  ```
  Implement F001
  ```

- **Review Steering File**: Validate a steering file before implementation
  ```
  Review steering file F001
  ```

---

**Last Updated**: 2026-02-08
