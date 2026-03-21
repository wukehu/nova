---
description: Use this skill when debugging software issues, fixing bugs, writing tests, troubleshooting problems, or ensuring software quality through testing strategies.
---

# Debugging and Testing Skill

## Purpose

Systematically identify, diagnose, and fix software bugs while creating comprehensive tests to prevent regressions and ensure long-term quality.

## When to Use This Skill

Activate this skill when:
- Debugging errors or unexpected behavior
- Investigating bug reports
- Writing tests for new or existing code
- Troubleshooting production issues
- Conducting root cause analysis
- Creating test strategies
- Performing code reviews for quality

## Core Competencies

### 1. Systematic Debugging

**Debugging Framework**:

**Phase 1: Understand**
- What is the expected behavior?
- What is the actual behavior?
- When does this happen?
- How often does it occur?
- Who is affected?

**Phase 2: Reproduce**
- Follow the exact steps
- Identify minimal reproduction
- Determine if intermittent
- Note environment/context

**Phase 3: Gather Data**
- Error logs and stack traces
- Variable states
- System metrics
- Recent changes
- Configuration

**Phase 4: Form Hypotheses**
- Brainstorm possible causes
- Prioritize by likelihood
- Plan verification steps

**Phase 5: Isolate**
- Binary search (comment out code)
- Add logging/debugging
- Check one variable at a time
- Use debugger

**Phase 6: Identify Root Cause**
- Use "Five Whys" technique
- Trace execution flow
- Check assumptions
- Verify data flow

**Phase 7: Fix**
- Address root cause, not symptoms
- Make minimal changes
- Add defensive code
- Document the fix

**Phase 8: Verify**
- Reproduce the bug (should be fixed)
- Test related functionality
- Check for regressions
- Verify performance not degraded

### 2. Test Strategy

**Test Pyramid**:
```
        E2E (10%)
       /       \
    Integration (30%)
   /               \
Unit Tests (60%)
```

**Unit Testing**:
- Test individual functions/methods
- Mock dependencies
- Fast execution
- High coverage (>80%)
- Test happy paths + edge cases

**Integration Testing**:
- Test component interactions
- Use real databases/external services
- Test API endpoints
- Test data access layers

**End-to-End Testing**:
- Test critical user journeys
- Minimal, focused tests
- Slow execution
- Use for smoke testing

### 3. Writing Good Tests

**Test Structure** (Arrange-Act-Assert):
```python
def test_create_order_with_valid_data():
    # Arrange
    user = create_user(id=1, name="Test")
    items = [Item(name="Widget", price=10.00)]

    # Act
    order = OrderService.create(user.id, items)

    # Assert
    assert order.user_id == 1
    assert order.total == 10.00
    assert order.status == OrderStatus.PENDING
```

**Test Naming**:
- Descriptive and specific
- Test what, not how
- Include scenario and expected outcome
```
test_[method]_[scenario]_[expected]()

Examples:
test_create_order_with_empty_items_raises_error()
test_calculate_total_with_discount_applies_correctly()
```

**Test Coverage**:
- Happy path (normal operation)
- Edge cases (boundaries, empty, null)
- Error conditions (exceptions, invalid input)
- Business rules (validation, constraints)

### 4. Common Bug Patterns

**Null/Undefined Errors**:
- Check for null before accessing
- Use optional chaining
- Provide default values

**Race Conditions**:
- Look for shared mutable state
- Check for missing synchronization
- Consider async/await issues
- Look for non-atomic operations

**Memory Leaks**:
- Unclosed connections/streams
- Event listeners not removed
- Circular references
- Growing caches

**Off-by-One Errors**:
- Loop boundaries
- Array indices
- Substring indices
- Date calculations

**Type Errors**:
- Implicit type conversions
- String vs number
- Truthy/falsy confusion
- Strict vs loose equality

### 5. Root Cause Analysis

**Five Whys Technique**:
```
Problem: Order processing failed

Why 1: Payment service rejected the transaction
Why 2: Invalid payment token
Why 3: Token format changed
Why 4: API updated without notice
Why 5: No integration tests for payment service

Root Cause: Missing integration tests + lack of API monitoring
```

**Fishbone Diagram** (Categories):
- People: Training, staffing
- Process: Procedures, workflows
- Machine: Tools, equipment
- Material: Resources, data
- Environment: Conditions, context
- Management: Planning, oversight

### 6. Testing Best Practices

**DO**:
- Write tests alongside code
- Use descriptive names
- Test behavior, not implementation
- Keep tests independent
- Make tests fast
- Use fixtures for common setup
- Mock external dependencies
- Test error conditions
- Maintain high coverage

**DON'T**:
- Test everything via E2E
- Write brittle tests
- Test implementation details
- Skip edge cases
- Write slow tests
- Over-mock (test mocks not code)
- Ignore failing tests
- Test without assertions

## Debugging Tools and Techniques

### Logging Strategy

```python
# Good logging
logger.info("Creating order", extra={
    "user_id": user.id,
    "item_count": len(items),
    "total": total
})

logger.error("Payment failed", extra={
    "order_id": order.id,
    "error": str(e),
    "payment_service": "stripe"
})
```

### Debugging Checklist

- [ ] Issue fully understood
- [ ] Reproduced the problem
- [ ] Root cause identified
- [ ] Fix designed
- [ ] Fix implemented
- [ ] Regression tests added
- [ ] Related functionality tested
- [ ] Fix documented
- [ ] Changes reviewed

### Code Review for Bugs

When reviewing code for potential bugs:
- Null/undefined checks
- Boundary conditions
- Error handling
- Resource cleanup
- Thread safety
- Input validation
- Edge cases
- Performance issues
- Security vulnerabilities

## Test Documentation

**Test Plan Template**:
```markdown
# Test Plan: [Feature]

## Scope
[What's being tested]

## Test Types
- Unit: [What and how many]
- Integration: [What and how many]
- E2E: [What and how many]

## Test Cases
### Unit Tests
- [Test case 1]: [Description]
- [Test case 2]: [Description]

### Integration Tests
- [Test case 1]: [Description]

### E2E Tests
- [Test case 1]: [Description]

## Coverage Target
- Unit: >80%
- Integration: Key paths
- E2E: Critical journeys

## Environment
- Test data: [How to set up]
- Dependencies: [What's needed]
- Configuration: [Settings]

## Execution
- How to run: [Commands]
- How long: [Time estimate]
```

## Quality Checklist

**For Bug Fixes**:
- [ ] Root cause identified
- [ ] Fix addresses root cause
- [ ] Regression tests added
- [ ] All tests pass
- [ ] No side effects
- [ ] Fix documented
- [ ] Similar issues checked

**For New Code**:
- [ ] Unit tests written (>80% coverage)
- [ ] Integration tests for interactions
- [ ] E2E tests for critical paths
- [ ] Edge cases tested
- [ ] Error conditions tested
- [ ] All tests pass
- [ ] Performance acceptable

## Related Skills

- **Code Development**: Writing quality code
- **Requirements Analysis**: Understanding what to test
- **Architecture Design**: Designing testable systems
