# Detailed Design Phase Template
# 详细设计阶段模板

## Phase: Detailed Design

### Objective
Create detailed technical specifications for {{project_name}} components based on architecture decisions.

### Context
- **Project**: {{project_name}}
- **Architecture**: {{architecture_document}}
- **Language**: {{language}}
- **Framework**: {{framework}}
- **Team**: {{team_members}}

---

## Detailed Design Process

### Step 1: API Design

#### REST API Design

**Resource Naming:**
```
GET    /api/users           - List users
GET    /api/users/{id}      - Get user by ID
POST   /api/users           - Create user
PUT    /api/users/{id}      - Update user
DELETE /api/users/{id}      - Delete user
```

**Request/Response Format:**
```json
// Request
{
  "username": "john_doe",
  "email": "john@example.com",
  "password": "SecurePass123!"
}

// Response (Success - 200/201)
{
  "id": 123,
  "username": "john_doe",
  "email": "john@example.com",
  "createdAt": "2026-03-21T10:00:00Z"
}

// Response (Error - 4xx/5xx)
{
  "error": "Validation Error",
  "message": "Email is required",
  "code": "VALIDATION_ERROR",
  "details": ["email field is required"]
}
```

**Pagination:**
```
GET /api/users?page=1&size=20&sort=createdAt:desc

Response:
{
  "data": [...],
  "pagination": {
    "page": 1,
    "size": 20,
    "total": 1000,
    "totalPages": 50
  }
}
```

**Filtering:**
```
GET /api/users?status=active&role=admin&createdAfter=2026-01-01
```

**Versioning:**
```
/api/v1/users - Current version
/api/v2/users - New version (breaking changes)
```

#### GraphQL API Design

```graphql
type User {
  id: ID!
  username: String!
  email: String!
  createdAt: DateTime!
  orders: [Order!]!
}

type Query {
  user(id: ID!): User
  users(limit: Int, offset: Int): [User!]!
}

type Mutation {
  createUser(input: CreateUserInput!): User!
  updateUser(id: ID!, input: UpdateUserInput!): User!
  deleteUser(id: ID!): Boolean!
}

input CreateUserInput {
  username: String!
  email: String!
  password: String!
}
```

### Step 2: Data Models

#### Database Schema

**Users Table:**
```sql
CREATE TABLE users (
    id BIGSERIAL PRIMARY KEY,
    username VARCHAR(50) UNIQUE NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    status VARCHAR(20) DEFAULT 'active',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    last_login_at TIMESTAMP,

    CONSTRAINT chk_status
        CHECK (status IN ('active', 'inactive', 'suspended'))
);

CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_users_username ON users(username);
CREATE INDEX idx_users_status ON users(status);
CREATE INDEX idx_users_created_at ON users(created_at);
```

**Orders Table:**
```sql
CREATE TABLE orders (
    id BIGSERIAL PRIMARY KEY,
    user_id BIGINT NOT NULL,
    total_amount DECIMAL(10, 2) NOT NULL,
    status VARCHAR(20) DEFAULT 'pending',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,

    CONSTRAINT fk_user
        FOREIGN KEY (user_id)
        REFERENCES users(id) ON DELETE CASCADE,
    CONSTRAINT chk_status
        CHECK (status IN ('pending', 'processing',
                         'shipped', 'delivered', 'cancelled'))
);

CREATE INDEX idx_orders_user_id ON orders(user_id);
CREATE INDEX idx_orders_status ON orders(status);
CREATE INDEX idx_orders_created_at ON orders(created_at);
```

#### Entity-Relationship Diagram

```
┌──────────────┐       ┌──────────────┐
│    Users     │       │    Orders    │
├──────────────┤       ├──────────────┤
│ id (PK)      │──┐    │ id (PK)      │
│ username     │  │    │ user_id (FK) │◄──┐
│ email        │  │    │ total_amount │   │
│ password_hash│  │    │ status       │   │
│ status       │  │    │ created_at   │   │
│ created_at   │  │    └──────────────┘   │
└──────────────┘  │                        │
                  │                        │
                  │              ┌──────────┴──────┐
                  │              │    OrderItems   │
                  │              ├─────────────────┤
                  │              │ id (PK)         │
                  │              │ order_id (FK)  │◄─┘
                  │              │ product_id (FK) │
                  │              │ quantity        │
                  │              │ price           │
                  │              └─────────────────┘
                  │
                  │              ┌──────────────┐
                  └─────────────►│   Products   │
                                 ├──────────────┤
                                 │ id (PK)      │
                                 │ name         │
                                 │ price        │
                                 │ stock        │
                                 └──────────────┘
```

### Step 3: Class/Component Design

#### Service Layer Design

**Interface Definition:**
```python
from abc import ABC, abstractmethod
from typing import Optional, List

class IUserService(ABC):
    """User service interface"""

    @abstractmethod
    def create_user(self, username: str, email: str, password: str) -> User:
        """Create a new user"""
        pass

    @abstractmethod
    def get_user(self, user_id: int) -> Optional[User]:
        """Get user by ID"""
        pass

    @abstractmethod
    def update_user(self, user_id: int, **kwargs) -> User:
        """Update user"""
        pass

    @abstractmethod
    def delete_user(self, user_id: int) -> bool:
        """Delete user"""
        pass

    @abstractmethod
    def list_users(self, page: int = 1, size: int = 20) -> PaginatedResult[User]:
        """List users with pagination"""
        pass
```

**Implementation:**
```python
class UserService(IUserService):
    """User service implementation"""

    def __init__(self,
                 user_repo: IUserRepository,
                 password_hasher: IPasswordHasher,
                 email_service: IEmailService):
        self._user_repo = user_repo
        self._password_hasher = password_hasher
        self._email_service = email_service

    def create_user(self, username: str, email: str, password: str) -> User:
        # Validate input
        self._validate_username(username)
        self._validate_email(email)
        self._validate_password(password)

        # Check if user exists
        if self._user_repo.exists_by_username(username):
            raise UserAlreadyExistsError(username)

        if self._user_repo.exists_by_email(email):
            raise EmailAlreadyInUseError(email)

        # Hash password
        password_hash = self._password_hasher.hash(password)

        # Create user
        user = User(
            username=username,
            email=email,
            password_hash=password_hash
        )

        # Save to database
        user = self._user_repo.save(user)

        # Send welcome email
        self._email_service.send_welcome_email(user.email)

        return user

    def get_user(self, user_id: int) -> Optional[User]:
        return self._user_repo.find_by_id(user_id)

    # ... other methods
```

#### Repository Design

```python
class IUserRepository(ABC):
    """User repository interface"""

    @abstractmethod
    def find_by_id(self, user_id: int) -> Optional[User]:
        pass

    @abstractmethod
    def find_by_username(self, username: str) -> Optional[User]:
        pass

    @abstractmethod
    def find_by_email(self, email: str) -> Optional[User]:
        pass

    @abstractmethod
    def save(self, user: User) -> User:
        pass

    @abstractmethod
    def delete(self, user_id: int) -> bool:
        pass

    @abstractmethod
    def exists_by_username(self, username: str) -> bool:
        pass

    @abstractmethod
    def exists_by_email(self, email: str) -> bool:
        pass
```

### Step 4: Data Validation

#### Validation Rules

**User Validation:**
```python
from pydantic import BaseModel, EmailStr, Field, validator

class CreateUserRequest(BaseModel):
    username: str = Field(
        ...,
        min_length=3,
        max_length=50,
        pattern=r'^[a-zA-Z0-9_-]+$'
    )
    email: EmailStr
    password: str = Field(
        ...,
        min_length=8,
        regex=r'^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)'
    )

    @validator('username')
    def validate_username(cls, v):
        if v in ['admin', 'root', 'system']:
            raise ValueError('Username is reserved')
        return v

    @validator('password')
    def validate_password(cls, v):
        if not any(c.isdigit() for c in v):
            raise ValueError('Password must contain a digit')
        if not any(c.isupper() for c in v):
            raise ValueError('Password must contain uppercase letter')
        return v

class UpdateUserRequest(BaseModel):
    email: Optional[EmailStr] = None
    status: Optional[str] = Field(
        None,
        pattern=r'^(active|inactive|suspended)$'
    )
```

#### Business Rules Validation

```python
class UserBusinessRules:
    """Business rules for user operations"""

    MIN_AGE = 13
    MAX_USERNAME_CHANGES = 3

    @staticmethod
    def can_user_change_username(user: User) -> bool:
        """Check if user can change username"""
        return user.username_change_count < UserBusinessRules.MAX_USERNAME_CHANGES

    @staticmethod
    def is_user_eligible(user: User) -> bool:
        """Check if user is eligible for service"""
        return (
            user.status == 'active' and
            user.age >= UserBusinessRules.MIN_AGE and
            not user.is_banned
        )
```

### Step 5: Error Handling

#### Error Hierarchy

```python
class ApplicationException(Exception):
    """Base application exception"""

    def __init__(self, message: str, code: str = None):
        self.message = message
        self.code = code or self.__class__.__name__
        super().__init__(self.message)

class ValidationError(ApplicationException):
    """Validation error"""
    pass

class NotFoundError(ApplicationException):
    """Resource not found error"""
    pass

class UnauthorizedError(ApplicationException):
    """Unauthorized access error"""
    pass

class BusinessRuleError(ApplicationException):
    """Business rule violation error"""
    pass

# Specific errors
class UserNotFoundError(NotFoundError):
    pass

class InvalidCredentialsError(UnauthorizedError):
    pass

class EmailAlreadyInUseError(BusinessRuleError):
    pass
```

#### Error Response Format

```python
{
    "error": {
        "code": "USER_NOT_FOUND",
        "message": "User with id 123 not found",
        "details": {
            "field": "id",
            "value": 123
        },
        "timestamp": "2026-03-21T10:00:00Z",
        "request_id": "req_abc123"
    }
}
```

### Step 6: Transaction Management

#### Transaction Design

```python
class OrderService:
    """Order service with transaction management"""

    def __init__(self,
                 order_repo: IOrderRepository,
                 user_repo: IUserRepository,
                 product_repo: IProductRepository,
                 payment_service: IPaymentService):
        self._order_repo = order_repo
        self._user_repo = user_repo
        self._product_repo = product_repo
        self._payment_service = payment_service

    def create_order(self, user_id: int, items: List[OrderItem]) -> Order:
        """Create order with transaction"""
        return self._order_repo.transactional(lambda:
            self._create_order_internal(user_id, items)
        )

    def _create_order_internal(self, user_id: int, items: List[OrderItem]) -> Order:
        # Create order
        order = Order(user_id=user_id, status='pending')

        # Calculate total
        total = Decimal('0.00')
        for item in items:
            product = self._product_repo.find_by_id(item.product_id)
            if not product:
                raise ProductNotFoundError(item.product_id)

            if product.stock < item.quantity:
                raise InsufficientStockError(product.name)

            # Update stock
            product.stock -= item.quantity
            self._product_repo.save(product)

            # Add order item
            order.add_item(product, item.quantity)
            total += product.price * item.quantity

        order.total_amount = total

        # Process payment
        payment_result = self._payment_service.process_payment(
            order.total_amount,
            self._user_repo.find_by_id(user_id).payment_method
        )

        if not payment_result.success:
            raise PaymentFailedError(payment_result.error_message)

        order.status = 'processing'
        order.payment_id = payment_result.payment_id

        return self._order_repo.save(order)
```

### Step 7: Caching Strategy

#### Cache Design

```python
from abc import ABC, abstractmethod
from typing import Optional, TypeVar, Generic

T = TypeVar('T')

class ICache(Generic[T], ABC):
    """Cache interface"""

    @abstractmethod
    def get(self, key: str) -> Optional[T]:
        pass

    @abstractmethod
    def set(self, key: str, value: T, ttl: int = 3600):
        pass

    @abstractmethod
    def delete(self, key: str):
        pass

    @abstractmethod
    def clear(self):
        pass

class CachedUserService(IUserService):
    """User service with caching"""

    def __init__(self, user_service: IUserService, cache: ICache[User]):
        self._user_service = user_service
        self._cache = cache

    def get_user(self, user_id: int) -> Optional[User]:
        cache_key = f"user:{user_id}"

        # Try cache first
        user = self._cache.get(cache_key)
        if user:
            return user

        # Cache miss - fetch from service
        user = self._user_service.get_user(user_id)
        if user:
            self._cache.set(cache_key, user, ttl=300)  # 5 minutes

        return user

    def update_user(self, user_id: int, **kwargs) -> User:
        user = self._user_service.update_user(user_id, **kwargs)

        # Invalidate cache
        self._cache.delete(f"user:{user_id}")

        return user
```

### Step 8: Logging & Monitoring

#### Logging Strategy

```python
import logging
from typing import Dict, Any

class StructuredLogger:
    """Structured logger"""

    def __init__(self, name: str):
        self._logger = logging.getLogger(name)

    def log(self, level: str, message: str, **kwargs):
        """Log structured message"""
        log_data = {
            'message': message,
            'timestamp': datetime.utcnow().isoformat(),
            **kwargs
        }
        getattr(self._logger, level)(json.dumps(log_data))

    def info(self, message: str, **kwargs):
        self.log('info', message, **kwargs)

    def error(self, message: str, **kwargs):
        self.log('error', message, **kwargs)

    def warning(self, message: str, **kwargs):
        self.log('warning', message, **kwargs)

# Usage
logger = StructuredLogger('UserService')

def create_user(self, username: str, email: str):
    logger.info("Creating user", username=username, email=email)
    try:
        user = self._create_user_internal(username, email)
        logger.info("User created successfully", user_id=user.id)
        return user
    except Exception as e:
        logger.error("Failed to create user",
                    username=username,
                    error=str(e),
                    error_type=type(e).__name__)
        raise
```

#### Metrics

```python
from prometheus_client import Counter, Histogram, Gauge

# Define metrics
user_created_total = Counter(
    'user_created_total',
    'Total number of users created'
)

user_creation_duration = Histogram(
    'user_creation_duration_seconds',
    'Time spent creating users'
)

active_users_total = Gauge(
    'active_users_total',
    'Number of active users'
)

class MonitoredUserService(IUserService):
    """User service with monitoring"""

    def __init__(self, user_service: IUserService):
        self._user_service = user_service

    @user_creation_duration.time()
    def create_user(self, username: str, email: str, password: str) -> User:
        try:
            user = self._user_service.create_user(username, email, password)
            user_created_total.inc()
            active_users_total.inc()
            return user
        except Exception:
            raise
```

### Step 9: Security Implementation

#### Authentication

```python
from abc import ABC, abstractmethod
from typing import Optional

class IAuthenticationService(ABC):
    """Authentication service interface"""

    @abstractmethod
    def authenticate(self, username: str, password: str) -> Optional[str]:
        """Authenticate and return token"""
        pass

    @abstractmethod
    def verify_token(self, token: str) -> Optional[User]:
        """Verify token and return user"""
        pass

class JWTAuthenticationService(IAuthenticationService):
    """JWT authentication implementation"""

    SECRET_KEY = os.getenv('JWT_SECRET_KEY')
    ALGORITHM = 'HS256'

    def __init__(self, user_repo: IUserRepository):
        self._user_repo = user_repo

    def authenticate(self, username: str, password: str) -> Optional[str]:
        user = self._user_repo.find_by_username(username)
        if not user:
            return None

        if not self._verify_password(password, user.password_hash):
            return None

        return self._create_token(user)

    def verify_token(self, token: str) -> Optional[User]:
        try:
            payload = jwt.decode(
                token,
                self.SECRET_KEY,
                algorithms=[self.ALGORITHM]
            )
            user_id = payload.get('sub')
            return self._user_repo.find_by_id(user_id)
        except JWTError:
            return None
```

#### Authorization

```python
from enum import Enum
from functools import wraps

class Permission(Enum):
    READ_USER = 'read_user'
    WRITE_USER = 'write_user'
    DELETE_USER = 'delete_user'
    READ_ORDER = 'read_order'
    WRITE_ORDER = 'write_order'

def require_permission(permission: Permission):
    """Decorator to require permission"""
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            user = get_current_user()
            if not user.has_permission(permission):
                raise ForbiddenError(
                    f"Permission {permission.value} required"
                )
            return func(*args, **kwargs)
        return wrapper
    return decorator

# Usage
@require_permission(Permission.READ_USER)
def get_user(self, user_id: int) -> Optional[User]:
    return self._user_repo.find_by_id(user_id)
```

### Step 10: Testing Strategy

#### Unit Test Design

```python
import pytest
from unittest.mock import Mock, patch

class TestUserService:
    """User service tests"""

    @pytest.fixture
    def user_service(self):
        mock_repo = Mock(spec=IUserRepository)
        mock_hasher = Mock(spec=IPasswordHasher)
        mock_email = Mock(spec=IEmailService)
        return UserService(mock_repo, mock_hasher, mock_email)

    def test_create_user_success(self, user_service):
        """Test successful user creation"""
        # Arrange
        username = "testuser"
        email = "test@example.com"
        password = "SecurePass123!"

        user_service._user_repo.exists_by_username.return_value = False
        user_service._user_repo.exists_by_email.return_value = False
        user_service._password_hasher.hash.return_value = "hashed"
        user_service._user_repo.save.return_value = User(
            id=1, username=username, email=email
        )

        # Act
        user = user_service.create_user(username, email, password)

        # Assert
        assert user.username == username
        assert user.email == email
        user_service._user_repo.save.assert_called_once()
        user_service._email_service.send_welcome_email.assert_called_once_with(email)

    def test_create_user_duplicate_username(self, user_service):
        """Test user creation with duplicate username"""
        # Arrange
        user_service._user_repo.exists_by_username.return_value = True

        # Act & Assert
        with pytest.raises(UserAlreadyExistsError):
            user_service.create_user("existing", "test@example.com", "pass")
```

#### Integration Test Design

```python
@pytest.mark.integration
class TestUserAPI:
    """User API integration tests"""

    @pytest.fixture
    def client(self):
        return TestClient(app)

    @pytest.fixture
    def db_session(self):
        # Create test database
        session = TestSession()
        yield session
        session.close()

    def test_create_user_endpoint(self, client, db_session):
        """Test user creation endpoint"""
        response = client.post('/api/users', json={
            'username': 'testuser',
            'email': 'test@example.com',
            'password': 'SecurePass123!'
        })

        assert response.status_code == 201
        data = response.json()
        assert data['username'] == 'testuser'
        assert data['email'] == 'test@example.com'
        assert 'id' in data
```

### Outputs

- API specification (OpenAPI/Swagger)
- Database schema (SQL scripts)
- Data models (ER diagrams)
- Class/component diagrams
- Interface definitions
- Validation rules
- Error handling specification
- Caching strategy
- Security implementation
- Test specifications

### Detailed Design Checklist

- [ ] All APIs defined with contracts
- [ ] Database schema finalized
- [ ] Data models documented
- [ ] Class interfaces defined
- [ ] Validation rules specified
- [ ] Error handling designed
- [ ] Authentication/authorization designed
- [ ] Caching strategy defined
- [ ] Logging strategy defined
- [ ] Transaction boundaries defined
- [ ] Test cases designed
- [ ] Performance considerations addressed
- [ ] Security measures specified

### Next Steps

After detailed design approval:
1. Implement interfaces
2. Create database migrations
3. Implement services
4. Write unit tests
5. Write integration tests
6. Code review

---

## Code Organization Patterns

### Layer Organization

```
src/
├── api/                    # API layer
│   ├── controllers/        # Request handlers
│   ├── middleware/         # Middleware
│   ├── routes/            # Route definitions
│   └── validators/        # Request validation
├── services/              # Business logic
│   ├── user_service.py
│   ├── order_service.py
│   └── payment_service.py
├── repositories/          # Data access
│   ├── user_repository.py
│   └── order_repository.py
├── models/                # Domain models
│   ├── user.py
│   └── order.py
├── schemas/               # DTOs/Request-Response
│   ├── user.py
│   └── order.py
├── utils/                 # Utilities
│   ├── validators.py
│   ├── decorators.py
│   └── helpers.py
└── config/               # Configuration
    └── settings.py
```

### Domain-Driven Design Organization

```
src/
├── domains/
│   ├── user/
│   │   ├── entities/      # Domain entities
│   │   ├── value_objects/ # Value objects
│   │   ├── services/      # Domain services
│   │   ├── repositories/  # Repository interfaces
│   │   └── events/        # Domain events
│   └── order/
│       ├── entities/
│       ├── value_objects/
│       ├── services/
│       ├── repositories/
│       └── events/
├── application/           # Application services
│   ├── commands/         # Command handlers
│   ├── queries/          # Query handlers
│   └── services/         # Application services
├── infrastructure/        # External concerns
│   ├── persistence/      # Database implementations
│   ├── messaging/        # Message queue
│   ├── cache/            # Cache implementations
│   └── logging/          # Logging
└── interfaces/           # Interface adapters
    ├── api/              # Controllers
    ├── cli/              # CLI commands
    └── grpc/             # gRPC services
```
