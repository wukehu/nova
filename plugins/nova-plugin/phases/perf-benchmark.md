# Performance Benchmarking Phase Template
# 性能基准测试阶段模板

## Phase: Performance Benchmarking

### Objective
Conduct comprehensive benchmarking to validate performance improvements for {{project_name}}.

### Context
- **Project**: {{project_name}}
- **Optimizations Applied**: {{optimization_list}}
- **Baseline Metrics**: {{baseline_metrics}}
- **Target Metrics**: {{target_metrics}}

### Benchmarking Strategy

#### 1. Test Environment Setup

##### Production-like Environment
Create a test environment that mirrors production:

```yaml
# docker-compose.test.yml
version: '3.8'
services:
  app:
    image: {{project_name}}:test
    environment:
      - ENV=test
      - DB_HOST=db
      - REDIS_HOST=redis
    depends_on:
      - db
      - redis

  db:
    image: postgres:15
    environment:
      - POSTGRES_DB=test_db
    volumes:
      - test_data:/var/lib/postgresql/data

  redis:
    image: redis:7-alpine

  load_generator:
    image: grafana/k6:latest
    volumes:
      - ./tests/performance:/scripts
    command: run /scripts/load-test.js
```

##### Test Data
Generate realistic test data:

{{#python}}
```python
import factory
from faker import Faker

fake = Faker()

class UserFactory(factory.Factory):
    class Meta:
        model = User

    username = factory.LazyAttribute(
        lambda _: fake.user_name()
    )
    email = factory.LazyAttribute(
        lambda _: fake.email()
    )
    # ... more fields

# Generate test data
def generate_test_data(count=10000):
    users = UserFactory.create_batch(count)
    return users
```
{{/python}}

#### 2. Load Testing

##### K6 Load Tests

```javascript
// tests/performance/api-load-test.js
import http from 'k6/http';
import { check, sleep } from 'k6';
import { Rate } from 'k6/metrics';

const errorRate = new Rate('errors');

export const options = {
  stages: [
    { duration: '2m', target: 100 },   // Ramp up
    { duration: '5m', target: 100 },   // Stay at 100
    { duration: '2m', target: 500 },   // Ramp up to 500
    { duration: '5m', target: 500 },   // Stay at 500
    { duration: '2m', target: 1000 },  // Ramp up to 1000
    { duration: '5m', target: 1000 },  // Stay at 1000
    { duration: '3m', target: 0 },     // Ramp down
  ],
  thresholds: {
    http_req_duration: ['p(95)<500'],  // 95% under 500ms
    http_req_failed: ['rate<0.01'],    // Error rate < 1%
    errors: ['rate<0.1'],
  },
};

const BASE_URL = __ENV.API_URL || 'http://localhost:8000';

export default function () {
  // Test 1: List users (pagination)
  let listRes = http.get(`${BASE_URL}/api/users?page=1&size=20`);
  check(listRes, {
    'list status is 200': (r) => r.status === 200,
    'list has users': (r) => JSON.parse(r.body).data.length > 0,
  }) || errorRate.add(1);

  sleep(1);

  // Test 2: Get user by ID
  const userId = Math.floor(Math.random() * 1000) + 1;
  let getRes = http.get(`${BASE_URL}/api/users/${userId}`);
  check(getRes, {
    'get status is 200': (r) => r.status === 200,
    'get has user data': (r) => JSON.parse(r.body).id === userId,
  }) || errorRate.add(1);

  sleep(1);

  // Test 3: Create user
  let createRes = http.post(
    `${BASE_URL}/api/users`,
    JSON.stringify({
      username: `user_${__VU}_${__ITER}`,
      email: `user_${__VU}_${__ITER}@example.com`,
      password: 'SecurePass123!',
    }),
    { headers: { 'Content-Type': 'application/json' } }
  );
  check(createRes, {
    'create status is 201': (r) => r.status === 201,
  }) || errorRate.add(1);

  sleep(2);
}
```

##### Artillery Load Tests

```yaml
# tests/performance/load-test.yml
config:
  target: 'http://localhost:8000'
  phases:
    - duration: 120
      arrivalRate: 10
      name: "Warm up"
    - duration: 300
      arrivalRate: 50
      name: "Sustained load"
    - duration: 120
      arrivalRate: 100
      name: "Peak load"
    - duration: 120
      arrivalRate: 10
      name: "Cool down"

scenarios:
  - name: "User Workflows"
    weight: 70
    flow:
      - get:
          url: "/api/users?page=1&size=20"
      - think: 1
      - get:
          url: "/api/users/{{ $randomNumber(1, 1000) }}"
      - think: 1
      - post:
          url: "/api/users"
          json:
            username: "testuser_{{ $randomString(8) }}"
            email: "test_{{ $randomString(8) }}@example.com"
            password: "SecurePass123!"

  - name: "Admin Workflows"
    weight: 30
    flow:
      - get:
          url: "/api/admin/users"
          headers:
            Authorization: "Bearer {{ $processEnvironment.ADMIN_TOKEN }}"
      - think: 2
```

#### 3. Database Benchmarks

##### Query Performance

```sql
-- Benchmark individual queries
EXPLAIN ANALYZE
SELECT * FROM users
WHERE email = 'test@example.com';

-- Benchmark with EXPLAIN
EXPLAIN (ANALYZE, BUFFERS, VERBOSE)
SELECT u.*, o.*
FROM users u
LEFT JOIN orders o ON o.user_id = u.id
WHERE u.id = 123;

-- Compare before/after
SELECT
    query,
    calls,
    total_time,
    mean_time,
    stddev_time
FROM pg_stat_statements
WHERE query LIKE '%users%'
ORDER BY mean_time DESC;
```

##### Connection Pool Testing

```python
# Test optimal pool size
import time
from concurrent.futures import ThreadPoolExecutor

def test_concurrent_requests(pool_size):
    start = time.time()
    with ThreadPoolExecutor(max_workers=pool_size) as executor:
        futures = [
            executor.submit(make_request)
            for _ in range(1000)
        ]
        results = [f.result() for f in futures]
    end = time.time()
    return end - start

for pool_size in [5, 10, 20, 50, 100]:
    duration = test_concurrent_requests(pool_size)
    print(f"Pool size {pool_size}: {duration:.2f}s")
```

#### 4. API Benchmarks

##### Response Time Percentiles

{{#python}}
```python
import asyncio
import aiohttp
import time
from statistics import mean, median, quantiles

async def benchmark_endpoint(session, url, iterations=100):
    times = []
    for _ in range(iterations):
        start = time.time()
        async with session.get(url) as response:
            await response.read()
        end = time.time()
        times.append((end - start) * 1000)  # ms

    return {
        'mean': mean(times),
        'median': median(times),
        'p95': quantiles(times, n=20)[18],  # 95th percentile
        'p99': quantiles(times, n=100)[98],  # 99th percentile
        'min': min(times),
        'max': max(times),
    }

async def main():
    async with aiohttp.ClientSession() as session:
        results = await benchmark_endpoint(
            session,
            'http://localhost:8000/api/users/1'
        )
        print(f"Mean: {results['mean']:.2f}ms")
        print(f"Median: {results['median']:.2f}ms")
        print(f"P95: {results['p95']:.2f}ms")
        print(f"P99: {results['p99']:.2f}ms")

asyncio.run(main())
```
{{/python}}

#### 5. Memory Benchmarks

##### Memory Profiling

{{#python}}
```python
import tracemalloc
import gc

def benchmark_memory(func, *args, **kwargs):
    tracemalloc.start()
    gc.collect()

    snapshot1 = tracemalloc.take_snapshot()

    # Run function
    result = func(*args, **kwargs)

    snapshot2 = tracemalloc.take_snapshot()
    tracemalloc.stop()

    # Calculate difference
    top_stats = snapshot2.compare_to(snapshot1, 'lineno')

    print("Memory allocation:")
    for stat in top_stats[:10]:
        print(stat)

    return result
```
{{/python}}

{{#javascript}}
```javascript
// Node.js memory benchmark
function measureMemory() {
  if (process.memoryUsage) {
    const usage = process.memoryUsage();
    console.log({
      rss: `${Math.round(usage.rss / 1024 / 1024)}MB`,
      heapUsed: `${Math.round(usage.heapUsed / 1024 / 1024)}MB`,
      heapTotal: `${Math.round(usage.heapTotal / 1024 / 1024)}MB`,
    });
  }
}

// Before
measureMemory();

// Run operations
yourFunction();

// After
measureMemory();
```
{{/javascript}}

#### 6. Comparison Report

##### Before vs After

```markdown
# Performance Benchmark Results

## Summary

| Metric | Before | After | Improvement |
|--------|--------|-------|-------------|
| p50 Response Time | 450ms | 85ms | **81%** ↓ |
| p95 Response Time | 1200ms | 210ms | **83%** ↓ |
| p99 Response Time | 2500ms | 450ms | **82%** ↓ |
| Throughput | 200 req/s | 1800 req/s | **800%** ↑ |
| Error Rate | 2.5% | 0.05% | **98%** ↓ |
| Memory Usage | 2.1GB | 0.9GB | **57%** ↓ |
| CPU Usage | 85% | 35% | **59%** ↓ |

## Detailed Results

### API Endpoints

#### GET /api/users
| Metric | Before | After | Change |
|--------|--------|-------|--------|
| Mean | 520ms | 95ms | -82% |
| Median | 480ms | 85ms | -82% |
| P95 | 1100ms | 180ms | -84% |
| P99 | 2100ms | 350ms | -83% |

#### GET /api/users/:id
| Metric | Before | After | Change |
|--------|--------|-------|--------|
| Mean | 180ms | 35ms | -81% |
| Median | 160ms | 30ms | -81% |
| P95 | 450ms | 75ms | -83% |
| P99 | 850ms | 120ms | -86% |

### Database Queries

#### users.email lookup
| Metric | Before | After | Change |
|--------|--------|-------|--------|
| Mean | 485ms | 9ms | -98% |
| Rows scanned | 1,000,000 | 1 | -99.99% |
| Index used | No | idx_users_email | - |

### Cache Performance

| Metric | Before | After | Change |
|--------|--------|-------|--------|
| Hit Rate | N/A | 94% | - |
| Avg Response | 485ms | 42ms | -91% |
| DB Queries | 10,000/s | 600/s | -94% |

## Load Test Results

### Sustained Load (500 concurrent users)

| Metric | Before | After | Change |
|--------|--------|-------|--------|
| Duration | 5 min | 5 min | - |
| Total Requests | 150,000 | 150,000 | - |
| Successful | 146,250 | 149,925 | +2.5% |
| Failed | 4,750 | 75 | -98.4% |
| P95 Latency | 1850ms | 285ms | -84.6% |
| Error Rate | 3.2% | 0.05% | -98.4% |

### Peak Load (1000 concurrent users)

| Metric | Before | After | Change |
|--------|--------|-------|--------|
| Duration | 5 min | 5 min | - |
| Total Requests | 300,000 | 300,000 | - |
| Successful | 282,000 | 298,800 | +5.9% |
| Failed | 18,000 | 1,200 | -93.3% |
| P95 Latency | 4200ms | 650ms | -84.5% |
| Error Rate | 6.0% | 0.4% | -93.3% |

## Optimizations Applied

1. **Database Indexes** (1 day)
   - Added idx_users_email
   - Added idx_orders_user_created
   - **Impact**: 98% query improvement

2. **Caching Layer** (2 days)
   - Implemented Redis caching
   - Cache hit rate: 94%
   - **Impact**: 91% response improvement

3. **Connection Pooling** (1 day)
   - Increased pool size from 5 to 20
   - **Impact**: 4x throughput

4. **N+1 Query Fix** (3 days)
   - Implemented eager loading
   - **Impact**: 10x for user listings

5. **Compression** (1 day)
   - Enabled gzip compression
   - **Impact**: 70% bandwidth reduction

## Conclusion

✅ **All targets exceeded:**
- Response time: Target was <500ms, achieved 210ms p95
- Throughput: Target was 1000 req/s, achieved 1800 req/s
- Error rate: Target was <0.1%, achieved 0.05%

**Total Effort**: 8 days
**Risk**: Low
**Recommendation**: Deploy to production
```

### Benchmarking Checklist

- [ ] Test environment prepared
- [ ] Test data generated
- [ ] Load tests executed
- [ ] API benchmarks completed
- [ ] Database benchmarks completed
- [ ] Memory benchmarks completed
- [ ] Before/after comparison made
- [ ] Targets validated
- [ ] Report generated
- [ ] Results documented

### Outputs

- Load test results (K6, Artillery)
- API benchmark data
- Database performance metrics
- Memory usage reports
- Comparison report
- Recommendations

### Next Steps

1. **Review results** with team
2. **Validate targets** are met
3. **Prepare deployment** plan
4. **Set up monitoring** for production
5. **Move to validation phase**
