---
description: Use this skill when creating detailed technical specifications including API contracts, data schemas, class structures, algorithm specifications, interface definitions, and implementation-ready blueprints.
---

# Detailed Design Skill

## Purpose

Create comprehensive, implementation-ready technical specifications that define APIs, data models, component interfaces, algorithms, and all details needed for development.

## When to Use This Skill

Activate this skill when:
- Architecture needs detailed specifications
- Creating API contracts
- Designing data models
- Defining component interfaces
- Specifying algorithms
- Creating implementation blueprints
- Documenting technical decisions

## Core Competencies

### 1. API Specification

**RESTful APIs**:
For each endpoint specify:
- HTTP method and path
- Request format (headers, query, body)
- Response format (success, errors)
- Authentication/authorization
- Validation rules
- Rate limiting
- Error codes

**Example**:
```markdown
### POST /api/orders

**Description**: Create a new order

**Authentication**: Bearer token required

**Request**:
- Headers:
  - Authorization: Bearer {token}
  - Content-Type: application/json
- Body:
  {
    "user_id": "integer",
    "items": [
      {
        "product_id": "integer",
        "quantity": "integer",
        "price": "decimal"
      }
    ]
  }

**Validation**:
- user_id: required, exists in users table
- items: required, min 1 item
- items[*].quantity: required, min 1

**Response**:
- Success (201):
  {
    "id": "integer",
    "total": "decimal",
    "status": "string",
    "created_at": "datetime"
  }
- Error (400):
  {
    "error": {
      "code": "VALIDATION_ERROR",
      "message": "Invalid input",
      "details": {...}
    }
  }

**Business Logic**:
1. Validate user exists
2. Validate products exist
3. Calculate total
4. Create order
5. Publish order.created event
```

### 2. Data Model Design

**Database Tables**:
```markdown
### orders

**Purpose**: Store customer orders

**Columns**:
| Column | Type | Nullable | Default | Description |
|--------|------|----------|---------|-------------|
| id | BIGINT | NO | AUTO | Primary key |
| user_id | BIGINT | NO | | Foreign key to users |
| total | DECIMAL(10,2) | NO | 0.00 | Order total |
| status | VARCHAR(50) | NO | 'pending' | Order status |
| created_at | TIMESTAMP | NO | NOW() | Creation time |
| updated_at | TIMESTAMP | NO | NOW() | Update time |

**Indexes**:
- PRIMARY (id)
- INDEX idx_user_id (user_id)
- INDEX idx_status (status)
- INDEX idx_created_at (created_at)

**Constraints**:
- FOREIGN KEY (user_id) → users(id)
- CHECK (total >= 0)
- CHECK (status IN ('pending', 'paid', 'shipped', 'delivered'))

**Triggers**:
- BEFORE INSERT: Set created_at
- BEFORE UPDATE: Set updated_at
```

**NoSQL Collections**:
```markdown
### orders

**Document Structure**:
{
  "_id": ObjectId,
  "user_id": ObjectId,
  "items": [{
    "product_id": ObjectId,
    "quantity": NumberInt,
    "price": NumberDecimal
  }],
  "total": NumberDecimal,
  "status": String,
  "created_at": Date,
  "updated_at": Date
}

**Indexes**:
- {user_id: 1}
- {status: 1, created_at: -1}
- {created_at: -1}

**Validation Rules**:
{
  "$jsonSchema": {
    "bsonType": "object",
    "required": ["user_id", "items", "total"],
    "properties": {
      "user_id": {"bsonType": "objectId"},
      "total": {"bsonType": "decimal", "minimum": 0},
      "status": {
        "bsonType": "string",
        "enum": ["pending", "paid", "shipped", "delivered"]
      }
    }
  }
}
```

### 3. Component Design

```markdown
### OrderService

**Responsibility**: Business logic for order management

**Public Interface**:
- `create_order(user_id: int, items: List[Item]) -> Order`
- `get_order(order_id: int) -> Order`
- `update_status(order_id: int, status: str) -> Order`
- `cancel_order(order_id: int) -> bool`

**Dependencies**:
- OrderRepository - persistence
- InventoryService - check availability
- PaymentService - process payment
- EventPublisher - publish events

**Configuration**:
- `tax_rate`: decimal (default: 0.10)
- `currency`: string (default: "USD")

**Error Handling**:
- ValidationError: Invalid input
- NotFoundError: Order not found
- BusinessError: Business rule violation

**State Machine**:
```
[pending] --pay--> [paid]
[paid] --ship--> [shipped]
[shipped] --deliver--> [delivered]
[pending] --cancel--> [cancelled]
```
```

### 4. Algorithm Specification

```markdown
### Calculate Order Total

**Purpose**: Calculate total price including tax

**Inputs**:
- `items`: List[Item] - Order items
- `tax_rate`: Decimal - Tax rate (default: 0.10)

**Output**:
- `Decimal`: Total amount

**Algorithm**:
1. Validate items not empty
2. Subtotal = sum(item.price * item.quantity for item in items)
3. Tax = Subtotal * tax_rate
4. Total = Subtotal + Tax
5. Return Total

**Complexity**:
- Time: O(n) where n = number of items
- Space: O(1)

**Edge Cases**:
- Empty items: ValidationError
- Negative price: ValidationError
- Zero quantity: Treat as 0

**Example**:
```
Input: [{price: 10, quantity: 2}, {price: 5, quantity: 1}]
Subtotal = 10*2 + 5*1 = 25
Tax = 25 * 0.10 = 2.50
Total = 25 + 2.50 = 27.50
```
```

## Design Document Structure

```markdown
# Detailed Design: [Feature/Component]

## Overview
[Brief description of what's being designed]

## API Specifications
[All endpoints with full details]

## Data Models
[All tables, collections, schemas]

## Component Specifications
[All components with interfaces]

## Algorithms
[Complex algorithms with pseudocode]

## State Machines
[Any state-dependent behavior]

## Error Handling
[Error codes, handling strategies]

## Security
[Authentication, authorization, validation]

## Performance
[Caching, optimization, constraints]

## Testing Strategy
[What to test and how]

## Deployment
[Configuration, environment variables]
```

## Best Practices

### DO:
- Specify everything needed for implementation
- Use standard formats (OpenAPI, JSON Schema)
- Include examples
- Consider edge cases
- Define error handling
- Specify non-functional requirements
- Make it implementation-ready

### DON'T:
- Leave anything ambiguous
- Skip error handling
- Forget edge cases
- Ignore performance
- Omit security considerations
- Be too vague

## Quality Checklist

- [ ] All APIs fully specified
- [ ] Data models complete
- [ ] Component interfaces defined
- [ ] Algorithms specified
- [ ] Error handling defined
- [ ] Security measures specified
- [ ] Performance considerations noted
- [ ] Testing strategy outlined
- [ ] Implementation can start immediately
- [ ] No ambiguities remain

## Related Skills

- **Architecture Design**: Input for detailed design
- **Code Development**: Implement the design
- **Requirements Analysis**: Understand requirements
