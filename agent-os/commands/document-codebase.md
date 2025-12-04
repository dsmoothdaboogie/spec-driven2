# Command: document-codebase — Generate Living Codebase Documentation

## Purpose
Generate deep, visual, and AI-friendly documentation for any repository (frontend, backend, infra, automation, data).
Docs are stored in agent-os/docs/ and may be safely regenerated at any time.

If the repository is small → generate a single file  
If the repository is large → generate structured multi-file documentation

## Documentation Mode Selection

If repo is small (single app or < 40 files):
Generate:
agent-os/docs/DOCUMENTATION.md

If repo is medium / large:
Generate:
agent-os/docs/CODEBASE-OVERVIEW.md
agent-os/docs/ARCHITECTURE.md
agent-os/docs/FRONTEND.md
agent-os/docs/BACKEND.md
agent-os/docs/PIPELINES.md
agent-os/docs/TESTING-QUALITY.md
agent-os/docs/GLOSSARY.md

Declare documentation mode clearly at the top of the file.
Documentation Mode: SINGLE FILE or MULTI FILE.

## Required Context
- agent-os/agents/architect.md
- agent-os/agents/reviewer.md
- agent-os/standards/*
- Repository structure

## Guardrails
- Read-only: Do not modify source
- Do not expose secrets
- Deterministic output
- Use Mermaid for diagrams
- Overwrites allowed

## Mandatory Diagrams
Each run must include:
- System architecture diagram
- Component / service tree
- CI/CD pipeline
- Data flow (if applicable)
All written in Mermaid syntax

## Output Definitions

### CODEBASE-OVERVIEW.md
Purpose, entry points, tech stack, architecture diagram, navigation help

### ARCHITECTURE.md
System layers, integrations, cross-cutting concerns

### FRONTEND.md
Component tree, routing, state, styling, guide

### BACKEND.md
Services, APIs, storage, integrations

### PIPELINES.md
CI/CD stages, environments, diagram

### TESTING-QUALITY.md
Testing layers and tools

### GLOSSARY.md
Domain terms

## Execution Steps
1. Scan directory tree
2. Identify subsystems
3. Build diagrams
4. Produce documentation
5. Apply timestamp
6. Output docs only

## Header Template for Each File

# <Document Title>
Documentation Mode: <SINGLE/MULTI>
Last Updated: 2025-12-04

## Re-Run Behavior
Re-running replaces docs fully.