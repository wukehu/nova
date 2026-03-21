# {{title}}

> **Document Info**
>
> - **Project**: {{project_name}}
> - **Version**: {{version}}
> - **Date**: {{date}}
> - **Authors**: {{authors}}
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

### 详细设计审核评分

| 评分项 | 分数 | 说明 |
|--------|------|------|
| API 设计 | {{api_design_score}}/10 | {{api_design_comment}} |
| 数据模型 | {{data_model_score}}/10 | {{data_model_comment}} |
| 接口定义 | {{interface_score}}/10 | {{interface_comment}} |
| 错误处理 | {{error_handling_score}}/10 | {{error_handling_comment}} |
| 安全设计 | {{security_design_score}}/10 | {{security_design_comment}} |
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

### 实施建议

{{#implementation_recommendations}}
**实施建议:**
1. {{recommendation_1}}
2. {{recommendation_2}}
{{/implementation_recommendations}}

---

## Introduction

{{introduction}}

## API Specification

### REST API

{{#rest_api}}
### {{resource_name}}

**Endpoint**: `{{http_method}} {{path}}`

**Description**: {{description}}

**Authentication**: {{authentication}}

**Request**:
```json
{{request_example}}
```

**Response (Success)**:
```json
{{response_success_example}}
```

**Response (Error)**:
```json
{{response_error_example}}
```

**Status Codes**:
- `200` - Success
- `201` - Created
- `400` - Bad Request
- `401` - Unauthorized
- `404` - Not Found
- `500` - Internal Server Error

{{/rest_api}}

### GraphQL API

```graphql
{{graphql_schema}}
```

## Data Models

### Entity Definitions

{{#entities}}
### {{entity_name}}

**Fields**:
| Field | Type | Constraints | Description |
|-------|------|-------------|-------------|
{{#fields}}
| {{name}} | {{type}} | {{constraints}} | {{description}} |
{{/fields}}

**Relationships**:
{{#relationships}}
- {{relation_type}} {{target_entity}}
{{/relationships}}

{{/entities}}

### Database Schema

```sql
{{sql_schema}}
```

## Component Design

### Service Interfaces

{{#service_interfaces}}
### {{service_name}}

```{{language_signature}}
{{interface_definition}}
```

**Methods**:
{{#methods}}
- `{{method_name}}({{params}}) -> {{return_type}}`
  - Description: {{description}}
  - Throws: {{exceptions}}
{{/methods}}

{{/service_interfaces}}

### Repository Interfaces

{{#repository_interfaces}}
### {{repository_name}}

```{{language_signature}}
{{interface_definition}}
```

**Methods**:
{{#methods}}
- `{{method_name}}({{params}}) -> {{return_type}}`
{{/methods}}

{{/repository_interfaces}}

## Validation Rules

### Input Validation

{{input_validation}}

### Business Rules

{{business_rules}}

## Error Handling

### Error Hierarchy

{{error_hierarchy}}

### Error Codes

| Code | Message | HTTP Status |
|------|---------|-------------|
{{#error_codes}}
| {{code}} | {{message}} | {{http_status}} |
{{/error_codes}}

## Caching Strategy

### Cache Keys

{{cache_keys}}

### Cache TTL

{{cache_ttl}}

### Cache Invalidation

{{cache_invalidation}}

## Security Implementation

### Authentication Flow

{{authentication_flow}}

### Authorization Model

{{authorization_model}}

### Data Encryption

{{data_encryption}}

## Transaction Management

### Transaction Boundaries

{{transaction_boundaries}}

### Isolation Levels

{{isolation_levels}}

## Logging Strategy

### Log Levels

{{log_levels}}

### Log Formats

{{log_formats}}

### Structured Logging

{{structured_logging}}

## Monitoring & Metrics

### Metrics

{{#metrics}}
- `{{name}}`: {{description}} ({{type}})
{{/metrics}}

### Health Checks

{{health_checks}}

## Testing Strategy

### Unit Tests

{{unit_tests}}

### Integration Tests

{{integration_tests}}

### E2E Tests

{{e2e_tests}}

---

## Appendix

### Data Dictionary

{{data_dictionary}}

### Sequence Diagrams

{{sequence_diagrams}}

### State Diagrams

{{state_diagrams}}

---

**Change History**

| Date | Version | Author | Changes |
|------|---------|--------|---------|
| {{date}} | {{version}} | {{authors}} | Initial version |
