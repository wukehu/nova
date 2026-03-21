# Code Phase Template
# 代码开发阶段模板

## Phase: Code Implementation

### Objective
Implement {{project_name}} according to the design document.

### Context
- **Language**: {{language}}
- **Framework**: {{framework}}
- **Rules**: {{rules}}
- **Design**: {{design_document}}

### Pre-Code Checklist
- [ ] Design document reviewed and approved
- [ ] Technical stack confirmed
- [ ] Development environment set up
- [ ] Dependencies installed
- [ ] Code repository initialized

### Implementation Strategy

#### 1. Project Structure
Set up the project structure according to {{language}} conventions:

{{#python}}
```python
src/
  {{package_name}}/
    __init__.py
    main.py
    api/
      __init__.py
      routes.py
    models/
      __init__.py
    services/
      __init__.py
tests/
  unit/
  integration/
pyproject.toml
README.md
```
{{/python}}

{{#javascript}}
```
src/
  index.js
  routes/
  services/
  models/
  middleware/
tests/
  unit/
  integration/
package.json
README.md
```
{{/javascript}}

#### 2. Core Implementation

Implement features in order of priority:
1. Core functionality
2. Error handling
3. Logging
4. Testing
5. Documentation

#### 3. Code Quality

Apply the following rules:

{{#clean_code}}
- Follow naming conventions
- Keep functions short and focused
- Don't repeat yourself (DRY)
- Use meaningful names
- Write self-documenting code
{{/clean_code}}

{{#security}}
- Validate all inputs
- Use parameterized queries
- Implement proper authentication
- Don't expose sensitive data
- Use secure algorithms
{{/security}}

### Language-Specific Guidelines

#### Python
```python
# Use type hints
def process_data(data: list[dict]) -> dict:
    """Process data and return results."""
    # Implementation
    pass

# Use context managers
with open("file.txt") as f:
    data = f.read()

# Use dataclasses
@dataclass
class User:
    name: str
    email: str
```

#### JavaScript
```javascript
// Use const/let
const apiUrl = "https://api.example.com";

// Use arrow functions
const processData = (data) => {
  // Implementation
};

// Use async/await
const fetchData = async () => {
  const response = await fetch(apiUrl);
  return response.json();
};
```

#### Java
```java
// Use interfaces
public interface UserService {
    User getUser(Long id);
    void saveUser(User user);
}

// Use Optional
public Optional<User> findById(Long id) {
    return repository.findById(id);
}
```

### Testing Strategy

#### Unit Tests
- Test each function/class in isolation
- Mock external dependencies
- Aim for >80% coverage

#### Integration Tests
- Test component interactions
- Test API endpoints
- Test database operations

{{#language}}
{{#python}}
Use pytest with fixtures:
```python
@pytest.fixture
def client():
    return TestClient(app)

def test_api_endpoint(client):
    response = client.get("/api/users")
    assert response.status_code == 200
```
{{/python}}

{{#javascript}}
Use vitest:
```javascript
import { describe, it, expect } from 'vitest';

describe('API', () => {
  it('should return users', async () => {
    const response = await fetch('/api/users');
    expect(response.status).toBe(200);
  });
});
```
{{/javascript}}
{{/language}}

### Documentation

#### Code Documentation
- Document all public APIs
- Use docstrings/comments
- Explain complex logic
- Provide examples

#### README
- Installation instructions
- Usage examples
- API documentation
- Contributing guidelines

### Outputs
- Source code in `src/`
- Unit tests in `tests/unit/`
- Integration tests in `tests/integration/`
- Documentation in `docs/`

### Quality Checks

Before marking as complete:
- [ ] All code follows {{language}} conventions
- [ ] All tests pass
- [ ] Code coverage > {{coverage_threshold}}%
- [ ] No linting errors
- [ ] Documentation complete
- [ ] Security checks pass

### Next Steps
After code implementation:
1. Run all tests
2. Perform code review
3. Create pull request
4. Deploy to staging
5. Perform integration testing

### Common Pitfalls to Avoid

{{#clean_code}}
- Don't write duplicate code
- Don't create god objects/classes
- Don't use magic numbers/strings
- Don't ignore error handling
- Don't skip testing
{{/clean_code}}

{{#security}}
- Don't trust user input
- Don't hardcode secrets
- Don't use weak crypto
- Don't expose stack traces
- Don't ignore vulnerabilities
{{/security}}
