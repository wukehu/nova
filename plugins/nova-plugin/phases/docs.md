# Documentation Phase Template
# 文档阶段模板

## Phase: Documentation

### Objective
Create comprehensive documentation for {{project_name}}.

### Context
- **Project**: {{project_name}}
- **Language**: {{language}}
- **Framework**: {{framework}}
- **Audience**: {{target_audience}}

### Documentation Strategy

#### 1. Documentation Types

##### User Documentation
For end users of the software:
- Installation guide
- Quick start tutorial
- User guide
- FAQ
- Troubleshooting

##### Developer Documentation
For developers working on the project:
- Architecture overview
- Development setup
- API documentation
- Contributing guide
- Code style guide

##### Operator Documentation
For DevOps/SRE teams:
- Deployment guide
- Configuration guide
- Monitoring guide
- Runbook
- Disaster recovery

#### 2. Required Documentation

##### README.md
Must include:
```markdown
# {{project_name}}

{{one_line_description}}

## Features
- Feature 1
- Feature 2

## Installation
\`\`\`bash
{{installation_command}}
\`\`\`

## Quick Start
\`\`\`language
{{quick_start_example}}
\`\`\`

## Documentation
{{link_to_full_docs}}

## Contributing
{{link_to_contributing_guide}}

## License
{{license_name}}
```

##### API Documentation

{{#rest_api}}
**OpenAPI/Swagger Specification:**
```yaml
openapi: 3.0.0
info:
  title: {{project_name}} API
  version: 1.0.0
  description: {{api_description}}

paths:
  /users:
    get:
      summary: List all users
      responses:
        '200':
          description: Successful response
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/User'
```
{{/rest_api}}

{{#graphql_api}}
**GraphQL Schema Documentation:**
```graphql
"""
User type representing a user in the system
"""
type User {
  """
  Unique identifier for the user
  """
  id: ID!

  """
  User's username
  """
  username: String!

  """
  User's email address
  """
  email: String!
}
```
{{/graphql_api}}

##### Architecture Documentation

**docs/architecture.md:**
```markdown
# Architecture Overview

## System Architecture
{{architecture_diagram}}

## Components
{{component_descriptions}}

## Data Flow
{{data_flow_diagram}}

## Technology Stack
{{tech_stack_details}}

## Design Decisions
{{design_decisions_log}}
```

##### Contributing Guide

**CONTRIBUTING.md:**
```markdown
# Contributing to {{project_name}}

## Setting Up Development Environment
{{dev_setup_instructions}}

## Running Tests
{{test_instructions}}

## Coding Standards
{{coding_standards}}

## Submitting Changes
{{submission_process}}

## Code Review Process
{{review_process}}
```

#### 3. Code Documentation

##### Inline Documentation

{{#python}}
**Python Docstrings (Google Style):**
```python
def calculate_discount(price: float, discount_percent: float) -> float:
    """Calculate discounted price.

    Args:
        price: Original price
        discount_percent: Discount percentage (0-100)

    Returns:
        Discounted price

    Raises:
        ValueError: If discount_percent is not between 0 and 100

    Examples:
        >>> calculate_discount(100.0, 20)
        80.0
    """
    if not 0 <= discount_percent <= 100:
        raise ValueError("Discount must be between 0 and 100")
    return price * (1 - discount_percent / 100)
```
{{/python}}

{{#javascript}}
**JSDoc Comments:**
```javascript
/**
 * Calculates the discounted price.
 *
 * @param {number} price - Original price
 * @param {number} discountPercent - Discount percentage (0-100)
 * @returns {number} Discounted price
 * @throws {Error} If discountPercent is not between 0 and 100
 *
 * @example
 * calculateDiscount(100.0, 20); // Returns 80.0
 */
function calculateDiscount(price, discountPercent) {
  if (discountPercent < 0 || discountPercent > 100) {
    throw new Error('Discount must be between 0 and 100');
  }
  return price * (1 - discountPercent / 100);
}
```
{{/javascript}}

{{#java}}
**JavaDoc Comments:**
```java
/**
 * Calculates the discounted price.
 *
 * @param price Original price
 * @param discountPercent Discount percentage (0-100)
 * @return Discounted price
 * @throws IllegalArgumentException if discountPercent is not between 0 and 100
 *
 * @example
 * calculateDiscount(100.0, 20); // Returns 80.0
 */
public double calculateDiscount(double price, double discountPercent) {
    if (discountPercent < 0 || discountPercent > 100) {
        throw new IllegalArgumentException("Discount must be between 0 and 100");
    }
    return price * (1 - discountPercent / 100);
}
```
{{/java}}

#### 4. Documentation Tools

{{#python}}
**Python Documentation Tools:**
```bash
# Generate API documentation
pdoc myapp --output-dir docs/api

# Check docstring coverage
interrogate -vv myapp

# Generate HTML docs from docstrings
sphinx-quickstart
```
{{/python}}

{{#javascript}}
**JavaScript Documentation Tools:**
```bash
# Generate JSDoc HTML
jsdoc src -d docs/api

# Type documentation
typedoc src --out docs/api

# Generate README from code
documentation readme src --section=API
```
{{/javascript}}

#### 5. Documentation Best Practices

##### Content Quality
- [ ] Clear and concise
- [ ] Accurate and up-to-date
- [ ] Include examples
- [ ] Use consistent terminology
- [ ] Address common questions
- [ ] Provide troubleshooting steps

##### Structure
- [ ] Logical organization
- [ ] Table of contents
- [ ] Cross-references
- [ ] Searchable
- [ ] Navigation aids

##### Maintenance
- [ ] Review and update regularly
- [ ] Version with code
- [ ] Document deprecations
- [ ] Archive old docs properly

#### 6. Documentation Templates

##### Feature Documentation
```markdown
# Feature Name

## Overview
{{feature_description}}

## Use Cases
{{use_cases}}

## Configuration
{{configuration_options}}

## Usage Examples
\`\`\`language
{{code_examples}}
\`\`\`

## Limitations
{{known_limitations}}

## Troubleshooting
{{common_issues_and_solutions}}
```

##### API Endpoint Documentation
```markdown
## POST /api/users

### Description
Creates a new user account.

### Request
**Headers:**
```
Content-Type: application/json
Authorization: Bearer {token}
```

**Body:**
```json
{
  "username": "string (required, 3-20 chars)",
  "email": "string (required, valid email)",
  "password": "string (required, min 8 chars)"
}
```

### Response
**Success (201):**
```json
{
  "id": 1,
  "username": "testuser",
  "email": "test@example.com",
  "created_at": "2026-03-21T10:00:00Z"
}
```

**Error (400):**
```json
{
  "error": "Validation error",
  "details": ["Email is required"]
}
```

### Examples
\`\`\`bash
curl -X POST https://api.example.com/users \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -d '{"username":"test","email":"test@example.com","password":"SecurePass123!"}'
\`\`\`
```

#### 7. Automated Documentation

##### Generate from Code
```bash
# Python
sphinx-apidoc -o docs src

# JavaScript
jsdoc -c jsdoc.conf.json src

# Generate OpenAPI from code
{{framework}} generate openapi
```

##### CI/CD Integration
```yaml
# .github/workflows/docs.yml
name: Build Documentation

on:
  push:
    branches: [main]

jobs:
  docs:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Setup Python
        uses: actions/setup-python@v4
      - name: Install dependencies
        run: pip install sphinx sphinx-rtd-theme
      - name: Build docs
        run: sphinx-build -b html docs docs/_build
      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./docs/_build
```

### Outputs
- README.md
- API documentation (OpenAPI/GraphQL)
- Architecture documentation
- Contributing guide
- User guide
- Operator guide
- Inline code documentation

### Documentation Checklist
- [ ] README is complete
- [ ] API documentation is generated
- [ ] Architecture is documented
- [ ] Contributing guide exists
- [ ] Code has docstrings/comments
- [ ] Examples are provided
- [ ] Troubleshooting guide exists
- [ ] Documentation is tested
- [ ] Links are valid
- [ ] Screenshots/diagrams included (if applicable)

### Next Steps
After documentation:
1. Review with team
2. Publish to documentation site
3. Link in README
4. Set up auto-deployment
5. Schedule regular reviews
