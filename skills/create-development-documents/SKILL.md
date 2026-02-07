---
name: create-development-documents
description: Create development documents described in CLAUDE.md.
allowed-tools: Read, Write, Edit, Grep, Glob
---

# Overview

This skill creates comprehensive development documents for the project based on templates and project specifications.

## Quick Start for New Projects

**For developers setting up a new project:**

1. **Copy the project template**: Find `PROJECT_TEMPLATE.md` in this skill directory
2. **Fill in your project details**: Replace all `[FILL IN]` sections with your actual technology stack, requirements, and specifications
3. **Save your filled template**: Keep it as `PROJECT_SPEC.md` or similar in your project root or `.claude/` directory
4. **Invoke this skill**: Reference your filled template, and the skill will generate all 8 documentation files in `docs/`

**Template Location**: `.claude/skills/create-development-documents/PROJECT_TEMPLATE.md`

**What the template includes:**

- Technology stack configuration (frontend, backend, database, cache, testing, etc.)
- Product requirements (business model, features, non-functional requirements)
- Functional design (user flows, data models, routes, API endpoints)
- Architecture decisions and rationale
- Repository structure preferences
- Development guidelines and coding standards
- Environment setup requirements
- Testing strategy and coverage goals
- Domain terminology (ubiquitous language)
- Deployment configuration

## Available Document Templates

The following system-agnostic templates are available in `.claude/skills/create-development-documents/examples/`:

1. **architecture.md** - Technical architecture, technology stack, system design, deployment strategy
2. **development-guidelines.md** - Coding standards, naming conventions, best practices, workflow procedures
3. **environments.md** - Development and production environment configurations, setup instructions
4. **functional-design.md** - User flows, UI/UX specifications, data models, components, routes, API design
5. **product-requirements.md** - Product vision, user needs, business requirements, functional/non-functional requirements
6. **repository-structure.md** - Directory structure, file naming conventions, import patterns, version control
7. **test-concepts.md** - Testing types (unit, integration, E2E), testing pyramid, mocking philosophy, TDD
8. **ubiquitous-language.md** - Domain-Driven Design terminology, business concepts, domain rules

## How to Use Templates

1. **Read the appropriate template** from the examples directory
2. **Adapt the template** to the specific project requirements below
3. **Replace all placeholders** (in [brackets]) with actual project-specific values
4. **Remove or modify sections** that don't apply to this project
5. **Preserve universal concepts** (especially in test-concepts.md)
6. **Write the document** to the `docs/` directory in the project root

## Important Notes

- Templates contain placeholders in [brackets] like [Framework], [Database], [Language] that must be replaced
- Templates include notes explaining they should be adapted - remove these notes from final documents
- Each template has section headers and structure that should be preserved
- Some sections may not be applicable to this project and can be removed
- Universal testing concepts in test-concepts.md should be kept as-is

## Updating Existing Documents

If a document already exists in `docs/`:

1. **Read the existing document** first
2. **Read the corresponding template** to see what sections might be missing
3. **Ask the user** whether to:
   - Update/enhance the existing document (add missing sections)
   - Replace the entire document with a new version
   - Create a backup before making changes
4. **Preserve existing content** that is already well-written and accurate
5. **Fill in gaps** using the template as a guide

---

# Project-Specific Information

> **Note**: This section should be customized for your specific project. Replace all placeholders with your actual project details.

Development documents should be created in accordance with the specification of your project.
Each document's details can be referenced in CLAUDE.md (if available) or gathered from the project requirements.

## Product Requirements Template

**Application Overview:**

- Application type: [e.g., E-commerce site, SaaS platform, Mobile app, etc.]
- Application name: [Your Project Name]
- Core business model: [Brief description of how the application works]
- Key stakeholders: [User types, roles, personas]
- Revenue model: [How the application generates revenue]
- Unique value proposition: [What makes this application special]

**Specifications to include:**

- Product vision and needs
- Target users and issues
- Logistics (if applicable)
- Business requirements
- Main functions of this system
- Functional requirements
- Non-functional requirements

## Functional Design Template

**Core User Actions:**
List the main actions users can perform in the application:

- [Action 1: e.g., Authentication - Sign in/Sign up]
- [Action 2: e.g., Browse content - View lists, search, filter]
- [Action 3: e.g., Transaction - Purchase, checkout, payment]
- [Action 4: e.g., Profile management - Update user information]
- [Action 5: e.g., Content management - Create, update, delete content]

**Specifications to include:**

- Architecture for each function above
- System structure diagram
- Data model definition
- Component design
- Routes structure (Path, Site map, Wireframe)
- API design

## Architecture Template

**Technology Stack:**

- Framework: [e.g., React Router v7, Next.js, Express, Django, etc.]
- Rendering: [e.g., SSR, CSR, SSG]
- Database: [e.g., PostgreSQL, MongoDB, MySQL]
- Cache: [e.g., Redis, Valkey, Memcached]
- Storage: [e.g., S3, Cloud Storage, Local]

**Specifications to include:**

- Dependencies
- Development tools and practices
- Performance requirements
- Infrastructure and deployment

## Repository Structure Template

**Specifications to include:**

- Directory and file structure
- Directory roles and responsibilities
- File naming conventions and rules
- Code organization patterns

## Development Guidelines Template

**Technology References:**

- Framework documentation: [e.g., React Router v7, Next.js, Django]
- External resources: [e.g., MCP servers, official docs, style guides]
- Package management: Refer to [package.json, requirements.txt, etc.]
- Styling: [e.g., Tailwind CSS, CSS Modules, styled-components]
- Testing: [e.g., Vitest, Jest, Pytest, etc.]

**Specifications to include:**

- Coding practices and patterns
- Naming conventions for methods and variables
- Validation strategies
- Styling approach
- Linter configuration
- Testing strategy

## Ubiquitous Language Template

**Domain Terminology:**
Define key domain terms and concepts:

- Project name: [Your Project Name]
- [Primary Entity 1]: [Definition]
- [Primary Entity 2]: [Definition]
- [Key Concept 1]: [Definition]
- [Key Concept 2]: [Definition]
- [Business Term 1]: [Definition]
- [Business Term 2]: [Definition]

## Environments Template

**Environment Configuration:**

- Development environment: [Local setup details]
- Staging/Test environment: [Staging setup details]
- Production environment: [Production setup details]
- CI/CD environment: [CI/CD pipeline details]

**Infrastructure Services:**

- Container orchestration: [e.g., Docker Compose, Kubernetes, etc.]
- Database setup: [How to set up database for each environment]
- Cache setup: [How to set up cache for each environment]
- Storage setup: [How to set up storage for each environment]
- Message queues: [If applicable, e.g., RabbitMQ, Kafka]
- Email service: [If applicable, e.g., SendGrid, SMTP]

**Environment Variables:**
List all environment variables needed:

- [ENV_VAR_1]: [Description and purpose]
- [ENV_VAR_2]: [Description and purpose]
- [DATABASE_URL]: [Connection string format]
- [API_KEY]: [Third-party service keys]

**Setup Instructions:**

- Prerequisites (software, tools, accounts needed)
- Step-by-step local development setup
- How to run the application in development
- How to run tests
- How to deploy to staging/production
- Troubleshooting common issues

**Specifications to include:**

- Local development environment setup
- Container configuration (Docker, etc.)
- Database and service initialization
- Environment variable management
- CI/CD pipeline configuration
- Deployment procedures
- Monitoring and logging setup

## Test Concepts Template

**Testing Strategy:**

- Testing philosophy: [e.g., TDD, Test-after, Behavior-driven]
- Test coverage goals: [e.g., 80% unit, 20% integration, 10% E2E]
- Testing tools: [List all testing frameworks and tools]

**Test Types:**

- Unit testing framework: [e.g., Vitest, Jest, Pytest, JUnit]
- Integration testing approach: [How integration tests are structured]
- E2E testing framework: [e.g., Playwright, Cypress, Selenium]
- Performance testing: [If applicable]
- Security testing: [If applicable]

**Testing Infrastructure:**

- Test database: [How test database is set up]
- Test services: [Docker containers, mock services, etc.]
- Test data management: [Fixtures, factories, seeds]
- CI/CD testing: [How tests run in pipeline]

**Mocking Strategy:**

- What to mock in unit tests
- What to mock in integration tests
- External service mocking approach
- Test doubles strategy

**Specifications to include:**

- Core testing concepts (preserved from universal template)
- Project-specific test structure and organization
- Testing pyramid distribution
- Mocking philosophy and decisions
- TDD practices (if applicable)
- Test execution strategy
- CI/CD integration
- Test data management

---

# Workflow for Creating Documents

## Recommended Approach (For New Projects)

**If a filled PROJECT_TEMPLATE.md exists:**

1. **Read the filled project template**: Look for `PROJECT_SPEC.md`, `PROJECT_TEMPLATE.md` (filled), or similar in project root or `.claude/` directory
2. **Extract project-specific information** from the filled template (tech stack, requirements, etc.)
3. **Read the appropriate document template** from `.claude/skills/create-development-documents/examples/[document-name].md`
4. **Replace template placeholders** with information from the filled project template
5. **Write the document** to `docs/[document-name].md`

## Alternative Approach (For Existing Projects)

**If no filled template exists, gather information manually:**

1. **Identify the document type** requested by the user
2. **Read the corresponding template** from `.claude/skills/create-development-documents/examples/[document-name].md`
3. **Analyze the template structure** and sections
4. **Gather project-specific information**:
   - From CLAUDE.md (project overview, tech stack)
   - From the "Project-Specific Information" section in this SKILL.md (if customized)
   - From the codebase using available tools (Grep, Glob, Read)
   - From package manager files (package.json, requirements.txt, Gemfile, etc.)
   - From configuration files (vite.config, next.config, django settings, etc.)
5. **Replace template placeholders** with actual values:
   - [Framework] → Your actual framework (e.g., React Router v7, Next.js, Django, Express)
   - [Database] → Your database (e.g., PostgreSQL, MongoDB, MySQL, SQLite)
   - [Cache Service] → Your cache (e.g., Redis, Valkey, Memcached)
   - [Container Tool] → Your container tool (e.g., Docker Compose, Podman, Kubernetes)
   - [Language] → Your language (e.g., TypeScript, JavaScript, Python, Java)
   - [ORM] → Your ORM (e.g., Prisma, TypeORM, SQLAlchemy, Hibernate)
   - [Test Framework] → Your test framework (e.g., Vitest, Jest, Pytest, JUnit)
   - [E2E Framework] → Your E2E tool (e.g., Playwright, Cypress, Selenium)
   - [Project Type] → Your project type (e.g., E-commerce site, SaaS platform, CMS)
   - [Project Name] → Your project name
   - etc.
6. **Adapt content to project specifics**:
   - Use actual file paths from the codebase
   - Include actual function/component names
   - Reference actual routes and endpoints
   - Include project-specific examples
7. **Remove template notes** (lines starting with "> **Note**: This is a template...")
8. **Write the document** to `docs/[document-name].md`
9. **Verify completeness** - ensure all sections are filled with meaningful content

## Example Replacements

**Example 1 - Framework Patterns:**

Template:

```markdown
### [Framework Name] Patterns

- Use [component pattern] for [use case]
- Use [data fetching pattern] for [scenario]
```

Becomes (React Router v7):

```markdown
### React Router v7 Patterns

- Use loader functions for data fetching
- Use action functions for mutations
```

Or becomes (Next.js):

```markdown
### Next.js Patterns

- Use Server Components for static content
- Use Server Actions for mutations
```

**Example 2 - Technology Stack:**

Template:

```markdown
- Database: [Database Name]
- ORM: [ORM Name]
- Cache: [Cache Service]
```

Becomes (Project A):

```markdown
- Database: PostgreSQL
- ORM: Prisma
- Cache: Redis
```

Or becomes (Project B):

```markdown
- Database: MongoDB
- ORM: Mongoose
- Cache: In-memory
```

## Tips

- **Be specific**: Replace generic placeholders with actual project values
- **Be comprehensive**: Include all relevant sections from the template
- **Be consistent**: Use the same terminology throughout the document
- **Be practical**: Include real examples from the codebase
- **Reference other docs**: Cross-reference related documents when appropriate
