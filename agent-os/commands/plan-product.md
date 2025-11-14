# Command: plan-product — Product Discovery & Strategy (ENTRY POINT)


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
Creates/updates under `agent-os/vision/`:
- **PRODUCT-VISION.md** — why we exist; target user & outcome
- **MISSION.md** — how we will win; north‑star objectives (12–24m)
- **PERSONAS.md** — primary/secondary users, jobs‑to‑be‑done
- **CAPABILITIES.md** — capability map with acceptance anchors
- **ROADMAP.md** — sequenced milestones (0–3m, 3–6m, 6–12m, 12–18m)

## Process (single file, no links)
1. Assume **Product Planner** role; ask up to **10 concise questions** about audience, outcomes, constraints, risks.
2. Draft Vision/Mission/Personas/Capabilities/Roadmap as **complete markdown files** (inline content).
3. Switch to **Architect**; list **3 architecture options** with tradeoffs and a recommendation; list any **Standards** deltas.
4. Hand‑off: suggest running `agent-os/commands/write-spec.md` next.
5. Stop for review.
