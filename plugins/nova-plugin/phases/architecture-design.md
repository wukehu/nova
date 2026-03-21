# Architecture Design Phase Template
# 架构设计阶段模板

## Phase: Architecture Design

### Objective
Create comprehensive system architecture for {{project_name}} based on requirements analysis.

### Context
- **Project**: {{project_name}}
- **Requirements**: {{requirements_document}}
- **Language**: {{language}}
- **Framework**: {{framework}}
- **Constraints**: {{constraints}}
- **Team Size**: {{team_size}}

---

## Software Design Principles Reference

### SOLID Principles

{{#solid}}
**S - Single Responsibility Principle (单一职责原则)**
- A class/module should have one reason to change
- Each component should have one responsibility
- Focus on doing one thing well

**O - Open/Closed Principle (开闭原则)**
- Software entities should be open for extension, closed for modification
- Use abstraction and polymorphism
- Plugin architecture

**L - Liskov Substitution Principle (里氏替换原则)**
- Subtypes must be substitutable for base types
- Derived classes must honor base class contracts
- Don't violate base class invariants

**I - Interface Segregation Principle (接口隔离原则)**
- Clients shouldn't depend on interfaces they don't use
- Prefer many small interfaces over large ones
- Role-based interfaces

**D - Dependency Inversion Principle (依赖倒置原则)**
- Depend on abstractions, not concretions
- High-level modules shouldn't depend on low-level modules
- Both should depend on abstractions
{{/solid}}

### Core Principles

**DRY (Don't Repeat Yourself)**
- Avoid duplication
- Extract common logic
- Reuse through abstraction

**KISS (Keep It Simple, Stupid)**
- Simple solutions are better
- Avoid over-engineering
- Premature optimization is evil

**YAGNI (You Aren't Gonna Need It)**
- Don't build what you don't need yet
- Build for current requirements
- Avoid speculative development

**Separation of Concerns**
- Divide system into distinct components
- Each component addresses a separate concern
- Clear boundaries between layers

**Law of Demeter (Principle of Least Knowledge)**
- Objects should only talk to immediate friends
- Minimize coupling
- Don't chain method calls

### Architecture Principles

**High Cohesion, Low Coupling**
- Group related functionality
- Minimize dependencies between modules
- Clear interfaces

**Layered Architecture**
- Presentation layer (UI/API)
- Business logic layer (Domain)
- Data access layer (Persistence)
- Clear dependencies between layers

**Domain-Driven Design (DDD)**
- Focus on domain logic
- Ubiquitous language
- Bounded contexts
- Aggregates and entities

---

## Architecture Design Process

### Step 1: Understand Requirements

{{#requirements_analysis}}
Based on requirements analysis:
- **Functional Requirements**: {{functional_requirements}}
- **Non-Functional Requirements**: {{non_functional_requirements}}
- **Constraints**: {{constraints}}
- **User Stories**: {{user_stories}}
{{/requirements_analysis}}

### Step 2: Choose Architectural Style

#### Common Architectural Patterns

**1. Layered Architecture (分层架构)**
```
┌─────────────────────────────────┐
│   Presentation Layer            │  UI, API
├─────────────────────────────────┤
│   Business Logic Layer          │  Domain Logic
├─────────────────────────────────┤
│   Data Access Layer             │  Database, External APIs
└─────────────────────────────────┘
```
**Use when**: Standard business applications
**Pros**: Simple, easy to understand
**Cons**: Can become rigid, tight coupling

**2. Microservices Architecture (微服务架构)**
```
┌─────────┐  ┌─────────┐  ┌─────────┐
│ Service │  │ Service │  │ Service │
│    A    │  │    B    │  │    C    │
└────┬────┘  └────┬────┘  └────┬────┘
     │            │            │
     └────────────┴────────────┘
                 │
          ┌──────┴──────┐
          │ API Gateway │
          └─────────────┘
```
**Use when**: Complex systems, multiple teams
**Pros**: Scalable, fault isolated, polyglot
**Cons**: Distributed complexity, data consistency

**3. Event-Driven Architecture (事件驱动架构)**
```
Producer → Event Bus → Consumer
```
**Use when**: Async processing, loose coupling
**Pros**: Scalable, decoupled, async
**Cons**: Eventual consistency, debugging complexity

**4. Hexagonal Architecture (六边形架构)**
```
     ┌──────────────────┐
     │   Application    │
     │      Core        │
     └────────┬─────────┘
              │
      ┌───────┴───────┐
      ↓               ↓
┌──────────┐   ┌──────────┐
│  Primary  │   │Secondary │
│  Ports    │   │  Ports   │
└──────────┘   └──────────┘
```
**Use when**: Complex business logic, testability
**Pros**: Testable, flexible core
**Cons**: More complex, learning curve

**5. CQRS (Command Query Responsibility Segregation)**
```
Command → Command Handler → Write Model
Query   → Query Handler    → Read Model
```
**Use when**: Complex read/write patterns, high scalability
**Pros**: Optimized for each operation, scalable
**Cons**: Complexity, eventual consistency

### Step 3: Design System Components

#### Component Identification

**Identify core components:**

1. **API Layer**
   - REST/GraphQL endpoints
   - Authentication/Authorization
   - Request validation
   - Response formatting

2. **Business Logic Layer**
   - Domain services
   - Business rules
   - Workflows
   - Validation

3. **Data Access Layer**
   - Repositories
   - ORM/Query builders
   - Caching
   - Transactions

4. **External Integrations**
   - Third-party APIs
   - Message queues
   - File storage
   - Email/SMS services

#### Component Design Principles

**Interface-Based Design:**
```python
# Define interfaces
class IUserRepository(ABC):
    @abstractmethod
    def find_by_id(self, user_id: int) -> Optional[User]:
        pass

    @abstractmethod
    def save(self, user: User) -> User:
        pass

# Implement interfaces
class SqlUserRepository(IUserRepository):
    def find_by_id(self, user_id: int) -> Optional[User]:
        # SQL implementation
        pass

class InMemoryUserRepository(IUserRepository):
    def find_by_id(self, user_id: int) -> Optional[User]:
        # In-memory implementation
        pass
```

**Dependency Injection:**
```python
# Inject dependencies
class UserService:
    def __init__(self, user_repo: IUserRepository):
        self._user_repo = user_repo

    def get_user(self, user_id: int) -> Optional[User]:
        return self._user_repo.find_by_id(user_id)
```

### Step 4: Data Architecture

#### Database Design

**1. Relational Database (PostgreSQL, MySQL)**
```
Users Table:
┌────────┬─────────┬──────────┬─────────┐
│ id     │ username│ email    │ created │
├────────┼─────────┼──────────┼─────────┤
│ PK     │ UNIQUE  │ UNIQUE   │ INDEX   │
└────────┴─────────┴──────────┴─────────┘

Orders Table:
┌────────┬──────────┬─────────────┬──────────┐
│ id     │ user_id  │ total       │ status   │
├────────┼──────────┼─────────────┼──────────┤
│ PK     │ FK       │ DECIMAL(10,2)│ ENUM  │
└────────┴──────────┴─────────────┴──────────┘
```
**Use when**: Structured data, relationships, ACID

**2. Document Database (MongoDB)**
```javascript
// User document
{
  _id: ObjectId("..."),
  username: "john",
  email: "john@example.com",
  profile: {
    firstName: "John",
    lastName: "Doe"
  },
  preferences: {
    theme: "dark",
    language: "en"
  },
  createdAt: ISODate("2026-03-21")
}
```
**Use when**: Flexible schema, document-oriented

**3. Key-Value Database (Redis)**
```
user:123 → JSON data
session:abc → session data
cache:users → cached list
```
**Use when**: Caching, sessions, fast lookups

#### Data Flow

**Request Flow:**
```
Client Request
    ↓
API Gateway
    ↓
Authentication
    ↓
Rate Limiting
    ↓
Controller
    ↓
Service Layer
    ↓
Repository Layer
    ↓
Database
    ↓
Response
```

### Step 5: Technology Stack

{{#language}}
**{{language}} Stack:**

{{#python}}
- **Language**: Python {{python_version}}
- **Framework**: {{framework}}
- **API**: REST/GraphQL
- **Database**: {{database}}
- **Cache**: Redis
- **Message Queue**: RabbitMQ/Redis
- **Task Queue**: Celery
- **Testing**: pytest, pytest-cov
{{/python}}

{{#javascript}}
- **Language**: JavaScript/TypeScript (Node.js {{node_version}})
- **Framework**: {{framework}}
- **API**: REST/GraphQL
- **Database**: {{database}}
- **Cache**: Redis
- **Message Queue**: RabbitMQ/NATS
- **Task Queue**: Bull/BullMQ
- **Testing**: vitest, playwright
{{/javascript}}

{{#java}}
- **Language**: Java {{java_version}}
- **Framework**: {{framework}}
- **API**: REST/GraphQL
- **Database**: {{database}}
- **Cache**: Redis
- **Message Queue**: RabbitMQ/Kafka
- **Testing**: JUnit 5, Mockito
{{/java}}

{{#go}}
- **Language**: Go {{go_version}}
- **Framework**: {{framework}}
- **API**: REST/gRPC
- **Database**: {{database}}
- **Cache**: Redis
- **Message Queue**: NATS/RabbitMQ
- **Testing**: testing, testify
{{/go}}

{{#cpp}}
- **Language**: C++ {{cpp_version}}
- **Framework**: {{framework}}
- **API**: REST/HTTP
- **Database**: {{database}}
- **Cache**: Redis
- **Testing**: Google Test
{{/cpp}}

{{#rust}}
- **Language**: Rust {{rust_version}}
- **Framework**: {{framework}}
- **API**: REST/gRPC
- **Database**: {{database}}
- **Cache**: Redis
- **Async Runtime**: Tokio
- **Testing**: Built-in, Criterion
{{/rust}}
{{/language}}

### Step 6: Non-Functional Architecture

#### Scalability

**Horizontal Scaling:**
- Load balancer
- Multiple instances
- Database read replicas
- Caching layer
- CDN for static content

**Vertical Scaling:**
- Larger servers
- Database optimization
- Connection pooling

#### Performance

**Optimization Strategies:**
- Database indexing
- Query optimization
- Caching (Redis, CDN)
- Compression (gzip, brotli)
- Async processing
- Connection pooling

#### Security

**Security Layers:**
1. **Network Security**
   - HTTPS/TLS
   - Firewalls
   - DDoS protection

2. **Application Security**
   - Authentication (JWT, OAuth2)
   - Authorization (RBAC, ABAC)
   - Input validation
   - Output encoding

3. **Data Security**
   - Encryption at rest
   - Encryption in transit
   - Secure key management
   - Data masking

#### Reliability

**High Availability:**
- Redundancy
- Failover
- Health checks
- Circuit breakers
- Retry logic
- Rate limiting

**Disaster Recovery:**
- Backups
- Replication
- Multi-region deployment
- Disaster recovery plan

### Step 7: Architecture Decision Records (ADR)

#### ADR Template

```markdown
# ADR-001: Choose {{framework}} as Web Framework

## Status
Accepted

## Context
{{project_name}} needs a web framework for building REST APIs.

## Decision
Use {{framework}} because:
- Team expertise
- Performance requirements
- Community support
- Required features

## Consequences
- **Positive**: Fast development, good documentation
- **Negative**: Learning curve for team
- **Neutral**: Requires {{language}} {{version}}
```

### Step 8: Architecture Diagrams

#### System Architecture Diagram

```
┌─────────────────────────────────────────────────────────┐
│                        Client                           │
│                    (Web, Mobile, CLI)                   │
└────────────────────────┬────────────────────────────────┘
                         │ HTTPS
                         ↓
┌─────────────────────────────────────────────────────────┐
│                      CDN / Load Balancer                │
└────────────────────────┬────────────────────────────────┘
                         │
        ┌────────────────┼────────────────┐
        ↓                ↓                ↓
┌──────────────┐  ┌──────────────┐  ┌──────────────┐
│  Instance 1  │  │  Instance 2  │  │  Instance 3  │
│  (API App)   │  │  (API App)   │  │  (API App)   │
└──────┬───────┘  └──────┬───────┘  └──────┬───────┘
       │                 │                 │
       └─────────────────┼─────────────────┘
                         │
        ┌────────────────┼────────────────┐
        ↓                ↓                ↓
┌──────────────┐  ┌──────────────┐  ┌──────────────┐
│   Master DB  │  │  Replica 1   │  │  Replica 2   │
│  (Primary)   │  │   (Read)     │  │   (Read)     │
└──────────────┘  └──────────────┘  └──────────────┘
       │
       ↓
┌──────────────┐
│    Redis     │
│    (Cache)   │
└──────────────┘
```

#### Component Diagram

```
┌──────────────────────────────────────────────────────┐
│                   API Gateway                        │
│  - Auth & Authz                                      │
│  - Rate Limiting                                     │
│  - Request Routing                                   │
└──────────────────────┬───────────────────────────────┘
                       ↓
┌──────────────────────────────────────────────────────┐
│                    Controllers                       │
│  - Request/Response Handling                        │
│  - Validation                                       │
└──────────────────────┬───────────────────────────────┘
                       ↓
┌──────────────────────────────────────────────────────┐
│                    Services                          │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐         │
│  │ UserService│ │OrderService│ │PaymentSvc│         │
│  └──────────┘  └──────────┘  └──────────┘         │
└──────────────────────┬───────────────────────────────┘
                       ↓
┌──────────────────────────────────────────────────────┐
│                   Repositories                        │
│  ┌──────────────┐  ┌──────────────┐                 │
│  │UserRepository│ │OrderRepository│                 │
│  └──────────────┘  └──────────────┘                 │
└──────────────────────┬───────────────────────────────┘
                       ↓
┌──────────────────────────────────────────────────────┐
│                      Database                         │
└──────────────────────────────────────────────────────┘
```

### Step 9: Deployment Architecture

#### Container-Based Deployment

```
┌─────────────────────────────────────────┐
│           Kubernetes Cluster            │
│                                         │
│  ┌─────────────────────────────────┐   │
│  │         Namespace: app           │   │
│  │                                 │   │
│  │  ┌─────────┐  ┌─────────┐      │   │
│  │  │  Pod 1  │  │  Pod 2  │      │   │
│  │  │  (API)   │  │  (API)   │      │   │
│  │  └────┬────┘  └────┬────┘      │   │
│  │       │            │            │   │
│  │       └────────────┘            │   │
│  │            ↓                   │   │
│  │  ┌──────────────────────┐      │   │
│  │  │      Service          │      │   │
│  │  └──────────────────────┘      │   │
│  │            ↓                   │   │
│  │  ┌──────────────────────┐      │   │
│  │  │    Ingress/Route     │      │   │
│  │  └──────────────────────┘      │   │
│  └─────────────────────────────────┘   │
│                                         │
│  ┌─────────────────────────────────┐   │
│  │    Namespace: database          │   │
│  │                                 │   │
│  │  ┌─────────┐  ┌─────────┐      │   │
│  │  │  Pod DB │  │Pod Redis│      │   │
│  │  └─────────┘  └─────────┘      │   │
│  └─────────────────────────────────┘   │
└─────────────────────────────────────────┘
```

### Outputs

- Architecture document
- Component diagrams
- Data flow diagrams
- Deployment diagrams
- Technology stack decisions
- ADRs (Architecture Decision Records)
- Non-functional requirements matrix

### Architecture Review Checklist

- [ ] All requirements addressed
- [ ] Architectural style chosen and justified
- [ ] Components identified and defined
- [ ] Data model designed
- [ ] APIs defined
- [ ] Security considered
- [ ] Performance requirements met
- [ ] Scalability addressed
- [ ] Reliability ensured
- [ ] Deployment strategy defined
- [ ] Diagrams created
- [ ] ADRs documented
- [ ] Team agreement on architecture

### Next Steps

After architecture approval:
1. Create detailed design documents
2. Set up development environment
3. Implement proof of concept if needed
4. Begin implementation

---

## Design Patterns Reference

### Creational Patterns (创建型模式)

**1. Singleton (单例模式)**
- Ensure only one instance exists
- Use for: Database connections, Logger, Config

**2. Factory Method (工厂方法模式)**
- Create objects without specifying exact class
- Use for: Framework integration, plugin systems

**3. Builder (建造者模式)**
- Construct complex objects step by step
- Use for: Complex object construction

### Structural Patterns (结构型模式)

**1. Adapter (适配器模式)**
- Convert interface of a class into another
- Use for: Third-party integrations

**2. Decorator (装饰器模式)**
- Add behavior dynamically
- Use for: Logging, caching, validation

**3. Facade (外观模式)**
- Provide simple interface to complex system
- Use for: API simplification

### Behavioral Patterns (行为型模式)

**1. Strategy (策略模式)**
- Define family of algorithms, encapsulate each
- Use for: Validation rules, sorting, payment methods

**2. Observer (观察者模式)**
- One-to-many dependency
- Use for: Event handling, notifications

**3. Command (命令模式)**
- Encapsulate request as object
- Use for: Undo/redo, task queues

---

## Anti-Patterns to Avoid

**1. God Object**
- One class does everything
- **Solution**: Split responsibilities

**2. Golden Hammer**
- Use same solution for every problem
- **Solution**: Choose right tool for job

**3. Boat Anchor**
- Useless parts of code
- **Solution**: Remove unused code

**4. Lava Flow**
- Dead code in branches
- **Solution**: Delete dead branches

**5. Spaghetti Code**
- Tangled control flow
- **Solution**: Refactor, use clear structure
