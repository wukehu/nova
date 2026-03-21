# Changelog

All notable changes to the Nova Plugins repository will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [2.0.0] - 2026-03-21

### Major Changes
- **Redesigned as multi-dimensional template system**
  - No longer fixed commands - now flexible template combination
  - 4 dimensions: Workflows, Phases, Languages, Rules
  - All components can be mixed and matched

### Added
- **Workflows**: 4 workflow templates (sdlc-full, sdlc-lite, bug-fix, performance-opt)
- **Phases**: 12 phase templates
  - SDLC: requirements, architecture-design, detail-design, code, test, review, docs
  - Performance: perf-analyze, perf-optimize, perf-benchmark, perf-validate
- **Languages**: 7 language configs (Python, JavaScript, Java, Go, C, C++, Rust)
- **Rules**: 4 rule sets (security, clean-code, performance, testing)
- **Commands**: 2 new commands (`/workflow`, `/template`)
- **Documentation**: Architecture document explaining the system

### Design Enhancements
- **Architecture Design Template**: Includes SOLID principles, DRY, KISS, YAGNI
- **Detailed Design Template**: Comprehensive API design, data models, validation
- **Design Patterns Reference**: Creational, structural, behavioral patterns
- **Anti-patterns Guide**: Common pitfalls to avoid

### Major Changes
- **Redesigned as multi-dimensional template system**
  - No longer fixed commands - now flexible template combination
  - 4 dimensions: Workflows, Phases, Languages, Rules
  - All components can be mixed and matched

### Added
- **Workflows**: 4 workflow templates (sdlc-full, sdlc-lite, bug-fix, performance-opt)
- **Phases**: 10 phase templates
  - SDLC: requirements, design, code, test, review, docs
  - Performance: perf-analyze, perf-optimize, perf-benchmark, perf-validate
- **Languages**: 7 language configs (Python, JavaScript, Java, Go, C, C++, Rust)
- **Rules**: 4 rule sets (security, clean-code, performance, testing)
- **Commands**: 2 new commands (`/workflow`, `/template`)
- **Documentation**: Architecture document explaining the system

### Changed
- Removed fixed command structure
- Templates are now YAML-based for better extensibility
- Configuration-driven instead of code-driven

### Removed
- Old fixed commands (`/clarify`, `/analyze`, `/design`, `/detail`, `/code`, `/test`)
- Old `templates/` directory structure

## [1.0.0] - 2026-03-21

### Added
- Initial release of Nova Plugins repository
- **Nova Plugin** (v1.0.0): Complete SDLC workflow support
  - 6 core commands: `/clarify`, `/analyze`, `/design`, `/detail`, `/code`, `/test`
  - 6 specialized skills for each SDLC phase
- Plugin marketplace configuration
- Multi-plugin repository structure

### Documentation
- Repository README with installation instructions
- Nova Plugin comprehensive documentation
- Usage examples and typical workflows

## [Unreleased]

### Added - Document Review System
- **Review Command**: `/review` command for managing document reviews
- **Review Tracking**: Complete review history and audit trail
- **Quality Metrics**: Review scoring, timing, and efficiency tracking
- **Review Templates**: Phase-specific review checklists
- **Document Templates**: Updated all document templates with review sections

### Review System Features
- **Human Review Information**: Each document includes reviewer info, timestamps, scores
- **Review Roles**: Multiple reviewer roles (requirements, architecture, technical, security)
- **Scoring System**: Multi-criteria scoring (completeness, accuracy, clarity, feasibility)
- **Comment Categories**: Blocking, major, minor, suggestions
- **Time Tracking**: Review start/end time, duration calculation
- **Approval Workflow**: Approve, request changes, reject with clear criteria

## Planned
- More workflow templates (data-pipeline, ml-model, microservices)
- More language support (Rust, Ruby, PHP, C#)
- More rule sets (reliability, observability, documentation)
- Visual configuration interface
- Template marketplace
- AI-assisted configuration generation
