# Document Index

> **Last Updated**: {{last_updated}}
> **Project**: {{project_name}}
> **Version**: {{version}}

---

## Table of Contents

- [Requirements](#requirements)
- [Architecture](#architecture)
- [Design](#design)
- [Implementation](#implementation)
- [Testing](#testing)
- [Review](#review)
- [User Documentation](#user-documentation)
- [Performance](#performance)

---

## Requirements

### Requirements Documents

| Document | Date | Version | Status | Link |
|----------|------|---------|--------|------|
{{#requirements_docs}}
| {{name}} | {{date}} | {{version}} | {{status}} | [{{filename}}](requirements/{{filename}}) |
{{/requirements_docs}}

---

## Architecture

### Architecture Documents

| Document | Date | Version | Status | Link |
|----------|------|---------|--------|------|
{{#architecture_docs}}
| {{name}} | {{date}} | {{version}} | {{status}} | [{{filename}}](architecture/{{filename}}) |
{{/architecture_docs}}

### Architecture Decision Records (ADRs)

| ID | Title | Date | Status | Link |
|----|-------|------|--------|------|
{{#adrs}}
| {{number}} | {{title}} | {{date}} | {{status}} | [{{filename}}](architecture/adr/{{filename}}) |
{{/adrs}}

---

## Design

### Design Documents

| Document | Date | Version | Status | Link |
|----------|------|---------|--------|------|
{{#design_docs}}
| {{name}} | {{date}} | {{version}} | {{status}} | [{{filename}}](design/{{filename}}) |
{{/design_docs}}

### API Specifications

| Document | Date | Version | Link |
|----------|------|---------|------|
{{#api_docs}}
| {{name}} | {{date}} | {{version}} | [{{filename}}](design/api/{{filename}}) |
{{/api_docs}}

### Database Schemas

| Document | Date | Version | Link |
|----------|------|---------|------|
{{#schema_docs}}
| {{name}} | {{date}} | {{version}} | [{{filename}}](design/database/{{filename}}) |
{{/schema_docs}}

---

## Implementation

### Implementation Notes

| Document | Date | Version | Link |
|----------|------|---------|------|
{{#implementation_docs}}
| {{name}} | {{date}} | {{version}} | [{{filename}}](implementation/{{filename}}) |
{{/implementation_docs}}

---

## Testing

### Test Reports

| Document | Date | Coverage | Link |
|----------|------|----------|------|
{{#test_docs}}
| {{name}} | {{date}} | {{coverage}} | [{{filename}}](testing/{{filename}}) |
{{/test_docs}}

---

## Review

### Code Review Reports

| Document | Date | Reviewer | Link |
|----------|------|----------|------|
{{#review_docs}}
| {{name}} | {{date}} | {{reviewer}} | [{{filename}}](review/{{filename}}) |
{{/review_docs}}

---

## User Documentation

### User Guides

| Document | Date | Version | Link |
|----------|------|---------|------|
{{#user_docs}}
| {{name}} | {{date}} | {{version}} | [{{filename}}](user/{{filename}}) |
{{/user_docs}}

---

## Performance

### Performance Documents

| Type | Document | Date | Link |
|------|----------|------|------|
{{#performance_docs}}
| {{type}} | {{name}} | {{date}} | [{{filename}}](performance/{{filename}}) |
{{/performance_docs}}

---

## Quick Links

- **Latest Requirements**: [{{latest_requirements}}](requirements/{{latest_requirements}})
- **Latest Architecture**: [{{latest_architecture}}](architecture/{{latest_architecture}})
- **Latest Design**: [{{latest_design}}](design/{{latest_design}})
- **Latest Test Report**: [{{latest_test}}](testing/{{latest_test}})

---

## Document Statistics

- **Total Documents**: {{total_documents}}
- **Last Updated**: {{last_updated}}
- **Current Version**: {{version}}
