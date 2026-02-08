# Example: Feature Request

## User Input
```
/create-steering-file
Add full-text search to the TODO list endpoint allowing users to search by keywords in title and description with relevance ranking
```

## Skill Processing

### Step 1: Type Detection
- ✓ No explicit prefix ("Feature:", "Bug:", "Fix:", "Refactor:")
- ✓ No explicit ID (F###, B###, R###)
- ✓ No bug keywords ("Fix", "Error", "Broken")
- ✓ No refactoring keywords ("Refactor", "Extract", "Improve code")
- **Result**: Default to **Feature**

### Step 2: ID Assignment
- Scan: `.steerings/features/*.md`
- Existing files: (none)
- **Result**: **F001**

### Step 3: Generate Short Description
- Input: "Add full-text search to the TODO list endpoint..."
- Remove "Add": "full-text search to the TODO list endpoint"
- Extract key words: "full-text search TODO list"
- Simplify: "todo search" (2 words, under 5 word limit)
- Kebab-case: **"todo-search"**

### Step 4: Populate Template
- Read: `.steerings/templates/feature-template.md`
- Replace `F###` → `F001`
- Replace `[Feature Name]` → "Full-text Search for TODOs"
- Fill sections:

```markdown
# F001: Full-text Search for TODOs

## Objective
Allow users to search their TODO items by keywords in the title and description fields using full-text search with relevance ranking. This enables users to quickly find specific tasks without manually browsing through their entire list.

## Context
Currently, the TODO list endpoint supports filtering by status and tags, but does not support text-based search. Users with many TODO items need a way to quickly locate specific tasks by searching for keywords.

## Constraints
- Performance requirements: Search queries must respond in <500ms
- Must follow Clean Architecture patterns
- Must achieve >80% test coverage
- Only return TODOs belonging to the authenticated user

## Acceptance Criteria
- [ ] User can search TODOs by keyword using query parameter
- [ ] Search covers both title and description fields
- [ ] Results are ranked by relevance
- [ ] Only authenticated user's TODOs are returned
- [ ] Empty search query returns all user's TODOs
- [ ] Search is case-insensitive
- [ ] Response time < 500ms for typical queries
- [ ] Handles special characters safely (no SQL injection)

## API Design (if applicable)
[TODO: Fill in - Define exact endpoint, parameters, and response format]

## Technical Approach
[TODO: Fill in - Consider PostgreSQL full-text search vs LIKE queries]

## Security Considerations
[TODO: Fill in - Input validation, SQL injection prevention, authorization checks]

## Testing Requirements
[TODO: Fill in - Unit tests for search logic, integration tests for endpoint]
```

### Step 5: Create File
- Path: `.steerings/features/F001-todo-search.md`
- Write populated content

### Step 6: Update README
- Read: `.steerings/README.md`
- Find: `### Active Features (Ready to Implement)`
- Add: `- [F001: Full-text Search for TODOs](features/F001-todo-search.md)`

### Step 7: Output Summary
```
✓ Detected type: Feature
✓ Generated ID: F001
✓ Created: .steerings/features/F001-todo-search.md
✓ Updated: .steerings/README.md

Summary:
- File: .steerings/features/F001-todo-search.md
- Sections populated:
  - Objective ✓
  - Context ✓
  - Constraints ✓
  - Acceptance Criteria ✓ (8 criteria generated)
- Sections needing attention:
  - API Design [TODO: Fill in]
  - Technical Approach [TODO: Fill in]
  - Security Considerations [TODO: Fill in]
  - Testing Requirements [TODO: Fill in]

Next steps:
1. Review and edit .steerings/features/F001-todo-search.md
2. Complete [TODO] sections with specific implementation details
3. Decide on search implementation (PostgreSQL full-text vs LIKE)
4. Define exact API endpoint and parameters
5. Run: Implement F001
```

## Result

**File Created**: `.steerings/features/F001-todo-search.md`

**README.md Updated**:
```markdown
### Active Features (Ready to Implement)
- [F001: Full-text Search for TODOs](features/F001-todo-search.md)
```

**User Action Required**:
1. Review the generated file
2. Fill in [TODO] sections:
   - API Design (endpoint, parameters, response format)
   - Technical Approach (PostgreSQL full-text search vs LIKE)
   - Security Considerations (input validation details)
   - Testing Requirements (specific test cases)
3. Run `Implement F001` when ready
