# Test Phase Template
# 测试阶段模板

## Phase: Testing

### Objective
Ensure {{project_name}} is thoroughly tested and meets quality standards.

### Context
- **Project**: {{project_name}}
- **Language**: {{language}}
- **Framework**: {{framework}}
- **Rules**: {{rules}}
- **Coverage Target**: {{coverage_threshold}}%

### Testing Strategy

#### 1. Test Pyramid

```
        ┌─────────┐
        │   E2E   │  ← Few, slow, expensive
        │  Tests  │
        ├─────────┤
        │Integration│
        │  Tests   │  ← Moderate number, medium speed
        ├─────────┤
        │  Unit    │  ← Many, fast, cheap
        │  Tests   │
        └─────────┘
```

#### 2. Unit Testing

##### Scope
- Test individual functions/methods
- Test classes/components in isolation
- Mock external dependencies
- Fast execution (ms scale)

{{#python}}
**Using pytest:**
```python
import pytest
from unittest.mock import Mock
from myapp.services.user_service import UserService

def test_create_user_success():
    # Arrange
    user_repo = Mock()
    user_service = UserService(user_repo)
    user_data = {"username": "test", "email": "test@example.com"}

    # Act
    result = user_service.create_user(user_data)

    # Assert
    assert result.username == "test"
    assert result.email == "test@example.com"
    user_repo.save.assert_called_once()

@pytest.mark.parametrize("input,expected", [
    ("valid@email.com", True),
    ("invalid", False),
    ("", False),
])
def test_email_validation(input, expected):
    assert validate_email(input) == expected
```
{{/python}}

{{#javascript}}
**Using vitest:**
```javascript
import { describe, it, expect, vi } from 'vitest';
import { UserService } from './user-service';

describe('UserService', () => {
  it('should create user successfully', () => {
    // Arrange
    const userRepo = { save: vi.fn() };
    const userService = new UserService(userRepo);
    const userData = { username: 'test', email: 'test@example.com' };

    // Act
    const result = userService.createUser(userData);

    // Assert
    expect(result.username).toBe('test');
    expect(result.email).toBe('test@example.com');
    expect(userRepo.save).toHaveBeenCalledOnce();
  });
});
```
{{/javascript}}

##### Coverage Requirements
- Minimum coverage: {{coverage_threshold}}%
- Critical paths: 100% coverage
- Error handling: covered

#### 3. Integration Testing

##### Scope
- Test component interactions
- Test database operations
- Test API endpoints
- Test external service integrations

{{#python}}
**API Integration Tests:**
```python
import pytest
from fastapi.testclient import TestClient
from myapp.main import app

client = TestClient(app)

def test_create_user_api():
    response = client.post(
        "/api/users",
        json={"username": "test", "email": "test@example.com"}
    )
    assert response.status_code == 201
    data = response.json()
    assert data["username"] == "test"
    assert "id" in data

def test_get_user_api():
    # First create a user
    create_response = client.post(
        "/api/users",
        json={"username": "test", "email": "test@example.com"}
    )
    user_id = create_response.json()["id"]

    # Then get the user
    response = client.get(f"/api/users/{user_id}")
    assert response.status_code == 200
    assert response.json()["username"] == "test"
```
{{/python}}

{{#javascript}}
**API Integration Tests:**
```javascript
import { describe, it, expect, beforeAll, afterAll } from 'vitest';
import { app } from './app';
import { Database } from './database';

describe('User API', () => {
  let db;

  beforeAll(async () => {
    db = new Database('test');
    await db.connect();
  });

  afterAll(async () => {
    await db.disconnect();
  });

  it('should create user', async () => {
    const response = await app.request('/api/users', {
      method: 'POST',
      body: JSON.stringify({ username: 'test', email: 'test@example.com' }),
    });

    expect(response.status).toBe(201);
    const data = await response.json();
    expect(data.username).toBe('test');
  });
});
```
{{/javascript}}

#### 4. End-to-End Testing

##### Scope
- Test complete user workflows
- Test UI interactions (if applicable)
- Test critical business paths
- Slow execution (seconds to minutes)

{{#web_app}}
**Using Playwright:**
```javascript
import { test, expect } from '@playwright/test';

test('user registration flow', async ({ page }) => {
  // Navigate to registration page
  await page.goto('/register');

  // Fill form
  await page.fill('[name="username"]', 'testuser');
  await page.fill('[name="email"]', 'test@example.com');
  await page.fill('[name="password"]', 'SecurePass123!');

  // Submit form
  await page.click('[type="submit"]');

  // Verify success
  await expect(page).toHaveURL('/dashboard');
  await expect(page.locator('h1')).toContainText('Welcome');
});
```
{{/web_app}}

#### 5. Performance Testing

##### Load Testing
- Define load scenarios
- Measure response times
- Identify bottlenecks
- Test scalability

{{#k6}}
```javascript
import http from 'k6/http';
import { check, sleep } from 'k6';

export let options = {
  stages: [
    { duration: '1m', target: 100 },  // Ramp up
    { duration: '3m', target: 100 },  // Stay at 100
    { duration: '1m', target: 0 },    // Ramp down
  ],
};

export default function () {
  let response = http.get('https://api.example.com/users');
  check(response, {
    'status is 200': (r) => r.status === 200,
    'response time < 500ms': (r) => r.timings.duration < 500,
  });
  sleep(1);
}
```
{{/k6}}

#### 6. Security Testing

{{#security}}
##### Security Checks
- SQL injection testing
- XSS testing
- Authentication bypass testing
- Authorization testing
- Input validation testing
- Dependency vulnerability scanning

```bash
# OWASP ZAP for security scanning
zap-cli quick-scan --self-contained http://localhost:3000

# Dependency vulnerability scan
npm audit
# or
pip-audit
```
{{/security}}

#### 7. Property-Based Testing

{{#python}}
**Using hypothesis:**
```python
from hypothesis import given, strategies as st
from myapp.validators import validate_email

@given(st.emails())
def test_email_validator_with_hypothesis(email):
    # Test that valid emails pass
    assert validate_email(email) == True

@given(st.text())
def test_email_validator_with_invalid_input(text):
    # Test that invalid emails fail appropriately
    if '@' not in text:
        assert validate_email(text) == False
```
{{/python}}

#### 8. Contract Testing

{{#api}}
**Using Pact:**
```python
from pact import Consumer, Provider

pact = Consumer('Frontend').has_pact_with(Provider('Backend'))

pact.given('user exists')\
    .upon_receiving('a request for user')\
    .with_request('GET', '/api/users/1')\
    .will_respond_with(200, body={
        'id': 1,
        'username': 'test',
        'email': 'test@example.com'
    })
```
{{/api}}

### Test Data Management

#### Test Data Strategy
- Use factories for test data generation
- Use fixtures for common test setups
- Clean up test data after tests
- Use transactions and rollback

{{#python}}
**Using factory_boy:**
```python
import factory
from myapp.models import User

class UserFactory(factory.Factory):
    class Meta:
        model = User

    username = factory.Sequence(lambda n: f"user{n}")
    email = factory.LazyAttribute(lambda o: f"{o.username}@example.com")

def test_with_factory():
    user = UserFactory()
    assert user.email.endswith("@example.com")
```
{{/python}}

### CI/CD Integration

#### Automated Testing Pipeline
```yaml
# .github/workflows/test.yml
name: Test Suite

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Setup {{language}}
        uses: actions/setup-{{language}}@v3
      - name: Install dependencies
        run: |
          {{install_command}}
      - name: Run unit tests
        run: |
          {{test_command}}
      - name: Run integration tests
        run: |
          {{integration_test_command}}
      - name: Upload coverage
        uses: codecov/codecov-action@v3
```

### Quality Gates

#### Pass/Fail Criteria
- ✅ All unit tests pass
- ✅ All integration tests pass
- ✅ Coverage ≥ {{coverage_threshold}}%
- ✅ No critical security vulnerabilities
- ✅ Performance benchmarks met
- ✅ E2E tests pass for critical paths

### Outputs
- Test reports (HTML, JSON, JUnit)
- Coverage reports
- Performance metrics
- Security scan results
- Test documentation

### Next Steps
After testing:
1. Review test results
2. Fix any failing tests
3. Address coverage gaps
4. Document test cases
5. Prepare for deployment

### Testing Checklist
- [ ] Unit tests written
- [ ] Integration tests written
- [ ] E2E tests written
- [ ] Performance tests run
- [ ] Security tests run
- [ ] Coverage meets threshold
- [ ] All tests passing
- [ ] Test documentation complete
