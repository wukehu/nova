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

### 审核评分

| 评分项 | 分数 | 说明 |
|--------|------|------|
| 完整性 | {{completeness_score}}/10 | {{completeness_comment}} |
| 准确性 | {{accuracy_score}}/10 | {{accuracy_comment}} |
| 清晰性 | {{clarity_score}}/10 | {{clarity_comment}} |
| 可行性 | {{feasibility_score}}/10 | {{feasibility_comment}} |
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

---

## Overview

{{overview}}

## Functional Requirements

### User Stories

{{user_stories}}

### Requirements List

| ID | Requirement | Priority | Status |
|----|------------|----------|--------|
{{#requirements}}
| {{id}} | {{description}} | {{priority}} | {{status}} |
{{/requirements}}

## Non-Functional Requirements

### Performance

{{performance_requirements}}

### Security

{{security_requirements}}

### Scalability

{{scalability_requirements}}

### Reliability

{{reliability_requirements}}

## Constraints

### Technical Constraints

{{technical_constraints}}

### Business Constraints

{{business_constraints}}

### Regulatory Constraints

{{regulatory_constraints}}

## Assumptions

{{assumptions}}

## Dependencies

{{dependencies}}

## Success Criteria

{{success_criteria}}

## Acceptance Criteria

{{acceptance_criteria}}

## Risks and Mitigation

| Risk | Impact | Probability | Mitigation |
|------|--------|-------------|------------|
{{#risks}}
| {{description}} | {{impact}} | {{probability}} | {{mitigation}} |
{{/risks}}

---

## Appendix

### Glossary

{{glossary}}

### References

{{references}}

---

**Change History**

| Date | Version | Author | Changes |
|------|---------|--------|---------|
| {{date}} | {{version}} | {{authors}} | Initial version |
