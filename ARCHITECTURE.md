# Nova Plugin - Multi-Dimensional Template System

> 灵活的多维度模板系统，支持工作流、阶段、语言、规则的自由组合

## 核心理念

Nova Plugin 采用**多维度模板系统**，不同于传统的固定命令模式，它允许用户在不同维度上自由组合：

1. **工作流维度** (Workflows) - 定义开发流程
2. **阶段维度** (Phases) - 定义各阶段任务
3. **语言维度** (Languages) - 定义语言特性
4. **规则维度** (Rules) - 定义代码规范

## 架构对比

### 传统架构（固定命令）

```
commands/
├── clarify.md
├── design.md
└── code.md
```

**问题**：
- ❌ 每个命令功能固定
- ❌ 无法组合不同维度
- ❌ 添加新功能需要新命令
- ❌ 不支持个性化定制

### Nova 多维度架构

```
nova-plugin/
├── workflows/          # 工作流维度
│   ├── sdlc-full.yaml
│   ├── sdlc-lite.yaml
│   └── bug-fix.yaml
├── phases/             # 阶段维度
│   ├── requirements.md
│   ├── design.md
│   └── code.md
├── lang/               # 语言维度
│   ├── python.yaml
│   ├── javascript.yaml
│   └── java.yaml
└── rules/              # 规则维度
    ├── security.yaml
    └── clean-code.yaml
```

**优势**：
- ✅ 灵活组合 4 个维度
- ✅ 轻松扩展新维度
- ✅ 支持用户自定义
- ✅ 适应不同场景

## 使用示例

### 场景 1: 快速开发 Web 应用

```bash
# 选择工作流
/workflow use sdlc-lite

# 选择语言
/config lang javascript

# 选择框架
/config framework react

# 选择规则
/config rules clean-code

# 开始开发
/workflow start
```

### 场景 2: 企业级 API 服务

```bash
# 完整 SDLC
/workflow use sdlc-full

# Python + FastAPI
/config lang python
/config framework fastapi

# 严格规则
/config rules security,clean-code,performance

/workflow start
```

### 场景 3: Bug 修复

```bash
# Bug 修复工作流
/workflow use bug-fix

# 继承项目语言配置
/workflow start --from-diagnosis bug-report.md
```

## 模板变量系统

模板支持变量替换和条件逻辑：

```yaml
# workflow.yaml
variables:
  project_name: "MyApp"
  language: "python"
  framework: "fastapi"
```

```markdown
<!-- phase template -->
# Implementing {{project_name}}

{{#python}}
Use Python best practices:
- Type hints
- Docstrings
- Context managers
{{/python}}

{{#javascript}}
Use JavaScript best practices:
- Arrow functions
- Async/await
- Template literals
{{/javascript}}
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
# rules/performance.yaml
name: "performance"
rules:
  - "Avoid O(n²) algorithms"
  - "Use caching"
  - "Optimize database queries"
```

## 模板引擎

模板引擎负责：
1. 解析 YAML 配置
2. 加载对应的模板文件
3. 应用变量替换
4. 执行条件逻辑
5. 生成最终输出

```
用户输入
    ↓
选择工作流 → 选择阶段 → 选择语言 → 选择规则
    ↓
模板引擎组合
    ↓
生成个性化指导
```

## 配置示例

### 项目配置 (.claude/config.yaml)

```yaml
workflow: "sdlc-full"
language: "python"
framework: "fastapi"
rules:
  - security
  - clean-code

variables:
  project_name: "MyAPI"
  team_size: 3
  timeline: "8 weeks"
```

### 阶段覆盖

```yaml
# 自定义某个阶段
phases:
  code:
    template: "phases/code-custom.md"
    skip_tests: false
    coverage: 90
```

## 优势总结

| 特性 | 传统固定命令 | Nova 多维度系统 |
|------|-------------|----------------|
| 灵活性 | ❌ 固定 | ✅ 可组合 |
| 扩展性 | ❌ 需修改代码 | ✅ 添加配置文件 |
| 个性化 | ❌ 一刀切 | ✅ 按需定制 |
| 场景适应 | ❌ 有限 | ✅ 无限组合 |
| 学习成本 | ✅ 简单 | ⚠️ 需要理解维度 |

## 最佳实践

1. **从简单开始**：使用 `sdlc-lite` + 默认配置
2. **逐步定制**：根据需要添加维度
3. **复用模板**：在团队间共享配置
4. **版本控制**：将配置提交到代码库
5. **文档化**：记录自定义配置的用途

## 路线图

- [ ] 更多预设工作流（data-pipeline, ml-model, etc）
- [ ] 更多语言支持（Rust, Ruby, PHP）
- [ ] 更多规则模板（testing, documentation）
- [ ] 可视化配置界面
- [ ] 模板市场（分享和发现模板）
- [ ] AI 辅助配置生成

---

这个架构实现了你早期设计的灵活性，同时保持了易用性。通过多维度组合，可以适应几乎任何开发场景。
