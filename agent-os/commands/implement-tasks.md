# Command: implement-tasks — Execute One Plan (Two‑Step)


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
- **Diff Plan** (no code) → approve → **Code + Tests** per plan

## Steps
**A. Diff Plan**
1. Read the **selected plan file only** plus SPEC + ACCEPTANCE + Standards.
2. Emit a **file‑by‑file diff plan** (paths, snippets, tests, acceptance mapping). **Wait for “Proceed.”**

**B. Code**
3. Generate code + tests **exactly** as planned.
4. No new dependencies unless the plan states so. Stop.
