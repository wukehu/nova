---
description: Configure technology stack for project - select preset or customize tech stack
argument-hint: [preset-name]
allowed-tools: [Read, Write, Grep, AskUserQuestion]
---

# Tech Stack Configuration

Configure technology stack for your Nova project. You can use presets or customize.

## Available Presets

Nova 2.0 provides pre-configured technology stacks:

### Frontend + Backend Stacks

**react-fastapi** - React + FastAPI
- Frontend: React 18+, TypeScript, Vite, Tailwind CSS, Zustand
- Backend: Python 3.11+, FastAPI, PostgreSQL, SQLAlchemy
- Testing: Vitest, Pytest, Playwright
- Deployment: Docker, Kubernetes, GitHub Actions

**vue-spring** - Vue + Spring Boot
- Frontend: Vue 3, TypeScript, Vite, Pinia
- Backend: Java 17+, Spring Boot, PostgreSQL, JPA
- Testing: Vitest, JUnit5, Cypress
- Deployment: Docker, Kubernetes, GitLab CI

**svelte-go** - Svelte + Go
- Frontend: SvelteKit, SvelteStore
- Backend: Go 1.21+, Gin, PostgreSQL, GORM
- Testing: Vitest, Go test, Playwright
- Deployment: Docker, Kubernetes, GitHub Actions

**rust-actix-postgresql** - Rust + Actix + PostgreSQL
- Backend: Rust 1.70+, Actix-web, PostgreSQL, Sea-ORM
- Testing: Rust test, Playwright
- Deployment: Docker, Kubernetes, GitHub Actions

### Backend-Only Stacks

**python-fastapi** - Python + FastAPI
- Backend: Python 3.11+, FastAPI, PostgreSQL, SQLAlchemy
- Testing: Pytest, Playwright
- Deployment: Docker, Kubernetes, GitHub Actions

**java-spring** - Java + Spring Boot
- Backend: Java 17+, Spring Boot, PostgreSQL, JPA
- Testing: JUnit5, REST Assured
- Deployment: Docker, Kubernetes, GitHub Actions

**node-express** - Node.js + Express
- Backend: Node.js 20+, Express, PostgreSQL, Prisma
- Testing: Jest, Playwright
- Deployment: Docker, Kubernetes, GitHub Actions

**go-gin** - Go + Gin
- Backend: Go 1.21+, Gin, PostgreSQL, GORM
- Testing: Go test, Playwright
- Deployment: Docker, Kubernetes, GitHub Actions

### Microservice Stacks

**microservice** - Generic Microservice Stack
- Architecture: API-first, event-driven, service discovery
- Communication: REST/gRPC, async messaging (Kafka/RabbitMQ)
- Resilience: Circuit breaker, retry, bulkhead, timeout
- Observability: Structured logging, metrics, tracing
- Security: JWT, RBAC, rate limiting
- Deployment: Docker, Kubernetes, CI/CD
- Language: Agnostic (can be used with any backend)

## Usage

### Option 1: Use a Preset

```bash
# Use React + FastAPI preset
/config tech-stack react-fastapi

# Use Java + Spring preset
/config tech-stack java-spring

# Use generic microservice preset
/config tech-stack microservice
```

This will:
1. Load tech stack configuration file
2. Display tech stack details
3. Ask for confirmation
4. Apply tech stack to current workflow

### Option 2: Customize Tech Stack

```bash
# Enter customization mode
/config tech-stack
```

You will be prompted to configure:
1. Frontend (if full stack)
   - Framework (React, Vue, Svelte)
   - State management
   - Styling
   - UI library

2. Backend
   - Language (Python, Java, Go, Node.js, Rust)
   - Framework (FastAPI, Spring Boot, Express, Gin, Actix)
   - Database (PostgreSQL, MySQL, MongoDB, Redis)
   - ORM (SQLAlchemy, JPA, Prisma, GORM)

3. Testing
   - Unit testing framework
   - Integration testing
   - E2E testing framework
   - Coverage target

4. Deployment
   - Container (Docker)
   - Orchestration (Kubernetes, Docker Compose)
   - CI/CD (GitHub Actions, GitLab CI)

5. Quality Rules
   - Security
   - Clean code
   - Performance
   - Testing
   - Documentation

## Output

After configuration, tech stack is saved to `.claude/tech-stack.yaml`:

```yaml
tech_stack:
  preset: "react-fastapi"
  
  frontend:
    framework: "react"
    language: "typescript"
    build_tool: "vite"
    state_management: "zustand"
    styling: "tailwindcss"
    ui_library: "shadcn/ui"
    
  backend:
    language: "python"
    framework: "fastapi"
    version: "0.104+"
    
  database:
    default: "postgresql"
    options:
      - "postgresql"
      - "mysql"
      - "sqlite"
    
  testing:
    framework: "pytest"
    e2e_framework: "playwright"
    coverage_target: 80
    
  deployment:
    container: "docker"
    orchestration: "kubernetes"
    ci_cd: "github-actions"
    
  rules:
    - "security"
    - "clean-code"
    - "performance"
    - "testing"
```

## Integration with Workflow

After configuring a tech stack, use it with workflow:

```bash
# Select workflow
/workflow use sdlc-full

# Configure tech stack
/config tech-stack react-fastapi

# Start development
/workflow start
```

The workflow will use tech stack configuration to:
- Generate appropriate project structure
- Apply language-specific best practices
- Set up testing framework
- Configure deployment
- Apply quality rules

## View Current Tech Stack

```bash
# View current tech stack configuration
/config tech-stack --status
```

## Reset Tech Stack

```bash
# Reset to default
/config tech-stack --reset
```

## Best Practices

1. **Start with presets**: Use proven tech stack presets for common scenarios
2. **Customize as needed**: Modify presets to fit your requirements
3. **Version control config**: Commit `.claude/tech-stack.yaml` to version control
4. **Share with team**: Include tech stack config in project repository
5. **Update regularly**: Keep tech stack up to date with latest practices

## Examples

### Full Stack Web App

```bash
/config tech-stack react-fastapi
```

### Backend API Service

```bash
/config tech-stack python-fastapi
```

### Microservice

```bash
/config tech-stack microservice
```

### Enterprise Application

```bash
/config tech-stack java-spring
```
