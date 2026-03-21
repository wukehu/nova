---
description: Use this skill when implementing software features, writing code, refactoring existing code, optimizing performance, or ensuring code quality and maintainability.
---

# Code Development Skill

## Purpose

Write clean, maintainable, well-tested code that follows best practices and design principles, turning specifications into working software.

## When to Use This Skill

Activate this skill when:
- Implementing new features
- Writing bug fixes
- Refactoring code
- Optimizing performance
- Writing tests
- Conducting code reviews
- Improving code quality

## Core Competencies

### 1. Clean Code Principles

**Meaningful Names**:
- Use intention-revealing names
- Avoid disinformation
- Make meaningful distinctions
- Use pronounceable names
- Use searchable names

**Functions**:
- Small (ideally < 20 lines)
- Do one thing
- One level of abstraction per function
- Descriptive names
- Few arguments (< 3 ideal)
- No side effects (or explicit)

**Comments**:
- Explain why, not what
- Don't comment bad code - rewrite it
- Keep comments up to date
- Use standard documentation formats

### 2. Design Principles

**SOLID**:
- **S**ingle Responsibility: One reason to change
- **O**pen/Closed: Open for extension, closed for modification
- **L**iskov Substitution: Subtypes must be substitutable
- **I**nterface Segregation: Many specific interfaces
- **D**ependency Inversion: Depend on abstractions

**DRY** (Don't Repeat Yourself):
- Extract duplicate code
- Use abstraction
- Normalize data

**KISS** (Keep It Simple, Stupid):
- Simple over clever
- Clear over concise
- Standard over custom

### 3. Error Handling

**Principles**:
- Use specific exception types
- Handle errors at appropriate layer
- Provide useful error messages
- Clean up resources (finally/context managers)
- Don't ignore errors
- Log all errors

**Pattern**:
```python
try:
    # Operation
except SpecificError as e:
    # Handle expected error
    log.warning(f"Specific error: {e}")
    raise UserFacingError("Clear message")
except Exception as e:
    # Handle unexpected error
    log.error(f"Unexpected error: {e}")
    raise
```

### 4. Testing Strategy

**Test Pyramid**:
```
        E2E (few)
       /       \
    Integration (more)
   /               \
Unit Tests (most)
```

**Unit Tests**:
- Test single functions/methods
- Mock dependencies
- Fast execution
- High coverage (>80%)

**Integration Tests**:
- Test component interactions
- Use real dependencies selectively
- Test database operations
- Test API endpoints

**E2E Tests**:
- Test critical user journeys
- Minimal number
- Slow execution
- Use for smoke testing

**Writing Good Tests**:
- Arrange-Act-Assert pattern
- Descriptive test names
- One assertion per test
- Independent tests
- Tests should be fast

### 5. Performance Optimization

**Guidelines**:
- Don't optimize prematurely
- Profile to find bottlenecks
- Optimize hot paths
- Consider algorithm complexity
- Use appropriate data structures
- Cache expensive operations
- Lazy load where appropriate
- Use async for I/O

**Common Optimizations**:
- Avoid nested loops
- Use sets/hashtables for lookups
- Batch operations
- Connection pooling
- Pagination
- Indexing

### 6. Security Best Practices

**Checklist**:
- [ ] Input validation (all inputs)
- [ ] Output encoding (prevent XSS)
- [ ] Parameterized queries (prevent SQL injection)
- [ ] No secrets in code
- [ ] Authentication/authorization
- [ ] HTTPS in production
- [ ] Secure headers
- [ ] Rate limiting
- [ ] Input sanitization
- [ ] Principle of least privilege

## Code Quality Standards

### Before Committing Code

**Self-Review**:
```markdown
## Code Review Checklist

### Functionality
- [ ] Does what it's supposed to do
- [ ] Handles edge cases
- [ ] Error handling in place

### Quality
- [ ] Clean and readable
- [ ] Follows style guide
- [ ] No code duplication
- [ ] Proper abstractions

### Testing
- [ ] Tests written
- [ ] Tests pass
- [ ] Coverage adequate
- [ ] Edge cases tested

### Documentation
- [ ] Code is self-documenting
- [ ] Complex logic commented
- [ ] API docs updated
- [ ] README updated (if needed)

### Security
- [ ] No hardcoded secrets
- [ ] Input validation
- [ ] Output encoding
- [ ] Proper error handling
- [ ] Authorization checks
```

## Common Patterns

### Repository Pattern

```python
class OrderRepository:
    def __init__(self, db):
        self.db = db

    def find_by_id(self, order_id: int) -> Optional[Order]:
        """Find order by ID"""
        return self.db.query(Order).filter_by(id=order_id).first()

    def save(self, order: Order) -> Order:
        """Save order"""
        self.db.add(order)
        self.db.commit()
        return order
```

### Service Layer Pattern

```python
class OrderService:
    def __init__(self, repo: OrderRepository, payment_svc: PaymentService):
        self.repo = repo
        self.payment_svc = payment_svc

    def create_order(self, user_id: int, items: List[Item]) -> Order:
        """Create a new order"""
        # Validation
        if not items:
            raise ValidationError("Items required")

        # Business logic
        order = Order(user_id=user_id, items=items)
        order.total = self._calculate_total(items)

        # Persistence
        return self.repo.save(order)

    def _calculate_total(self, items: List[Item]) -> Decimal:
        """Calculate order total"""
        return sum(item.price for item in items)
```

### Factory Pattern

```python
class PaymentProcessorFactory:
    @staticmethod
    def create(method: str) -> PaymentProcessor:
        """Create payment processor by method"""
        if method == "credit_card":
            return CreditCardProcessor()
        elif method == "paypal":
            return PayPalProcessor()
        else:
            raise ValueError(f"Unknown method: {method}")
```

## Refactoring Guidelines

### When to Refactor
- Rule of three: Three times, refactor
- Duplication: Extract common code
- Long methods: Break into smaller ones
- Large classes: Split responsibilities
- Complex conditionals: Simplify

### Refactoring Steps
1. Ensure tests pass
2. Make small changes
3. Run tests after each change
4. Commit frequently
5. Document why

### Common Refactorings

**Extract Method**:
```python
# Before
def process_order(order):
    # Validate
    if not order.user_id:
        raise Error("No user")
    if not order.items:
        raise Error("No items")
    # ... 50 lines ...

# After
def process_order(order):
    self._validate_order(order)
    self._calculate_totals(order)
    self._save_order(order)

def _validate_order(self, order):
    if not order.user_id:
        raise Error("No user")
    if not order.items:
        raise Error("No items")
```

**Replace Conditional with Polymorphism**:
```python
# Before
def calculate_discount(order):
    if order.type == "regular":
        return order.total * 0.05
    elif order.type == "premium":
        return order.total * 0.10
    elif order.type == "vip":
        return order.total * 0.15

# After
class Order:
    def __init__(self, type):
        self.type = OrderTypeFactory.create(type)

    def calculate_discount(self):
        return self.type.discount_rate * self.total
```

## Best Practices

### DO:
- Follow style guides consistently
- Write tests as you code (or right after)
- Keep functions small and focused
- Use meaningful names
- Handle errors properly
- Log important events
- Document non-obvious code
- Review your own code

### DON'T:
- Duplicate code
- Write long functions (> 50 lines)
- Use magic numbers
- Ignore errors
- Over-optimize prematurely
- Write clever code (write clear code)
- Skip tests
- Commit untested code

## Quality Checklist

**For Each Function/Method**:
- [ ] Does one thing
- [ ] Has a clear name
- [ ] Is short (< 20 lines ideal)
- [ ] Has no side effects (or explicit)
- [ ] Handles errors
- [ ] Is tested

**For Each Class/Module**:
- [ ] Single responsibility
- [ ] Clear interface
- [ ] Minimal dependencies
- [ ] Properly encapsulated
- [ ] Well documented

**For Each Feature**:
- [ ] Requirements met
- [ ] Edge cases handled
- [ ] Tests written
- [ ] Tests pass
- [ ] Performance acceptable
- [ ] Security considered
- [ ] Code reviewed

## Related Skills

- **Detailed Design**: Input for implementation
- **Debugging and Testing**: Ensure quality
- **Architecture Design**: Understand big picture
