---
description: Document and phase review management - request reviews, track status, manage review assignments, and generate review reports
argument-hint: <action> [options]
allowed-tools: [Read, Write, Edit, Grep, AskUserQuestion]
---

# Review Management

Manage document and phase reviews with tracking, assignment, and quality metrics.

## Usage

```
/review request                   # Request review for current phase
/review assign <reviewer>         # Assign reviewer
/review start                     # Start review process
/review complete                  # Mark review as complete
/review approve                    # Approve document
/review request_changes           # Request changes
/review reject                     # Reject document
/review status                     # Show review status
/review metrics                    # Show review metrics
/review history <document>        # Show review history
```

## Review Workflow

### 1. Request Review

```bash
/review request
```

This will:
- Create review request for current phase document
- Assign reviewer (auto or manual)
- Set review status to "pending"
- Send notification to reviewer

### 2. Start Review

```bash
/review start
```

Reviewer actions:
- Open document for review
- Start review timer
- Set status to "in_progress"

### 3. Add Comments

```bash
/review comment "Section 3.2 needs more detail"
```

Comment types:
- `--blocking` - Critical issue, must fix
- `--major` - Important issue
- `--minor` - Suggestion
- `--info` - Information only

### 4. Complete Review

```bash
/review complete
```

This will:
- Stop review timer
- Calculate review duration
- Generate review summary
- Set status based on scores

## Review Scoring

### Automated Scoring

Based on checklist completion:
```yaml
scoring:
  completeness: 20%  # All sections present
  accuracy: 25%      # No errors or inconsistencies
  clarity: 30%       # Clear and understandable
  feasibility: 25%   # Practical and achievable
```

### Manual Scoring

Reviewer can adjust scores:
```bash
/review score completeness 8/10 "Missing some edge cases"
/review score accuracy 9/10
/review score clarity 10/10
/review score feasibility 8/10
```

## Review Status

### Check Status

```bash
/review status
```

Output:
```
Document: requirements_20260321_143000.md
Status: In Review
Reviewer: John Doe
Started: 2026-03-21 14:30:00
Elapsed: 45 minutes
Progress: ████████░░░░ 80%

Scores:
  Completeness: ██████████░ 9/10
  Accuracy: ███████████░ 9/10
  Clarity: █████████████ 10/10
  Feasibility: ████████░░░░ 7/10

Overall: ██████████░ 35/40 (87.5%)
```

## Review Actions

### Approve

```bash
/review approve
```

Requirements:
- All scores ≥ 7/10
- No blocking comments
- Overall score ≥ 70%

### Request Changes

```bash
/review request_changes
```

Use when:
- Scores < 7/10
- Blocking comments exist
- Overall score < 70%

### Reject

```bash
/review reject
```

Use when:
- Major structural issues
- Fundamental flaws
- Incomplete document

## Review Metrics

### View Metrics

```bash
/review metrics
```

Output:
```
Review Metrics (Last 30 Days)

Total Reviews: 15
Approved: 12 (80%)
Changes Requested: 2 (13%)
Rejected: 1 (7%)

Average Review Time:
  Requirements: 1.5 hours
  Architecture: 3.2 hours
  Detail Design: 2.8 hours

Top Reviewers:
  John Doe: 5 reviews
  Jane Smith: 4 reviews
  Bob Johnson: 3 reviews

Average Scores:
  Completeness: 8.5/10
  Accuracy: 8.8/10
  Clarity: 9.2/10
  Feasibility: 8.0/10
```

## Review Templates

### Requirements Review Template

```markdown
## Requirements Review

**Document**: {{document_name}}
**Reviewer**: {{reviewer_name}}
**Date**: {{review_date}}

### Review Checklist

#### Completeness (20 points)
- [ ] All functional requirements listed
- [ ] All non-functional requirements defined
- [ ] All constraints identified
- [ ] All success criteria defined

**Score**: {{completeness_score}}/20

#### Accuracy (25 points)
- [ ] No contradictions
- [ ] No ambiguous statements
- [ ] Terminology is consistent
- [ ] Data requirements are specific

**Score**: {{accuracy_score}}/25

#### Clarity (30 points)
- [ ] Well-organized structure
- [ ] Clear language
- [ ] Good use of diagrams
- [ ] Table of contents present

**Score**: {{clarity_score}}/30

#### Feasibility (25 points)
- [ ] Technically feasible
- [ ] Time budget realistic
- [ ] Resource requirements reasonable
- [ ] Risks are acceptable

**Score**: {{feasibility_score}}/25

### Total Score

{{total_score}}/100

### Review Comments

#### Blocking Issues
{{#blocking_comments}}
- [ ] {{comment}}
{{/blocking_comments}}

#### Major Issues
{{#major_comments}}
- [ ] {{comment}}
{{/major_comments}}

#### Suggestions
{{#suggestions}}
- [ ] {{comment}}
{{/suggestions}}

### Recommendation

{{recommendation}}

**Next Steps**:
{{next_steps}}
```

## Review History

### Show History

```bash
/review history requirements_20260321_143000.md
```

Output:
```
Review History

Review #1 - 2026-03-21 14:30
  Reviewer: John Doe
  Duration: 1 hour 23 minutes
  Score: 87/100
  Status: Changes Requested
  Comments:
    - Blocking: Section 3 needs more detail
    - Minor: Consider adding examples

Review #2 - 2026-03-22 10:15
  Reviewer: Jane Smith
  Duration: 45 minutes
  Score: 92/100
  Status: Approved
  Comments:
    - All issues from previous review addressed
    - Document is now complete and clear
```

## Best Practices

### For Reviewers

1. **Be Thorough**: Review entire document carefully
2. **Be Constructive**: Provide helpful feedback
3. **Be Timely**: Complete reviews within time limits
4. **Be Clear**: Use specific, actionable comments
5. **Be Fair**: Apply consistent standards

### For Authors

1. **Self-Review**: Review your own document first
2. **Check Checklist**: Use review checklist before submitting
3. **Be Responsive**: Address review comments promptly
4. **Be Professional**: Accept feedback gracefully
5. **Learn**: Improve based on review feedback

## Review Quality Metrics

### Good Review Indicators

- Specific, actionable comments
- Balanced feedback (positive + constructive)
- References to specific sections
- Clear rationale for scores
- Reasonable completion time

### Poor Review Indicators

- Vague comments like "needs improvement"
- Only negative feedback
- No rationale for scores
- Excessive time taken
- Inconsistent standards

## Integration with Workflow

### Automatic Review Trigger

```yaml
# workflow.yaml
phases:
  - id: "requirements"
    output:
      document:
        auto_request_review: true
        required_reviewers: 1
```

### Review Gates

```yaml
# Cannot proceed to next phase until:
gates:
  - document_approved: true
  - blocking_issues_resolved: true
  - overall_score >= 70
```

## See Also

- `/workflow` - Workflow execution
- `/template` - Template management
