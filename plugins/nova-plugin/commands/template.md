---
description: Template management - list, create, customize, and switch between different SDLC workflow templates
argument-hint: <action> [options]
allowed-tools: [Read, Write, Grep, AskUserQuestion]
---

# Template Management

Manage SDLC workflow templates for different project types and development scenarios.

## Usage

```
/template list                    # List all available templates
/template show <name>             # Show template details
/template use <name>              # Switch to a template
/template create <name>           # Create a custom template
/template edit <name>             # Edit an existing template
/template validate <name>         # Validate template configuration
/template export <name> <file>    # Export template to file
/template import <file>           # Import template from file
```

## Available Templates

### Built-in Templates

1. **base** - Base SDLC workflow
   - Standard 6-phase workflow
   - Suitable for general software development
   - Minimal configuration required

2. **web-app** - Web application development
   - Extended with frontend/backend phases
   - Includes UI/UX design considerations
   - Pre-configured for modern web frameworks

3. **api-service** - API/microservice development
   - API-first approach
   - Contract testing and documentation
   - Performance and scalability focus

4. **mobile-app** - Mobile application development
   - Platform-specific considerations (iOS/Android)
   - Offline-first architecture
   - App store deployment workflow

5. **data-pipeline** - Data engineering projects
   - ETL/ELT workflow design
   - Data quality and validation
   - Infrastructure as code focus

## Template Structure

Templates are defined in YAML format:

```yaml
name: "Template Name"
description: "Template description"
extends: "base"  # Optional: inherit from base template

phases:
  - id: "phase-id"
    name: "Phase Name"
    description: "Phase description"
    template: "path/to/template.md"
    required: true
    depends_on: ["previous-phase"]
    output: "output-file.md"

variables:
  variable_name:
    description: "Variable description"
    default: "default-value"
    options: ["option1", "option2"]
```

## Creating Custom Templates

### Option 1: Interactive Creation

```bash
/template create my-template
```

You will be prompted for:
- Template name and description
- Phases to include
- Variables to define
- Code generation templates

### Option 2: Manual Creation

1. Copy an existing template:
```bash
cp -r templates/web-app templates/my-template
```

2. Edit the workflow.yaml:
```bash
/template edit my-template
```

### Option 3: Extend Existing Template

```yaml
# templates/my-template/workflow.yaml
name: "My Custom Template"
extends: "web-app"  # Inherit from web-app

phases:
  # Override a phase
  - id: "clarify"
    extends: "web-app.clarify"
    custom_questions:
      - "My custom question?"

  # Add a new phase
  - id: "custom-phase"
    name: "Custom Phase"
    template: "phases/custom.md"
    insert_after: "design"
```

## Template Variables

Templates support variables that can be referenced in phase templates:

```yaml
variables:
  project_name:
    description: "Project name"
    required: true

  tech_stack:
    description: "Technology stack"
    default: "auto"
    options: ["python", "javascript", "java", "go"]
```

Usage in phase templates:
```markdown
# Project: {{project_name}}
# Tech Stack: {{tech_stack}}
```

## Template Inheritance

Templates can extend other templates:

- **extends**: Specify parent template to inherit from
- **Override**: Redefine phases to override parent
- **Insert**: Use `insert_after`/`insert_before` to add phases
- **Remove**: Use `remove: true` to exclude parent phases

## Validating Templates

Check your template for errors:

```bash
/template validate my-template
```

Validation checks:
- YAML syntax
- Phase dependencies
- Required fields
- Template file existence
- Variable references

## Example Workflows

### Quick Web App Development

```bash
# Switch to web-app template
/template use web-app

# Start development
/workflow start --interactive

# The workflow will:
# 1. Ask about frontend/backend preferences
# 2. Generate project structure
# 3. Guide through each phase
# 4. Generate boilerplate code
```

### Custom Microservice Template

```bash
# Create from web-app template
/template create microservice --extends=web-app

# Customize: remove frontend, add API design
/template edit microservice
  --remove frontend-design
  --add api-contract

# Use it
/template use microservice
/workflow start
```

## Best Practices

1. **Start Simple**: Begin with `base` template, extend as needed
2. **Reuse Phases**: Copy phase templates between custom templates
3. **Document Well**: Add clear descriptions for custom phases
4. **Test Locally**: Validate templates before sharing
5. **Version Control**: Commit templates to your repo
6. **Share with Team**: Export/import templates for team consistency

## Template Locations

Templates are stored in:
- **Built-in**: `templates/` (in plugin directory)
- **User**: `~/.config/Claude/templates/` (user-specific)
- **Project**: `.claude/templates/` (project-specific)

Priority: Project > User > Built-in

## See Also

- `/workflow` - Execute workflow phases
- Template customization guide
- Phase template reference
