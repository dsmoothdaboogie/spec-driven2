# Command: write-spec — Formalize the First SPEC


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
Creates/updates `agent-os/specs/<YYYY-MM-DD>-<slug>-v1/`:
- **SPEC.md** — Problem/Goals, Constraints, Architecture Intent, Domain & Data Model, Non‑Functionals, Acceptance (ref), Risks, Rollout
- **ACCEPTANCE.md** — unambiguous **GWT** criteria
- **plan.01-foundation.md** — initial plan (10–15 tasks, deps, risks, acceptance mapping, explicit paths)

## Steps
1. Ask for feature **slug** and initial **scope** (or propose both).
2. Emit folder path + inline contents for SPEC, ACCEPTANCE, plan.01.
3. Ask up to 7 clarifying questions; stop.
