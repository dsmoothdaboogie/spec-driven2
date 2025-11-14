# Command: create-tasks — Expand Plans from SPEC


## Required Context (Read Before Acting)
- **Agents**: `agent-os/agents/**`
- **Standards**: `agent-os/standards/**`
- **Vision**: `agent-os/vision/**`
- **Current Spec** (optional): `agent-os/specs/<feature>/**`



## Guardrails
- **Plan-before-code**: produce a file‑by‑file diff plan before generating code.
- **No scope creep**: execute only the active phase/plan.
- **Traceability**: map outputs to acceptance and standards.
- **Determinism**: explicit file paths, named functions, and tests.
- **Security**: follow `standards/security.md`; never include secrets/PII.


## Outcomes
Emits additional plan files (as needed), each with 10–15 tasks, deps, risks, acceptance mapping, and **explicit file paths**.
Examples:
- `plan.02-core-ui.md` (if UI)
- `plan.02-core-services.md` (if API/services)
- `plan.03-data.md` (if storage/migrations)
- `plan.04-auth.md` (if authn/z)
- `plan.05-observability.md`
- `plan.06-testing-ci.md`

## Steps
1. Read SPEC + ACCEPTANCE + Standards.
2. Propose minimal new plan files and output full contents inline.
3. Stop.
