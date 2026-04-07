# Nova Plugin 2.0 - 标准开发模板系统

> **通用软件开发底座 + 智能化模板系统 = 全流程、全栈、全语言**

---

## 🚀 快速开始

Nova 2.0 提供了一套简单易用的命令，让你可以直接启动各个工作流阶段：

```bash
# 📝 需求澄清 - 深入理解需求
/clarify-requirements "Build a todo app"

# 📊 需求分析 - 拆解需求为用户故事和用例
/analyze-requirements [requirements-doc.md]

# 🏗️ 架构设计 - 设计多种架构方案
/design-architecture [requirements]

# 📐 详细设计 - 设计 API、数据模型和接口
/detail-design [architecture-design]

# 💻 代码开发 - 实现功能
/dev-code [design-document]

# 🐛 测试调试 - 调试和修复问题
/debug-test [issue-description]

# 📚 文档生成 - 生成完整文档
/generate-docs [scope]
```

## 🎯 核心特性

Nova 2.0 是一个**标准开发模板系统**，而非虚拟团队助手。它通过多维度组合，让团队遵循最佳实践：

> **"标准化 + 灵活性 = 高质量 + 高效率"**

---

## 🔧 四个维度

```
┌─────────────────────────────────────────────────────┐
│  Nova 2.0 - 标准开发模板系统              │
├─────────────────────────────────────────────────────┤
│                                                        │
│  🎯 工作流维度 (Workflows)                          │
│  ├─ sdlc-full       - 完整 SDLC (12 阶段)            │
│  ├─ sdlc-lite       - 轻量原型 (3 阶段)                 │
│  ├─ bug-fix         - Bug 修复流程                        │
│  ├─ feature-dev     -   功能开发流程                       │
│  ├─ hotfix         - 紧急修复流程                        │
│  └─ performance-opt - 性能优化 (4 阶段)                │
│                                                        │
│  📋 阶段维度 (Phases)                                │
│  ├─ requirements       - 需求分析                      │
│  ├─ architecture-design - 架构设计                      │
│  ├─ detail-design      - 详细设计 (API/数据模型)         │
│  ├─ frontend-dev     - 前端开发                      │
│  ├─ backend-dev      - 后端开发                       │
│  ├─ integration       - 集成开发                       │
│  ├─ unit-test        - 单元测试                        │
│  ├─ integration-test  - 集成测试                        │
│   - e2e-test        - 端到端测试                      │
│  ├─ security-audit   - 安全审计                        │
│  ├─ performance-test - 性能测试                        │
│  ├─ code-review      - 代码审查                        │
│  ├─ deploy          - 部署                           │
│  ├─ monitor         - 监控配置                        │
│  └─ document         - 文档生成                        │
│                                                        │
│  🔧 技术栈维度 (Tech Stack) - 新增              │
│  │                                                        │
│  │  前端 (Frontend)                                    │
│  │  ├─ React        - TypeScript, Next.js, Tailwind      │
│  │  ├─ Vue          - Vue 3, Nuxt, Pinia           │
│  │  ├─ Svelte       - SvelteKit, SvelteStore         │
│  │  └─ Native       - React Native, Flutter           │
│  │                                                        │
│  │  后端 (Backend)                                       │
│  │  ├─ Python       - FastAPI, Django, Flask           │
│  │  ├─ Node.js      - Express, NestJS, Koa          │
│  │  ├─ Java         - Spring Boot, Quarkus            │
│  │  ├─ Go           - Gin, Echo, Fiber               │
│  │  ├─ Rust         - Actix, Axum, Tokio            │
│  │  ├─ C++          - Drogon, Oat++, Boost.Asio      │
│  │  └─ C            - libmicrohttpd, libevent           │
│  │                                                        │
│  │ 数据库 (Database)                                    │
│  │  ├─ Relational    - PostgreSQL, MySQL, SQLite       │
│  │  ├─ NoSQL        - MongoDB, Redis, Cassandra      │
│  │  └─ Graph        - Neo4j, ArangoDB              │
│  │                                                        │
│  │ 测试 (Testing)                                       │
│  │  ├─ Unit         - pytest, Jest, JUnit, Go test    │
│  │  ├─ Integration  - Testcontainers, Mock             │
│  │  └─ E2E          - Playwright, Cypress, Selenium    │
│  │                                                        │
│  │ 部署 (Deployment)                                   │
│  │  ├─ Docker       - Compose, Swarm, K8s           │
│  │  ├─ Cloud        - AWS, GCP, Azure               │
│  │  └─ CI/CD        - GitHub Actions, GitLab CI      │
│  │                                                        │
│  ✅ 规则维度 (Rules)                                    │
│  ├─ security      - OWASP Top 10, 认证/授权        │
│  ├─ clean-code    - SOLID, DRY, 命名规范            │
│  ├─ performance   - 缓存, 异步, 查询优化          │
│  └─ testing       - 测试金字塔, TDD, 覆盖率   │
│  └─ documentation  - API 文档, 代码注释, README      │
│                                                        │
└─────────────────────────────────────────────────────┘
```

---

## 🚀 快速开始示例

### 场景 1: 快速 Web 应用（React + FastAPI）

```bash
# 1. 选择工作流
/workflow use sdlc-lite

# 2. 配置语言和框架（Nova 1.0 方式）
/config lang python
/config framework django
/config rules clean-code

# 3. 开始开发
/workflow start
```

### 场景 2: 企业级 API 服务（Python）

```bash
# 1. 使用完整 SDLC
/workflow use sdlc-full

# 2. 配置技术栈（Nova 2.0 方式）
/config tech-stack python-fastapi

# 3. 配置规则
/config rules clean-code,security,performance,testing,documentation

# 4. 开始开发
/workflow start
```

### 场景 3: Bug 修复

```bash
# 1. 使用 Bug 修复工作流
/workflow use bug-fix

# 2. 开始修复（从诊断报告开始）
/workflow start --from-diagnosis bug-report.md
```

### 场景 4: 高性能微服务（Rust）

```bash
# 1. 使用微服务工作流
/workflow use microservice

# 2. 使用 Rust 技术栈
/config tech-stack rust-actix-postgresql

# 3. 配置性能和安全规则
/config rules performance,security,clean-code

# 4. 开始开发
/workflow start
```

### 场景 5: 数据管道开发

```bash
# 1. 使用数据管道工作流
/workflow use data-pipeline

# 2. 配置 Python 技术栈
/config tech-stack python-spark-airflow

# 3. 开始开发
/workflow start
```

---

## 🎯 技术栈预设

Nova 2.0 提供了多种经过验证的技术栈预设：

### 前端 + 后端全栈

| 名称 | 前端 | 后端 | 数据库 | 测试 | 部署 |
|------|------|------|--------|------|------|
| **react-fastapi** | React | FastAPI | PostgreSQL | Vitest/Playwright | Docker/K8s |
| **vue-spring** | Vue | Spring Boot | PostgreSQL | Vitest/Cypress | Docker/K8s |
| **svelte-go** | Svelte | Go | PostgreSQL | Vitest/Playwright | Docker/K8s |
| **rust-actix-postgresql** | - | Rust + Actix | PostgreSQL | Rust test/Playwright | Docker/K8s |

### 后端专用栈

| 名称 | 语言 | 框架 | 数据库 | 测试 | 部署 |
|------|------|------|--------|------|------|
| **python-fastapi** | Python | FastAPI | PostgreSQL | Pytest/Playwright | Docker/K8s |
| **java-spring** | Java | Spring Boot | PostgreSQL | JUnit5/REST Assured | Docker/K8s |
| **node-express** | Node.js | Express | PostgreSQL | Jest/Playwright | Docker/K8s |
| **go-gin** | Go | Gin | PostgreSQL | Go test/Playwright | Docker/K8s |

### 微服务架构

| 名称 | 特性 |
|------|------|
| **microservice** | API-first、事件驱动、服务发现、断路器、可观测性、安全、K8s、语言无关 |

---

## 📋 完整 SDLC 工作流

Nova 2.0 的完整 SDLC 工作流包含 12 个阶段：

1. **需求分析** (Requirements)
   - 需求澄清
   - 需求分析

2. **架构设计** (Architecture Design)
   - 架构设计
   - 创建 ADR

3. **详细设计** (Detail Design)
   - 详细设计
   - API 规范
   - 数据模型

4. **项目初始化** (Setup)
   - 前端设置
   - 后端设置
   - 数据库设置
   - 测试设置

5. **前端开发** (Frontend Development)
   - 环境设置
   - 实现组件
   - 实现页面
   - 编写前端测试
   - Linting

6. **后端开发** (Backend Development)
   - 环境设置
   - 实现模型
   - 实现服务
   - 实现 API 端点
   - 编写后端测试
   - Linting
   - 类型检查

7. **集成开发** (Integration)
   - 集成前后端
   - 编写集成测试

8. **单元测试** (Unit Tests)
   - 运行前端单元测试
   - 运行后端单元测试
   - 检查覆盖率

9. **集成测试** (Integration Tests)
   - 运行集成测试
   - 测试 API 契约

10. **端到端测试** (E2E Tests)
   - 设置 E2E 环境
   - 编写 E2E 测试
   - 运行 E2E 测试

11. **安全审计** (Security Audit)
   - 运行安全扫描
   - 检查漏洞
   - 生成安全报告

12. **性能测试** (Performance Tests)
   - 建立性能基线
   - 运行负载测试
   - 分析性能

13. **代码审查** (Code Review)
   - 自我审查
   - 同伴审查
   - 检查代码规范
   - 检查类型安全

14. **部署** (Deploy)
   - 构建 Docker 镜像
   - 在 Docker 中运行测试
   - 部署到暂存环境
   - 运行冒烟测试
   - 推广到生产环境

15. **监控配置** (Monitor)
   - 设置监控
   - 配置告警
   - 设置日志
   - 创建仪表板

16. **文档生成** (Document)
   - 生成 API 文档
   - 生成用户指南
   - 生成开发者指南
   - 更新 CHANGELOG

---

## 🎯 质量保证

Nova 2.0 通过质量门禁确保代码质量：

### 自动质量检查

- ✅ **测试覆盖率** - 目标 80%+
- ✅ **安全扫描** - OWASP Top 10 检查
- ✅ **代码规范** - Linting、类型检查、格式化
- ✅ **性能基准** - 确保无性能回归

### 质量门禁配置

```yaml
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
```

---

## 🔧 命令系统

### 工作流命令

```bash
/workflow use <template>        # 选择工作流模板
/workflow start                  # 开始工作流
/workflow start --from <phase>   # 从特定阶段开始
/workflow status                 # 查看状态
/workflow next                   # 执行下一阶段
```

### 技术栈配置命令

```bash
/config tech-stack <[preset]>      # 选择技术栈预设（可选）
/config rules <rules>             # 选择规则集
/config variables                  # 配置变量
```

**可用技术栈预设**：
- `react-fastapi` - React + FastAPI
- `vue-spring` - Vue + Spring Boot
- `python-fastapi` - Python + FastAPI
- `java-spring` - Java + Spring Boot
- `go-gin` - Go + Gin
- `rust-actix-postgresql` - Rust + Actix + PostgreSQL
- `microservice` - 通用微服务架构

### 发布命令

```bash
/ship [message]                 # 同步、测试、推送、创建 PR
```

### 审查管理命令

```bash
/review request                   # 请求审核
/review status                     # 查看审核状态
/review metrics                    # 查看审核指标
```

---

## 📚 项目结构

```
nova-plugin/
├── workflows/              # 工作流模板
│   ├── sdlc-full.yaml
│   ├── sdlc-lite.yaml
│   ├── bug-fix.yaml
│   ├── feature-dev.yaml
│   ├── hotfix.yaml
│   ├── data-pipeline.yaml
│   └── performance-opt.yaml
├── phases/                 # 阶段模板
│   ├── requirements.md
│   ├── architecture-design.md
│   ├── detail-design.md
│   ├── code.md
│   ├── test.md
│   └── ...
├── tech-stacks/             # 技术栈配置
│   ├── python-fastapi.yaml
│   ├── react-fastapi.yaml
│   ├── java-spring.yaml
│   ├── go-gin.yaml
│   ├── rust-actix-postgresql.yaml
│   ├── cpp-drogon.yaml
│   ├── c.yaml
│   ├── microservice.yaml
└── rules/                  # 规则集
│   ├── security.yaml
│   ├── clean-code.yaml
│   ├── performance.yaml
│   └── testing.yaml
│   └── documentation.yaml
├── templates/               # 文档模板
│   └── docs/
│       ├── requirements.md
│       ├── architecture.md
│       └── detail-design.md
│       └── INDEX.md
├── skills/                 # 技能定义
└── commands/               # 命令实现
│   ├── workflow/
│   │   ├── start.md
│   │   └── template/
│   └── config/
│   │   ├── tech-stack.md
│   │   └── rules.md
│   └── ship/
└── config/                 # 配置文件
```

---

## 📚 自动文档生成

Nova 2.0 会自动为每个阶段生成时间戳命名的文档：

```bash
/workflow start sdlc-full

# 自动生成文档到 docs/ 目录：
# docs/requirements/requirements_20260407_143000.md
# docs/architecture/architecture_20260407_150530.md
# docs/design/detail_design_20260407_163045.md
# docs/implementation/implementation_notes_20260407_173000.md
# docs/testing/test_report_20260407_180000.md
# docs/review/code_review_20260407_190000.md
# docs/user/user_guide_20260407_200000.md
```

---

## 🎯 最佳实践

### 模板设计

1. **标准化但不僵化**：每个模板遵循标准但允许定制
2. **可组合**：通过维度组合适应不同场景
3. **经过验证**：每个模板都经过实际项目验证
4. **文档完善**：每个模板都有详细的文档和示例

### 开发流程

1. **遵循模板**：选择模板并遵循其工作流
2. **保持灵活**：可以根据项目需要调整
3. **质量优先**：通过质量门禁确保质量
4. **持续改进**：根据反馈持续改进模板

### 团队协作

1. **共享模板**：在团队间共享经过验证的模板
2. **版本控制**：将模板提交到代码库
3. **标准化**：使用相同模板确保一致性
4. **持续学习**：从项目中学习并改进模板

---

## 🎯 扩展性

### 添加新工作流

```yaml
# workflows/mobile-app.yaml
name: "mobile-app"
extends: "sdlc-full"
phases:
  - id: "ui-design"
    insert_after: "design"
  - id: "app-store"
    insert_after: "test"
```

### 添加新语言

```yaml
# lang/rust.yaml
name: "rust"
version: "1.70+"
frameworks:
  web: ["actix-web", "axum"]
  cli: ["clap"]
```

### 添加新规则

```yaml
# rules/reliability.yaml
name: "reliability"
rules:
  - "Implement circuit breakers"
  - "Add retry logic"
```

---

## 📊 与其他插件的对比

| 特性 | 传统固定命令 | Nova 多维度系统 | Nova 2.0 |
|------|-------------|----------------|------------|
| 设计理念 | 固定命令 | 多维度模板系统 | **标准模板系统** |
| 核心理念 | 无系统 | 灵活组合 | 用户主导 + AI 辅助 |
| 工作流 | 固定流程 | 可选模板 | 可选模板 + 智能增强 |
| 语言支持 | 硬编码语言 | 配置文件 | 完整技术栈（前端+后端+数据库+测试+部署） |
| 代码规范 | 无规则 | 可插拔规则集 | **技术栈级 + 规则级** |
| 测试 | 基础测试 | 基础测试模板 | **技术栈测试 + Playwright + CI/CD** |
| 发布 | 无发布命令 | 无统一发布 | **标准化发布流程** |
| 文档 | 手动生成 | 自动文档生成 | **自动生成 + 技术栈提取** |
| 智能化 | 无 | 无 | 无 | 无 | AI 智能辅助（可选） |

---

## 🚀 与 gstack 的对比

| 特性 | Nova 2.0 | gstack |
|------|----------|-------|
| 定位 | **通用底座** | AI 团队工具 |
| 设计理念 | 标准模板系统 | 虚拟团队系统 |
| 核心理念 | 用户主导 | AI 决策 | 用户主导 |
| 工作流 | 可选模板 | 固定流程 |
| 适用范围 | 所有团队 | 单个开发者 |
| 代码质量 | 技术栈规则 | 多角色审查 |
| 测试 | 技术栈测试 + CI/CD | Playwright |

---

## 📈 Nova 2.0 vs gstack

**关键区别**：

| 维度 | Nova 2.0 | gstack |
|------|----------|-------|
| **核心理念** | 标准模板系统 | 虚拟团队系统 |
| **用户主导** | ✅ 用户控制所有关键决策 | ⚠️ AI 辅助（但用户最终确认） |
| **工作流** | 可选模板 + 智能增强 | 固定流程（Think→Plan→Build→Ship） |
| **技术栈** | 配置维度（可选） | 固定流程（强制） |
| **灵活性** | 高 | 中 | 中 |
| **心智负担** | 低 | 高 | 中 |

**最佳结合**：
- ✅ 使用 gstack 的 **完整工作流思想** 作为可选增强
- ✅ 使用 gstack 的 **Playwright 集成** 作为测试增强
- ✅ 使用 gstack 的 **统一发布流程** 作为发布增强
- ✅ 保持 Nova 的 **多维度灵活性** 作为核心
- ✅ 添加 gstack 的 **智能辅助** 作为可选增强

---

## 📖 版本历史

### v1.0.0 - 初始版本
- 基础多维度模板系统
- 支持工作流、阶段、语言、规则 4 个维度

### v2.0.0 - 技术栈维度
- 将语言维度升级为技术栈（前端+后端+数据库+测试+部署）
- 添加了 Python、React、Java、Go、C++、Rust 等技术栈配置

### v2.0.1 - 完善化设计
- 重新设计为"标准开发模板系统"
- 明确了用户主导权的核心理念
- 添加了完善架构文档

### v2.0.2 - 第一版实现
- 实现了技术栈维度系统
- 添加了多个完整的技术栈配置
- 创建了简化命令示例
- 更新了工作流配置以使用技术栈

---

## 📞 许可证

MIT License

## 📔 链接

- [主仓库文档](../../README.md)
- [架构文档](../../ARCHITECTURE.md)
- [Nova 2.0 设计文档](docs/NOVA_2.0_ARCHITECTURE_REDIGN.md)
- [改进方案文档](docs/NOVA_2.0_ARCHITECTURE_DESIGN.md)
- [变更日志](CHANGELOG.md)
