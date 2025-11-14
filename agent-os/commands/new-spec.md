# Command: new-spec — Create a New Feature Spec (Optional)


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
Creates a new dated spec folder with SPEC/ACCEPTANCE/plan.01 seeded.

## Steps
1. Choose `{slug}` and `{YYYY-MM-DD}`; propose folder path.
2. Emit inline contents for `SPEC.md`, `ACCEPTANCE.md`, and `plan.01-foundation.md`.
3. Ask ≤10 clarifying questions; stop.
