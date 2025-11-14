# Agent‑OS Generic Starter (Flattened)

A **domain‑agnostic**, **spec‑driven** starter you can drop into any repo. It follows an Agent‑OS–style flow,
but with **single‑file commands** to keep things simple for humans and AI (especially GitHub Copilot).

## Why this exists
- Teams want a **repeatable product → spec → plan → implement → verify** loop.
- New devs and AI assistants struggle with deep folder/link trees.
- This keeps **agents** and **standards** modular, and collapses **workflows** into **single commands**.

---

## Folder structure (flattened)
```
agent-os/
  README.md
  MIGRATION.md                 # mapping from nested profiles/workflows → flattened commands
  agents/                      # role runbooks (product-planner, architect, implementer, qa, security, reviewer)
  standards/                   # engineering baselines (frontend, backend, testing, security, ops)
  vision/                      # created/maintained by plan-product (vision, mission, personas, capabilities, roadmap)
  specs/                       # per-feature folders containing SPEC.md / ACCEPTANCE.md / plan.*.md
  commands/                    # single-file commands (paste into Copilot Chat)
    plan-product.md            # ENTRY POINT — asks discovery questions; drafts vision/mission/roadmap
    write-spec.md              # formalize first SPEC + ACCEPTANCE + plan.01
    create-tasks.md            # expand into plan.* files
    implement-tasks.md         # two-step: diff plan → code + tests
    orchestrate-verify.md      # verification report + next steps
    new-spec.md                # optional: standalone “create a new spec folder”

.github/
  prompts/                     # Copilot prompt files (detected by suffix .prompt.md)
    plan-product.prompt.md
    write-spec.prompt.md
    create-tasks.prompt.md
    implement-tasks.prompt.md
    orchestrate-verify.prompt.md
    meta-help.prompt.md
```

---

## How to use (common scenarios)

### A) Start a **brand new project** (empty or greenfield repo)
1. Copy the `agent-os/` folder into your repo.
2. Open **Copilot Chat** → **Prompt files** → run **`plan-product.prompt.md`**.
3. Answer up to ~10 discovery questions.
4. The tool drafts:
   - `agent-os/vision/PRODUCT-VISION.md`
   - `agent-os/vision/MISSION.md`
   - `agent-os/vision/PERSONAS.md`
   - `agent-os/vision/CAPABILITIES.md`
   - `agent-os/vision/ROADMAP.md`
5. Review/edit those files, then run **`write-spec.prompt.md`** to generate the *first* feature’s SPEC, ACCEPTANCE, and `plan.01-*`.
6. Run **`create-tasks.prompt.md`** to expand additional plans (optional), then **`implement-tasks.prompt.md`** to build with a two‑step flow.
7. Close the loop with **`orchestrate-verify.prompt.md`**.

### B) Integrate into an **existing project**
1. Drop `agent-os/` into the repo root (or a `/docs`/`/design` folder if preferred).
2. Skim `agent-os/standards/*`; tune to match your stack.
3. If you already have product docs, copy any **Vision/Mission/Personas** material into `agent-os/vision/*.md`.
4. Run **`write-spec.prompt.md`** directly to formalize the first SPEC for an upcoming feature; or run **`plan-product.prompt.md`** if your product docs are incomplete.
5. Use **`create-tasks.prompt.md`** to break work into plan files; then **`implement-tasks.prompt.md`** to implement in a guarded manner.

### C) Create a **new feature spec**
1. Run **`write-spec.prompt.md`** (or **use `agent-os/commands/new-spec.md`** if you prefer a standalone scaffold) to create:
   - `agent-os/specs/<YYYY-MM-DD>-<slug>-v1/SPEC.md`
   - `agent-os/specs/<...>/ACCEPTANCE.md`
   - `agent-os/specs/<...>/plan.01-foundation.md`
2. Answer any clarifying questions and review the generated files.
3. If needed, run **`create-tasks.prompt.md`** to add more plan files (UI, services, auth, data, observability, CI/testing, etc.).
4. Use **`implement-tasks.prompt.md`** to implement one plan at a time:
   - **Step A**: Copilot outputs a **file‑by‑file diff plan** (no code).  
   - **Your approval**: reply **“Proceed.”**  
   - **Step B**: Copilot generates **code + tests** as planned (no scope creep).

---

## Agents (who does what)
- **Product Planner** (`agent-os/agents/product-planner.md`) — discovery → Vision/Mission/Personas/Capabilities/Roadmap
- **Architect** (`agent-os/agents/architect.md`) — architecture options, boundaries, contracts, standards deltas
- **Implementer** (`agent-os/agents/implementer.md`) — two‑step implementation (diff plan → code+tests), scoped to plan
- **QA** (`agent-os/agents/qa.md`) — GWT acceptance, risk‑based test layering
- **Security** (`agent-os/agents/security.md`) — threat model, authn/z, secrets, retention, outbound policy
- **Reviewer** (`agent-os/agents/reviewer.md`) — PR and design review heuristics

---

## Standards (how we build)
Tune `agent-os/standards/*` to your org:
- **frontend.md** — TypeScript, framework choice, testing, a11y, perf
- **backend.md** — runtime, API style, observability, data
- **testing.md** — layering strategy, CI, fixtures
- **security.md** — authn/z, secrets, data protection, supply chain
- **ops.md** — branching, CI/CD, rollout/rollback, SLOs

These are **baselines**; each SPEC can append deltas.

---

## Copilot: how to run commands
- Use the built‑in prompt files under **`.github/prompts/*.prompt.md`** (recommended), **or**
- Open a file under `agent-os/commands/*.md`, copy its content, and paste into **Copilot Chat**.

**Two‑step implementation flow**
1. Run **`implement-tasks.prompt.md`** → Copilot outputs a **diff plan** only.
2. Review/adjust; then reply **“Proceed.”** → Copilot emits **code + tests** for that plan file only.

---

## CI suggestion (spec‑gate)
- Fail PR if code changed but no `agent-os/specs/**/plan.*.md` was updated.
- Optional: require a pointer in the PR description to the active plan/acceptance items.

---

## FAQ
**Q: Do we need multiple “profiles”?**  
A: Not with this flattened layout. If you later need environment‑specific behavior, add `profiles/` back.

**Q: Can we run this without Copilot?**  
A: Yes — any LLM that can read workspace files will work. The commands are copy‑paste friendly.

**Q: Where do diagrams live?**  
A: Reference diagram placeholders in SPEC; store actual images in your repo’s docs or wiki.
