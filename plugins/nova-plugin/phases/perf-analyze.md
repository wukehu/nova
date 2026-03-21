# Performance Analysis Phase Template
# 性能分析阶段模板

## Phase: Performance Analysis

### Objective
Analyze {{project_name}} to identify performance bottlenecks and optimization opportunities.

### Context
- **Project**: {{project_name}}
- **Language**: {{language}}
- **Framework**: {{framework}}
- **Current Issues**: {{performance_issues}}
- **Baseline Metrics**: {{baseline_metrics}}

### Analysis Approach

#### 1. Define Performance Goals

##### Primary Metrics
Define what success looks like:
```
Response Time:
  - p50: {{target_p50}}
  - p95: {{target_p95}}
  - p99: {{target_p99}}

Throughput:
  - Requests per second: {{target_throughput}}
  - Concurrent users: {{target_concurrency}}

Resource Usage:
  - CPU: < {{target_cpu}}%
  - Memory: < {{target_memory}}MB
  - Database: < {{target_db_connections}} connections
```

##### Secondary Metrics
- Cache hit rate
- Error rate
- Availability/uptime
- Startup time

#### 2. Establish Baseline

{{#baseline_required}}
##### Current Performance Measurement
Measure current performance before optimization:

```bash
# Response time measurement
{{measure_response_time_command}}

# Throughput measurement
{{measure_throughput_command}}

# Resource usage monitoring
{{monitor_resources_command}}

# Database performance
{{measure_db_performance}}
```

**Baseline Results:**
```
Current p50: {{current_p50}}
Current p95: {{current_p95}}
Current p99: {{current_p99}}
Current throughput: {{current_throughput}}
```
{{/baseline_required}}

#### 3. Profiling Analysis

##### CPU Profiling
Identify CPU-intensive operations:

{{#python}}
```bash
# Profile Python application
python -m cProfile -o profile.stats your_app.py
python -m pstats profile.stats

# Visualize with snakeviz
snakeviz profile.stats

# Real-time profiling with py-spy
py-spy top --pid <PID>
py-spy record --pid <PID> -o profile.svg
```
{{/python}}

{{#javascript}}
```bash
# Profile Node.js application
node --prof your_app.js
node --prof-process isolate-0xnnnnnnnnnnnn-v8.log > processed.txt

# Flame graph with 0x
0x -- your_app.js

# Clinic.js for diagnosis
clinic doctor -- your_app.js
clinic flame -- your_app.js
```
{{/javascript}}

{{#java}}
```bash
# Java profiling
jps -l  # Find PID
jstat -gc <PID> 1000  # GC statistics
jmap -histo:live <PID>  # Heap histogram

# VisualVM / JProfiler
jvisualvm  # GUI profiler
```
{{/java}}

{{#go}}
```bash
# Go profiling
go test -cpuprofile=cpu.prof -memprofile=mem.prof -bench=.
go tool pprof cpu.prof
go tool pprof -http=:8080 cpu.prof  # Web UI

# Runtime profiling
curl localhost:6060/debug/pprof/profile?seconds=30 > cpu.prof
```
{{/go}}

##### Memory Profiling
Identify memory leaks and high usage:

{{#python}}
```python
# Memory profiling
import tracemalloc
tracemalloc.start()

# ... run code ...

snapshot = tracemalloc.take_snapshot()
top_stats = snapshot.statistics('lineno')
for stat in top_stats[:10]:
    print(stat)
```
{{/python}}

{{#javascript}}
```bash
# Node.js memory profiling
node --heapsnapshot-signal=SIGUSR2 your_app.js
# Send SIGUSR2 to capture heap snapshot
kill -USR2 <PID>
```
{{/javascript}}

##### Database Profiling
Analyze database performance:

```sql
-- Slow query log
SHOW VARIABLES LIKE 'slow_query_log';
SHOW VARIABLES LIKE 'long_query_time';

-- Analyze slow queries
SELECT * FROM mysql.slow_log ORDER BY query_time DESC LIMIT 10;

-- Query execution plan
EXPLAIN ANALYZE SELECT * FROM users WHERE email = 'test@example.com';

-- Missing indexes
SELECT
    table_name,
    index_name
FROM information_schema.statistics
WHERE table_schema = 'your_database';
```

#### 4. Common Bottlenecks

##### Database Issues
- **N+1 Queries**: Multiple queries for related data
- **Missing Indexes**: Full table scans
- **Inefficient Queries**: Complex joins, subqueries
- **Connection Pooling**: Too few/many connections

**Detection:**
```sql
-- Find N+1 queries
-- Check query count vs expected
-- Analyze query patterns
```

**Impact**: High (often 10-100x improvement possible)

##### API Issues
- **Chatty APIs**: Too many round trips
- **Over-fetching**: Returning too much data
- **No Pagination**: Loading all records at once
- **No Compression**: Not using gzip/brotli

**Detection:**
```bash
# Count API calls
# Measure response sizes
# Check compression headers
```

**Impact**: Medium (2-5x improvement possible)

##### Caching Issues
- **No Caching**: Everything computed/queried fresh
- **Cache Misses**: Poor cache strategy
- **No CDN**: Static assets not cached
- **Long TTL**: Stale data

**Detection:**
```bash
# Measure cache hit rate
# Check CDN usage
# Analyze response headers
```

**Impact**: High (10-100x improvement possible)

##### Algorithmic Issues
- **O(n²) Algorithms**: Nested loops
- **Inefficient Data Structures**: List instead of hash map
- **String Operations**: Excessive string concatenation
- **Serialization**: Expensive serialization

**Detection:**
```python
# Look for nested loops
# Check algorithmic complexity
# Profile hot functions
```

**Impact**: High (potentially 100-1000x improvement)

##### Concurrency Issues
- **Blocking I/O**: Synchronous operations
- **Lock Contention**: Excessive locking
- **Thread Starvation**: Not enough workers
- **Context Switching**: Too many threads/goroutines

**Detection:**
```bash
# Check thread/goroutine count
# Monitor lock contention
# Analyze thread dumps
```

**Impact**: Medium (2-10x improvement possible)

#### 5. Analysis Checklist

- [ ] Performance goals defined
- [ ] Baseline metrics established
- [ ] CPU profiling completed
- [ ] Memory profiling completed
- [ ] Database analysis completed
- [ ] API analysis completed
- [ ] Caching analysis completed
- [ ] Network analysis completed
- [ ] Bottlenecks identified
- [ ] Prioritized optimization list

### Analysis Outputs

#### Performance Analysis Report

```markdown
# Performance Analysis Report

## Executive Summary
- **Current p95**: {{current_p95}}
- **Target p95**: {{target_p95}}
- **Gap**: {{performance_gap}}
- **Top Bottleneck**: {{top_bottleneck}}

## Findings

### Critical Issues (High Impact, Low Effort)
1. **Missing Index on users.email**
   - Impact: 50x query improvement
   - Evidence: Query takes 500ms, should be 10ms
   - Location: `api/endpoints/users.py:45`

### High Priority (High Impact, Medium Effort)
1. **N+1 Query Problem**
   - Impact: 10x improvement
   - Evidence: 1000 queries for 1000 records
   - Location: `api/endpoints/orders.py:78`

2. **No Response Caching**
   - Impact: 100x for cached responses
   - Evidence: All queries hit database
   - Location: All endpoints

### Medium Priority (Medium Impact, Low Effort)
1. **No Compression**
   - Impact: 3x bandwidth reduction
   - Evidence: Responses not compressed
   - Location: Configuration

2. **Connection Pooling Too Small**
   - Impact: 2x throughput
   - Evidence: Queued connections
   - Location: Database configuration

### Low Priority (Low Impact, High Effort)
1. **Algorithm Optimization**
   - Impact: 2x improvement
   - Evidence: O(n²) algorithm
   - Location: `services/analytics.py:234`

## Recommendations
1. Add database indexes (1 day)
2. Implement caching (2 days)
3. Fix N+1 queries (3 days)
4. Enable compression (1 day)

## Expected Impact
- **Estimated improvement**: 10-50x overall
- **Effort**: 1-2 weeks
- **Risk**: Low
```

### Prioritization Matrix

```
High Impact │ Quick Wins  │ Major Projects
───────────┼─────────────┼───────────────
           │  Indexing   │ Architecture
           │  Caching    │ Sharding
───────────┼─────────────┼───────────────
Low Impact │ Fillers     │ Thankless Tasks
           │ Compression │ Micro-opts
           └─────────────┴───────────────
             Low Effort    High Effort
```

### Next Steps

1. **Review analysis** with team
2. **Prioritize optimizations** based on impact/effort
3. **Create optimization plan**
4. **Implement quick wins first**
5. **Measure improvements** after each change

### Tools Summary

{{#python}}
- **Profiling**: cProfile, py-spy, memory_profiler
- **Visualization**: snakeviz, gprof2dot
- **Monitoring**: prometheus, grafana
- **APM**: datadog, newrelic
{{/python}}

{{#javascript}}
- **Profiling**: Node.js profiler, 0x, clinic.js
- **Flame graphs**: 0x, clinic flame
- **Monitoring**: prometheus, grafana
- **APM**: datadog, newrelic
{{/javascript}}

{{#java}}
- **Profiling**: VisualVM, JProfiler, Java Mission Control
- **Monitoring**: JMX, prometheus
- **APM**: datadog, newrelic
{{/java}}

{{#go}}
- **Profiling**: pprof, go tool pprof
- **Runtime**: /debug/pprof
- **Monitoring**: prometheus, grafana
- **Tracing**: jaeger, opentelemetry
{{/go}}
