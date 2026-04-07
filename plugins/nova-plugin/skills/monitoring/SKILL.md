---
description: Use this skill when setting up monitoring, configuring alerts, implementing logging, or managing observability
---

# Monitoring and Observability Skill

## Purpose

Set up comprehensive monitoring, alerting, logging, and observability for applications and infrastructure.

## When to Use This Skill

Activate this skill when:
- Setting up application monitoring
- Configuring alerts and notifications
- Implementing logging systems
- Managing observability stacks
- Analyzing performance metrics
- Troubleshooting with logs and traces
- Setting up dashboards

## Core Competencies

### 1. Metrics

**Application Metrics**:
- Request rate and count
- Response time (p50, p90, p95, p99)
- Error rate and count
- Active connections
- Queue lengths

**Business Metrics**:
- User registrations
- Orders processed
- Revenue generated
- Conversion rates
- Custom business KPIs

**Infrastructure Metrics**:
- CPU usage
- Memory usage
- Disk I/O
- Network I/O
- Resource availability

**Database Metrics**:
- Connection pool usage
- Query latency
- Query throughput
- Deadlocks
- Replication lag

### 2. Logging

**Application Logs**:
- Request/response logging
- Error logging with stack traces
- Warning logging
- Debug logging
- Contextual logging

**Structured Logging**:
- JSON format
- Log levels (DEBUG, INFO, WARN, ERROR, FATAL)
- Request ID correlation
- User ID tracking
- Timestamps

**Log Management**:
- Log rotation
- Log retention policies
- Log aggregation
- Log parsing and indexing

### 3. Tracing

**Distributed Tracing**:
- Trace context propagation
- Span creation
- Span attributes
- Span events
- Span links

**Trace Analysis**:
- Request flow visualization
- Service dependency mapping
- Latency breakdown
- Error propagation tracking
- Bottleneck identification

### 4. Alerting

**Alert Rules**:
- Threshold-based alerts
- Rate-based alerts
- Anomaly detection
- Composite alerts
- Alert suppression

**Notification Channels**:
- Email
- Slack
- PagerDuty
- OpsGenie
- Webhooks

**Alert Management**:
- Alert routing
- Alert escalation
- On-call schedules
- Alert acknowledgment
- Alert silencing

## Monitoring Stack

### Metrics Collection
**Prometheus**:
- Pull-based metric collection
- Time-series database
- Query language (PromQL)
- Alerting rules
- Service discovery

**InfluxDB**:
- Time-series database
- High write throughput
- SQL support
- Cloud-native features

**Datadog**:
- Hosted monitoring
- APM integration
- Log integration
- Metric-based alerting

**Grafana**:
- Visualization dashboards
- Multiple data sources
- Alerting
- Annotations

### Logging Stack
**ELK Stack**:
- Elasticsearch (storage/search)
- Logstash (log processing)
- Kibana (visualization)
- Beats (log shippers)

**Loki**:
- Log aggregation
- Label-based indexing
- Grafana integration
- Lightweight

**CloudWatch** (AWS):
- Log aggregation
- Metric collection
- Log insights
- Metric insights

### Tracing Stack
**Jaeger**:
- Distributed tracing
- Span collection
- Trace visualization
- Sampling

**Zipkin**:
- Distributed tracing
- Span collection
- Trace visualization

**OpenTelemetry**:
- Vendor-neutral
- Metrics, logs, traces
- Automatic instrumentation
- Multiple exporters

### Alerting Stack
**Alertmanager**:
- Alert routing
- Alert deduplication
- Alert grouping
- Silencing
- Inhibition

**PagerDuty**:
- On-call management
- Alert routing
- Escalation policies
- Incident response

## Monitoring Best Practices

### Metrics
- **Use RED Method** (Rate, Errors, Duration)
- **Use USE Method** (Utilization, Saturation, Errors)
- **Include relevant labels**
- **Avoid high cardinality labels**
- **Use appropriate metric types**
  - Counter for counting events
  - Gauge for current values
  - Histogram for distributions
  - Summary for aggregations

### Logging
- **Use structured logging**
- **Include request ID in all logs**
- **Log at appropriate levels**
- **Don't log sensitive data**
- **Log entry and exit points**
- **Log errors with full context**
- **Use log sampling for high-volume logs**

### Tracing
- **Propagate trace context everywhere**
- **Create spans for async operations**
- **Add relevant attributes to spans**
- **Use appropriate sampling**
- **Don't trace in production loops**

### Alerting
- **Set meaningful thresholds**
- **Implement alert escalation**
- **Use alert grouping**
- **Set up on-call rotation**
- **Provide actionable alert messages**
- **Include runbooks in alerts**
- **Avoid alert fatigue**

## Observability Levels

### Level 1: Basic
- Application logs
- Error tracking
- Basic metrics
- Health checks

### Level 2: Enhanced
- Structured logging
- Custom metrics
- Basic tracing
- Dashboards

### Level 3: Advanced
- Distributed tracing
- Advanced metrics
- Log aggregation
- Alerting

### Level 4: Full
- APM integration
- Synthetic monitoring
- Real user monitoring (RUM)
- Advanced alerting
- SLO/SLI tracking

## Service Level Objectives (SLOs)

**SLI (Service Level Indicator)**:
- Error rate
- Latency (p95, p99)
- Availability
- Throughput

**SLO (Service Level Objective)**:
- Error rate < 0.1%
- p95 latency < 500ms
- Availability > 99.9%
- Throughput > 1000 req/s

**SLA (Service Level Agreement)**:
- Contract with customers
- Legal obligations
- Compensation terms
- Reporting requirements

**Error Budget**:
- Budget = (1 - SLO) × Time period
- Track budget consumption
- Halt deployments when exhausted
- Alert on budget threshold

## Troubleshooting Workflow

### 1. Identify Problem
- Check alert details
- Review dashboard
- Identify affected services
- Determine impact scope

### 2. Gather Information
- Review error logs
- Check performance metrics
- Review trace data
- Check recent deployments

### 3. Analyze
- Identify root cause
- Determine impact
- Assess severity
- Define resolution steps

### 4. Resolve
- Implement fix
- Test resolution
- Deploy fix
- Monitor recovery

### 5. Post-Mortem
- Document incident
- Update runbooks
- Improve monitoring
- Update SLOs

## Dashboards

### Essential Dashboards
**Application Overview**:
- Request rate
- Error rate
- Response time percentiles
- Active users
- Error types breakdown

**Performance**:
- Response time histogram
- Request latency breakdown
- Database query time
- External API time
- Cache hit rate

**Infrastructure**:
- CPU, Memory, Disk, Network
- Container resource usage
- Pod health status
- Node availability

**Business**:
- KPIs
- Conversion funnels
- Revenue metrics
- User activity
- Custom business metrics

## Related Skills

- **Security Audit**: Security monitoring
- **Deployment**: Deployment monitoring
- **Performance Optimization**: Performance analysis
- **Code Development**: Application instrumentation
