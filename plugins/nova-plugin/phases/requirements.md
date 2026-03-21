# Requirements Phase Template
# 需求阶段模板

## Phase: Requirements

### Objective
Gather and clarify requirements for {{project_name}}.

### Context
- **Project**: {{project_name}}
- **Type**: {{project_type}}
- **Team Size**: {{team_size}}
- **Timeline**: {{timeline}}

### Tasks

#### 1. Stakeholder Analysis
Identify all stakeholders and their needs:
- Who are the users?
- What are their roles?
- What are their goals?
- What are their pain points?

#### 2. Functional Requirements
List all functional requirements:
- What features must the system have?
- What user stories need to be implemented?
- What are the acceptance criteria?

{{#if web_app}}
- Frontend requirements (UI/UX)
- Backend requirements (API)
- Data requirements
{{/if}}

{{#if api_service}}
- API endpoints
- Request/response formats
- Authentication/authorization
{{/if}}

#### 3. Non-Functional Requirements
Define non-functional requirements:
- Performance (response time, throughput)
- Scalability (concurrent users, data volume)
- Security (authentication, authorization, encryption)
- Reliability (uptime, error handling)
- Maintainability (code quality, documentation)

#### 4. Constraints
Identify constraints:
- Technical constraints (tech stack, frameworks)
- Business constraints (budget, timeline)
- Regulatory constraints (compliance, privacy)
- Operational constraints (deployment, monitoring)

#### 5. Assumptions & Dependencies
Document assumptions and dependencies:
- What are we assuming to be true?
- What external systems do we depend on?
- What data sources do we need?
- What APIs do we integrate with?

### Outputs
- `docs/requirements.md` - Complete requirements document
- `docs/user-stories.md` - User stories breakdown
- `docs/acceptance-criteria.md` - Acceptance criteria

### Next Steps
Once requirements are clear:
{{#if full_workflow}}
1. Review and approve requirements
2. Move to Design phase
{{/if}}

{{#if lite_workflow}}
1. Create basic design
2. Start implementation
{{/if}}

### Template Variables Applied
- Language: {{language}} - Applies language-specific requirements
- Framework: {{framework}} - Adds framework-specific considerations
- Rules: {{rules}} - Ensures compliance with selected rules

### Language-Specific Considerations

{{#python}}
- Python version requirements
- Package dependencies
- Deployment environment (Python version, virtual environments)
{{/python}}

{{#javascript}}
- Node.js version requirements
- Package manager choice (npm/yarn/pnpm)
- Build tools and bundlers
{{/javascript}}

{{#java}}
- Java version requirements
- Build system (Maven/Gradle)
- Application server requirements
{{/java}}

### Rule-Specific Checks

{{#security}}
- Security requirements (authentication, authorization)
- Data protection requirements
- Compliance requirements (GDPR, SOC2, etc.)
{{/security}}

{{#performance}}
- Performance requirements (response time, throughput)
- Scalability requirements
- Caching strategies
{{/security}}
