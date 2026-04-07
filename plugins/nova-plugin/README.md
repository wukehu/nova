# Nova Plugin - Multi-Dimensional Template System

> **灵活的多维度模板系统**：支持工作流、阶段、语言、规则的自由组合

## 🚀 快速开始 - 简单命令示例

Nova Plugin 提供了一套简单易用的命令，让你可以直接启动各个工作流阶段：

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

### 场景示例

#### 场景 1: 快速开发 Web 应用
```bash
# 1. 先澄清需求
/clarify-requirements "Build a simple task manager"

# 2. 分析需求
/analyze-requirements

# 3. 设计架构
/design-architecture

# 4. 详细设计
/detail-design

# 5. 开始编码
/dev-code
```

#### 场景 2: 修复 Bug
```bash
# 调试和修复问题
/debug-test "User login fails with invalid credentials"
```

#### 场景 3: 完善文档
```bash
# 生成项目文档
/generate-docs "all"
```

## 核心特性

Nova Plugin 不是一个传统的固定命令插件，而是一个**多维度模板系统**。

### 🎯 四个维度

```
┌─────────────────────────────────────────────────────┐
│  Nova Plugin Multi-Dimensional Template System    │
├─────────────────────────────────────────────────────┤
│                                                      │
│  工作流维度 (Workflows)                              │
│  ├─ sdlc-full       - 完整 SDLC (6 阶段)             │
│  ├─ sdlc-lite       - 轻量原型 (3 阶段)              │
│  ├─ bug-fix         - Bug 修复流程                   │
│  └─ performance-opt - 性能优化 (4 阶段)              │
│                                                      │
│  阶段维度 (Phases)                                   │
│  ├─ requirements       - 需求澄清                    │
│  ├─ architecture-design- 架构设计 (含SOLID等原则)   │
│  ├─ detail-design      - 详细设计 (API/数据模型)     │
│  ├─ code               - 代码开发                    │
│  ├─ test               - 测试                        │
│  ├─ review             - 代码审查                    │
│  ├─ docs               - 文档生成                    │
│  ├─ perf-analyze       - 性能分析                    │
│  ├─ perf-optimize      - 性能优化                    │
│  ├─ perf-benchmark     - 基准测试                    │
│  └─ perf-validate      - 验证监控                    │
│                                                      │
│  语言维度 (Languages)                                │
│  ├─ Python      - FastAPI, Django, Flask           │
│  ├─ JavaScript  - React, Vue, Node.js               │
│  ├─ Java        - Spring Boot, Quarkus              │
│  ├─ Go          - Gin, Echo                         │
│  ├─ C           - libmicrohttpd, libevent           │
│  ├─ C++         - Drogon, Oat++, Boost.Asio         │
│  └─ Rust        - Actix-web, Axum, Tokio            │
│                                                      │
│  规则维度 (Rules)                                    │
│  ├─ security      - 安全规则                        │
│  ├─ clean-code    - 代码质量                        │
│  ├─ performance   - 性能优化                        │
│  └─ testing       - 测试规则                        │
│                                                      │
└─────────────────────────────────────────────────────┘
```

## 快速开始

### 自动文档生成 + 人工审核

Nova Plugin 会自动为每个阶段生成文档并进行人工审核跟踪：

```bash
/workflow start sdlc-full

# 自动生成文档并请求审核：
# Phase 1: 需求 → docs/requirements/requirements_20260321_143000.md
#   → 自动请求审核
#   → 审核人开始审核
#   → 审核完成并记录审核信息
```

### 审核信息示例

每个文档包含完整的人工审核信息：

```markdown
## 人工审核信息

> **审核状态**: 已通过
> - **审核人**: 张三 (架构审核员)
> - **审核开始时间**: 2026-03-21 14:30:00
> - **审核结束时间**: 2026-03-21 15:45:00
> - **审核用时**: 1小时15分钟
> - **审核评分**: 87/100

### 审核详情

| 项目 | 内容 |
|------|------|
| **审核人** | 张三 |
| **审核角色** | 架构审核员 |
| **审核开始** | 2026-03-21 14:30:00 |
| **审核结束** | 2026-03-21 15:45:00 |
| **审核用时** | 1小时15分钟 |
| **审核状态** | 已通过 |

### 架构审核评分

| 评分项 | 分数 | 说明 |
|--------|------|------|
| 设计完整性 | 9/10 | 完整，覆盖所有组件 |
| 技术可行性 | 8/10 | 可行，需注意性能 |
| 可扩展性 | 9/10 | 扩展性良好 |
| 安全性 | 8/10 | 安全措施到位 |
| 性能考虑 | 9/10 | 性能考虑充分 |
| **总分** | **87/100** | |

### 审核意见

**✅ 通过的方面:**
- 架构设计完整清晰
- 技术栈选择合理
- 安全考虑周全

**⚠️ 需要改进的方面:**
- 建议增加缓存策略的详细说明
- 部分组件接口可以进一步优化
```

### 审核管理命令

```bash
# 请求审核
/review request

# 查看审核状态
/review status

# 查看审核指标
/review metrics

# 审核历史
/review history requirements_20260321_143000.md
```

## 自动文档生成

Nova Plugin 会自动为每个阶段生成时间戳命名的文档：

```bash
/workflow start sdlc-full

# 自动生成文档到 docs/ 目录：
# docs/requirements/requirements_20260321_143000.md
# docs/architecture/architecture_20260321_150530.md
# docs/design/detail_design_20260321_163045.md
# ...
```

### 场景 1: 快速 Web 原型

```bash
/workflow use sdlc-lite
/config lang javascript
/config framework react
/config rules clean-code
/workflow start
```

### 场景 2: 企业级 API 服务

```bash
/workflow use sdlc-full
/config lang python
/config framework fastapi
/config rules security,clean-code,performance
/workflow start
```

### 场景 3: Bug 修复

```bash
/workflow use bug-fix
/workflow start --from-diagnosis bug-report.md
```

### 场景 4: 性能优化

```bash
/workflow use performance-opt
/workflow start
```

### 场景 5: 系统级应用 (C/C++)

```bash
/workflow use sdlc-full
/config lang cpp
/config framework drogon
/config rules security,performance
/workflow start
```

### 场景 6: 高性能服务 (Rust)

```bash
/workflow use sdlc-full
/config lang rust
/config framework actix-web
/config rules performance
/workflow start
```

## 项目结构

```
nova-plugin/
├── workflows/              # 工作流模板
│   ├── sdlc-full.yaml
│   ├── sdlc-lite.yaml
│   ├── bug-fix.yaml
│   └── performance-opt.yaml
├── phases/                 # 阶段模板
│   ├── requirements.md
│   ├── architecture-design.md
│   ├── detail-design.md
│   ├── code.md
│   ├── test.md
│   ├── review.md
│   ├── docs.md
│   ├── perf-analyze.md
│   ├── perf-optimize.md
│   ├── perf-benchmark.md
│   └── perf-validate.md
├── templates/              # 文档模板
│   └── docs/
│       ├── requirements.md
│       ├── architecture.md
│       ├── detail-design.md
│       ├── INDEX.md
│       └── ...
├── lang/                   # 语言配置
│   ├── python.yaml
│   ├── javascript.yaml
│   ├── java.yaml
│   ├── go.yaml
│   ├── c.yaml
│   ├── cpp.yaml
│   └── rust.yaml
├── rules/                  # 规则集
│   ├── security.yaml
│   ├── clean-code.yaml
│   ├── performance.yaml
│   └── testing.yaml
├── config/                 # 配置文件
│   └── document-output.yaml
├── skills/                 # 技能定义
│   ├── document-generator/ # 文档生成技能
│   └── ...
└── commands/
    ├── workflow.md         # 工作流执行
    └── template.md         # 模板管理
```

## 自动文档生成

### 文档输出规范

每个工作流阶段会自动生成：

**输出格式**: Markdown (.md)
**目录结构**: docs/{phase}/
**文件命名**: {phase}_{timestamp}.md
**时间戳格式**: YYYYMMDD_HHMMSS

### 生成的文档

```
docs/
├── requirements/
│   └── requirements_20260321_143000.md
├── architecture/
│   ├── architecture_20260321_150530.md
│   └── adr/
│       ├── adr_001_use_fastapi.md
│       └── adr_002_database_choice.md
├── design/
│   ├── detail_design_20260321_163045.md
│   ├── api/
│   │   └── api_v1_20260321_163045.md
│   └── database/
│       └── schema_20260321_163045.md
├── implementation/
│   └── implementation_notes_20260321_173000.md
├── testing/
│   ├── test_report_20260321_180000.md
│   └── coverage/
│       └── coverage_20260321_180000.md
├── review/
│   └── code_review_20260321_190000.md
├── user/
│   └── user_guide_20260321_200000.md
└── performance/
    ├── performance_analysis_20260321_210000.md
    ├── optimization_plan_20260321_220000.md
    ├── benchmark_results_20260321_230000.md
    └── performance_validation_20260321_240000.md
```

### 文档内容

每个文档包含：
- 标准化头部（版本、日期、作者、状态）
- 目录和章节
- 变更历史
- 元数据

## 命令

### /workflow - 工作流执行

```bash
/workflow use <template>        # 选择工作流模板
/workflow start                  # 开始工作流
/workflow start --from <phase>   # 从特定阶段开始
/workflow status                 # 查看状态
/workflow next                   # 执行下一阶段
```

**可用工作流：**
- `sdlc-full` - 完整 SDLC (requirements → design → code → test → review → docs)
- `sdlc-lite` - 轻量原型 (requirements → code → test)
- `bug-fix` - Bug 修复 (diagnose → fix → verify → regression-test)
- `performance-opt` - 性能优化 (analyze → optimize → benchmark → validate)

### /template - 模板管理

```bash
/template list                   # 列出所有模板
/template show <name>            # 显示模板详情
/template use <name>             # 使用模板
/template create <name>          # 创建自定义模板
```

## 模板示例

### 工作流模板

```yaml
# workflows/sdlc-full.yaml
name: "sdlc-full"
phases:
  - id: "requirements"
    prompt: "phases/requirements.md"
    required: true
  - id: "design"
    prompt: "phases/design.md"
    required: true
  - id: "code"
    prompt: "phases/code.md"
    required: true
```

### 语言配置

```yaml
# lang/python.yaml
name: "python"
version: "3.12+"
frameworks:
  web:
    - name: "fastapi"
      templates: ["api-endpoint", "pydantic-model"]
```

### 规则集

```yaml
# rules/security.yaml
name: "security"
rules:
  - id: "SEC001"
    name: "Injection Prevention"
    check:
      - "Use parameterized queries"
      - "Validate user input"
```

## 扩展性

### 添加新工作流

```yaml
# workflows/mobile-app.yaml
name: "mobile-app"
extends: "sdlc-full"
phases:
  - id: "ui-design"
    insert_after: "design"
```

### 添加新语言

```yaml
# lang/rust.yaml
name: "rust"
version: "1.70+"
frameworks:
  web: ["actix-web", "axum"]
```

### 添加新规则

```yaml
# rules/reliability.yaml
name: "reliability"
rules:
  - "Implement circuit breakers"
  - "Add retry logic"
```

## 对比传统命令

| 特性 | 传统固定命令 | Nova 多维度系统 |
|------|-------------|----------------|
| 工作流 | ❌ 固定流程 | ✅ 可选择/自定义 |
| 语言支持 | ❌ 硬编码 | ✅ 配置文件 |
| 代码规范 | ❌ 内置规则 | ✅ 可插拔规则集 |
| 扩展性 | ❌ 需改代码 | ✅ 添加配置文件 |
| 组合能力 | ❌ 无法组合 | ✅ 4 维度自由组合 |

## 技术细节

### 模板变量系统

模板支持变量替换和条件逻辑：

```markdown
# Implementing {{project_name}}

{{#python}}
Use Python best practices:
- Type hints
- Docstrings
{{/python}}

{{#javascript}}
Use JavaScript best practices:
- Arrow functions
- Async/await
{{/javascript}}
```

### 配置优先级

1. 项目配置 (`.claude/config.yaml`)
2. 用户配置 (`~/.config/Claude/nova/config.yaml`)
3. 默认配置

## 最佳实践

1. **从简单开始**：使用 `sdlc-lite` + 默认配置
2. **逐步定制**：根据需要添加维度
3. **复用模板**：在团队间共享配置
4. **版本控制**：将配置提交到代码库
5. **文档化**：记录自定义配置的用途

## 贡献

欢迎贡献！可以添加：
- 更多工作流模板
- 更多语言支持
- 更多规则集
- 更好的文档

## 许可证

MIT License

## 链接

- [主仓库文档](../../README.md)
- [架构文档](../../ARCHITECTURE.md)
- [变更日志](CHANGELOG.md)
