# Command: manage-testids — Enforce & Document `data-testid` Usage

## Purpose

Ensure all relevant interactive frontend elements:

1. Have meaningful, unique `data-testid` attributes.
2. Follow the naming convention in `agent-os/standards/frontend.md`.
3. Are registered in `agent-os/docs/FRONTEND-TESTIDS.md` with:
   - data-testid value
   - file path(s)
   - element type
   - description of purpose.

This command can be run in **review** or **apply** mode, and scoped to a **single file**, a **folder**, or the **entire frontend codebase**.

---

## Supported Scopes

You may run this command against:

1. **Single file**  
   Example: `src/app/login/login.component.ts`

2. **Folder / feature**  
   Example: `src/app/accounts/`

3. **Entire frontend codebase**  
   Example: `src/app/` or `src/`

When invoking this command (either via Copilot prompt or another agent), you must specify:

- `scope`: one of `file`, `folder`, `repo`
- `target`: path for file/folder/repo root

If not specified, default to:

- `scope = "repo"`
- `target = "src/app"` (or `src/` if `src/app` does not exist).

---

## Modes: Review vs Apply

### REVIEW Mode (default, safe)

- No code is changed.
- The command analyzes the scope and outputs:
  - A per-file list of **proposed `data-testid` changes**.
  - A **proposed updated** `agent-os/docs/FRONTEND-TESTIDS.md` table.
  - A summary of:
    - Missing `data-testid`s
    - Duplicated IDs
    - Non-descriptive or non-compliant names.

Use this mode for planning, refactors, or PR preparation.

### APPLY Mode (explicit, opt-in)

Executed only when a human explicitly requests it, e.g.:

- "Apply manage-testids changes"
- "Proceed with manage-testids in apply mode"

In this mode, the agent:

1. Applies the previously proposed or freshly recomputed changes to code.
2. Updates `agent-os/docs/FRONTEND-TESTIDS.md` to match actual usage.
3. Outputs a summary of all modifications.

---

## Required Context

Read:

- `agent-os/standards/frontend.md`
- `agent-os/docs/FRONTEND-TESTIDS.md` (if present)
- Frontend source files in the requested scope.

Do not read or expose secrets or credentials. Do not modify any configuration related to secrets or credentials.

---

## Guardrails

- Do **not** change component behavior; only add/rename `data-testid` attributes.
- Do **not** remove an existing `data-testid` without:
  - Updating `FRONTEND-TESTIDS.md`, and
  - Calling out potential impacts for tests/analytics.
- Ensure `data-testid` values remain **globally unique** across the app.
- Follow the documented naming convention (descriptive, kebab-case, feature-scoped).
- When unsure about renaming an ID used in existing tests/analytics, propose the change and highlight it instead of silently changing it.

---

## Registry File: `agent-os/docs/FRONTEND-TESTIDS.md`

Format the registry as a Markdown table:

```markdown
# Frontend data-testid Registry

Last Updated: 2025-12-08

| data-testid                  | File path(s)                               | Element type | Description                                      |
|------------------------------|--------------------------------------------|--------------|--------------------------------------------------|
| requests-filter-apply-button | src/app/requests/requests-page.component.ts| button       | Apply filter on Requests list                   |
| login-email-input            | src/app/auth/login-form.component.ts       | input        | Email address field on login form               |
```

If file does not exist, create it with header + empty table and a note:

> This registry is generated and maintained by the `manage-testids` command and must be kept in sync with the codebase.

On re-runs, the table may be **fully rewritten** to match the scanned code.

---

## Element Scope

Inspect at minimum:

- `button`, `a`, `input`, `select`, `textarea`
- Elements with `role="button"` or `role="link"`
- Elements with click/interaction handlers (`(click)`, `(keyup.enter)`, `onClick`, etc.)

For each element capture:

- File path
- (If possible) surrounding component/container name
- Element type
- Existing `data-testid` (if any)

---

## REVIEW Mode Behavior

1. Scan the selected scope.
2. For each interactive element:
   - Check whether `data-testid` exists.
   - If missing, propose a new one using the naming convention:
     - `feature-context-element-action` (e.g., `requests-filter-apply-button`).
   - If present but non-descriptive or duplicated, propose a clearer, unique name.
3. Build the **proposed** `FRONTEND-TESTIDS.md` table:
   - `data-testid`
   - file path(s)
   - element type
   - short description
4. Output:
   - Summary of findings (counts, duplicates, missing, renames).
   - Per-file suggested changes (no code modifications).
   - Full contents for `agent-os/docs/FRONTEND-TESTIDS.md` as it *should* look after applying changes.

No code is modified in REVIEW mode.

---

## APPLY Mode Behavior

Triggered only when user explicitly asks to apply.

1. Use the latest suggested mapping (or recompute deterministically).
2. Modify code in the specified scope to:
   - Add missing `data-testid` attributes.
   - Rename non-compliant/duplicated IDs as per the plan.
3. Write/update `agent-os/docs/FRONTEND-TESTIDS.md` to match new usage.
4. Output:
   - Summary of changes per file.
   - Updated registry table.

The apply pass should be idempotent given current code and registry.

---

## Naming Convention (Summary)

- `data-testid` must be descriptive, kebab-case, and feature-scoped where possible.
- Recommended shape: `feature-context-element-action`.
  - `requests-filter-apply-button`
  - `login-email-input`
  - `nav-profile-menu-toggle`
- Avoid generic IDs like `submit-button`, `cta1`, `button1`.

---

## Example Invocation (Conceptual)

- Single file, review:  
  "Run manage-testids in review mode for `src/app/login/login.component.ts`."

- Folder, review:  
  "Run manage-testids in review mode for `src/app/requests`."

- Repo-wide, apply:  
  "Run manage-testids in apply mode for `src/app` using the previous review suggestions."

---

## Re-run Behavior

This command may be re-run at any time.

- In REVIEW mode, it recomputes proposed changes and registry content without touching code.
- In APPLY mode, it applies/normalizes IDs and aligns the registry.

The registry is always expected to reflect the **current, actual** codebase state.