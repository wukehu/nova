# Nova Plugins - Claude Code Plugin Collection

> **灵活的多维度模板系统**，支持工作流、阶段、语言、规则的自由组合

## 项目简介

Nova Plugins 不是一个传统的固定命令插件，而是一个**多维度模板系统**。它允许开发者在不同维度上自由组合：

- 🔄 **工作流维度**：完整 SDLC、轻量原型、Bug 修复等
- 📋 **阶段维度**：需求、设计、编码、测试等
- 💻 **语言维度**：Python、JavaScript、Java、Go 等
- 📏 **规则维度**：安全、Clean Code、性能等

## 核心特性

### 🎯 多维度组合

不同于传统固定命令，Nova 支持 4 个维度的灵活组合：

```
工作流 (sdlc-full) + 阶段 (code) + 语言 (python) + 规则 (security)
    ↓
生成个性化的代码开发指导
```

### 🚀 灵活扩展

- 添加新工作流：只需创建 YAML 配置
- 添加新语言：定义语言特性
- 添加新规则：配置检查规则
- 无需修改核心代码

### 📦 预设模板

**工作流模板**：
- `sdlc-full` - 完整 SDLC（6 阶段）
- `sdlc-lite` - 轻量原型（3 阶段）
- `bug-fix` - Bug 修复流程

**语言模板**：
- Python (FastAPI, Django, Flask)
- JavaScript (React, Vue, Node.js)
- Java (Spring Boot)
- Go (标准库)

**规则模板**：
- Security（安全规则）
- Clean Code（代码质量）
- Performance（性能优化）

## 可用插件

### Nova Plugin - Multi-Dimensional Template System

**核心插件，提供灵活的多维度模板系统**

**特点：**
- 🔄 **工作流维度**：4 种工作流（完整 SDLC、轻量原型、Bug 修复、性能优化）
- 📋 **阶段维度**：10 个阶段模板（需求、设计、编码、测试、审查、文档、性能分析、性能优化、基准测试、验证）
- 💻 **语言维度**：7 种语言（Python、JavaScript、Java、Go、C、C++、Rust）
- 📏 **规则维度**：4 种规则集（安全、Clean Code、性能、测试）

**路径：** [plugins/nova-plugin](plugins/nova-plugin)

**架构文档：** [ARCHITECTURE.md](ARCHITECTURE.md)

**版本：** 2.0.0（多维度模板系统）

## 安装

### 安装整个插件仓库

```bash
# Linux/macOS
cd ~/.config/Claude/plugins/
git clone https://github.com/wukehu/nova.git

# Windows
cd %APPDATA%\Claude\plugins\
git clone https://github.com/wukehu/nova.git
```

### 单独安装某个插件

```bash
# 只安装 nova-plugin
cd ~/.config/Claude/plugins/
git clone --depth 1 --filter=blob:none --sparse https://github.com/wukehu/nova.git
cd nova
git sparse-checkout set plugins/nova-plugin
```

## 使用方法

安装后，所有插件中的命令和技能将自动可用。

### Nova Plugin 命令

```bash
# 需求澄清
/clarify 实现一个用户登录功能

# 需求分析
/analyze ./requirements.md

# 架构设计
/design 系统需要支持10万并发用户

# 详细设计
/detail 需要定义用户认证API

# 代码开发
/code 实现用户认证服务

# 测试调试
/test 登录时出现500错误
```

详细使用说明请参考 [Nova Plugin 文档](plugins/nova-plugin/README.md)。

## 项目结构

```
nova-plugins/
├── .claude-plugin/
│   └── marketplace.json       # 插件市场配置
├── plugins/                    # 插件目录
│   └── nova-plugin/           # Nova SDLC 插件
│       ├── .claude-plugin/
│       │   └── plugin.json   # 插件配置
│       ├── commands/          # 命令文件
│       ├── skills/            # 技能定义
│       ├── README.md          # 插件文档
│       └── CHANGELOG.md       # 变更日志
├── plugins.json               # 插件清单
├── CHANGELOG.md               # 仓库变更日志
├── LICENSE                    # MIT 许可证
└── README.md                  # 仓库说明
```

## 贡献

欢迎贡献！请查看各个插件目录中的 README 和 CONTRIBUTING 文档了解详情。

## 许可证

MIT License - 详见 [LICENSE](LICENSE) 文件

## 联系方式

- **GitHub**: https://github.com/wukehu/nova
- **Issues**: https://github.com/wukehu/nova/issues
- **邮箱**: w.khu@163.com

---

**Nova Plugins** - 让软件开发更高效、更规范
