
# Bringing Structure to AI-Assisted Delivery: Introducing an Agent-OS Inspired Workflow at Citi

## TL;DR

> **We are introducing an Agent-OS inspired workflow to bring structure, clarity, and safety to AI-assisted development at Citi.**

Instead of letting AI write code against vague tickets, we:

- **Plan** the intent (vision + roadmap)  
- **Specify** the work (spec + acceptance criteria)  
- **Build** from an agreed plan (human + AI)  
- **Verify** with evidence  

This works with:
- **VS Code + GitHub Copilot**
- **Jira**
- **Any AI tool (Copilot, Cursor, Claude, Devin, etc.)**

The goal is simple:

> **Make AI predictable, auditable, and aligned with how we already deliver.**

---

## Why This Matters

Over the past year, many of us have started experimenting with AI tools in our development workflows — GitHub Copilot, ChatGPT, Cursor, Claude, and even emerging autonomous agents like Devin.

And while these tools are undeniably powerful, one thing has become increasingly clear:

> **We added AI to our workflow… but we didn’t change the workflow.**

We’re still relying on the same processes, the same ticket structures, the same tribal knowledge, and the same mental models — just with faster code generation. That creates a real risk:  
AI amplifies **both** good structure and bad structure.

This is where I started exploring **Agent-OS** — an open-source project created by buildermethods — and why I’ve been working on a simplified, enterprise-friendly version that we can use inside Citi with the tools we already trust.

This post explains:
- What Agent-OS is (and isn’t)
- Why it matters for us
- How we can use it today with VS Code, GitHub Copilot, and even Devin.ai
- And how I’ve adapted it to fit our environment and constraints

---

## Credit Where It’s Due

The foundation of this work is inspired by the excellent **Agent-OS** project by **buildermethods**.

Agent-OS introduces a structured, spec-driven workflow designed specifically for AI-assisted development. It’s opinionated, well thought-out, and built with a deep understanding of how agents reason and operate.

My goal was **not** to replace Agent-OS, but to:
- Simplify it
- Adapt it for enterprise constraints
- Integrate it into tools we already use (VS Code, Copilot, Jira)
- And make it approachable for teams at Citi

So this is very much:
> **Agent-OS inspired, Citi adapted.**

---

## The Agent-OS Operating Model

At its core, the workflow is simple:

### **PLAN → SPECIFY → BUILD → VERIFY**

### PLAN — Vision & Roadmap  
We start by clarifying:
- What problem are we solving?
- Why does it matter?
- What does success look like?

This produces:
- A clear product vision
- A prioritized roadmap

---

### SPECIFY — Specs & Acceptance Criteria  
Next, we turn roadmap items into:
- A clear spec (what we’re building)
- Explicit acceptance criteria (how we know it’s done)

If we can’t describe “done” clearly, AI will guess — and guessing is expensive.

---

### BUILD — Planned Implementation  
Only after the spec is agreed do we plan the implementation.

This workflow forces:
- A change plan
- A diff plan
- A clear understanding of what will be modified

**No code is written by AI until there is an agreed plan.**

---

### VERIFY — Evidence of Completion  
Finally, we verify that:
- The acceptance criteria were met
- The expected behavior exists
- The change can be demonstrated

This is evidence-based completion, not “looks good to me”.

---

## Visual: How the Workflow Works

```
         ┌─────────────────────┐
         │     Business Idea   │
         │  (Leadership / PM)  │
         └─────────┬───────────┘
                   │
                   ▼
        ┌────────────────────────┐
        │         PLAN           │
        │  Vision + Roadmap      │
        │  (plan-product)        │
        └─────────┬──────────────┘
                   │
                   ▼
        ┌────────────────────────┐
        │        SPECIFY         │
        │  Spec + Acceptance     │
        │  (write-spec)          │
        └─────────┬──────────────┘
                   │
                   ▼
        ┌────────────────────────┐
        │         BUILD          │
        │  Implementation Plan  │
        │  + Code (AI assisted) │
        │  (implement-tasks)    │
        └─────────┬──────────────┘
                   │
                   ▼
        ┌────────────────────────┐
        │        VERIFY          │
        │  Evidence of completion│
        │  (verify-work)         │
        └─────────┬──────────────┘
                   │
                   ▼
        ┌────────────────────────┐
        │     Jira / Release     │
        │  Tracking + Delivery  │
        └────────────────────────┘
```

> **Jira tracks execution. Agent-OS governs thinking. AI executes.**

---

## Visual: Tool Positioning

```
            ┌──────────────────────────┐
            │       Agent-OS           │
            │  (Operating Model)       │
            │  - Plan                  │
            │  - Spec                  │
            │  - Build                 │
            │  - Verify                │
            └─────────────┬────────────┘
                          │
        ┌─────────────────┼─────────────────┐
        │                 │                 │
        ▼                 ▼                 ▼
  GitHub Copilot      Cursor / Claude       Devin.ai
  (Developer AI)      (Developer AI)        (Autonomous AI)
        │                 │                 │
        └─────────────┬───┴───┬─────────────┘
                      │       │
                      ▼       ▼
                    VS Code  Automation
                      │
                      ▼
                  Codebase
                      │
                      ▼
                    Jira
               (Tracking only)
```

---

## Example: What This Looks Like in Practice

### Scenario
> Product wants a new feature:  
> **“Allow users to filter transactions by date range.”**

---

### Step 1 — PLAN

Run: `plan-product`

AI asks:
- Who is this for?
- Why does it matter?
- How will we measure success?

Output:
- Product vision
- Roadmap item: “Transaction filtering by date range”

---

### Step 2 — SPECIFY

Run: `write-spec`

AI generates:
- `SPEC.md`
- `ACCEPTANCE.md`

Example acceptance criteria:
- User can select start and end date
- Results update without page refresh
- Invalid ranges show an error
- Filter state is preserved on navigation

---

### Step 3 — BUILD

Run: `implement-tasks`

AI produces:
- File change plan
- Component impact list
- Data flow summary

Only after review does AI write code.

---

### Step 4 — VERIFY

Run: `verify-work`

AI generates:
- Checklist
- Evidence notes
- Test references

---

## How Jira Fits In

We still:
- Create Jira stories
- Track status
- Manage releases

But now Jira tracks **well-defined work**, not vague intent.

---

## Final Thought

This isn’t about process for the sake of process.  
And it’s not about chasing AI trends.

It’s about answering one simple question:

> **How do we scale AI safely in a highly regulated, highly complex environment?**

For me, Agent-OS (and this simplified adaptation) is the most compelling answer I’ve seen so far.
