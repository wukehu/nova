# {{title}}

> **Document Info**
>
> - **Project**: {{project_name}}
> - **Version**: {{version}}
> - **Date**: {{date}}
> - **Architect**: {{authors}}
> - **Status**: {{status}}

---

## 人工审核信息

> **审核状态**: {{review_status}}
> - **审核人**: {{reviewer_name}}
> - **审核开始时间**: {{review_start_time}}
> - **审核结束时间**: {{review_end_time}}
> - **审核用时**: {{review_duration}}
> - **审核评分**: {{review_score}}/10
> - **审核意见**: {{review_comments}}

### 审核详情

| 项目 | 内容 |
|------|------|
| **审核人** | {{reviewer_name}} |
| **审核角色** | {{reviewer_role}} |
| **审核开始** | {{review_start_time}} |
| **审核结束** | {{review_end_time}} |
| **审核用时** | {{review_duration}} |
| **审核状态** | {{review_status}} |

### 架构审核评分

| 评分项 | 分数 | 说明 |
|--------|------|------|
| 设计完整性 | {{design_completeness_score}}/10 | {{design_completeness_comment}} |
| 技术可行性 | {{technical_feasibility_score}}/10 | {{technical_feasibility_comment}} |
| 可扩展性 | {{scalability_score}}/10 | {{scalability_comment}} |
| 安全性 | {{security_score}}/10 | {{security_comment}} |
| 性能考虑 | {{performance_score}}/10 | {{performance_comment}} |
| **总分** | **{{review_score}}/10** | |

### 审核意见

{{#review_comments_positive}}
**✅ 通过的方面:**
- {{positive_comment}}

{{/review_comments_positive}}

{{#review_comments_improvement}}
**⚠️ 需要改进的方面:**
- {{improvement_comment}}

{{/review_comments_improvement}}

{{#review_comments_blocking}}
**❌ 阻塞问题:**
- {{blocking_comment}}

{{/review_comments_blocking}}

### 审核结论

{{review_conclusion}}

### 后续行动

{{#action_items}}
**行动项:**
1. {{action_item_1}}
2. {{action_item_2}}
{{/action_items}}

---

## Executive Summary

{{executive_summary}}

## Architecture Overview

{{architecture_overview}}

```
System Architecture Diagram:

┌─────────────────────────────────────────────────────┐
│                     Client Layer                    │
└────────────────────────┬────────────────────────────────┘
                         │
┌────────────────────────┴────────────────────────────────┐
│                    API Gateway                         │
│  - Authentication                                      │
│  - Rate Limiting                                       │
│  - Request Routing                                     │
└────────────────────────┬────────────────────────────────┘
                         │
        ┌────────────────┼────────────────┐
        ↓                ↓                ↓
┌──────────────┐  ┌──────────────┐  ┌──────────────┐
│  Service A   │  │  Service B   │  │  Service C   │
└──────┬───────┘  └──────┬───────┘  └──────┬───────┘
       │                 │                 │
       └─────────────────┼─────────────────┘
                         ↓
              ┌──────────────────────┐
              │    Data Layer         │
              │  - Database          │
              │  - Cache             │
              │  - File Storage      │
              └──────────────────────┘
```

## Design Principles

{{design_principles}}

## System Components

{{#components}}
### {{name}}

**Purpose**: {{purpose}}

**Responsibilities**:
{{#responsibilities}}
- {{item}}
{{/responsibilities}}

**Interfaces**:
{{#interfaces}}
- `{{method}}({{params}}) -> {{return}}`
{{/interfaces}}

**Technology**: {{technology}}
{{/components}}

## Data Architecture

### Data Model

```
Data Model Diagram:

┌──────────────┐       ┌──────────────┐
│    User      │──────►│    Order     │
├──────────────┤       ├──────────────┤
│ id (PK)      │       │ id (PK)      │
│ username     │       │ user_id (FK) │
│ email        │       │ total        │
│ password_hash│       │ status       │
└──────────────┘       └──────────────┘
```

### Data Flow

{{data_flow}}

## Technology Stack

### Backend

- **Language**: {{language}}
- **Framework**: {{framework}}
- **Runtime**: {{runtime}}

### Frontend

{{#frontend}}
- **Framework**: {{framework}}
- **UI Library**: {{ui_library}}
- **State Management**: {{state_management}}
{{/frontend}}

### Database

- **Primary**: {{primary_database}}
- **Cache**: {{cache}}
- **Search**: {{search_engine}}

### Infrastructure

- **Hosting**: {{hosting}}
- **Container**: {{container}}
- **Orchestration**: {{orchestration}}
- **CI/CD**: {{ci_cd}}

## Security Architecture

### Authentication

{{authentication}}

### Authorization

{{authorization}}

### Data Protection

{{data_protection}}

## Deployment Architecture

### Development Environment

{{dev_environment}}

### Staging Environment

{{staging_environment}}

### Production Environment

{{prod_environment}}

```
Deployment Diagram:

┌──────────────────────────────────────────┐
│            Load Balancer               │
└────────┬─────────────────┬───────────────┘
         │                 │
    ┌────▼────┐       ┌────▼────┐
    │ Server 1│       │ Server 2│
    └────┬────┘       └────┬────┘
         │                 │
         └────────┬────────┘
                  ↓
         ┌──────────────┐
         │   Database   │
         └──────────────┘
```

## Quality Attributes

### Performance

{{performance}}

### Scalability

{{scalability}}

### Reliability

{{reliability}}

### Maintainability

{{maintainability}}

## Architecture Decision Records

{{#adrs}}
### ADR-{{number}}: {{title}}

**Status**: {{status}}
**Date**: {{date}}
**Context**: {{context}}

**Decision**: {{decision}}

**Consequences**:
- **Positive**: {{positive_consequences}}
- **Negative**: {{negative_consequences}}

{{/adrs}}

## Cross-Cutting Concerns

### Logging

{{logging}}

### Monitoring

{{monitoring}}

### Error Handling

{{error_handling}}

### Configuration Management

{{configuration_management}}

## Future Considerations

{{future_considerations}}

---

## Appendix

### Component Matrix

| Component | Type | Technology | Purpose |
|-----------|------|------------|---------|
{{#component_matrix}}
| {{name}} | {{type}} | {{technology}} | {{purpose}} |
{{/component_matrix}}

### Technology Rationale

{{technology_rationale}}

---

**Change History**

| Date | Version | Author | Changes |
|------|---------|--------|---------|
| {{date}} | {{version}} | {{authors}} | Initial version |
