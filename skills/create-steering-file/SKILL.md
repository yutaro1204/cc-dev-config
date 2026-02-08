---
name: create-steering-file
description: Generate a steering file (Feature/Bug/Refactoring) from a natural language description
allowed-tools: Read, Write, Edit, Glob, Grep
disable-model-invocation: true
---

# Create Steering File Skill

This skill generates well-structured steering files to guide feature implementation, bug fixes, or refactoring tasks.

## What This Skill Does

1. Parses your natural language feature request, bug report, or refactoring idea
2. Determines the appropriate type (Feature/Bug/Refactoring)
3. Calculates the next available ID (F###, B###, R###)
4. Selects and populates the appropriate template
5. Creates the steering file in the correct directory
6. Updates the `.steerings/README.md` index

## Usage

Invoke with: `/create-steering-file` or provide as context

Then provide your request in natural language:

**For Features:**
```
Add full-text search with pagination support
```

**For Bugs:**
```
Fix: Authentication token expires prematurely
```

**For Refactoring:**
```
Refactor: Extract validation logic into reusable functions
```

**With Explicit ID:**
```
F042: Add WebSocket support for real-time updates
```

## Type Detection

The skill uses these rules to determine the type:

1. **Explicit Keywords**: "Feature:", "Bug:", "Fix:", "Refactor:"
2. **Explicit ID**: F### (Feature), B### (Bug), R### (Refactoring)
3. **Heuristics**:
   - "Fix", "Error", "Issue", "Not working", "Broken" → Bug
   - "Refactor", "Extract", "Improve", "Clean up", "Restructure" → Refactoring
   - Default → Feature

## ID Assignment

- Scans existing files in the target directory
- Uses next sequential number (F001, F002, F003...)
- Skips gaps (if F001 and F003 exist, next is F004)
- Allows explicit ID override (but warns if duplicate exists)

## Template Population

The skill intelligently fills in:

- **Objective/Summary**: Extracted from your description
- **Context/Motivation**: Basic context from description
- **Acceptance Criteria**: Auto-generated based on description
- **Files to Change**: Marked as [TODO: Fill in]
- **Testing**: Structure provided, details needed

## Workflow Algorithm

```
1. READ user's natural language request
2. PARSE request → Extract type, description, ID (if explicit)
3. OPTIONALLY READ project documentation to understand context (if available):
     - CHECK and READ CLAUDE.md if it exists (project overview, domain model, patterns)
     - CHECK and READ docs/ files if they exist:
       - docs/functional-design.md (API specs, data models)
       - docs/architecture.md (architecture patterns)
       - docs/repository-structure.md (directory organization, file naming)
       - docs/ubiquitous-language.md (domain terminology)
       - Other relevant documentation files
     - Extract available: domain entities, naming conventions, patterns, constraints
     - IF no documentation found, proceed with generic approach
4. IF no explicit ID:
     GLOB .steerings/{features,bugs,refactoring}/*.md
     CALCULATE next_id = max(existing_ids) + 1
5. GENERATE short_description from first sentence (kebab-case, max 5 words)
6. READ appropriate template from .steerings/templates/
7. POPULATE template using available context:
     - Replace [Feature Name] with description
     - Fill Objective section
     - Fill Context section using project knowledge (if available)
     - Fill Constraints section with project-specific requirements (if found)
     - Generate acceptance criteria based on description and discovered patterns
     - Suggest likely files to change based on request and project structure
     - Reference relevant documentation (if found)
     - Mark incomplete sections with [TODO: Fill in]
8. WRITE file to .steerings/{type}/{ID}-{short_description}.md
9. READ .steerings/README.md
10. EDIT .steerings/README.md:
     - Add new entry under "Active Features" (or appropriate section)
     - Format: - [F###: Description](features/F###-description.md)
11. OUTPUT summary:
     - File path
     - Assigned ID
     - Populated sections
     - Sections needing attention
     - Next steps
```

## Smart Features

### Project Context Understanding
- **Optionally reads CLAUDE.md** if it exists to understand domain model, architecture patterns, naming conventions
- **Optionally reads docs/ files** if they exist for detailed specifications, patterns, and requirements
- Extracts technical terms from documentation when available
- Recognizes common patterns (CRUD, filtering, search, pagination) from available documentation
- Suggests likely files to modify based on discovered project structure and patterns
- Applies project-specific constraints found in documentation
- Uses correct terminology from project documentation when available

### Acceptance Criteria Generation
Auto-generates criteria based on type:

**Feature:**
- Core functionality works as described
- Appropriate authorization/access controls if applicable
- Error handling for edge cases
- Performance requirements (use project standards if documented)
- Test coverage requirements (use project standards if documented)

**Bug:**
- Steps to reproduce
- Expected vs actual behavior
- Verification steps
- No regression on related features

**Refactoring:**
- No behavior changes
- All existing tests pass
- Code quality metrics improved (reduced complexity, duplication)
- No performance regression

### Short Description Rules
- Max 5 words
- Kebab-case (lowercase with hyphens)
- Remove articles (a, an, the)
- Use action verbs

Examples:
- "Add full-text search" → "full-text-search"
- "Fix authentication token expiry" → "auth-token-expiry"
- "Refactor validation into helpers" → "extract-validators"
- "Add date range filtering" → "date-range-filtering"

## Output Format

```
✓ Detected type: [Feature|Bug|Refactoring]
✓ Generated ID: [ID]
✓ Created: .steerings/{type}/{ID}-{description}.md
✓ Updated: .steerings/README.md

Summary:
- File: [path]
- Sections populated: [list]
- Sections needing attention: [list]

Next steps:
1. Review and edit [filename]
2. Complete [TODO sections]
3. Run: Implement [ID]
```

## Error Handling

- **Missing .steerings/**: Error - directory structure should exist
- **Duplicate ID**: Warn and suggest next available
- **Ambiguous type**: Ask clarifying question via AskUserQuestion tool
- **Empty description**: Prompt for details via AskUserQuestion tool
- **Invalid ID format**: Suggest correct format (F###, B###, R###)

## Examples

### Example 1: Simple Feature
```
Input: Add date range filtering to data list

Process:
- Type: Feature (no keywords, default)
- ID: F001 (first feature)
- Description: date-range-filtering

Populated:
- Objective: Allow users to filter data by date ranges
- Acceptance Criteria:
  - [ ] User can filter by start date
  - [ ] User can filter by end date
  - [ ] Can combine with existing filters
  - [ ] Appropriate authorization checks
  - [ ] Performance meets project standards
```

### Example 2: Bug Fix
```
Input: Fix: Authorization check missing in data endpoint

Process:
- Type: Bug (detected "Fix:" prefix)
- ID: B001 (first bug)
- Severity: Critical (auto-detected from "security" context)

Populated:
- Summary: Authorization check missing in data endpoint
- Current Behavior: All data returned regardless of user
- Expected: Only authorized data should be visible
- Steps to Reproduce: [TODO: Fill in]
- Affected Code: [TODO: Identify based on project structure]
```

### Example 3: Refactoring
```
Input: Refactor: Extract validation logic into reusable validator functions

Process:
- Type: Refactoring (detected "Refactor:" prefix)
- ID: R001 (first refactoring)

Populated:
- Objective: Extract validation logic into reusable functions
- Motivation: Reduce code duplication across codebase
- Current State: Validation logic duplicated in multiple places
- Files Affected: [TODO: Identify based on project structure]
```

### Example 4: With Explicit ID
```
Input: F042: Add CSV export functionality

Process:
- Type: Feature (from F prefix)
- ID: F042 (explicit, verify not duplicate)
- Description: csv-export

Output:
✓ Using explicit ID: F042
✓ Created: .steerings/features/F042-csv-export.md
```

## Implementation Instructions

### Step 1: Parse User Request
- Extract the full description from user input
- Check for explicit keywords (Feature:, Bug:, Fix:, Refactor:)
- Check for explicit ID format (F###, B###, R###)
- Apply heuristics if no explicit markers

### Step 2: Read Project Documentation (Optional)
Attempt to read relevant documentation to understand project context:

**Check and read if available:**
- `CLAUDE.md` - Project overview, domain model, patterns, naming conventions
- `README.md` - Project description, setup, conventions
- `docs/` directory - Any relevant documentation files

**Common documentation files to check:**
- `docs/functional-design.md` - API specifications, data models, endpoints
- `docs/architecture.md` - Architecture patterns, technology stack
- `docs/repository-structure.md` - Directory organization, file naming conventions
- `docs/ubiquitous-language.md` or similar - Domain terminology and naming rules
- `docs/development-guidelines.md` or `CONTRIBUTING.md` - Coding standards, best practices
- `docs/test-concepts.md` or testing documentation - Testing requirements and patterns

**If documentation found, extract:**
- Domain entities and their relationships
- API/endpoint naming conventions
- Architecture patterns and layers
- Security requirements and patterns
- Testing requirements and coverage standards
- Database/persistence patterns
- Validation patterns and frameworks
- File organization and structure conventions

**Use discovered context when:**
- Suggesting files to change
- Generating acceptance criteria
- Filling Context section
- Adding Constraints
- Creating code examples
- Referencing documentation

**If no documentation found:**
- Proceed with generic approach
- Use basic best practices for acceptance criteria
- Mark more sections as [TODO: Fill in]
- Focus on user's description for guidance

### Step 3: Determine Next ID (if not explicit)
```python
# Pseudo-code
files = glob(".steerings/{type}/*.md")
existing_ids = [extract_number(filename) for filename in files]
next_id = max(existing_ids) + 1 if existing_ids else 1
formatted_id = f"{prefix}{next_id:03d}"  # F001, B012, R003
```

### Step 4: Generate Short Description
- Take first sentence or complete description
- Remove "Add", "Fix:", "Refactor:" prefixes
- Convert to lowercase
- Remove articles (a, an, the)
- Replace spaces with hyphens
- Truncate to max 5 words
- Validate kebab-case format

### Step 5: Read Template
Read the appropriate template:
- Feature: `.steerings/templates/feature-template.md`
- Bug: `.steerings/templates/bug-template.md`
- Refactoring: `.steerings/templates/refactoring-template.md`

### Step 6: Populate Template

**For Features:**
- Replace `F###` with actual ID
- Replace `[Feature Name]` with short description
- Fill `Objective` section with 2-3 sentences from user description
- Fill `Context` section using project documentation knowledge (if available)
- Fill `Constraints` section with project-specific requirements from docs (if found)
- Generate acceptance criteria based on description and discovered patterns
- Suggest likely files to change based on:
  - Request content and affected functionality
  - Discovered project structure and patterns
  - Common conventions if no docs available
- Add references to relevant documentation (if found)
- Mark remaining sections: `[TODO: Fill in]`

**For Bugs:**
- Replace `B###` with actual ID
- Replace `[Bug Title]` with short description
- Fill `Summary` with one-line description
- Check severity based on keywords (Critical: security, data loss; High: broken feature)
- Fill `Current Behavior` and `Expected Result`
- Suggest affected code files based on:
  - Bug description and symptoms
  - Discovered project structure
  - Related file patterns
- Mark remaining sections: `[TODO: Fill in]`

**For Refactoring:**
- Replace `R###` with actual ID
- Replace `[Refactoring Title]` with short description
- Fill `Objective` with 2-3 sentences
- Fill `Motivation` with why refactoring is needed
- Suggest files that might be affected based on:
  - Refactoring scope from description
  - Discovered project patterns
  - Common code organization principles
- Reference architecture patterns from documentation (if available)
- Mark remaining sections: `[TODO: Fill in]`

### Step 7: Create File
- Filename format: `{ID}-{short_description}.md`
- Path: `.steerings/{type}/{filename}`
- Write populated template content

### Step 8: Update README.md
- Read `.steerings/README.md`
- Find the "Active Features" (or appropriate section for bugs/refactoring)
- Add new entry: `- [F###: Description](features/F###-description.md)`
- Write updated README

### Step 9: Provide Summary
Output to user:
- Success indicators (✓)
- File path created
- ID assigned
- Sections that were populated
- Sections marked [TODO: Fill in]
- Next steps with explicit instruction

## Key Principles

1. **Read Documentation First (if available)**: Check for CLAUDE.md, README.md, and docs/ files to understand project context before populating the template
2. **Use Project Patterns (when found)**: Apply project-specific patterns, naming conventions, and architecture from documentation when available
3. **Adapt to Project**: If no documentation exists, use generic best practices and common conventions
4. **Don't Overdo It**: Mark sections as [TODO] rather than making up content or assumptions
5. **Extract from User Input**: Use the user's words for objective/summary
6. **Generate Smart Defaults**: Create reasonable acceptance criteria from description and any discovered patterns
7. **Suggest Files Intelligently**: Base suggestions on request content, discovered structure, and common practices
8. **Clear Next Steps**: Tell user what to complete and how to proceed
9. **Error Gracefully**: Provide helpful error messages and suggestions
10. **Maintain Structure**: Preserve all template sections even if marked [TODO]

## Edge Cases

1. **First Steering File**: Handle case where no files exist (ID = 001)
2. **Gaps in Numbering**: Use max(existing) + 1, don't fill gaps
3. **Duplicate Explicit ID**: Warn user, suggest next available
4. **Ambiguous Description**: Ask clarifying questions
5. **Very Long Description**: Use first 2-3 sentences for objective
6. **Missing Keywords**: Apply heuristics confidently

## Success Criteria

The skill is successful when it:
- ✓ Checks for and reads available documentation before creating steering file
- ✓ Creates valid steering file with correct ID
- ✓ Populates template with user's description and any discovered project context
- ✓ Generates helpful acceptance criteria based on description and discovered patterns
- ✓ Suggests likely files to change based on request and project structure
- ✓ References relevant documentation when found
- ✓ Applies discovered project constraints and standards
- ✓ Updates README.md index
- ✓ Provides clear next steps
- ✓ Handles all three types (Feature/Bug/Refactoring)
- ✓ Marks incomplete sections clearly
- ✓ Uses proper filename format
- ✓ Works effectively even without project documentation
