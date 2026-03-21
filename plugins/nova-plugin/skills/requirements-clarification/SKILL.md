---
description: Use this skill when you need to clarify software requirements by identifying ambiguities, missing information, and potential misunderstandings. Ask targeted questions to ensure requirements are complete, clear, and actionable.
---

# Requirements Clarification Skill

## Purpose

Transform vague or incomplete requirements into clear, unambiguous, and actionable specifications through systematic questioning and analysis.

## When to Use This Skill

Activate this skill when:
- Requirements are vague or unclear
- User describes a problem but not a solution
- Technical details are missing
- Edge cases or constraints are undefined
- Multiple interpretations are possible
- Assumptions need validation

## Core Competencies

### 1. Ambiguity Detection

Identify unclear aspects across multiple dimensions:
- **Functional ambiguities**: What exactly should the system do?
- **Data ambiguities**: What formats, ranges, constraints?
- **UI/UX ambiguities**: What should users experience?
- **Performance ambiguities**: What response times, loads, scales?
- **Security ambiguities**: Authentication, authorization, permissions?
- **Error handling**: What happens when things fail?

### 2. Gap Analysis

Systematically identify missing information:
- User roles and permissions
- Business rules and validation
- Technical and business constraints
- Success criteria and metrics
- Non-functional requirements
- Integration requirements

### 3. Edge Case Identification

Think about unusual situations:
- Empty or null inputs
- Boundary conditions
- Concurrent access
- Failure modes
- Invalid data
- High load scenarios
- Migration strategies

### 4. Assumption Validation

Make implicit assumptions explicit and verify them:
- Technology preferences
- Deployment environment
- User expertise
- Data volumes
- Budget and timeline
- Regulatory requirements

## Questioning Framework

### The 5 Ws and H

1. **Who**: Who are the users? What are their roles?
2. **What**: What exactly needs to be built?
3. **Where**: Where will this be used? Environment?
4. **When**: When is this needed? Timeline constraints?
5. **Why**: Why is this needed? Business value?
6. **How**: How should this work? Technical approach?

### CE Framework (Clarify, Expand, Validate)

**Clarify**:
- "Can you give an example of X?"
- "What do you mean by Y?"
- "How would Z work in practice?"

**Expand**:
- "What about [edge case]?"
- "Have you considered [scenario]?"
- "What happens when [condition]?"

**Validate**:
- "Is my understanding correct that...?"
- "So you're saying that...?"
- "Let me confirm: [summary]"

## Output Format

Generate a clarified requirements document with:

```markdown
# Clarified Requirements

## Overview
[Clear summary of what's being built and why]

## Confirmed Requirements
- [Requirement 1 - clear and unambiguous]
- [Requirement 2 - clear and unambiguous]

## Decisions Made
1. [Question asked]: [Answer decided]
2. [Question asked]: [Answer decided]

## Validated Assumptions
- [Assumption 1]: [Confirmed]
- [Assumption 2]: [Confirmed]

## Open Questions
- [Question 1]: [Needs decision]
- [Question 2]: [Needs decision]

## Edge Cases Identified
- [Case]: [How to handle]
- [Case]: [How to handle]

## Success Criteria
- [ ] [Measurable criterion 1]
- [ ] [Measurable criterion 2]

## Constraints
- **Technical**: [Limitations]
- **Business**: [Requirements]
- **Timeline**: [Deadlines]
```

## Best Practices

### DO:
- Ask specific, focused questions
- Explain why information is needed
- Suggest options when helpful
- Think from multiple perspectives (user, developer, tester, operator)
- Document decisions and assumptions
- Validate your understanding

### DON'T:
- Make assumptions without asking
- Ask vague questions
- Overwhelm with too many questions at once
- Ignore edge cases
- Skip validation of assumptions

## Quality Checklist

- [ ] All ambiguities identified and clarified
- [ ] Missing information requested
- [ ] Edge cases considered
- [ ] Assumptions validated
- [ ] Requirements are unambiguous
- [ ] Requirements are testable
- [ ] Success criteria defined
- [ ] Constraints documented

## Related Skills

- **Requirements Analysis**: Break down clarified requirements into user stories
- **Architecture Design**: Design system based on clear requirements
- **Detailed Design**: Create specifications from requirements
