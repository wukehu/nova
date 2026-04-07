---
description: Analyze and break down clarified requirements into structured user stories, use cases, and architectural considerations
argument-hint: <requirements document or description>
allowed-tools: [Read, Write, Grep, TodoWrite]
---

# Requirements Analysis

You are analyzing clarified software requirements and breaking them down into structured user stories, use cases, and architectural considerations.

## Core Principles

- **User-centric**: Focus on user needs and value delivery
- **Structured**: Use proven techniques like user stories, use cases, and MoSCoW prioritization
- **Comprehensive**: Consider all functional and non-functional requirements
- **Iterative**: Continuously refine analysis as requirements evolve

---

## Phase 1: Requirements Import

**Goal**: Import and validate requirements

Input: $ARGUMENTS

**Actions**:
1. Create a todo list to track analysis progress
2. If requirements are in a document, read and parse it
3. Verify requirements are clear and complete
4. Identify any remaining ambiguities that need clarification

---

## Phase 2: User Story Creation

**Goal**: Break down requirements into user stories

**Actions**:
1. Transform requirements into user stories using:
   - **As a [role]**: Identify all user roles and personas
   - **I want [feature]**: Describe what the user needs
   - **So that [benefit]**: Explain the business value

2. Create user story templates:
```markdown
## User Story 1: [Title]
**As a**: [User Role]
**I want**: [Feature Description]
**So that**: [Business Benefit]

**Acceptance Criteria**:
- [ ] [Testable condition 1]
- [ ] [Testable condition 2]
- [ ] [Testable condition 3]

**Estimate**: [Story Points or T-Shirt Size]
```

---

## Phase 3: Use Case Analysis

**Goal**: Identify use cases and flow diagrams

**Actions**:
1. Identify primary and secondary use cases
2. Create use case diagrams and sequence diagrams
3. Document normal, alternative, and exception flows

**Use Case Template**:
```markdown
## Use Case: [Use Case Name]

**Primary Actor**: [Main User Role]
**Goal**: [What the user is trying to accomplish]

**Preconditions**:
- [Condition 1]
- [Condition 2]

**Main Flow**:
1. [Step 1 - Action taken by actor]
2. [Step 2 - System response]
3. [Step 3 - Action taken by actor]
4. [Step 4 - System response]
5. ...

**Alternative Flows**:
- **Flow 1.1**: [Alternative scenario 1]
- **Flow 1.2**: [Alternative scenario 2]

**Postconditions**:
- [Result after successful completion]
```

---

## Phase 4: Requirements Prioritization

**Goal**: Prioritize requirements using MoSCoW method

**Actions**:
1. Categorize requirements as:
   - **Must Have (M)**: Critical requirements that must be included
   - **Should Have (S)**: Important but not critical
   - **Could Have (C)**: Desirable but optional
   - **Won't Have (W)**: Out of scope for this iteration

2. Create prioritization matrix:
```markdown
## Requirements Prioritization

### Must Have (M)
- [Requirement 1]
- [Requirement 2]

### Should Have (S)
- [Requirement 3]
- [Requirement 4]

### Could Have (C)
- [Requirement 5]
- [Requirement 6]

### Won't Have (W)
- [Requirement 7]
- [Requirement 8]
```

---

## Phase 5: Architecture Considerations

**Goal**: Identify technical architecture implications

**Actions**:
1. Identify technical constraints and architecture patterns
2. Determine technology stack requirements
3. Identify integration points with existing systems
4. Consider scalability, performance, and security needs

**Architecture Analysis Template**:
```markdown
## Architecture Analysis

### Technical Constraints
- [Constraint 1]
- [Constraint 2]

### Technology Stack Requirements
- [Technology 1 - Reason]
- [Technology 2 - Reason]

### Integration Points
- [System/API 1 - Purpose]
- [System/API 2 - Purpose]

### Scalability Considerations
- [Requirement 1]
- [Requirement 2]

### Security Considerations
- [Requirement 1]
- [Requirement 2]
```

---

## Phase 6: Deliverable Generation

**Goal**: Generate comprehensive requirements documentation

**Actions**:
1. Compile all analysis into a structured requirements document
2. Create a requirements traceability matrix (RTM)
3. Generate visual diagrams (use case diagrams, sequence diagrams)
4. Prepare presentation materials for stakeholders

**Requirements Document Structure**:
```markdown
# Software Requirements Specification

## 1. Introduction
- Project Overview
- Scope
- Business Context

## 2. User Stories
- All user stories with acceptance criteria

## 3. Use Cases
- Detailed use case descriptions

## 4. Functional Requirements
- Detailed functional requirements

## 5. Non-Functional Requirements
- Performance, security, reliability requirements

## 6. Architecture
- Technical architecture and constraints

## 7. Requirements Traceability
- RTM linking user stories to requirements

## 8. Appendices
- Glossary
- References
- Change History
```

---

## Phase 7: Validation and Review

**Goal**: Validate analysis and prepare for design phase

**Actions**:
1. Share analysis with stakeholders for review
2. Address feedback and refine requirements
3. Confirm prioritization decisions
4. Prepare hand-off to design team

---

## Best Practices

1. **Collaborate with stakeholders**: Involve product owners, developers, and testers early
2. **Keep requirements traceable**: Link user stories to requirements and test cases
3. **Document assumptions**: Capture and validate all assumptions
4. **Prioritize effectively**: Use MoSCoW or RICE scoring for prioritization
5. **Visualize**: Use diagrams to communicate complex relationships
6. **Iterate**: Continuously update requirements as the project progresses

---

## Output Format

Your final analysis should include:
- Structured user stories with acceptance criteria
- Detailed use case descriptions
- Prioritization matrix
- Requirements traceability matrix
- Architecture considerations
- Visual diagrams

Mark all todos complete once analysis is finalized.
