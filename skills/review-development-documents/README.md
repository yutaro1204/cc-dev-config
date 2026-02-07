# Review Development Documents Skill

This skill reviews development documentation against actual implementation to ensure documentation accurately reflects the codebase. It's technology-agnostic and domain-agnostic, working with any software project.

## 📁 Directory Structure

```
review-development-documents/
├── SKILL.md                    # Skill configuration and review framework
└── README.md                   # This file
```

## 🎯 Why This Exists

Documentation often becomes outdated as code evolves. This skill helps you:

- **Verify accuracy**: Ensure documentation matches actual implementation
- **Find gaps**: Identify missing or incomplete documentation
- **Maintain quality**: Keep documentation up-to-date with code changes
- **Onboard faster**: Trust that documentation reflects reality
- **Reduce confusion**: Eliminate contradictions between docs and code

## 🚀 Quick Start

### Basic Usage

```
User: Please review my development documents against the codebase

Claude: [Reviews all documents in docs/ directory and generates DOCUMENTATION_REVIEW_REPORT.md]
```

### Review Specific Document

```
User: Review the functional-design.md against implementation

Claude: [Reviews only functional-design.md and provides findings]
```

### Focus on Specific Area

```
User: Check if our API endpoints match the functional design

Claude: [Reviews API implementation against documented endpoints]
```

## 📋 What Gets Reviewed

The skill comprehensively reviews eight types of documentation:

### 1. Product Requirements (`product-requirements.md`)

Reviews product requirements against technical architecture to ensure business needs are technically supported.

**Checks:**
- Business goals alignment with technical architecture
- Feature requirements support
- User experience requirements feasibility
- Non-functional requirements (performance, security, scalability)
- Data requirements coverage
- Integration requirements planning
- Compliance and legal requirements

### 2. Functional Design (`functional-design.md`)

Reviews functional design against actual implementation to ensure specifications match reality.

**Checks:**
- Routing system implementation (all routes exist, paths match)
- Component architecture (components exist, hierarchy matches)
- Data model implementation (entities, fields, relationships)
- API implementation (endpoints, request/response formats)
- Business logic services
- State management
- Type definitions (TypeScript/Flow)
- User flow validation
- UI/UX implementation
- Validation and error handling

### 3. Architecture (`architecture.md`)

Reviews technical architecture for completeness, consistency, and best practices.

**Checks:**
- Architecture overview and diagrams
- Component architecture
- Data architecture (database design, data flow)
- API architecture
- Security architecture
- Performance architecture
- Scalability architecture
- Reliability and resilience
- Observability (logging, monitoring, tracing)
- Development and build architecture
- Testing architecture
- Third-party services and dependencies
- Infrastructure architecture

### 4. Ubiquitous Language (`ubiquitous-language.md`)

Reviews domain terminology for consistency across codebase.

**Checks:**
- Terminology definitions clarity
- Terminology usage in code (variables, functions, classes)
- Business rules documentation alignment
- API and data model consistency
- UI/UX terminology
- Cross-document consistency
- Domain-specific patterns (entities, actions, value objects)

### 5. Test Concepts (`test-concepts.md`)

Reviews test concepts document against actual testing implementation.

**Checks:**
- Testing strategy (pyramid, coverage goals)
- Unit testing (coverage, quality, patterns)
- Integration testing (coverage, quality)
- End-to-end testing (critical flows, stability)
- Test data management
- Testing best practices
- Performance testing (if applicable)
- Security testing (if applicable)
- Test automation and CI/CD integration

### 6. Repository Structure (`repository-structure.md`)

Reviews repository structure document against actual codebase organization.

**Checks:**
- Directory structure matches documentation
- File organization follows patterns
- Source code structure (entry points, features, components)
- Configuration files exist and are correctly placed
- Test structure matches documentation
- Documentation structure
- Build and output directories
- Version control patterns (.gitignore, hooks)
- Dependency management

### 7. Development Guidelines (`development-guidelines.md`)

Reviews development guidelines for clarity and ensures code follows documented practices.

**Checks:**
- Coding standards (formatting, style, naming conventions)
- Git workflow (branch naming, commit messages, PR process)
- Code review process
- Testing requirements
- Documentation requirements
- Security practices
- Performance guidelines
- Error handling and logging
- Dependency management
- CI/CD practices
- Onboarding and setup instructions

### 8. Environments (`environments.md`)

Reviews environments documentation against actual environment configuration.

**Checks:**
- Environment definitions (dev, staging, production)
- Development environment setup
- Environment variables documentation
- Configuration management
- Database configuration
- External services configuration
- Build and deployment processes
- Testing environments
- Staging/pre-production environment
- Production environment
- Environment parity
- Troubleshooting guides

## 📊 Review Report

After review, the skill generates `docs/DOCUMENTATION_REVIEW_REPORT.md` with:

### Overall Summary Table

| Document/Section       | DocumentationQuality | ImplementationStatus |
| ---------------------- | -------------------- | -------------------- |
| Product Requirements   | ✅/👍/⚠️/❌/❓       | ✅/👍/⚠️/❌/❓       |
| Functional Design      | ✅/👍/⚠️/❌/❓       | ✅/👍/⚠️/❌/❓       |
| Architecture           | ✅/👍/⚠️/❌/❓       | ✅/👍/⚠️/❌/❓       |
| Ubiquitous Language    | ✅/👍/⚠️/❌/❓       | ✅/👍/⚠️/❌/❓       |
| Test Concepts          | ✅/👍/⚠️/❌/❓       | ✅/👍/⚠️/❌/❓       |
| Repository Structure   | ✅/👍/⚠️/❌/❓       | ✅/👍/⚠️/❌/❓       |
| Development Guidelines | ✅/👍/⚠️/❌/❓       | ✅/👍/⚠️/❌/❓       |
| Environments           | ✅/👍/⚠️/❌/❓       | ✅/👍/⚠️/❌/❓       |

**Status Indicators:**
- ✅ **Excellent**: Fully compliant, no issues
- 👍 **Good**: Adequate with minor improvements needed
- ⚠️ **Partial**: Significant gaps exist
- ❌ **Missing**: Not addressed or severely incomplete
- ❓ **Unclear**: Cannot determine status

### Detailed Findings

For each section, the report includes:

1. **Status**: Visual indicator of compliance level
2. **Findings**: Specific gaps, concerns, or observations
3. **Evidence**: References to documentation sections and code files
4. **Recommendations**: Concrete actions to address issues
5. **Priority**: Critical | High | Medium | Low

## 🔧 How It Works

### Review Process

1. **Preparation**
   - Identifies project specifics (tech stack, domain)
   - Locates documentation files in `docs/`
   - Sets up review context

2. **Systematic Review**
   - Reviews each document type systematically
   - Uses comprehensive checklists adapted to project
   - Documents findings with evidence

3. **Cross-Document Validation**
   - Compares findings across documents
   - Identifies inconsistencies between documents
   - Verifies alignment between requirements, design, and implementation

4. **Prioritization**
   - Categorizes findings by priority
   - Focuses on critical issues first
   - Groups related findings

5. **Reporting**
   - Generates comprehensive review report
   - Includes summary table and detailed findings
   - Provides actionable recommendations

## 📝 Usage Examples

### Example 1: Comprehensive Review

```
User: Review all development documents

Claude: I'll review all documents in your docs/ directory.
        [Reads all documents, inspects codebase, generates report]

        Created DOCUMENTATION_REVIEW_REPORT.md with:
        - Overall summary showing 8 documents reviewed
        - 15 critical findings requiring immediate attention
        - 23 high-priority recommendations
        - Detailed evidence from codebase
```

### Example 2: Post-Implementation Review

```
User: We just implemented a new feature.
      Check if functional-design.md needs updates.

Claude: [Reviews functional design, compares with recent code changes,
         identifies discrepancies and missing documentation]
```

### Example 3: Pre-Release Audit

```
User: We're releasing v2.0 next week.
      Audit all documentation for accuracy.

Claude: [Comprehensive review of all documents,
         focuses on critical gaps that could affect release,
         prioritizes fixes needed before launch]
```

### Example 4: Onboarding Preparation

```
User: New team members start next month.
      Verify our documentation is accurate for onboarding.

Claude: [Reviews setup instructions, development guidelines,
         tests setup procedures against actual requirements,
         identifies outdated information]
```

## 🎯 Benefits

### For Developers

- **Trust Documentation**: Confidently rely on docs being accurate
- **Faster Debugging**: Eliminate confusion from outdated docs
- **Better Onboarding**: New team members get accurate information
- **Quality Assurance**: Catch documentation drift early

### For Teams

- **Knowledge Preservation**: Documentation stays current with code
- **Reduced Support**: Fewer questions from inaccurate docs
- **Improved Collaboration**: Everyone works from same source of truth
- **Professional Image**: Maintain high-quality documentation standards

### For Projects

- **Maintainability**: Easier to maintain and evolve codebase
- **Compliance**: Meet documentation requirements for audits
- **Risk Reduction**: Prevent issues from doc-code mismatches
- **Scalability**: Documentation supports project growth

## 🔄 When to Use This Skill

### Regular Intervals

- **Weekly/Sprint**: Quick check for recent changes
- **Monthly**: Comprehensive review of key documents
- **Quarterly**: Full audit of all documentation

### Specific Events

- **Before Release**: Ensure docs match upcoming release
- **After Major Features**: Update docs for new functionality
- **Team Changes**: Verify docs for onboarding new members
- **Refactoring**: Update docs after architectural changes
- **Compliance Audits**: Prepare for external reviews

## 💡 Tips for Best Results

### 1. Keep Documentation Accessible

```
docs/
├── product-requirements.md
├── functional-design.md
├── architecture.md
├── ubiquitous-language.md
├── test-concepts.md
├── repository-structure.md
├── development-guidelines.md
└── environments.md
```

### 2. Provide Context

Give the skill context about recent changes:
```
User: Review functional-design.md.
      We recently added authentication and user profiles.
```

### 3. Focus Reviews

Target specific areas when needed:
```
User: Check if our API endpoints match functional design
```

### 4. Act on Findings

- Address **Critical** issues immediately
- Plan **High** priority items for current sprint
- Schedule **Medium** items for next sprint
- Track **Low** items for future consideration

### 5. Regular Maintenance

- Review docs with each major feature
- Update docs before they diverge significantly
- Make documentation updates part of Definition of Done

## 🔍 Understanding Review Findings

### Documentation Quality

Evaluates the documentation itself:
- **✅ Excellent**: Comprehensive, clear, well-structured
- **👍 Good**: Adequate with minor gaps
- **⚠️ Partial**: Significant gaps or unclear sections
- **❌ Missing**: Absent or severely incomplete

### Implementation Status

Evaluates how well implementation matches docs:
- **✅ Excellent**: Fully matches documentation
- **👍 Good**: Mostly matches with minor deviations
- **⚠️ Partial**: Significant gaps between docs and code
- **❌ Missing**: Features documented but not implemented

## 🤝 Contributing

When improving this skill:

1. Keep framework technology-agnostic
2. Focus on universal patterns
3. Add framework-specific checks where helpful
4. Test with different tech stacks
5. Update documentation

## 📚 Related Skills

- **create-development-documents**: Generate comprehensive documentation from templates
- **update-development-documents**: Update specific sections of existing documentation

## ⚙️ Customization

### Add Project-Specific Checks

Before running the review, you can specify:

```
User: Review documents. We're a fintech app,
      so extra attention to security and compliance.

Claude: [Adapts review to focus on financial regulations,
         PCI compliance, security architecture]
```

### Technology-Specific Focus

```
User: Review functional design. We use React Router v7.

Claude: [Uses React Router-specific patterns:
         loader functions, action functions, etc.]
```

## 📞 Support

If you encounter issues:

1. Check SKILL.md for detailed review framework
2. Ensure documents are in `docs/` directory
3. Verify document naming matches expected names
4. Review DOCUMENTATION_REVIEW_REPORT.md for findings

## 🏆 Best Practices

### 1. Document First, Then Code

Keep documentation slightly ahead of implementation:
```
1. Write/update documentation
2. Review against existing code
3. Implement new features
4. Re-review to verify accuracy
```

### 2. Make Reviews Part of Workflow

Include in CI/CD or regular team practices:
```
- Code review checklist: "Documentation updated?"
- Sprint end: Review docs for changes this sprint
- Release prep: Comprehensive documentation audit
```

### 3. Address Findings Systematically

Don't let review reports pile up:
```
- Triage findings by priority
- Create tickets for high-priority items
- Schedule time for documentation maintenance
- Track documentation debt
```

### 4. Maintain Documentation Standards

Use this skill to enforce consistency:
```
- Regular reviews ensure standards are followed
- Identify patterns in findings
- Update guidelines based on common issues
- Share findings with team for learning
```

## 🎓 Understanding the Framework

The review framework is based on:

- **Software Architecture Best Practices**: Industry-standard patterns
- **Domain-Driven Design**: Ubiquitous language principles
- **Documentation Standards**: Clear, comprehensive, accurate
- **Quality Assurance**: Verification and validation
- **Agile Practices**: Living documentation that evolves with code

## 📈 Measuring Success

Track improvement over time:

- **Trend Analysis**: Are findings decreasing?
- **Priority Distribution**: Are critical issues being addressed?
- **Documentation Completeness**: Are gaps being filled?
- **Team Velocity**: Do accurate docs help move faster?
- **Onboarding Time**: Do new members get productive faster?

---

**Keep Your Documentation Accurate! 📖✅**
