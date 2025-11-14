---
mode: "agent"
description: "Two-step: diff plan → code + tests"
---
# Implement Tasks (Two-Step)

A) Diff Plan (no code)
- Read the selected plan file + SPEC + ACCEPTANCE + `agent-os/standards/*`.
- Output a file-by-file **diff plan** (paths, snippets, tests, acceptance mapping). Await approval.

B) Code
- After approval, generate code + tests exactly as planned. No new deps unless the plan says so.
