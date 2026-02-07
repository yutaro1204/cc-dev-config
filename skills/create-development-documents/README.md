# Create Development Documents Skill

This skill generates comprehensive development documentation for software projects by combining system-agnostic templates with project-specific information.

## 📁 Directory Structure

```
create-development-documents/
├── SKILL.md                 # Skill configuration and instructions
├── PROJECT_TEMPLATE.md      # Template for developers to fill in
├── README.md               # This file
└── examples/               # System-agnostic document templates
    ├── architecture.md
    ├── development-guidelines.md
    ├── environments.md
    ├── functional-design.md
    ├── product-requirements.md
    ├── repository-structure.md
    ├── test-concepts.md
    └── ubiquitous-language.md
```

## 🚀 Quick Start

### For Developers Setting Up a New Project

1. **Copy the project template**

   ```bash
   cp .claude/skills/create-development-documents/PROJECT_TEMPLATE.md PROJECT_SPEC.md
   ```

2. **Fill in your project details**
   - Open `PROJECT_SPEC.md`
   - Replace all `[FILL IN]` sections with your actual information
   - Include technology stack, requirements, features, etc.

3. **Invoke the skill**
   - Ask Claude Code to create development documents using your filled template
   - Example: "Use my PROJECT_SPEC.md to create all development documents"

4. **Review generated documents**
   - Documents will be created in `docs/` directory
   - Review and refine as needed

### For Developers Working on Existing Projects

If you don't have a filled template, the skill can gather information from:

- `CLAUDE.md` (if exists)
- Codebase inspection (package.json, config files, etc.)
- Direct questions to you

## 📚 Available Templates

### 1. Product Requirements (`product-requirements.md`)

Documents business goals, user needs, and feature specifications.

**Covers:**

- Product vision and market needs
- Target user segments
- Business requirements and revenue model
- Functional requirements (features)
- Non-functional requirements (performance, security, scalability)

### 2. Functional Design (`functional-design.md`)

Details user flows, UI/UX specifications, and feature behavior.

**Covers:**

- User flows and interaction patterns
- System architecture diagrams
- Data models and entity relationships
- Component design
- Route structure and wireframes
- API design and endpoints

### 3. Architecture (`architecture.md`)

Describes technical architecture and system design decisions.

**Covers:**

- Technology stack (frontend, backend, database, cache, etc.)
- System design patterns
- Infrastructure and deployment
- Performance considerations
- Security architecture

### 4. Repository Structure (`repository-structure.md`)

Explains code organization and file conventions.

**Covers:**

- Directory structure
- File naming conventions
- Import patterns and path aliases
- Code organization principles
- Version control practices

### 5. Development Guidelines (`development-guidelines.md`)

Provides coding standards and best practices.

**Covers:**

- Coding patterns and conventions
- Naming conventions
- Validation strategies
- Styling approach
- Linter and formatter configuration
- Workflow procedures

### 6. Ubiquitous Language (`ubiquitous-language.md`)

Defines domain-specific terminology (Domain-Driven Design).

**Covers:**

- Core entities and their definitions
- Business concepts
- Transaction concepts
- Domain rules
- Anti-patterns (terms to avoid)
- Usage guidelines

### 7. Environments (`environments.md`)

Specifies environment configurations and setup.

**Covers:**

- Local development setup
- Staging/test environment
- Production environment
- Container configuration (Docker, etc.)
- Environment variables
- CI/CD pipeline
- Deployment procedures

### 8. Test Concepts (`test-concepts.md`)

Explains testing strategy and best practices.

**Covers:**

- Testing types (Unit, Integration, E2E)
- Testing pyramid distribution
- Mocking philosophy
- Test-Driven Development (TDD)
- Test infrastructure setup
- Best practices and common misconceptions

## 🔧 How It Works

### Template System

1. **System-Agnostic Templates** (`examples/`)
   - Generic templates with `[placeholder]` syntax
   - Universal concepts preserved (e.g., testing pyramid, TDD principles)
   - Adaptable to any technology stack

2. **Project Template** (`PROJECT_TEMPLATE.md`)
   - Structured form for developers to fill in
   - Covers all aspects: tech stack, requirements, architecture, etc.
   - Single source of truth for project specifications

3. **Skill Logic** (`SKILL.md`)
   - Reads filled project template or gathers info from codebase
   - Matches placeholders in templates with actual values
   - Generates complete, project-specific documentation

### Placeholder Replacement Examples

**Template:**

```markdown
- Framework: [Framework]
- Database: [Database]
- Testing: [Test Framework]
```

**With PROJECT_TEMPLATE filled in:**

```markdown
- Framework: React Router v7
- Database: PostgreSQL
- Testing: Vitest
```

## 📝 Usage Examples

### Example 1: Generate All Documents

```
User: I've filled in PROJECT_SPEC.md with my project details.
      Please create all development documents.

Claude: [Reads PROJECT_SPEC.md, then generates all 8 documents in docs/]
```

### Example 2: Generate Specific Document

```
User: Create the architecture.md document using my PROJECT_SPEC.md

Claude: [Reads PROJECT_SPEC.md, reads architecture.md template,
         replaces placeholders, writes to docs/architecture.md]
```

### Example 3: Update Existing Document

```
User: Update the test-concepts.md document with new TDD practices

Claude: [Reads existing docs/test-concepts.md,
         reads template for guidance,
         adds new content while preserving existing]
```

## 🎯 Benefits

### For Developers

- **Fast Setup**: Fill one template, get 8 comprehensive documents
- **Consistency**: All documents follow the same style and structure
- **Best Practices**: Templates include industry-standard patterns
- **Technology Agnostic**: Works with any tech stack

### For Teams

- **Onboarding**: New team members have comprehensive documentation
- **Alignment**: Everyone follows the same terminology and practices
- **Maintenance**: Easy to update as project evolves
- **Knowledge Preservation**: Documentation stays in sync with code

### For Projects

- **Professional**: Complete documentation set from day one
- **Scalable**: Structure supports project growth
- **Comprehensive**: Covers all aspects (business, technical, operational)
- **Living Documentation**: Easy to keep updated

## 🔄 Updating Templates

### For General Use (System-Agnostic)

If you want to improve the templates for all future projects:

1. Edit files in `examples/` directory
2. Keep placeholders in `[brackets]` format
3. Preserve universal concepts (especially in test-concepts.md)
4. Add template notes explaining customization needs

### For Specific Project

If you want to customize for your current project only:

1. Generate documents using the skill
2. Edit generated documents in `docs/` directory
3. Don't edit templates in `examples/` directory

## 📚 Related Resources

- **Core Testing Concepts**: `.claude/references/test-core-concepts.md` - Universal testing principles without framework-specific examples
- **CLAUDE.md**: Project root - Main project documentation reference
- **Skills Documentation**: See other skills in `.claude/skills/` directory

## ⚙️ Customization

### Adding New Document Types

1. Create new template in `examples/[document-name].md`
2. Add entry to "Available Document Templates" in `SKILL.md`
3. Add corresponding section to `PROJECT_TEMPLATE.md`
4. Update this README

### Modifying Workflow

Edit `SKILL.md` to change how the skill:

- Gathers information
- Processes templates
- Writes documents
- Handles existing documents

## 🤝 Contributing

When improving this skill:

1. Keep templates system-agnostic
2. Use `[placeholder]` format consistently
3. Add clear instructions and examples
4. Test with different technology stacks
5. Update documentation

## 💡 Tips

- **Start with PROJECT_TEMPLATE.md**: It's easier to fill one template than create 8 documents
- **Be specific**: The more details you provide, the better the generated documents
- **Review generated docs**: Always review and refine generated documentation
- **Keep in sync**: Update PROJECT_SPEC.md when your stack changes
- **Version control**: Commit both PROJECT_SPEC.md and generated docs
- **Iterate**: It's okay to regenerate documents as requirements evolve

## 📞 Support

If you encounter issues or have questions:

1. Check the examples in `examples/` directory
2. Review SKILL.md for detailed workflow
3. Examine PROJECT_TEMPLATE.md for all available fields
4. Look at generated documents in `docs/` for structure

---

**Happy Documenting! 📖**
