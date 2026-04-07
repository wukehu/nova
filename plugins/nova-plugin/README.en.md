# Nova Plugin 2.0 - Standard Development Template System

> **Ultimate best practices + flexible template system = full-process, full-stack, full-language**

---

## 🚀 Quick Start

Nova 2.0 provides a simple, easy-to-use command set for launching various workflow phases:

**```bash**
# 📝 Requirements Clarification - Deep understanding of requirements
/clarify-requirements "Build a todo app"

# 📊 Requirements Analysis - Break down requirements into user stories and use cases
/analyze-requirements [requirements-doc.md]

# 🏗️ Architecture Design - Design multiple architecture approaches
/design-architecture [requirements]

# 📐 Detail Design - Design APIs, data models, and interfaces
/detail-design [architecture-design]

# 💻 Code Development - Implement features
/dev-code [design-document]

# 🐛 Testing and Debugging - Debug and fix issues
/debug-test [diagnosis]

# 📚 Documentation Generation - Generate complete documentation
/generate-docs [scope]
**```**

## 🎯 Core Features

Nova 2.0 is a **Standard Development Template System** that helps teams follow best practices while maintaining flexibility:

> **"Standardization + Flexibility = High Quality + High Efficiency"**

---

## 🔧 Four Dimensions

**```
┌─────────────────────────────────────────────────────────────┐
│  Nova 2.0 - Standard Development Template System          │
├─────────────────────────────────────────────────────────────┤
│                                                        │
│  🎯 Workflows                                        │
│  ├─ sdlc-full       - Complete SDLC (12 phases)       │
│  ├─ sdlc-lite       - Lightweight prototype (3 phases)     │
│  ├─ bug-fix         - Bug fix workflow                    │
│  ├─ feature-dev     - Feature development workflow          │
│  ├─ hotfix         - Urgent fix workflow                │
│  └─ performance-opt - Performance optimization (4 phases)   │
│                                                        │
│  📋 Phases                                          │
│  ├─ requirements       - Requirements analysis          │
│  ├─ architecture-design - Architecture design              │
│  ├─ detail-design      - Detail design (API/data models)  │
│  ├─ frontend-dev     - Frontend development          │
│  ├─ backend-dev      - Backend development           │
│  ├─ integration       - Integration development        │
│  ├─ unit-test        - Unit testing                │
│  ├─ integration-test  - Integration testing         │
│  ├─ e2e-test        - End-to-end testing          │
│  ├─ security-audit   - Security audit               │
│  ├─ performance-test - Performance testing          │
│  ├─ code-review      - Code review                 │
│  ├─ deploy          - Deployment                  │
│  ├─ monitor         - Monitoring configuration     │
│  └─ document         - Documentation generation     │
│                                                        │
│  🔧 Tech Stack                                  │
│                                                        │
│  Frontend                                             │
│  ├─ React        - TypeScript, Next.js, Tailwind      │
│  ├─ Vue          - Vue 3, Nuxt, Pinia           │
│  ├─ Svelte       - SvelteKit, SvelteStore         │
│  └─ Native       - React Native, Flutter           │
│                                                        │
│  Backend                                            │
│  ├─ Python       - FastAPI, Django, Flask           │
│  ├─ Node.js      - Express, NestJS, Koa          │
│  ├─ Java         - Spring Boot, Quarkus            │
│  ├─ Go           - Gin, Echo, Fiber               │
│  ├─ Rust         - Actix, Axum, Tokio            │
│  └─ C++          - Drogon, Oat++, Boost.Asio      │
│                                                        │
│  Database                                            │
│  ├─ Relational    - PostgreSQL, MySQL, SQLite       │
│  ├─ NoSQL        - MongoDB, Redis, Cassandra      │
│  └─ Graph        - Neo4j, ArangoDB              │
│                                                        │
│  Testing                                             │
│  ├─ Unit         - pytest, Jest, JUnit, Go test    │
│  ├─ Integration  - Testcontainers, Mock             │
│  ├─ E2E          - Playwright, Cypress, Selenium    │
│  └─ Performance  - k6, JMeter, Locust           │
│                                                        │
│  Deployment                                          │
│  ├─ Docker       - Compose, Swarm, K8s           │
│  ├─ Cloud        - AWS, GCP, Azure               │
│  └─ CI/CD        - GitHub Actions, GitLab CI      │
│                                                        │
│  ✅ Rules                                            │
│  ├─ security      - OWASP Top 10, auth/authorization  │
│  ├─ clean-code    - SOLID, DRY, naming conventions   │
│  ├─ performance   - Caching, async, query optimization   │
│  └─ documentation  - API docs, code comments, README    │
│                                                        │
└─────────────────────────────────────────────────────────────┘
**```**

---

## 🚀 Quick Start Examples

### Scenario 1: Quick Web App (React + FastAPI)

**```bash**
# 1. Select workflow
/workflow use sdlc-lite

# 2. Configure language and framework (Nova 1.0 style)
/config lang python
/config framework django
/config rules clean-code

# 3. Start development
/workflow start
**```**

### Scenario 2: Enterprise API Service (Python)

**```bash**
# 1. Use complete SDLC
/workflow use sdlc-full

# 2. Configure tech stack (Nova 2.0 style)
/config tech-stack python-fastapi

# 3. Configure rules
/config rules clean-code,security,performance,testing,documentation

# 4. Start development
/workflow start
**```**

### Scenario 3: Bug Fix

**```bash**
# 1. Use bug fix workflow
/workflow use bug-fix

# 2. Start fix (from diagnosis report)
/workflow start --from-diagnosis bug-report.md
**```**

### Scenario 4: High-Performance Microservice (Rust)

**```bash**
# 1. Use microservice workflow
/workflow use microservice

# 2. Use Rust tech stack
/config tech-stack rust-actix-postgresql

# 3. Configure performance and security rules
/config rules performance,security,clean-code

# 4. Start development
/workflow start
**```**

---

## 🎯 Tech Stack Presets

Nova 2.0 provides multiple validated tech stack presets:

### Frontend + Backend Full Stack

| Name | Frontend | Backend | Database | Testing | Deployment |
|------|----------|---------|----------|---------|------------|
| **react-fastapi** | React | FastAPI | PostgreSQL | Vitest/Playwright | Docker/K8s |
| **vue-spring** | Vue | Spring Boot | PostgreSQL | Vitest/Cypress | Docker/K8s |
| **svelte-go** | Svelte | Go | PostgreSQL | Vitest/Playwright | Docker/K8s |
| **rust-actix-postgresql** | - | Rust + Actix | PostgreSQL | Rust test/Playwright | Docker/K8s |

### Backend-Only Stacks

| Name | Language | Framework | Database | Testing | Deployment |
|------|----------|-----------|----------|---------|------------|
| **python-fastapi** | Python | FastAPI | PostgreSQL | Pytest/Playwright | Docker/K8s |
| **java-spring** | Java | Spring Boot | PostgreSQL | JUnit5/REST Assured | Docker/K8s |
| **node-express** | Node.js | Express | PostgreSQL | Jest/Playwright | Docker/K8s |
| **go-gin** | Go | Gin | PostgreSQL | Go test/Playwright | Docker/K8s |

### Microservice Architecture

| Name | Features |
|------|----------|
| **microservice** | API-first, event-driven, service discovery, circuit breakers, observability, security, K8s, language-agnostic |

---

## 📋 Complete SDLC Workflow

Nova 2.0's complete SDLC workflow includes 12 phases:

1. **Requirements Analysis** (Requirements)
   - Requirements clarification
   - Requirements analysis

2. **Architecture Design** (Architecture Design)
   - Architecture design
   - Create ADR

3. **Detail Design** (Detail Design)
   - Detail design
   - API specification
   - Data model

4. **Project Setup** (Setup)
   - Frontend setup
   - Backend setup
   - Database setup
   - Testing setup

5. **Frontend Development** (Frontend Development)
   - Environment setup
   - Implement components
   - Implement pages
   - Write frontend tests
   - Linting

6. **Backend Development** (Backend Development)
   - Environment setup
   - Implement models
   - Implement services
   - Implement API endpoints
   - Write backend tests
   - Linting
   - Type checking

7. **Integration Development** (Integration)
   - Integrate frontend and backend
   - Write integration tests

8. **Unit Tests** (Unit Tests)
   - Run frontend unit tests
   - Run backend unit tests
   - Check coverage

9. **Integration Tests** (Integration Tests)
   - Run integration tests
   - Test API contracts

10. **End-to-End Tests** (E2E Tests)
    - Setup E2E environment
    - Write E2E tests
    - Run E2E tests

11. **Security Audit** (Security Audit)
    - Run security scans
    - Check vulnerabilities

12. **Performance Tests** (Performance Tests)
    - Establish performance baseline
    - Run load tests
    - Analyze performance

13. **Code Review** (Code Review)
    - Self review
    - Peer review
    - Check code standards
    - Check type safety

14. **Deployment** (Deploy)
    - Build Docker images
    - Run tests in Docker
    - Deploy to staging
    - Run smoke tests
    - Promote to production

15. **Monitoring Configuration** (Monitor)
    - Setup monitoring
    - Configure alerts
    - Setup logging
    - Create dashboards

16. **Documentation Generation** (Document)
    - Generate API documentation
    - Generate user guide
    - Generate developer guide
    - Update CHANGELOG

---

## 🎯 Quality Assurance

Nova 2.0 ensures code quality through quality gates:

### Automated Quality Checks

- ✅ **Test coverage** - Target 80%+
- ✅ **Security scanning** - OWASP Top 10 checks
- ✅ **Code standards** - Linting, type checking, formatting
- ✅ **Performance baseline** - Ensure no performance regression

### Quality Gate Configuration

**```yaml**
# workflow.yaml
quality_gates:
  test_coverage:
    enabled: true
    minimum: 80
    on_stages: ["unit-test", "integration-test"]

  security_scan:
    enabled: true
    on_stages: ["security-audit"]

  code_quality:
    enabled: true
    checks:
      - linting
      - type_checking
      - security_review
    on_stages: ["code-review"]
**```**

---

## 🔧 Command System

### Workflow Commands

**```bash**
/workflow use <template>        # Select workflow template
/workflow start                  # Start workflow
/workflow start --from <phase>   # Start from specific phase
/workflow status                 # View status
/workflow next                   # Execute next phase
**```**

### Tech Stack Configuration Commands

**```bash**
/config tech-stack <[preset]>      # Select tech stack preset (optional)
/config rules <rules>             # Select rule set
/config variables                  # Configure variables
**```**

**Available tech stack presets**:
- `react-fastapi` - React + FastAPI
- `vue-spring` - Vue + Spring Boot
- `python-fastapi` - Python + FastAPI
- `java-spring` - Java + Spring Boot
- `go-gin` - Go + Gin
- `rust-actix-postgresql` - Rust + Actix + PostgreSQL
- `react-native` - React Native mobile apps
- `svelte-go` - SvelteKit + Go
- `node-express` - Node.js + Express
- `microservice` - Generic microservice architecture

### Release Commands

**```bash**
/ship [message]                 # Sync, test, push, create PR
**```**

### Review Management Commands

**```bash**
/review request                   # Request review
/review status                     # View review status
/review metrics                    # View review metrics
**```**

---

## 📚 Project Structure

**```
nova-plugin/
├── workflows/              # Workflow templates
│   ├── sdlc-full.yaml
│   ├── sdlc-lite.yaml
│   ├── bug-fix.yaml
│   ├── feature-dev.yaml
│   ├── hotfix.yaml
│   ├── data-pipeline.yaml
│   └── performance-opt.yaml
├── phases/                 # Phase templates
│   ├── requirements.md
│   ├── architecture-design.md
│   ├── detail-design.md
│   ├── code.md
│   └── test.md
├── tech-stacks/             # Tech stack configs
│   ├── python-fastapi.yaml
│   ├── react-fastapi.yaml
│   ├── java-spring.yaml
│   ├── go-gin.yaml
│   ├── rust-actix-postgresql.yaml
│   ├── cpp-drogon.yaml
│   ├── react-native.yaml
│   ├── svelte-go.yaml
│   ├── node-express.yaml
│   ├── vue-spring.yaml
│   └── microservice.yaml
├── rules/                  # Rule sets
│   ├── security.yaml
│   ├── clean-code.yaml
│   ├── performance.yaml
│   ├── testing.yaml
│   ├── documentation.yaml
│   ├── reliability.yaml
│   ├── scalability.yaml
│   └── accessibility.yaml
├── templates/               # Document templates
│   └── docs/
│       ├── requirements.md
│       ├── architecture.md
│       └── detail-design.md
│       └── INDEX.md
├── skills/                 # Skill definitions
│   ├── requirements-clarification/
│   ├── requirements-analysis/
│   ├── architecture-design/
│   ├── detailed-design/
│   ├── code-development/
│   ├── testing/
│   ├── debugging-testing/
│   ├── security-audit/
│   ├── deployment/
│   ├── monitoring/
│   └── document-generator/
└── commands/               # Command implementations
    ├── workflow.md
    ├── config-tech-stack.md
    └── ship.md
```

---

## 📚 Automatic Documentation Generation

Nova 2.0 automatically generates timestamped documents for each phase:

**```bash**
/workflow start sdlc-full

# Automatically generates documents to docs/ directory:
# docs/requirements/requirements_20260407_143000.md
# docs/architecture/architecture_20260407_150530.md
# docs/design/detail_design_20260407_163045.md
# docs/implementation/implementation_notes_20260407_173000.md
# docs/testing/test_report_20260407_180000.md
# docs/review/code_review_20260407_190000.md
# docs/user/user_guide_20260407_200000.md
**```**

---

## 🎯 Best Practices

### Template Design

1. **Standard but not rigid**: Each template follows standards but allows customization
2. **Composable**: Adapt to different scenarios through dimension combinations
3. **Validated**: Each template is validated through actual projects
4. **Well-documented**: Each template has detailed documentation and examples

### Development Workflow

1. **Follow templates**: Select a template and follow its workflow
2. **Stay flexible**: Adjust according to project needs
3. **Quality first**: Ensure quality through quality gates
4. **Continuous improvement**: Continuously improve templates based on feedback

### Team Collaboration

1. **Share templates**: Share validated templates across the team
2. **Version control**: Commit templates to the code repository
3. **Standardize**: Use the same template to ensure consistency
4. **Continuous learning**: Learn from projects and improve templates

---

## 🎯 Extensibility

### Add New Workflow

**```yaml
# workflows/mobile-app.yaml
name: "mobile-app"
extends: "sdlc-full"
phases:
  - id: "ui-design"
    insert_after: "design"
  - id: "app-store"
    insert_after: "test"
**```**

### Add New Language

**```yaml
# lang/rust.yaml
name: "rust"
version: "1.70+"
frameworks:
  web: ["actix-web", "axum"]
  cli: ["clap"]
**```**

### Add New Rule

**```yaml
# rules/reliability.yaml
name: "reliability"
rules:
  - "Implement circuit breakers"
  - "Add retry logic"
**```**

---

## 📊 Comparison with Other Plugins

| Feature | Traditional Fixed Commands | Nova Multi-Dim System | Nova 2.0 |
|----------|--------------------------|------------------------|-------------|
| Design Philosophy | Fixed commands | Multi-dim template system | **Standard template system** |
| Core Philosophy | No system | Flexible combinations | User-led + AI-assisted |
| Workflow | Fixed process | Optional template | Optional template + AI enhancement |
| Language Support | Hard-coded languages | Config file | Complete tech stack (frontend+backend+database+testing+deployment) |
| Code Standards | No rules | Pluggable rule sets | **Tech stack level + rule level** |
| Testing | Basic test templates | Basic test templates | **Tech stack tests + Playwright + CI/CD** |
| Release | No release command | No unified release | **Standardized release process** |
| Documentation | Manual generation | Auto doc generation | **Auto generation + tech stack extraction** |
| Intelligence | No | No | None | AI intelligent assistance (optional) |

---

## 🚀 Comparison with gstack

| Feature | Nova 2.0 | gstack |
|----------|----------|-------|
| Positioning | **Universal foundation** | AI team tool |
| Design Philosophy | Standard template system | Virtual team system |
| Core Philosophy | User-led | AI decision-making | User-led |
| Workflow | Optional template | Fixed process (Think→Plan→Build→Ship) |
| Applicable Scope | All teams | Individual developer |
| Code Quality | Tech stack rules | Multi-role review |
| Testing | Tech stack tests + CI/CD | Playwright |

---

## 📈 Nova 2.0 vs gstack

**Key Differences**:

| Dimension | Nova 2.0 | gstack |
|----------|----------|-------|
| **Core Philosophy** | Standard template system | Virtual team system |
| **User-Led** | ✅ User controls all key decisions | ⚠️ AI-assisted (but user final confirm) |
| **Workflow** | Optional template + AI enhancement | Fixed process (Think→Plan→Build→Ship) |
| **Tech Stack** | Config dimension (optional) | Fixed process (mandatory) |
| **Flexibility** | High | Medium |
| **Mental Load** | Low | Medium |

**Best Combination**:
- ✅ Use gstack's **complete workflow philosophy** as optional enhancement
- ✅ Use gstack's **Playwright integration** as test enhancement
- ✅ Use gstack's **unified release process** as release enhancement
- ✅ Keep Nova's **multi-dimensional flexibility** as core
- ✅ Add gstack's **intelligent assistance** as optional enhancement

---

## 📖 Version History

### v1.0.0 - Initial Release
- Basic multi-dim template system
- Support for workflow, phase, language, rule 4 dimensions

### v2.0.0 - Tech Stack Dimension
- Upgraded language dimension to tech stack (frontend+backend+database+testing+deployment)
- Added Python, React, Java, Go, C++, Rust tech stack configs

### v2.0.1 - Enhanced Design
- Redesigned as "Standard Development Template System"
- Clarified user-led core philosophy
- Added comprehensive architecture documentation

### v2.0.2 - First Implementation
- Implemented tech stack dimension system
- Added multiple complete tech stack configurations
- Created simplified command examples
- Updated workflow configuration to use tech stack

### v2.0.3 - Comprehensive Enhancement
- Added 6 new tech stack configurations (Vue+Spring, Node.js, Svelte+Go, React Native)
- Added 4 new workflow templates (feature-dev, hotfix, data-pipeline, ml-model)
- Added 4 new rule configurations (documentation, reliability, scalability, accessibility)
- Added 3 new skill definitions (security-audit, deployment, monitoring)
- Created English README for internationalization
- Updated all documentation comments to English

---

## 📞 License

MIT License

## 🔗 Links

- [Main Repository Documentation](../../README.md)
- [Architecture Documentation](../../ARCHITECTURE.md)
- [Nova 2.0 Architecture Design](docs/NOVA_2.0_ARCHITECTURE.md)
- [Chinese README](README.md)
- [Change Log](CHANGELOG.md)
