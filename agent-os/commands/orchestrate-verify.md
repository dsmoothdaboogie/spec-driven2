# Command: orchestrate-verify — System Verification & Next Steps


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
- `verification.md` with acceptance **pass/fail**, evidence (file + test), gaps, prioritized follow‑ups
- A recommended **next plan**

## Steps
1. Evaluate each acceptance item; record pass/fail and evidence.
2. List gaps; propose remediations or next plan files.
3. Emit `verification.md`; stop.
