# Review Phase Template
# 代码审查阶段模板

## Phase: Code Review

### Objective
Conduct thorough code review to ensure {{project_name}} meets quality standards.

### Context
- **Project**: {{project_name}}
- **Language**: {{language}}
- **Rules**: {{rules}}
- **Reviewer(s)**: {{reviewers}}
- **Changes**: {{pull_request_link}}

### Review Process

#### 1. Pre-Review Checklist

Before starting the review:
- [ ] PR description is clear and complete
- [ ] Linked to relevant issue/ticket
- [ ] Tests are included
- [ ] Documentation is updated
- [ ] CI/CD checks pass
- [ ] No merge conflicts

#### 2. Automated Checks

{{#clean_code}}
##### Code Quality
```bash
# Linting
{{linter_command}}

# Formatting check
{{formatter_command}} --check

# Type checking
{{type_checker_command}}
```
{{/clean_code}}

{{#security}}
##### Security Scanning
```bash
# Dependency vulnerability scan
npm audit
# or
pip-audit

# SAST scan
semgrep scan
```
{{/security}}

#### 3. Manual Review Checklist

##### Functionality
- [ ] Code implements the requirements
- [ ] Edge cases are handled
- [ ] Error handling is appropriate
- [ ] No obvious bugs

##### Code Quality
{{#clean_code}}
- [ ] Code is readable and understandable
- [ ] Functions are short and focused
- [ ] Names are descriptive
- [ ] No code duplication
- [ ] Proper abstraction
- [ ] Comments explain "why", not "what"
- [ ] No commented-out code
- [ ] No debugging code left in
{{/clean_code}}

##### Design & Architecture
- [ ] Follows established patterns
- [ ] Proper separation of concerns
- [ ] Dependencies are appropriate
- [ ] API design is consistent
- [ ] Data structures are appropriate

##### Testing
- [ ] Tests cover the changes
- [ ] Tests are well-written
- [ ] Edge cases are tested
- [ ] No hardcoded test data
- [ ] Tests are maintainable

##### Security
{{#security}}
- [ ] No hardcoded secrets/credentials
- [ ] Input validation is present
- [ ] Output encoding is correct
- [ ] Authentication/authorization checks
- [ ] SQL injection prevention
- [ ] XSS prevention
- [ ] CSRF protection (if applicable)
- [ ] Proper error messages (no info leakage)
{{/security}}

##### Performance
- [ ] No obvious performance issues
- [ ] Efficient algorithms used
- [ ] No unnecessary database queries
- [ ] Proper caching (if applicable)
- [ ] No memory leaks

##### Documentation
- [ ] Code is self-documenting
- [ ] Complex logic has comments
- [ ] Public APIs have documentation
- [ ] README is updated (if needed)
- [ ] CHANGELOG is updated (if needed)

#### 4. Language-Specific Checks

{{#python}}
##### Python
- [ ] Type hints used
- [ ] Docstrings in Google style
- [ ] Follows PEP 8
- [ ] Uses context managers
- [ ] Uses f-strings for formatting
- [ ] Uses dataclasses for data
- [ ] Uses pathlib for paths
- [ ] No mutable default arguments
- [ ] Imports are sorted
- [ ] Virtual environment requirements updated
{{/python}}

{{#javascript}}
##### JavaScript
- [ ] Uses const/let (no var)
- [ ] Uses arrow functions appropriately
- [ ] Uses async/await (no .then())
- [ ] Uses template literals
- [ ] Uses destructuring
- [ ] Uses optional chaining (?.)
- [ ] Uses nullish coalescing (??)
- [ ] No console.log left in
- [ ] Dependencies are necessary
- [ ] package.json updated
{{/javascript}}

{{#java}}
##### Java
- [ ] Follows Java conventions
- [ ] Uses interfaces appropriately
- [ ] Uses @Override annotations
- [ ] Uses Optional for nullable returns
- [ ] Implements toString, equals, hashCode
- [ ] Uses try-with-resources
- [ ] Proper exception handling
- [ ] No raw types
- [ ] Generics used correctly
{{/java}}

#### 5. Review Guidelines

##### Be Constructive
- Focus on the code, not the person
- Explain the reasoning for suggestions
- Provide examples for improvements
- Acknowledge good code

##### Be Thorough
- Don't rush the review
- Test the changes if possible
- Consider edge cases
- Think about maintenance

##### Be Respectful
- Assume good intentions
- Ask questions instead of making demands
- Be open to discussion
- Admit when you're wrong

#### 6. Review Feedback Template

```markdown
## Code Review: {{pr_title}}

### Summary
{{overall_impression}}

### Issues Requiring Changes
{{must_fix_items}}

### Suggestions for Improvement
{{should_fix_items}}

### Nitpicks (Optional)
{{nice_to_have_items}}

### Positive Feedback
{{good_points}}

### Approval Status
- [ ] Approve
- [ ] Request changes
- [ ] Comment only

### Additional Notes
{{any_other_feedback}}
```

#### 7. Common Issues to Look For

##### Bug Patterns
- Off-by-one errors
- Null/undefined dereferences
- Race conditions
- Resource leaks
- Uninitialized variables

##### Code Smells
- Long functions (> 20 lines)
- God objects/classes
- Duplicated code
- Magic numbers/strings
- Overly complex conditions

##### Security Issues
- SQL injection vectors
- XSS vulnerabilities
- Hardcoded credentials
- Missing authentication
- Insecure data handling

#### 8. Review Metrics

Track review effectiveness:
- Review time
- Number of issues found
- Types of issues
- Rework required
- Approval rate

### Outputs
- Review comments on PR
- Review summary document
- Action items for author
- Metrics for process improvement

### Follow-Up Actions

#### For Author
- Address all "Must Fix" items
- Consider "Should Fix" items
- Respond to all comments
- Update tests if needed
- Request re-review if significant changes

#### For Reviewer
- Verify fixes
- Approve when satisfied
- Document decisions
- Provide final feedback

### Best Practices

1. **Small PRs**: Keep PRs small and focused
2. **Clear Descriptions**: Explain what and why
3. **Self-Review**: Review your own code first
4. **Quick Feedback**: Provide initial feedback quickly
5. **Thorough Follow-up**: Ensure all issues are addressed

### Tools

#### Review Tools
- GitHub/GitLab PR reviews
- Codecov for coverage
- SonarQube for quality analysis
- LGTM.com for security analysis

#### Automated Review
```yaml
# .github/workflows/review.yml
name: Automated Review

on:
  pull_request:
    types: [opened, synchronize]

jobs:
  review:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Run linter
        run: {{linter_command}}
      - name: Run type checker
        run: {{type_checker_command}}
      - name: Check coverage
        run: {{coverage_command}}
      - name: Security scan
        run: {{security_scan_command}}
```

### Next Steps
After review:
1. Author addresses feedback
2. Re-review if necessary
3. Approve and merge
4. Delete branch (if merged)
5. Archive review documentation
