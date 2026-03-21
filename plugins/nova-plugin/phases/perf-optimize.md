# Performance Optimization Phase Template
# 性能优化阶段模板

## Phase: Performance Optimization

### Objective
Implement performance optimizations for {{project_name}} based on analysis findings.

### Context
- **Project**: {{project_name}}
- **Language**: {{language}}
- **Analysis Report**: {{analysis_report}}
- **Baseline Metrics**: {{baseline_metrics}}
- **Target Metrics**: {{target_metrics}}

### Optimization Strategy

#### 1. Quick Wins (High Impact, Low Effort)

##### Database Optimizations

{{#database}}
**Add Missing Indexes:**
```sql
-- Index for email lookups
CREATE INDEX idx_users_email ON users(email);

-- Composite index for common queries
CREATE INDEX idx_orders_user_created ON orders(user_id, created_at);

-- Covering index
CREATE INDEX idx_products_category_active
ON products(category, status) INCLUDE (name, price);
```

**Optimize Queries:**
```sql
-- Before: N+1 query problem
SELECT * FROM orders WHERE user_id = 1;
SELECT * FROM items WHERE order_id = 1;
SELECT * FROM items WHERE order_id = 2;
...

-- After: Single query with JOIN
SELECT o.*, i.*
FROM orders o
LEFT JOIN items i ON i.order_id = o.id
WHERE o.user_id = 1;

-- Or use eager loading
{{#python}}
# SQLAlchemy
orders = session.query(Order)\
    .options(joinedload(Order.items))\
    .filter_by(user_id=user_id)\
    .all()
{{/python}}
```

**Connection Pooling:**
{{#python}}
```python
from sqlalchemy.pool import QueuePool

engine = create_engine(
    DATABASE_URL,
    poolclass=QueuePool,
    pool_size=20,        # Increased from 5
    max_overflow=40,     # Increased from 10
    pool_pre_ping=True,  # Verify connections
    pool_recycle=3600    # Recycle after 1 hour
)
```
{{/python}}

{{#javascript}}
```javascript
const pool = mysql.createPool({
  connectionLimit: 20,   // Increased from 5
  queueLimit: 0,
  waitForConnections: true
});
```
{{/javascript}}
{{/database}}

##### Caching Layer

{{#redis}}
**Implement Redis Caching:**
{{#python}}
```python
import redis
from functools import lru_cache
import json

redis_client = redis.Redis(host='localhost', port=6379, db=0)

def cache_result(key, ttl=3600):
    def decorator(func):
        def wrapper(*args, **kwargs):
            cache_key = f"{key}:{args}:{kwargs}"
            cached = redis_client.get(cache_key)
            if cached:
                return json.loads(cached)
            result = func(*args, **kwargs)
            redis_client.setex(
                cache_key,
                ttl,
                json.dumps(result)
            )
            return result
        return wrapper
    return decorator

@cache_result("user:get", ttl=300)  # 5 minutes
def get_user(user_id):
    return db.query(User).filter_by(id=user_id).first()
```
{{/python}}

{{#javascript}}
```javascript
const Redis = require('ioredis');
const redis = new Redis();

async function cacheResult(key, fn, ttl = 3600) {
  const cached = await redis.get(key);
  if (cached) {
    return JSON.parse(cached);
  }
  const result = await fn();
  await redis.setex(key, ttl, JSON.stringify(result));
  return result;
}

async function getUser(userId) {
  return cacheResult(`user:${userId}`, async () => {
    return await db.query(
      'SELECT * FROM users WHERE id = ?',
      [userId]
    );
  }, 300);  // 5 minutes
}
```
{{/javascript}}
{{/redis}}

**Cache Invalidation Strategy:**
- Time-based expiration (TTL)
- Event-based invalidation
- Cache tagging for bulk invalidation
- Write-through vs write-back

##### Response Compression

{{#web_server}}
**Enable Compression:**
{{#python}}
```python
from gzip_middleware import GZipMiddleware

app = GZipMiddleware(app, min_size=1000)

# Or with FastAPI
from fastapi.middleware.gzip import GZipMiddleware

app.add_middleware(GZipMiddleware, minimum_size=1000)
```
{{/python}}

{{#nginx}}
```nginx
# nginx.conf
gzip on;
gzip_vary on;
gzip_proxied any;
gzip_comp_level 6;
gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;
gzip_min_length 1000;
```
{{/nginx}}
{{/web_server}}

#### 2. Medium-Term Optimizations

##### API Optimization

**Implement Pagination:**
{{#python}}
```python
from fastapi import Query
from typing import List

@app.get("/users")
async def list_users(
    page: int = Query(1, ge=1),
    size: int = Query(20, ge=1, le=100)
):
    offset = (page - 1) * size
    users = db.query(User)\
        .offset(offset)\
        .limit(size)\
        .all()
    return {
        "data": users,
        "page": page,
        "size": size,
        "total": db.query(User).count()
    }
```
{{/python}}

**Field Selection (GraphQL-style):**
```python
# Allow clients to specify fields needed
@app.get("/users")
async def list_users(fields: str = None):
    query = db.query(User)
    if fields:
        columns = fields.split(',')
        query = query.with_entities(*[
            getattr(User, col) for col in columns
            if hasattr(User, col)
        ])
    return query.all()
```

**Batch Operations:**
```python
@app.post("/users/batch")
async def create_users(users: List[UserCreate]):
    # Instead of N individual INSERTs
    # Use bulk insert
    db.bulk_insert_mappings(User, [u.dict() for u in users])
    db.commit()
```

##### Frontend Optimization

{{#javascript}}
**Code Splitting:**
```javascript
// Instead of importing everything upfront
import { heavyComponent } from './heavy';

// Lazy load
const heavyComponent = lazy(() => import('./heavy'));

function App() {
  return (
    <Suspense fallback={<Loading />}>
      <heavyComponent />
    </Suspense>
  );
}
```

**Image Optimization:**
```javascript
// Use next/image for Next.js
import Image from 'next/image';

<Image
  src="/hero.png"
  width={800}
  height={600}
  priority
  placeholder="blur"
/>

// Or lazy load
<img loading="lazy" src="/image.jpg" />
```

**Bundle Size Reduction:**
```javascript
// Tree shaking
import { debounce } from 'lodash-es';  // ES modules

// Instead of
import { debounce } from 'lodash';     // CommonJS
```
{{/javascript}}

##### Concurrency Optimization

{{#async}}
**Async/Await Patterns:**
{{#python}}
```python
import asyncio
import aiohttp

async def fetch_user(user_id):
    async with aiohttp.ClientSession() as session:
        async with session.get(f"/api/users/{user_id}") as resp:
            return await resp.json()

# Concurrent requests
async def fetch_users(user_ids):
    tasks = [fetch_user(uid) for uid in user_ids]
    return await asyncio.gather(*tasks)

# Instead of sequential (slow)
async def fetch_users_sequential(user_ids):
    results = []
    for uid in user_ids:
        result = await fetch_user(uid)  # Wait for each
        results.append(result)
    return results
```
{{/python}}

{{#javascript}}
```javascript
// Promise.all for concurrent requests
async function fetchUsers(userIds) {
  const promises = userIds.map(id =>
    fetch(`/api/users/${id}`).then(r => r.json())
  );
  return Promise.all(promises);
}

// Instead of sequential (slow)
async function fetchUsersSequential(userIds) {
  const results = [];
  for (const id of userIds) {
    const user = await fetch(`/api/users/${id}`);
    results.push(await user.json());
  }
  return results;
}
```
{{/javascript}}
{{/async}}

#### 3. Algorithmic Optimizations

**Improve Time Complexity:**
```python
# O(n²) - Bad
def find_duplicates_slow(arr):
    duplicates = []
    for i in range(len(arr)):
        for j in range(i + 1, len(arr)):
            if arr[i] == arr[j]:
                duplicates.append(arr[i])
    return duplicates

# O(n) - Good
def find_duplicates_fast(arr):
    seen = set()
    duplicates = set()
    for item in arr:
        if item in seen:
            duplicates.add(item)
        seen.add(item)
    return list(duplicates)
```

**Use Efficient Data Structures:**
```python
# List lookup: O(n)
if item in items:  # Slow for large lists

# Set lookup: O(1)
if item in set(items):  # Fast
```

**String Optimization:**
{{#python}}
```python
# Bad: O(n²) for n concatenations
result = ""
for item in items:
    result += str(item)  # Creates new string each time

# Good: O(n)
result = "".join(str(item) for item in items)
```
{{/python}}

{{#javascript}}
```javascript
// Bad: Creates intermediate strings
let result = "";
for (const item of items) {
  result += item.toString();
}

// Good: Efficient
const result = items.map(item => item.toString()).join("");
```
{{/javascript}}

#### 4. Architecture Changes

**Horizontal Scaling:**
- Load balancing
- Database read replicas
- Caching layer (Redis, Memcached)
- CDN for static assets

**Vertical Scaling:**
- Increase server resources
- Optimize JVM/Python runtime
- Tune database parameters

**Microservices:**
- Decompose monolith
- Independent scaling
- Service-specific optimizations

### Optimization Checklist

#### Database
- [ ] Added missing indexes
- [ ] Optimized slow queries
- [ ] Implemented connection pooling
- [ ] Fixed N+1 query problems
- [ ] Added query caching
- [ ] Implemented read replicas (if needed)

#### Caching
- [ ] Implemented Redis/Memcached
- [ ] Added response caching
- [ ] Configured cache TTL
- [ ] Implemented cache invalidation
- [ ] Added CDN for static assets

#### API
- [ ] Implemented pagination
- [ ] Added compression
- [ ] Optimized serialization
- [ ] Implemented batch operations
- [ ] Added field selection

#### Concurrency
- [ ] Used async I/O
- [ ] Implemented connection pooling
- [ ] Optimized thread/goroutine pool
- [ ] Reduced lock contention

#### Algorithms
- [ ] Improved time complexity
- [ ] Used appropriate data structures
- [ ] Optimized string operations
- [ ] Minimized allocations

### Testing Optimizations

Before & After Comparison:
```python
# Benchmark critical paths
import time

def benchmark(func, *args, iterations=1000):
  start = time.time()
  for _ in range(iterations):
    func(*args)
  end = time.time()
  return (end - start) / iterations

# Compare
old_time = benchmark(old_implementation, data)
new_time = benchmark(new_implementation, data)
improvement = (old_time - new_time) / old_time * 100

print(f"Old: {old_time:.4f}s")
print(f"New: {new_time:.4f}s")
print(f"Improvement: {improvement:.1f}%")
```

### Risk Mitigation

1. **Backup Everything**:
   - Database backups
   - Code rollback
   - Configuration snapshots

2. **Gradual Rollout**:
   - Feature flags
   - A/B testing
   - Canary deployment

3. **Monitor Continuously**:
   - Error rates
   - Response times
   - Resource usage
   - Business metrics

4. **Rollback Plan**:
   - Document rollback procedure
   - Test rollback process
   - Quick rollback mechanism

### Outputs

- Optimization implementation code
- Configuration changes
- Migration scripts (if needed)
- Optimization checklist (completed)

### Next Steps

1. **Implement optimizations** (prioritized)
2. **Test each optimization** individually
3. **Measure improvements** vs baseline
4. **Document results**
5. **Move to benchmarking phase**
