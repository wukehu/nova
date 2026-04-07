---
description: Generate comprehensive documentation from requirements, design, and implementation
argument-hint: <documentation type or scope>
allowed-tools: [Read, Write, Edit, Grep, Bash, Agent]
---

# Document Generation

You are generating comprehensive documentation from requirements, design, and implementation. Create clear, well-structured documentation.

## Core Principles

- **User-centric**: Write for your audience (developers, users, operators)
- **Structured**: Organize information logically with clear sections
- **Comprehensive**: Cover all relevant aspects
- **Maintainable**: Keep documentation in sync with code and design

---

## Phase 1: Documentation Scope

**Goal**: Determine what documentation to generate

Input: $ARGUMENTS

**Actions**:
1. Create a todo list to track documentation progress
2. Determine documentation scope:
   - Project overview
   - Architecture documentation
   - API documentation
   - User guides
   - Development guides
3. Identify available sources of information:
   - Requirements analysis
   - Architecture design
   - Detailed design
   - Codebase
4. Plan the documentation structure

---

## Phase 2: Documentation Generation

**Goal**: Generate documentation from sources

**Actions**:
1. For each documentation type:
   - **Project Overview**: Create README.md with project info
   - **Architecture**: Generate ARCHITECTURE.md from designs
   - **API Documentation**: Extract from code comments or design
   - **User Guides**: Create step-by-step instructions
   - **Development Guides**: Document setup and workflow

**Project Overview (README.md)**:
```markdown
# [Project Name]

[Brief project description]

## Features

- [Feature 1]
- [Feature 2]
- [Feature 3]

## Quick Start

### Prerequisites
- [Requirement 1]
- [Requirement 2]

### Installation
```bash
# Installation commands
```

### Usage
```bash
# Example usage
```

## Architecture

[High-level architecture description]

## Documentation

- [Architecture](./docs/architecture.md)
- [API](./docs/api.md)
- [User Guide](./docs/user-guide.md)

## Contributing

[Contribution guidelines]

## License

[License information]
```

---

## Phase 3: API Documentation Generation

**Goal**: Generate API documentation

**Actions**:
1. Extract API endpoints from:
   - Code comments and annotations
   - Swagger/OpenAPI documentation
   - Design documents
2. Organize endpoints by resource
3. Include examples

**API Documentation Template**:
```markdown
# API Documentation

## Authentication

All endpoints require authentication using:
- Bearer token: `Authorization: Bearer <token>`
- API key: `X-API-Key: <key>`

## Rate Limits

- 100 requests per minute per user
- 1000 requests per minute per IP

## Resources

### [Resource]

#### List [Resources]
```http
GET /api/v1/[resources]
```

**Response**:
```json
{
  "data": [
    {
      "id": "123",
      "name": "Item 1"
    }
  ],
  "meta": {
    "total": 1,
    "page": 1,
    "per_page": 10
  }
}
```

#### Create [Resource]
```http
POST /api/v1/[resources]
Content-Type: application/json
```

**Request**:
```json
{
  "name": "New Item"
}
```

**Response**:
```json
{
  "id": "124",
  "name": "New Item"
}
```
```

---

## Phase 4: User Guide Creation

**Goal**: Create user-friendly documentation

**Actions**:
1. Write step-by-step guides for common tasks
2. Include screenshots and examples
3. Use simple, clear language
4. Organize by user role

**User Guide Template**:
```markdown
# [Feature] User Guide

## Overview

[What this feature does and why it's useful]

## Prerequisites

- [Requirement 1]
- [Requirement 2]

## Getting Started

### Step 1: [First Step]
[Instructions]

### Step 2: [Second Step]
[Instructions]

### Step 3: [Third Step]
[Instructions]

## Advanced Usage

### [Advanced Feature 1]
[Detailed instructions]

### [Advanced Feature 2]
[Detailed instructions]

## Troubleshooting

### Common Issues

1. **Issue 1**: [Description]
   - Solution: [Steps to fix]

2. **Issue 2**: [Description]
   - Solution: [Steps to fix]

## Support

If you need help:
1. Check the FAQ section
2. Search the issue tracker
3. Contact support
```

---

## Phase 5: Documentation Validation

**Goal**: Ensure documentation is complete and accurate

**Actions**:
1. Review generated documentation:
   - Check for completeness
   - Verify technical accuracy
   - Ensure examples work
2. Get feedback from stakeholders
3. Make revisions based on feedback
4. Keep documentation in sync with code and design

---

## Phase 6: Delivery and Storage

**Goal**: Deliver documentation to users

**Actions**:
1. Save documentation in the appropriate location:
   - Project root: README.md, ARCHITECTURE.md
   - docs/ directory: API docs, user guides
   - Wiki or documentation site if needed
2. Update version control
3. Inform users about the new documentation

---

## Best Practices

1. **Single source of truth**: Keep documentation close to code
2. **Automate when possible**: Use tools to generate docs from code
3. **Keep it current**: Update documentation when code changes
4. **Use examples**: Show rather than tell
5. **Be consistent**: Follow documentation style guidelines
6. **Organize logically**: Use clear structure and navigation
7. **Write for your audience**: Tailor content to users' needs
8. **Review regularly**: Schedule documentation reviews

---

## Common Tools

- **Markdown**: Simple, readable format for docs
- **Mermaid**: Diagrams and flowcharts
- **Swagger/OpenAPI**: API documentation
- **Sphinx**: Python documentation
- **Javadoc/Doxygen**: Code comments to documentation

---

## Output Format

Your final documentation should be:
- Well-structured with clear headings
- Complete and accurate
- Easy to navigate
- Up-to-date with current codebase
- Available in a format accessible to users

Mark todos complete once documentation is finalized and delivered.
