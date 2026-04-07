---
description: Use this skill when conducting security audits, vulnerability scanning, security testing, or implementing security best practices
---

# Security Audit Skill

## Purpose

Conduct comprehensive security audits to identify vulnerabilities, ensure compliance, and implement security best practices throughout the software development lifecycle.

## When to Use This Skill

Activate this skill when:
- Conducting security audits
- Running vulnerability scans
- Implementing security controls
- Reviewing code for security issues
- Setting up security testing
- Configuring security tools
- Responding to security incidents

## Core Competencies

### 1. Vulnerability Assessment

**Static Application Security Testing (SAST)**:
- Analyze source code for security issues
- Identify SQL injection vulnerabilities
- Detect XSS vulnerabilities
- Find authentication/authorization flaws

**Dynamic Application Security Testing (DAST)**:
- Test running application
- Identify runtime vulnerabilities
- Test API endpoints
- Test authentication flows

**Software Composition Analysis (SCA)**:
- Scan dependencies for vulnerabilities
- Check for known CVEs
- Identify outdated packages
- Monitor for new vulnerabilities

**Interactive Application Security Testing (IAST)**:
- Combine SAST and DAST
- Test during runtime
- Provide detailed vulnerability information

### 2. Security Testing

**Authentication Testing**:
- Test login mechanisms
- Test session management
- Test password policies
- Test multi-factor authentication
- Test token management

**Authorization Testing**:
- Test role-based access
- Test resource ownership
- Test permission checks
- Test privilege escalation
- Test API authorization

**Input Validation Testing**:
- Test for SQL injection
- Test for XSS
- Test for command injection
- Test for path traversal
- Test for file inclusion

**Session Management Testing**:
- Test session fixation
- Test session hijacking
- Test session timeout
- Test cookie security

### 3. Security Configuration

**HTTPS/TLS Configuration**:
- Enforce HTTPS in production
- Configure TLS properly
- Use strong cipher suites
- Enable HSTS
- Implement certificate pinning

**CORS Configuration**:
- Configure allowed origins
- Configure allowed methods
- Configure allowed headers
- Implement preflight caching
- Test CORS policies

**Security Headers**:
- Implement Content Security Policy
- Implement X-Frame-Options
- Implement X-Content-Type-Options
- Implement Strict-Transport-Security
- Implement X-XSS-Protection

**Rate Limiting**:
- Implement rate limiting per endpoint
- Implement rate limiting per user
- Implement distributed rate limiting
- Provide rate limit feedback

### 4. OWASP Top 10 Testing

Test for OWASP Top 10 vulnerabilities:

1. **A01: Broken Access Control**
   - Test horizontal privilege escalation
   - Test vertical privilege escalation
   - Test parameter tampering

2. **A02: Cryptographic Failures**
   - Test encryption implementation
   - Test random number generation
   - Test key management

3. **A03: Injection**
   - Test SQL injection
   - Test NoSQL injection
   - Test command injection
   - Test XSS

4. **A04: Insecure Design**
   - Review security architecture
   - Test threat models
   - Review security patterns

5. **A05: Security Misconfiguration**
   - Test default credentials
   - Test error messages
   - Test debug features

6. **A06: Vulnerable Components**
   - Scan dependencies
   - Check for outdated libraries
   - Monitor for CVEs

7. **A07: Auth Failures**
   - Test authentication bypass
   - Test credential stuffing
   - Test password recovery

8. **A08: Data Integrity Failures**
   - Test data serialization
   - Test insecure deserialization
   - Test integrity checks

9. **A09: Logging Failures**
   - Test log injection
   - Test sensitive data logging
   - Test log tampering

10. **A10: SSRF**
    - Test server-side request forgery
    - Test internal network access
    - Test cloud metadata access

### 5. Security Monitoring

**Logging**:
- Log security events
- Log authentication attempts
- Log authorization failures
- Log suspicious activities

**Monitoring**:
- Monitor for attacks
- Monitor for anomalies
- Monitor for policy violations
- Set up alerts

**Incident Response**:
- Implement incident detection
- Implement incident response
- Implement incident recovery
- Implement post-incident analysis

## Security Tools

### SAST Tools
- **SonarQube** - Code security scanning
- **Checkmarx** - Source code security
- **Fortify** - Application security
- **CodeQL** - Code query and analysis

### DAST Tools
- **OWASP ZAP** - Dynamic security scanner
- **Burp Suite** - Web application security testing
- **Nessus** - Vulnerability scanner
- **OpenVAS** - Vulnerability scanner

### SCA Tools
- **Snyk** - Dependency vulnerabilities
- **Trivy** - Container and dependency scanning
- **Dependency-Check** - Dependency audit
- **npm audit / pip-audit** - Package manager audits

### IAST Tools
- **Contrast Security** - Interactive security testing
- **Fortify IAST** - Runtime security analysis
- **AppSec** - Application security

### Other Tools
- **Gitleaks** - Secret scanning
- **TruffleHog** - Secret scanning
- **GitGuardian** - Secret detection
- **Bandit** - Python security scanning
- **ESLint Security** - JavaScript security

## Security Audit Process

### Phase 1: Planning
1. Define scope
2. Identify testing goals
3. Select tools
4. Set up testing environment

### Phase 2: Discovery
1. Information gathering
2. Application mapping
3. Technology identification
4. Attack surface analysis

### Phase 3: Testing
1. Run SAST scans
2. Run DAST scans
3. Run dependency scans
4. Manual security testing

### Phase 4: Analysis
1. Review findings
2. Assess risk levels
3. Prioritize vulnerabilities
4. Recommend remediation

### Phase 5: Reporting
1. Generate security report
2. Document findings
3. Provide remediation guidance
4. Track remediation status

## Vulnerability Classification

### Severity Levels
- **Critical** - Immediate exploit, system compromise
- **High** - Significant impact, requires patch
- **Medium** - Moderate impact, should patch
- **Low** - Minor impact, nice to fix
- **Info** - Informational, no risk

### CVSS Scoring
Use Common Vulnerability Scoring System (CVSS):
- Base score (intrinsic qualities)
- Temporal score (exploitability)
- Environmental score (impact to organization)

## Security Best Practices

### Development
- **Never trust user input**
- **Use parameterized queries**
- **Validate all inputs**
- **Use HTTPS only**
- **Implement proper authentication**
- **Implement proper authorization**
- **Use strong encryption**
- **Manage secrets properly**
- **Log security events**
- **Keep dependencies updated**

### Deployment
- **Use security-hardened images**
- **Scan containers for vulnerabilities**
- **Use network segmentation**
- **Implement firewalls**
- **Use WAF**
- **Enable security monitoring**
- **Configure proper SSL/TLS**
- **Implement rate limiting**
- **Use security headers**
- **Enable audit logging**

### Operations
- **Monitor for security events**
- **Respond to incidents quickly**
- **Regular security audits**
- **Penetration testing**
- **Red team exercises**
- **Security training**
- **Compliance monitoring**
- **Incident response planning**

## Output Format

Generate security reports with:

```markdown
# Security Audit Report

## Executive Summary
[High-level overview of findings]

## Scope
[What was tested and why]

## Methodology
[Tools and techniques used]

## Findings
| ID | Severity | Title | Description | Recommendation |
|-----|----------|-------|-------------|----------------|
| 1   | Critical | SQL Injection | ... | ... |

## Compliance
[Compliance status with standards]

## Remediation
[Step-by-step remediation plan]

## Timeline
[Recommended remediation timeline]
```

## Quality Checklist

- [ ] All OWASP Top 10 tested
- [ ] SAST scan completed
- [ ] DAST scan completed
- [ ] Dependency scan completed
- [ ] Manual testing completed
- [ ] Findings documented
- [ ] Recommendations provided
- [ ] Remediation plan created

## Related Skills

- **Code Development**: Implement security fixes
- **Architecture Design**: Design secure architecture
- **Deployment**: Secure deployment practices
- **Monitoring**: Security monitoring
