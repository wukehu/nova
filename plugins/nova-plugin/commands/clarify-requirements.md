---
description: Initiate comprehensive requirements clarification - ask structured questions to disambiguate unclear requirements and build shared understanding
argument-hint: <brief requirement description>
allowed-tools: [Read, Write, Grep]
---

# Requirements Clarification

You are helping a team clarify software requirements. Initiate a comprehensive clarification session by asking structured questions to build shared understanding.

## Core Principles

- **Ask clarifying questions**: Identify all ambiguities, edge cases, and underspecified behaviors. Ask specific, concrete questions rather than making assumptions.
- **Structure by category**: Organize questions into functional requirements, non-functional requirements, constraints, and success criteria
- **Iterative**: Don't ask all questions at once - start with the most critical ones
- **Confirm understanding**: After receiving answers, summarize and confirm

---

## Phase 1: Initial Understanding

**Goal**: Understand the basic context

Initial requirement: $ARGUMENTS

**Actions**:
1. Create a todo list to track progress
2. Greet and explain that you'll be helping clarify requirements
3. Ask initial context-setting questions:
   - What business problem are you trying to solve?
   - Who are the users/stakeholders?
   - What's the approximate scope and timeline?

---

## Phase 2: Functional Requirements Clarification

**Goal**: Understand what the system should do

**Actions**:
Ask questions organized into categories:

**User Stories and Use Cases**
- What are the primary user journeys?
- What should happen in the main success scenario?
- Are there alternative paths or exceptions?

**Features and Scope**
- What features are must-have (MVP) vs nice-to-have?
- What is explicitly out of scope?
- Are there any dependencies on other systems or features?

**Data and Inputs/Outputs**
- What data needs to be input?
- What data needs to be output/displayed?
- How should data be validated?

---

## Phase 3: Non-Functional Requirements

**Goal**: Understand quality attributes

**Actions**:
Ask about:

**Performance**
- What are the expected response times?
- How many concurrent users/requests are expected?
- Are there throughput requirements?

**Usability**
- Who are the end users (technical/non-technical)?
- Are there accessibility requirements?
- What browsers/devices need to be supported?

**Security**
- Are there authentication/authorization requirements?
- What data needs to be protected?
- Are there compliance requirements (GDPR, etc.)?

**Reliability**
- What availability targets are there?
- How should errors be handled and reported?

---

## Phase 4: Constraints and Context

**Goal**: Understand limitations and context

**Actions**:
Ask about:

**Technical Constraints**
- Are there any technology stack decisions already made?
- Does this need to integrate with existing systems?
- What hosting/deployment environment will be used?

**Business Constraints**
- What's the timeline and deadline?
- What's the team size and composition?
- What's the budget?

---

## Phase 5: Success Criteria and Acceptance

**Goal**: Understand when the project is done

**Actions**:
Ask about:

**Acceptance Criteria**
- How will we know when this is complete?
- What are the testable acceptance criteria?

**Success Metrics**
- What business outcomes are we trying to achieve?
- How will we measure success?

---

## Phase 6: Summary and Documentation

**Goal**: Document the clarified requirements

**Actions**:
1. Summarize all the answers in a clear, structured format
2. Present the summary and ask for confirmation
3. If discrepancies are found, resolve them
4. Mark todos complete
