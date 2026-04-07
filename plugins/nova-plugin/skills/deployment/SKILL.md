---
description: Use this skill when deploying applications, configuring infrastructure, setting up CI/CD pipelines, or managing cloud resources
---

# Deployment Skill

## Purpose

Execute deployment operations for applications, including infrastructure provisioning, CI/CD configuration, containerization, and cloud resource management.

## When to Use This Skill

Activate this skill when:
- Deploying applications to staging/production
- Setting up CI/CD pipelines
- Configuring infrastructure
- Managing cloud resources
- Setting up monitoring and logging
- Implementing deployment automation
- Troubleshooting deployment issues

## Core Competencies

### 1. Containerization

**Docker Configuration**:
- Multi-stage Dockerfiles
- Image optimization
- Security hardening
- Health checks
- Volume and network configuration

**Best Practices**:
- Use minimal base images (Alpine, Distroless)
- Optimize layer caching
- Use non-root users
- Scan images for vulnerabilities
- Implement proper signal handling

### 2. Orchestration

**Kubernetes Configuration**:
- Deployments and StatefulSets
- Services and Ingress
- ConfigMaps and Secrets
- Resource limits and requests
- Health checks (liveness/readiness)

**Best Practices**:
- Use immutable infrastructure
- Implement rolling updates
- Set up HPA (Horizontal Pod Autoscaler)
- Use persistent volumes for state
- Implement pod disruption budgets

### 3. CI/CD Pipelines

**Continuous Integration**:
- Automated testing
- Code quality checks
- Security scanning
- Artifact building

**Continuous Deployment**:
- Automated deployment to staging
- Manual approval for production
- Canary deployments
- Blue-green deployments
- Rollback mechanisms

### 4. Infrastructure as Code

**Tools**:
- **Terraform** - Multi-cloud IaC
- **Ansible** - Configuration management
- **Helm** - Kubernetes package manager
- **Kustomize** - Kubernetes configuration
- **Pulumi** - Cross-platform IaC

**Principles**:
- Version control infrastructure
- Make changes reviewable
- Make changes reversible
- Document infrastructure

### 5. Cloud Resources

**AWS Services**:
- EC2, ECS, EKS
- S3, RDS, ElastiCache
- Lambda, API Gateway
- CloudFormation, CDK

**GCP Services**:
- Compute Engine, GKE
- Cloud Storage, Cloud SQL
- Cloud Functions
- Cloud Deployment Manager

**Azure Services**:
- Virtual Machines, AKS
- Blob Storage, SQL Database
- Functions, API Management
- ARM Templates, Bicep

## Deployment Strategies

### 1. Rolling Update
Gradually replace old instances with new ones.

**Benefits**:
- Zero downtime
- Easy rollback
- Gradual rollout

**When to Use**:
- Stateless applications
- Can handle multiple versions
- Want simple deployment

### 2. Blue-Green Deployment
Maintain two identical production environments.

**Benefits**:
- Instant rollback
- Safe testing
- No version mixing

**When to Use**:
- Critical applications
- Need instant rollback
- Can afford double resources

### 3. Canary Deployment
Gradually shift traffic to new version.

**Benefits**:
- Reduced risk
- Phased rollout
- Quick failure detection

**When to Use**:
- High-traffic applications
- Want gradual rollout
- Need A/B testing

### 4. Feature Flags
Deploy code behind flags.

**Benefits**:
- Instant rollback (toggle flag)
- Gradual rollout
- A/B testing
- Emergency disable

**When to Use**:
- Frequent releases
- Need instant rollback
- Want controlled releases

## Deployment Process

### Phase 1: Preparation
1. **Code Review**
   - Review all changes
   - Approve merge

2. **Testing**
   - Run all tests
   - Run security scans
   - Run performance tests

3. **Build**
   - Build application
   - Build container image
   - Scan for vulnerabilities

### Phase 2: Staging Deployment
1. **Deploy to Staging**
   - Apply configuration
   - Deploy containers
   - Verify health

2. **Verification**
   - Run smoke tests
   - Run integration tests
   - Verify functionality

3. **Manual Approval**
   - Review test results
   - Approve production deployment

### Phase 3: Production Deployment
1. **Pre-Deployment**
   - Create backup
   - Prepare rollback plan
   - Notify team

2. **Deploy**
   - Apply production config
   - Deploy new version
   - Monitor deployment

3. **Post-Deployment**
   - Run health checks
   - Run smoke tests
   - Monitor metrics
   - Verify logs

### Phase 4: Monitoring
1. **Monitor**
   - Watch error rates
   - Watch response times
   - Watch resource usage

2. **Alerting**
   - Set up alerts
   - Notify team on issues
   - Auto-rollback on critical failure

## Quality Gates

### Pre-Deployment Checks
- [ ] All tests passing
- [ ] Code review approved
- [ ] No security vulnerabilities
- [ ] Performance regression acceptable

### Staging Checks
- [ ] Deployment successful
- [ ] Health checks passing
- [ ] Smoke tests passing
- [ ] Integration tests passing

### Production Checks
- [ ] Deployment successful
- [ ] Health checks passing
- [ ] Error rates acceptable
- [ ] Response times performance baselined

## Monitoring

### Health Checks
- **Liveness** - Is the pod alive?
- **Readiness** - Is the pod ready to serve traffic?
- **Startup** - Did the application start successfully?

### Metrics
- **Application Metrics**
  - Request rate
  - Error rate
  - Response time (p50, p90, p95, p99)
  - Active connections

- **Infrastructure Metrics**
  - CPU usage
  - Memory usage
  - Disk I/O
  - Network I/O

- **Deployment Metrics**
  - Deployment success rate
  - Rollback frequency
  - Deployment duration

### Logging
- Application logs
- Access logs
- Error logs
- Security logs
- Audit logs

## Rollback Procedures

### 1. Database Rollback
- Revert database migrations
- Restore from backup
- Update application code

### 2. Application Rollback
- Revert to previous container image
- Restart pods
- Verify functionality

### 3. Infrastructure Rollback
- Reapply previous Terraform state
- Restore from configuration backup
- Verify resources

## Best Practices

### DO
- Use infrastructure as code
- Version control everything
- Test deployments in staging
- Monitor deployments
- Have rollback plans
- Use immutable infrastructure
- Implement health checks
- Set up alerts
- Document procedures
- Regularly update dependencies

### DON'T
- Deploy directly to production
- Skip staging tests
- Ignore health check failures
- Forget rollback plans
- Use manual processes
- Store secrets in code
- Skip security scans
- Ignore alerts
- Deploy on Fridays
- Deploy multiple changes at once

## Tools

### Container Tools
- Docker
- Podman
- Buildah
- Kaniko

### Orchestration Tools
- Kubernetes
- Docker Swarm
- Nomad
- ECS

### CI/CD Tools
- GitHub Actions
- GitLab CI
- Jenkins
- CircleCI
- ArgoCD

### IaC Tools
- Terraform
- Ansible
- Chef
- Puppet
- Pulumi

### Cloud Tools
- AWS CLI
- gcloud
- az
- kubectl
- helm

## Related Skills

- **Security Audit**: Security scanning
- **Performance Optimization**: Performance monitoring
- **Testing**: Pre-deployment testing
