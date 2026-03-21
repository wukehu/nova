---
description: Execute workflow phases - guide through the current SDLC workflow with context-aware assistance
argument-hint: <action> [phase-name] [options]
allowed-tools: [Read, Write, Edit, Grep, Bash, AskUserQuestion]
---

# Workflow Execution

Execute and manage the current SDLC workflow based on the active template.

## Usage

```
/workflow start                    # Start workflow from beginning
/workflow start --from <phase>     # Start from specific phase
/workflow status                   # Show current workflow status
/workflow next                     # Execute next phase
/workflow jump <phase>             # Jump to specific phase
/workflow skip <phase>             # Skip a phase
/workflow reset                    # Reset workflow progress
/workflow complete                 # Mark workflow as complete
```

## Workflow States

A workflow can be in one of these states:

1. **Not Started** - Workflow initialized but not started
2. **In Progress** - Currently executing phases
3. **Blocked** - Waiting for dependencies or user input
4. **Completed** - All phases finished
5. **Failed** - A phase failed and needs attention

## Workflow Phases

### Standard Phases (base template)

```
┌─────────────┐
│  Clarify    │ → 需求澄清
└──────┬──────┘
       ↓
┌─────────────┐
│  Analyze    │ → 需求分析
└──────┬──────┘
       ↓
┌─────────────┐
│   Design    │ → 架构设计
└──────┬──────┘
       ↓
┌─────────────┐
│   Detail    │ → 详细设计 (可选)
└──────┬──────┘
       ↓
┌─────────────┐
│    Code     │ → 代码开发
└──────┬──────┘
       ↓
┌─────────────┐
│    Test     │ → 测试调试
└─────────────┘
```

### Extended Phases (web-app template)

```
┌─────────────┐
│  Clarify    │ → 需求澄清 (含前后端问题)
└──────┬──────┘
       ↓
┌─────────────┐
│  Analyze    │ → 需求分析
└──────┬──────┘
       ↓
┌─────────────┐
│   Design    │ → 架构设计
└──────┬──────┘
       ├─────────────────┐
       ↓                 ↓
┌──────────────┐  ┌──────────────┐
│ Frontend     │  │  Backend     │
│  Design      │  │   Design     │
└──────┬───────┘  └──────┬───────┘
       │                 │
       └────────┬────────┘
                ↓
        ┌─────────────┐
        │    Code     │ → 前后端开发
        └──────┬──────┘
               ↓
        ┌─────────────┐
        │    Test     │ → 集成测试
        └─────────────┘
```

## Starting a Workflow

### Interactive Mode (Recommended)

```bash
/workflow start
```

This will:
1. Load the active template
2. Check for existing workflow state
3. Prompt for any required variables
4. Guide through each phase interactively

### Non-Interactive Mode

```bash
/workflow start --non-interactive
```

Execute phases automatically without prompts (useful for CI/CD).

### Starting from Specific Phase

```bash
/workflow start --from design
```

Skip earlier phases and start from design phase.

## Workflow State

The workflow state is stored in `.claude/workflow.yaml`:

```yaml
template: "web-app"
current_phase: "design"
started_at: "2026-03-21T10:00:00Z"
completed_phases:
  - "clarify"
  - "analyze"
variables:
  project_name: "MyApp"
  frontend_framework: "react"
  backend_framework: "fastapi"
outputs:
  clarify: "clarified-requirements.md"
  analyze: "requirements-analysis.md"
```

## Phase Execution

### Executing a Phase

When you execute a phase, Claude will:

1. **Load Phase Template**: Read the phase template file
2. **Context Analysis**: Analyze existing code and documents
3. **Generate Output**: Create the phase output document
4. **Update State**: Mark phase as completed
5. **Next Steps**: Suggest next actions

### Phase Inputs

Each phase can use inputs from:
- Previous phase outputs
- Template variables
- Existing project files
- User prompts

### Phase Outputs

Each phase produces:
- Primary output document (as defined in template)
- Supporting artifacts (diagrams, schemas, etc.)
- Metrics (time spent, decisions made, etc.)

## Skipping Phases

Skip optional phases if not needed:

```bash
/workflow skip detail
```

Or skip multiple:

```bash
/workflow start --skip detail,test
```

## Jumping Between Phases

Jump to a specific phase (even if not next):

```bash
/workflow jump code
```

**Warning**: This may bypass dependencies. Use with caution.

## Workflow Status

Check current progress:

```bash
/workflow status
```

Output:
```
Template: web-app
Started: 2026-03-21 10:00:00
Current Phase: design
Progress: ████████░░░░░░░░░ 40%

Completed Phases:
  ✅ clarify (15 min)
  ✅ analyze (25 min)

Current Phase:
  🔄 design (in progress, 10 min)

Remaining Phases:
  ⏳ detail (optional)
  ⏳ code
  ⏳ test
```

## Workflow Completion

When all required phases are complete:

```bash
/workflow complete
```

This will:
1. Validate all required outputs exist
2. Generate summary report
3. Archive workflow state
4. Provide deployment/publishing guidance

## Customizing Workflow Behavior

### Environment Variables

```bash
export CLAUDE_WORKFLOW_AUTO_CONTINUE=true
export CLAUDE_WORKFLOW_PARALLEL=false
export CLAUDE_WORKFLOW_TIMEOUT=3600
```

### Project Configuration

Create `.claude/workflow.config.yaml`:

```yaml
# Override template settings
auto_continue: false
parallel_phases: false
timeout: 3600

# Phase-specific settings
phases:
  code:
    auto_test: true
    coverage_threshold: 80

  test:
    parallel: true
    max_retries: 3
```

## Examples

### Example 1: Quick Start with Web App

```bash
# Use web-app template
/template use web-app

# Start workflow interactively
/workflow start

# Answer prompts:
# - Project name? MyTodoApp
# - Frontend? React
# - Backend? FastAPI
# - Database? PostgreSQL

# Workflow guides you through each phase
```

### Example 2: Continue from Design Phase

```bash
# You have design document, start from code
/workflow start --from code

# Claude will:
# 1. Read architecture-design.md
# 2. Generate code structure
# 3. Implement features
# 4. Write tests
```

### Example 3: Skip Detail Design

```bash
# For simple projects, skip detailed design
/workflow start --skip detail

# Workflow: clarify → analyze → design → code → test
```

### Example 4: Parallel Execution

```bash
# Run frontend and backend design in parallel
/workflow start --parallel

# Requires: parallel_phases: true in template
```

## Workflow Artifacts

Each workflow generates:

```
.claude/
├── workflow.yaml           # Current state
├── workflow.history.yaml   # Past workflows
└── outputs/
    ├── clarify/
    │   └── clarified-requirements.md
    ├── analyze/
    │   └── requirements-analysis.md
    ├── design/
    │   ├── architecture-design.md
    │   └── diagrams/
    ├── detail/
    │   └── detailed-design.md
    ├── code/
    │   └── implementation-notes.md
    └── test/
        └── test-report.md
```

## Troubleshooting

### Workflow State Corrupted

```bash
/workflow reset
```

Clear state and start fresh.

### Phase Failed

```bash
/workflow retry <phase>
```

Retry a failed phase.

### Missing Dependencies

```bash
/workflow validate
```

Check all dependencies and outputs.

## Best Practices

1. **Commit Workflow State**: Track `.claude/workflow.yaml` in git
2. **Document Decisions**: Each phase should document key decisions
3. **Review Outputs**: Don't auto-accept all outputs, review them
4. **Iterate**: You can revisit phases, workflow is not strictly linear
5. **Save Artifacts**: Keep phase outputs for future reference

## Integration with Other Tools

### CI/CD Integration

```yaml
# .github/workflows/development.yml
- name: Run SDLC Workflow
  run: |
    /workflow start --non-interactive
    /workflow status --json > workflow-status.json
```

### Project Management

```bash
# Export phases as tasks
/workflow export --format jira > jira-tasks.csv
/workflow export --format github > github-issues.md
```

### Documentation

```bash
# Generate documentation from workflow
/workflow docs --format markdown
```

## See Also

- `/template` - Template management
- Phase template reference
- Workflow customization guide
