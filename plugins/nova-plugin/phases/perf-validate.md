# Performance Validation Phase Template
# 验证与监控阶段模板

## Phase: Performance Validation

### Objective
Validate performance improvements in production-like environment and set up continuous monitoring.

### Context
- **Project**: {{project_name}}
- **Optimization Results**: {{benchmark_results}}
- **Baseline Metrics**: {{baseline_metrics}}
- **Target Metrics**: {{target_metrics}}

### Validation Strategy

#### 1. Pre-Production Validation

##### Staging Environment Test

Deploy to staging and run full test suite:

```yaml
# .github/workflows/performance-validation.yml
name: Performance Validation

on:
  pull_request:
    branches: [main]

jobs:
  performance-test:
    runs-on: ubuntu-latest
    services:
      postgres:
        image: postgres:15
        env:
          POSTGRES_PASSWORD: postgres
        options: >-
          --health-cmd pg_isready
          --health-interval 10s
          --health-timeout 5s
          --health-retries 5

      redis:
        image: redis:7-alpine
        options: >-
          --health-cmd "redis-cli ping"
          --health-interval 10s
          --health-timeout 5s
          --health-retries 5

    steps:
      - uses: actions/checkout@v3

      - name: Setup Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.12'

      - name: Install dependencies
        run: |
          pip install -r requirements.txt
          pip install pytest-benchmark locust

      - name: Run benchmarks
        run: |
          pytest tests/performance/ --benchmark-only

      - name: Run load tests
        run: |
          locust -f tests/performance/locustfile.py \
            --headless \
            --users 100 \
            --spawn-rate 10 \
            --run-time 5m \
            --host http://localhost:8000

      - name: Check thresholds
        run: |
          python scripts/check_performance.py \
            --threshold-p95 500 \
            --threshold-error-rate 0.1
```

##### Regression Testing

Ensure optimizations didn't break functionality:

{{#python}}
```python
# tests/test_performance_optimizations.py
import pytest
from api.endpoints.users import get_user
from db.models import User

def test_get_user_returns_same_data():
    """Verify optimization didn't change returned data"""
    user = UserFactory.create()
    result = get_user(user.id)

    assert result.id == user.id
    assert result.username == user.username
    assert result.email == user.email

def test_cache_invalidation():
    """Verify cache invalidates correctly"""
    user = UserFactory.create()

    # First call - cache miss
    result1 = get_user(user.id)
    assert result1.username == user.username

    # Update user
    user.username = "updated"
    user.save()

    # Second call - should get updated data
    result2 = get_user(user.id)
    assert result2.username == "updated"

def test_concurrent_updates():
    """Verify concurrent updates work correctly"""
    import threading

    user = UserFactory.create(balance=100)

    def update_balance():
        for _ in range(100):
            user.balance += 1
            user.save()

    threads = [threading.Thread(target=update_balance) for _ in range(10)]

    for t in threads:
        t.start()
    for t in threads:
        t.join()

    # Should be 100 + 100*10 = 1100
    assert user.balance == 1100
```
{{/python}}

#### 2. Production Deployment

##### Canary Deployment

Roll out to small percentage of users first:

```yaml
# kubernetes/canary-deployment.yaml
apiVersion: flagger.app/v1beta1
kind: Canary
metadata:
  name: {{project_name}}
  namespace: production
spec:
  targetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: {{project_name}}
  service:
    port: 8080
  analysis:
    interval: 1m
    threshold: 5
    maxWeight: 50
    stepWeight: 10
    metrics:
      - name: request-success-rate
        thresholdRange:
          min: 99
        interval: 1m
      - name: request-duration
        thresholdRange:
          max: 500
        interval: 1m
  webhooks:
    - name: slack-notifier
      url: https://hooks.slack.com/services/YOUR/WEBHOOK
```

##### Feature Flags

Use feature flags to enable optimizations:

```python
# services/feature_flags.py
from flagsmith import Flagsmith

flags = Flagsmith(api_key=os.getenv('FLAGSMITH_KEY'))

def is_enabled(feature_name, default=False):
    return flags.is_feature_enabled(feature_name, default)

# Usage
if is_enabled('use-caching'):
    return get_user_cached(user_id)
else:
    return get_user_db(user_id)
```

#### 3. Monitoring Setup

##### Application Performance Monitoring (APM)

{{#datadog}}
**Datadog Setup:**
```python
from ddtrace import tracer
from ddtrace import patch_all

# Patch all libraries
patch_all()

# Configure tracer
tracer.configure(
    hostname='agent.datadoghq.com',
    port=8126,
    env='production',
    service='{{project_name}}',
    tags=['version:1.0.0', 'region:us-east-1']
)

# Custom spans
@tracer.wrap('user.get')
def get_user(user_id):
    # ... implementation
    pass
```
{{/datadog}}

{{#prometheus}}
**Prometheus Metrics:**
```python
from prometheus_client import Counter, Histogram, Gauge
import time

# Define metrics
request_duration = Histogram(
    'api_request_duration_seconds',
    'API request duration',
    ['endpoint', 'method']
)

request_count = Counter(
    'api_request_count_total',
    'Total API requests',
    ['endpoint', 'method', 'status']
)

active_connections = Gauge(
    'db_active_connections',
    'Active database connections'
)

# Use in code
@app.get("/users/{user_id}")
@request_duration.labels(endpoint='/users/{id}', method='GET').time()
def get_user(user_id: int):
    start = time.time()

    try:
        result = db.get_user(user_id)
        request_count.labels(
            endpoint='/users/{id}',
            method='GET',
            status=200
        ).inc()
        return result
    except Exception as e:
        request_count.labels(
            endpoint='/users/{id}',
            method='GET',
            status=500
        ).inc()
        raise
```

**Prometheus Configuration:**
```yaml
# prometheus.yml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: '{{project_name}}'
    static_configs:
      - targets: ['app:8000']
    metrics_path: '/metrics'

rule_files:
  - '/etc/prometheus/alerts.yml'

alerting:
  alertmanagers:
    - static_configs:
        - targets: ['alertmanager:9093']
```

**Alert Rules:**
```yaml
# alerts.yml
groups:
  - name: api_performance
    interval: 30s
    rules:
      - alert: HighResponseTime
        expr: histogram_quantile(0.95, api_request_duration_seconds_bucket) > 0.5
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "API response time too high"
          description: "P95 response time is {{ $value }}s"

      - alert: HighErrorRate
        expr: rate(api_request_count_total{status=~"5.."}[5m]) > 0.01
        for: 2m
        labels:
          severity: critical
        annotations:
          summary: "High error rate detected"
          description: "Error rate is {{ $value }} requests/sec"

      - alert: LowCacheHitRate
        expr: rate(cache_hits_total[5m]) / rate(cache_requests_total[5m]) < 0.8
        for: 10m
        labels:
          severity: warning
        annotations:
          summary: "Cache hit rate below 80%"
```
{{/prometheus}}

##### Grafana Dashboards

```json
{
  "dashboard": {
    "title": "{{project_name}} Performance",
    "panels": [
      {
        "title": "Request Rate",
        "targets": [
          {
            "expr": "sum(rate(api_request_count_total[5m]))"
          }
        ]
      },
      {
        "title": "Response Time (p95)",
        "targets": [
          {
            "expr": "histogram_quantile(0.95, api_request_duration_seconds_bucket)"
          }
        ]
      },
      {
        "title": "Error Rate",
        "targets": [
          {
            "expr": "sum(rate(api_request_count_total{status=~\"5..\"}[5m]))"
          }
        ]
      },
      {
        "title": "Cache Hit Rate",
        "targets": [
          {
            "expr": "rate(cache_hits_total[5m]) / rate(cache_requests_total[5m])"
          }
        ]
      },
      {
        "title": "Database Pool Usage",
        "targets": [
          {
            "expr": "db_active_connections / db_pool_size"
          }
        ]
      },
      {
        "title": "Memory Usage",
        "targets": [
          {
            "expr": "process_resident_memory_bytes / 1024 / 1024"
          }
        ]
      }
    ]
  }
}
```

#### 4. Continuous Validation

##### Automated Performance Tests

Run performance tests on every commit:

```yaml
# .github/workflows/continuous-performance.yml
name: Continuous Performance

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  benchmark:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Setup Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.12'

      - name: Install dependencies
        run: pip install -r requirements.txt

      - name: Run benchmarks
        run: |
          pytest tests/performance/ \
            --benchmark-only \
            --benchmark-json=output.json

      - name: Store benchmark result
        uses: benchmark-action/github-action-benchmark@v1
        with:
          tool: 'pytest'
          output-file-path: output.json
          github-token: ${{ secrets.GITHUB_TOKEN }}
          auto-push: true
          alert-threshold: '200%'
          comment-on-alert: true
          fail-on-alert: true
```

##### Performance Regression Detection

```python
# scripts/detect_regression.py
import json
import sys

def check_regression(current, baseline, threshold=1.2):
    """Check if current performance regressed vs baseline"""
    regressions = []

    for metric, value in current.items():
        if metric in baseline:
            baseline_value = baseline[metric]
            ratio = value / baseline_value

            # For response times, higher is worse
            if 'duration' in metric or 'time' in metric:
                if ratio > threshold:
                    regressions.append({
                        'metric': metric,
                        'current': value,
                        'baseline': baseline_value,
                        'ratio': ratio
                    })

            # For throughput, lower is worse
            elif 'throughput' in metric or 'rate' in metric:
                if ratio < (1 / threshold):
                    regressions.append({
                        'metric': metric,
                        'current': value,
                        'baseline': baseline_value,
                        'ratio': ratio
                    })

    return regressions

# Load benchmark results
with open('current_benchmark.json') as f:
    current = json.load(f)

with open('baseline_benchmark.json') as f:
    baseline = json.load(f)

# Check for regressions
regressions = check_regression(current, baseline)

if regressions:
    print("PERFORMANCE REGRESSION DETECTED:")
    for reg in regressions:
        print(f"  {reg['metric']}: {reg['ratio']:.2f}x degradation")
    sys.exit(1)
else:
    print("No performance regressions detected")
    sys.exit(0)
```

#### 5. Validation Checklist

- [ ] All optimization changes reviewed
- [ ] Staging environment tests passed
- [ ] Load tests passed
- [ ] Regression tests passed
- [ ] Feature flags configured
- [ ] Canary deployment ready
- [ ] Monitoring/alerting configured
- [ ] Dashboard created
- [ ] Runbook documented
- [ ] Rollback plan tested

### Validation Report

```markdown
# Performance Validation Report

## Executive Summary
- **Status**: ✅ Passed
- **Deployment**: Canary (10%)
- **Duration**: 7 days
- **Recommendation**: Proceed to full rollout

## Pre-Production Results

| Metric | Target | Actual | Status |
|--------|--------|--------|--------|
| P95 Response Time | <500ms | 210ms | ✅ |
| Throughput | >1000 req/s | 1800 req/s | ✅ |
| Error Rate | <0.1% | 0.05% | ✅ |
| Cache Hit Rate | >80% | 94% | ✅ |

## Production Validation (Canary)

### Day 1-3 (10% traffic)
- **P95 Latency**: 225ms (within 7% of staging)
- **Throughput**: 180 req/s (steady)
- **Error Rate**: 0.06% (within target)
- **No incidents**: ✅

### Day 4-7 (25% traffic)
- **P95 Latency**: 235ms (within 12% of staging)
- **Throughput**: 450 req/s (steady)
- **Error Rate**: 0.07% (within target)
- **No incidents**: ✅

## Monitoring Summary

### Alerts Triggered
- None in validation period

### Anomalies Detected
- Minor latency spike during deployment (expected)
- Slight increase in cache misses on Day 2 (investigated - normal)

### Customer Impact
- Zero customer complaints
- Improved NPS score (from 72 to 78)
- Reduced page load time (from 2.1s to 0.8s)

## Comparison: Before vs After

| Metric | Before | After | Improvement |
|--------|--------|-------|-------------|
| P95 Response Time | 1200ms | 210ms | 83% ↓ |
| Throughput | 200 req/s | 1800 req/s | 800% ↑ |
| Error Rate | 2.5% | 0.05% | 98% ↓ |
| Cost/User | $0.015 | $0.003 | 80% ↓ |

## Risks and Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| Cache stampede | Low | Medium | Implemented lock-based caching |
| Memory leak | Low | High | Continuous monitoring |
| DB connection exhaustion | Low | High | Connection pooling + alerts |
| Rollback needed | Low | Medium | Feature flags + automated rollback |

## Recommendations

### Immediate
1. ✅ **Proceed to full rollout** - All targets met
2. Extend monitoring period by 2 weeks
3. Document lessons learned

### Future Optimizations
1. Implement GraphQL for flexible queries
2. Add edge caching (Cloudflare)
3. Consider database read replicas
4. Explore HTTP/3 for better performance

## Conclusion

All performance optimizations validated successfully. The system shows:
- **83% improvement** in response times
- **800% increase** in throughput
- **98% reduction** in error rates
- **80% cost reduction** per user

**Approved for full production deployment.**

---

Report Generated: 2026-03-21
Validated By: Performance Engineering Team
Next Review: 2026-04-04 (2 weeks)
```

### Outputs

- Validation report
- Monitoring dashboards
- Alert configurations
- Runbook documentation
- Rollback procedures

### Next Steps

1. **Full rollout** to production
2. **Monitor** continuously
3. **Review** in 2 weeks
4. **Plan** next optimization cycle
