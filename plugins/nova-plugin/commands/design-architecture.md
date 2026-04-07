---
description: Design software architecture with multiple approaches, trade-off analysis, and recommendations
argument-hint: <requirements document or description>
allowed-tools: [Read, Write, Edit, Grep, Agent, TodoWrite]
---

# Architecture Design

You are designing software architecture based on requirements. Create multiple approaches, analyze trade-offs, and recommend the best solution.

## Core Principles

- **Multiple approaches**: Design at least 2-3 different approaches (minimal, clean, pragmatic)
- **Trade-off analysis**: Compare options based on maintainability, performance, scalability, and cost
- **Evidence-based**: Ground recommendations in requirements and constraints
- **Iterative**: Start with high-level design, then refine with details

---

## Phase 1: Requirements Review and Context Analysis

**Goal**: Understand what needs to be built

Input: $ARGUMENTS

**Actions**:
1. Create a todo list to track design progress
2. Review requirements and constraints
3. Explore codebase if this is an existing project
4. Identify technical constraints, existing systems, and deployment environment

---

## Phase 2: Approach 1 - Minimal Change (Maximum Reuse)

**Goal**: Design approach that minimizes disruption and reuses existing infrastructure

**Actions**:
1. Design approach that:
   - Leverages existing code patterns
   - Reuses components wherever possible
   - Makes minimal changes to architecture
   - Focuses on quick delivery

2. Document the approach:
```markdown
## Approach 1: Minimal Change

### Overview
[Brief description of this approach]

### Architecture
- High-level diagram
- Key components
- How they interact

### Components
1. [Component 1]: [Purpose and responsibilities]
2. [Component 2]: [Purpose and responsibilities]
3. [Component 3]: [Purpose and responsibilities]

### Advantages
- [ ] Quick to implement
- [ ] Low risk
- [ ] Leverages existing knowledge
- [ ] Minimal changes required

### Disadvantages
- [ ] May not scale well
- [ ] Could accumulate technical debt
- [ ] Less clean architecturally

### Implementation Effort
- Timeline: [Estimate]
- Risk: [Low/Medium/High]
- Cost: [Low/Medium/High]
```

---

## Phase 3: Approach 2 - Clean Architecture (Optimal Design)

**Goal**: Design approach that prioritizes maintainability, testability, and architectural elegance

**Actions**:
1. Design approach that:
   - Follows clean architecture principles (hexagonal, onion, etc.)
   - Proper separation of concerns
   - Testable and maintainable
   - Future-proof and extensible

2. Document the approach:
```markdown
## Approach 2: Clean Architecture

### Overview
[Brief description of this approach]

### Architecture Principles
- [Principle 1]
- [Principle 2]
- [Principle 3]

### Architecture
- High-level diagram
- Layer breakdown
- Dependency direction

### Layers
1. **Domain Layer**
   - Core business logic
   - No external dependencies

2. **Application Layer**
   - Use cases and application services
   - Orchestrates domain objects

3. **Infrastructure Layer**
   - External integrations (DB, APIs, etc.)
   - Implements interfaces from domain layer

4. **Presentation Layer**
   - User interface or API endpoints
   - Thin layer, delegates to application layer

### Advantages
- [ ] Highly maintainable
- [ ] Easy to test
- [ ] Flexible and extensible
- [ ] Technology-independent core

### Disadvantages
- [ ] More upfront design
- [ ] Higher initial implementation effort
- [ ] Learning curve for team

### Implementation Effort
- Timeline: [Estimate]
- Risk: [Low/Medium/High]
- Cost: [Low/Medium/High]
```

---

## Phase 4: Approach 3 - Pragmatic Balance

**Goal**: Design approach that balances speed and quality - practical, not perfect

**Actions**:
1. Design approach that:
   - Balances the other two approaches
   - Makes pragmatic trade-offs
   - Good enough for now but leaves room to improve
   - Avoids both over-engineering and under-engineering

2. Document the approach:
```markdown
## Approach 3: Pragmatic Balance

### Overview
[Brief description of this approach]

### Key Decisions
- [Decision 1 - Rationale]
- [Decision 2 - Rationale]
- [Decision 3 - Rationale]

### Architecture
- High-level diagram
- Key components
- How they interact

### Pragmatic Trade-offs
1. [Trade-off 1]: [What we do and why]
2. [Trade-off 2]: [What we do and why]
3. [Trade-off 3]: [What we do and why]

### Advantages
- [ ] Balanced approach
- [ ] Practical for current needs
- [ ] Leaves room to evolve
- [ ] Reasonable effort/risk

### Disadvantages
- [ ] Not the "perfect" architecture
- [ ] May need refactoring later
- [ ] Some compromises made

### Implementation Effort
- Timeline: [Estimate]
- Risk: [Low/Medium/High]
- Cost: [Low/Medium/High]
```

---

## Phase 5: Trade-off Analysis and Recommendation

**Goal**: Compare approaches and recommend the best one

**Actions**:
1. Create comparison matrix:
```markdown
## Comparison Matrix

| Criteria | Approach 1 (Minimal) | Approach 2 (Clean) | Approach 3 (Pragmatic) |
|----------|----------------------|---------------------|-------------------------|
| **Implementation Time** | [Rating] | [Rating] | [Rating] |
| **Risk** | [Rating] | [Rating] | [Rating] |
| **Maintainability** | [Rating] | [Rating] | [Rating] |
| **Scalability** | [Rating] | [Rating] | [Rating] |
| **Testability** | [Rating] | [Rating] | [Rating] |
| **Flexibility** | [Rating] | [Rating] | [Rating] |
| **Team Fit** | [Rating] | [Rating] | [Rating] |
| **Overall** | [Rating] | [Rating] | [Rating] |

[Rating Scale: 🔴 Poor | 🟡 Fair | 🟢 Good | 🔵 Excellent]
```

2. Provide your recommendation:
```markdown
## Recommendation

### Recommended Approach: [Approach Name]

### Rationale
1. [Reason 1 - Key factor]
2. [Reason 2 - Key factor]
3. [Reason 3 - Key factor]

### Why Not the Others?
- **Approach 1**: [Why not suitable for this case]
- **Approach 2**: [Why not suitable for this case]

### Next Steps
1. Validate this recommendation with stakeholders
2. Once approved, proceed to detailed design
3. Update architecture document (ARCHITECTURE.md)
```

---

## Phase 6: Detailed Component Design

**Goal**: Design individual components in more detail (once approach is approved)

**Actions**:
1. For each major component:
   - Define API/interface
   - Describe responsibilities
   - Identify dependencies
   - Document data models

2. Create ADRs (Architecture Decision Records) for key decisions:
```markdown
## ADR 001: [Decision Title]

**Date**: [Date]
**Status**: [Proposed/Accepted/Rejected/Superseded]

### Context
[What is the issue we're trying to solve?]

### Decision
[What have we decided?]

### Rationale
[Why did we decide this way?]

### Consequences
- Positive: [What are the benefits?]
- Negative: [What are the trade-offs?]
```

---

## Phase 7: Architecture Documentation

**Goal**: Generate comprehensive architecture documentation

**Actions**:
1. Generate ARCHITECTURE.md document with:
   - System overview
   - High-level diagrams
   - Component descriptions
   - Architecture principles
   - ADRs

2. Update todos as you complete sections

---

## Best Practices

1. **Understand before designing**: Always explore existing code first
2. **Multiple options**: Don't just present one approach - give choices
3. **Involve stakeholders**: Get feedback early and often
4. **Document decisions**: Use ADRs for important architectural decisions
5. **Diagram first**: Use diagrams to communicate complex ideas
6. **Iterative refinement**: Start high-level, then add details

---

## Output Format

Your final deliverable should include:
- 2-3 architecture approaches with pros/cons
- Trade-off comparison matrix
- Your recommendation with rationale
- Detailed design for chosen approach
- ADRs for key decisions
- Architecture diagrams

Mark all todos complete once design is finalized.
