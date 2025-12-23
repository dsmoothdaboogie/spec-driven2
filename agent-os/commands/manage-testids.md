# Command: manage-testids — Enforce `data-testid` Usage & Glassbox Tracking Readiness

## Purpose

Ensure frontend tracking readiness by enforcing a consistent, auditable contract between:

- UI code
- Automated tests
- Analytics (Google Analytics)
- Session replay (Glassbox)
- AI agents

This command is responsible for:

1. Enforcing meaningful, unique `data-testid` attributes on interactive elements.
2. Following the naming convention defined in `agent-os/standards/frontend.md`.
3. Maintaining a central registry at `agent-os/docs/FRONTEND-TESTIDS.md`.
4. Verifying that the Glassbox tracking bootstrap script is present and correctly integrated.
5. Copying the appropriate Glassbox script (IIFE or ESM) from `agent-os/scripts/` into the application when missing.
6. Safely proposing or applying Glassbox integration when required.

All behavior follows a **review-first, apply-explicitly** workflow.

---

## Supported Scopes

This command may be run against:

1. **Single file**  
   Example: `src/app/login/login.component.ts`

2. **Folder / feature**  
   Example: `src/app/accounts/`

3. **Entire frontend codebase**  
   Example: `src/app/` or `src/`

Invocation parameters:

- `scope`: one of `file`, `folder`, `repo`
- `target`: path for file/folder/repo root

Defaults if not specified:

- `scope = "repo"`
- `target = "src/app"` (or `src/` if `src/app` does not exist)

---

## Modes: Review vs Apply

### REVIEW Mode (default, safe)

- **No code is changed.**
- Outputs:
  - Proposed `data-testid` changes
  - Proposed `FRONTEND-TESTIDS.md`
  - Summary of missing, duplicated, or weak IDs
  - Proposed Glassbox integration plan (if missing)

### APPLY Mode (explicit)

Executed only when explicitly approved.

Applies:
- `data-testid` changes
- Glassbox integration (if approved)
- Registry updates

---

## Framework Detection

Detect frontend framework:

- Angular
- React

If unsupported, skip Glassbox integration.

---

## Glassbox Verification & Integration

1. Verify whether a Glassbox script is already present.
2. If missing:
   - Select the correct script version from `agent-os/scripts/`:
     - `glassbox.event-logger-enhanced.js` for IIFE-based integration
     - `glassbox.event-logger.esm.js` (or `.js`) for ES module integration
   - Copy the selected script into the agreed location in the application's source tree **as part of APPLY mode only**.
3. Ask up to **5 clarification questions** before proceeding:
   - Framework (Angular / React)
   - Script type (IIFE or ESM)
   - Destination path in the source tree
   - Initialization location & timing
   - Review vs apply
4. Propose an integration plan in REVIEW mode.
5. Apply integration only when explicitly approved.

---

## Enforcing `data-testid`

Inspect:

- `button`, `a`, `input`, `select`, `textarea`
- Elements with interactive roles or handlers

Naming:
- kebab-case
- descriptive
- feature-scoped
- `feature-context-element-action`

---

## Registry

`agent-os/docs/FRONTEND-TESTIDS.md`

```md
| data-testid | File path(s) | Element type | Description |
```

Registry is rewritten on re-run to reflect current state.

---

## Re-run Behavior

- REVIEW: proposals only
- APPLY: deterministic changes

Registry always reflects the actual codebase.
