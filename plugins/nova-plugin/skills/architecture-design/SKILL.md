---
description: Use this skill when designing system architecture, evaluating multiple architectural approaches, making tech stack decisions, designing data models and interfaces, creating implementation blueprints, or documenting architecture decisions.
---

# Architecture Design Skill

## Purpose

Design robust, scalable, maintainable system architectures by evaluating multiple approaches, making informed trade-offs, and creating comprehensive implementation blueprints.

## When to Use This Skill

Activate this skill when:
- Starting a new project or major feature
- Evaluating technology stack options
- Designing system components and their interactions
- Planning data storage and retrieval strategies
- Documenting architectural decisions
- Scaling existing systems
- Integrating with external systems

## Core Competencies

### 1. Multi-Option Analysis

Generate and evaluate 2-3 architectural approaches:

**Option A: Minimal/Pragmatic**
- Fastest delivery
- Least code/change
- May accumulate technical debt

**Option B: Clean/Modular**
- Best practices
- Highly maintainable
- Longer time to market

**Option C: Balanced**
- Pragmatic compromise
- Reasonable quality
- Acceptable timeline

### 2. Trade-off Analysis

Evaluate across dimensions:
- Development time
- Complexity
- Scalability
- Maintainability
- Performance
- Risk
- Team skills
- Operational overhead

### 3. System Decomposition

Break systems into:
- Layers (presentation, application, domain, data)
- Components (cohesive units)
- Services (if microservices)
- Modules (logical groupings)

### 4. Data Architecture

Design:
- Data models (entities, relationships)
- Storage strategies (SQL, NoSQL, cache)
- Data flow (between components)
- Data lifecycle (creation to archival)

### 5. Integration Patterns

Define:
- API contracts (REST, GraphQL, gRPC)
- Event-driven communication (pub/sub, message queues)
- Synchronous vs asynchronous
- Error handling and retries

## Architecture Decision Records (ADRs)

For each significant decision, document:

```markdown
# ADR-XXX: [Decision Title]

## Status
Accepted / Proposed / Deprecated / Superseded

## Context
[What situation requires this decision?]
[What problem are we solving?]

## Decision
[What did we decide?]
[What is the solution?]

## Consequences
### Positive
- [Benefit 1]
- [Benefit 2]

### Negative
- [Drawback 1]
- [Drawback 2]

## Alternatives Considered
1. [Alternative 1]
   - Why rejected: [Reason]

2. [Alternative 2]
   - Why rejected: [Reason]

## Related Decisions
- ADR-XXX: [Related decision]
```

## Output Format

Generate a comprehensive architecture document:

```markdown
# Architecture Design

## Executive Summary
[High-level overview for stakeholders]

## Recommended Approach
[Which option and why]

## System Architecture
[Layered architecture diagram]
[Component overview]

## Detailed Design

### Components
[For each component:]
- Name, purpose, responsibilities
- Interfaces (APIs, methods)
- Dependencies
- Data managed

### Data Model
[Entities, relationships, schemas]
[Storage decisions]

### APIs and Communication
[Endpoint specifications]
[Protocols and formats]
[Authentication/authorization]

## Cross-Cutting Concerns

### Security
[Authentication, authorization, encryption]

### Performance
[Caching, optimization strategies]

### Scalability
[Horizontal/vertical scaling]

### Reliability
[Error handling, retries, circuit breakers]

### Observability
[Logging, metrics, monitoring, tracing]

## Technology Stack
[Languages, frameworks, databases, tools]
[Justification for each choice]

## Architecture Decision Records
[Links to ADRs for major decisions]

## Implementation Roadmap
[Phases, milestones, dependencies]

## Risk Assessment
[Risks and mitigation strategies]
```

## Architectural Patterns

Know when to use:

### Monolith
- Simple apps
- Small teams
- Fast development needed

### Layered Architecture
- Standard enterprise apps
- Clear separation needed
- Team specialization

### Microservices
- Complex domains
- Multiple teams
- Independent scaling needed

### Event-Driven
- Async processing
- Loose coupling
- High scalability

### CQRS
- Complex read/write patterns
- Different data models for read/write
- High read volume

### Space-Based
- Extreme scalability
- Distributed processing
- Cloud-native

## Best Practices

### DO:
- Consider multiple approaches
- Make trade-offs explicit
- Think long-term (3-5 years)
- Document decisions
- Design for failure
- Use tried patterns
- Consider operations from day 1

### DON'T:
- Jump to first solution
- Ignore trade-offs
- Over-engineer
- Choose tech based on hype
- Ignore team skills
- Forget about operations
- Design for perfect cases only

## Quality Checklist

- [ ] Multiple options considered
- [ ] Trade-offs analyzed and documented
- [ ] Recommendation justified
- [ ] Components have clear responsibilities
- [ ] Data model designed
- [ ] APIs defined
- [ ] Security considered
- [ ] Performance evaluated
- [ ] Scalability planned
- [ ] Reliability addressed
- [ ] Observability included
- [ ] ADRs created for major decisions
- [ ] Implementation roadmap defined

## Related Skills

- **Requirements Analysis**: Input to architecture design
- **Detailed Design**: Refine architecture into specifications
- **Code Development**: Implement the architecture
