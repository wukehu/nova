---
description: Use this skill when analyzing requirements to break them down into user stories, identify dependencies between features, assess technical feasibility, estimate effort, and create prioritized implementation plans.
---

# Requirements Analysis Skill

## Purpose

Transform clarified requirements into actionable development plans by breaking down into user stories, mapping dependencies, assessing feasibility, and prioritizing work.

## When to Use This Skill

Activate this skill when:
- Requirements are clarified and need breakdown
- Planning a sprint or release
- Estimating effort for features
- Identifying what can be done in parallel
- Assessing technical feasibility
- Creating implementation roadmaps

## Core Competencies

### 1. User Story Breakdown

Decompose requirements into hierarchy:

**Epics** (Large, high-level initiatives):
- Multiple related features
- Span multiple sprints
- Significant business value

**Features** (Deliverable capabilities):
- Part of an epic
- Can be completed in 1-2 sprints
- User-visible functionality

**User Stories** (Small, testable units):
- Part of a feature
- Can be completed in a few days
- Follow format:
  ```
  As a [user role]
  I want [action/feature]
  So that [business value]

  Acceptance Criteria:
  - [ ] Criterion 1
  - [ ] Criterion 2
  ```

### 2. Dependency Mapping

**Types of dependencies**:
- **Strong**: Must complete before
- **Weak**: Can parallel but should coordinate
- **None**: Completely independent

**Mapping**:
- Identify blockers (what waits for what)
- Find parallelization opportunities
- Sequence work effectively

### 3. Feasibility Assessment

**For each epic/feature**:
- **Technical complexity**: Low/Medium/High
- **Uncertainties**: What don't we know?
- **Risks**: What could go wrong?
- **Spikes needed**: What requires research?

### 4. Estimation

**Use story points** (relative sizing):
- 1: Trivial (few hours)
- 2: Small (1 day)
- 3: Medium (2-3 days)
- 5: Large (3-5 days)
- 8: Very large (1 week)
- 13: Epic (split further)

**Consider**:
- Complexity
- Uncertainty
- Effort
- Risk

### 5. Prioritization

**MoSCoW Method**:
- **Must Have**: Critical for MVP
- **Should Have**: Important but not critical
- **Could Have**: Nice to have
- **Won't Have**: Out of scope

**RICE Scoring**:
- **R**each: How many users affected?
- **I**mpact: How much value?
- **C**onfidence: How sure?
- **E**ffort: How much work?

Score = (Reach × Impact × Confidence) / Effort

## Output Format

```markdown
# Requirements Analysis

## User Story Breakdown

### Epic 1: [Name]
**Business Value**: [Why this matters]
**Story Points**: [Total]

#### Feature 1.1: [Name]
**User Stories**:
- Story 1.1.1 (2 pts): As a...
- Story 1.1.2 (3 pts): As a...

#### Feature 1.2: [Name]
**User Stories**:
- Story 1.2.1 (5 pts): As a...

### Epic 2: [Name]
...

## Dependency Map

### Blocking Dependencies
- [Story A] must be before [Story B]
- [Story C] blocks [Story D]

### Parallel Opportunities
- [Story E] and [Story F] can be parallel
- [Story G] and [Story H] can be parallel

### Critical Path
1. [Story A] (blocks 3 others)
2. [Story B] (blocks 2 others)
3. [Story C]

## Feasibility Assessment

| Feature | Complexity | Risk | Unknowns | Spike Needed |
|---------|-----------|------|----------|--------------|
| Feature 1 | Medium | Low | None | No |
| Feature 2 | High | High | Tech choice | Yes (2 days) |

## Prioritization

### Must Have (MVP)
1. Feature A (15 pts) - RICE: 120
2. Feature B (8 pts) - RICE: 95

### Should Have
1. Feature C (13 pts) - RICE: 70

### Could Have
1. Feature D (5 pts) - RICE: 30

## Implementation Plan

### Sprint 1 (2 weeks)
**Goal**: [MVP subset]
**Stories**:
- Story A.1 (3 pts)
- Story A.2 (5 pts)
- Story B.1 (5 pts)

**Velocity**: ~13 pts

### Sprint 2 (2 weeks)
**Goal**: [More features]
**Stories**:
- Story B.2 (3 pts)
- Story C.1 (8 pts)

**Velocity**: ~11 pts

## Timeline Estimate
- MVP: [X] weeks
- Full Release: [Y] weeks
- Confidence: [Low/Medium/High]
```

## Analysis Framework

### Step 1: Understand
- Read clarified requirements
- Identify all epics/features
- Create initial todo list

### Step 2: Break Down
- Decompose into epics → features → stories
- Write user stories in standard format
- Define acceptance criteria

### Step 3: Map Dependencies
- Identify relationships between stories
- Classify dependency strength
- Find critical path

### Step 4: Assess Feasibility
- Evaluate technical complexity
- Identify risks
- Note unknowns
- Plan spikes

### Step 5: Estimate
- Assign story points
- Consider uncertainty
- Buffer for unknowns

### Step 6: Prioritize
- Apply MoSCoW or RICE
- Consider dependencies
- Business value
- Technical risk

### Step 7: Plan
- Group into sprints
- Sequence by priority and dependencies
- Identify parallel work
- Estimate timeline

## Best Practices

### DO:
- Break down to manageable size (< 2 weeks)
- Involve developers in estimation
- Consider uncertainty in estimates
- Re-estimate as you learn more
- Validate with stakeholders
- Plan for the unexpected

### DON'T:
- Create epics that are too large
- Ignore technical dependencies
- Overestimate team velocity
- Skip risk assessment
- Plan too far ahead (> 3 months)
- Ignore team capacity

## Quality Checklist

- [ ] All requirements broken down into stories
- [ ] Stories follow standard format
- [ ] Acceptance criteria defined
- [ ] Dependencies mapped
- [ ] Estimates include team input
- [ ] Feasibility assessed
- [ ] Priorities justified
- [ ] Plan is realistic
- [ ] Stakeholders agree

## Related Skills

- **Requirements Clarification**: Input for analysis
- **Architecture Design**: Next phase after analysis
- **Detailed Design**: Next phase after architecture
