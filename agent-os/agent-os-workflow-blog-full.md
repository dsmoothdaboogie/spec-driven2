
# Bringing Structure to AI-Assisted Delivery: Introducing an Agent-OS Inspired Workflow at Citi

## Executive Summary

> **This initiative introduces a structured, Agent-OS inspired workflow to safely scale AI-assisted development at Citi by making intent, standards, and acceptance criteria explicit before any code is generated.**

Instead of relying on AI to interpret loosely defined Jira stories, this approach enforces a disciplined flow:

**Standards → Plan → Specify → Build → Verify**

This ensures that:
- Engineering standards are defined before AI is used
- Product intent is captured before implementation begins
- Work is specified and decomposed before code is generated
- All changes are evidence-based and reviewable

The workflow integrates seamlessly with **VS Code, GitHub Copilot, Jira, and emerging agents like Devin**, allowing teams to benefit from AI acceleration without compromising architectural integrity, compliance, or delivery quality.

In short:

> **This is how we make AI an asset — not a liability — in a regulated, large-scale environment.**

---

## TL;DR

> **We are introducing an Agent-OS inspired workflow to bring structure, clarity, and safety to AI-assisted development at Citi.**

Instead of letting AI write code against vague tickets, we:

- **Define Standards first** (how we build)
- **Plan** the intent (vision + roadmap)
- **Specify** the work (spec + acceptance + tasks)
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

## What This Is Not (Important)

This initiative is intentionally designed to complement — not disrupt — how we already work. To avoid any misunderstanding:

**This is NOT:**
- A replacement for Jira or Agile ceremonies
- An attempt to bypass product management or architecture review
- A mandate to use a specific AI tool
- An experiment in “letting AI run the show”
- A new heavyweight process framework

**This IS:**
- A lightweight structure around how we think before we build
- A way to make AI predictable, reviewable, and safe
- A way to improve spec quality without slowing teams down
- A way to scale AI without sacrificing engineering discipline

> **We are not changing who decides. We are changing how clearly decisions are expressed.**

---

## The Importance of Standards (Before Anything Else)

One of the most important — and often overlooked — parts of this workflow is **standards**.

Before we ask AI to plan, spec, or build anything, we define:
- Frontend standards
- Backend standards
- Testing standards
- Security standards
- Architecture patterns

These live under:

```
agent-os/standards/
```

Why this matters:

> **AI is only as good as the rules it follows.**

If we don’t tell AI:
- how we structure components
- how we name things
- how we handle errors
- how we test
- how we instrument analytics

…it will invent its own patterns. And at scale, that’s dangerous.

By defining standards first, we ensure:
- Consistency across teams
- Predictable output from AI
- Easier code review
- Stronger architectural integrity

This is the foundation layer. Everything else builds on this.

---

## The Agent-OS Operating Model

At its core, the workflow is simple:

### **STANDARDS → PLAN → SPECIFY → BUILD → VERIFY**

---

### PLAN — Vision & Roadmap

We start by clarifying:
- What problem are we solving?
- Why does it matter?
- What does success look like?
- Who is this for?

This produces:
- A clear product vision
- A prioritized roadmap

This is typically driven by:
- Business ideas
- Product needs
- **Jira epics / initiatives**

The key shift here is:

> We don’t jump from Jira straight to code.  
> We jump from Jira to **intent**.

---

### SPECIFY — Specs, Acceptance Criteria & Tasks

Next, we turn roadmap items into:

- A clear spec (what we’re building)
- Explicit acceptance criteria (how we know it’s done)
- A concrete task breakdown (how it will be implemented)

This is where we run:
- `write-spec.md`
- `create-tasks.md`

This step removes ambiguity and breaks work into:
- Logical units
- Reviewable steps
- AI-friendly chunks

If we can’t describe “done” clearly, AI will guess — and guessing is expensive.

---

### BUILD — Planned Implementation

Only after the spec and tasks are agreed do we plan the implementation.

This workflow forces:
- A change plan
- A diff plan
- A clear understanding of what will be modified

**No code is written by AI until there is an agreed plan.**

This is one of the biggest safety mechanisms in the model.

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
         ┌───────────────────────────────┐
         │   Business Idea / Jira Story  │
         │    (Leadership / Product)     │
         └───────────────┬───────────────┘
                         │
                         ▼
        ┌───────────────────────────────┐
        │           STANDARDS            │
        │  How we build, test, secure,  │
        │  observe (agent-os/standards) │
        └───────────────┬───────────────┘
                         │
                         ▼
        ┌───────────────────────────────┐
        │             PLAN              │
        │     Vision + Roadmap           │
        │       (plan-product)           │
        └───────────────┬───────────────┘
                         │
                         ▼
        ┌───────────────────────────────┐
        │            SPECIFY             │
        │  Spec + Acceptance + Tasks     │
        │ (write-spec, create-tasks)     │
        └───────────────┬───────────────┘
                         │
                         ▼
        ┌───────────────────────────────┐
        │             BUILD              │
        │  Implementation Plan + Code    │
        │     (implement-tasks)           │
        └───────────────┬───────────────┘
                         │
                         ▼
        ┌───────────────────────────────┐
        │            VERIFY              │
        │   Evidence of completion       │
        │        (verify-work)           │
        └───────────────┬───────────────┘
                         │
                         ▼
        ┌───────────────────────────────┐
        │        Jira / Release          │
        │   Tracking + Delivery          │
        └───────────────────────────────┘
```

---

## Example: What This Looks Like in Practice

### Scenario

> Product raises a Jira story:  
> **“Allow users to filter transactions by date range.”**

---

### Step 0 — STANDARDS

Before doing anything, the AI reads:
- Frontend standards
- API standards
- Testing standards

So it knows:
- How we structure components
- How we name things
- How we test
- How we instrument analytics

This prevents pattern drift.

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

Run:
- `write-spec`
- `create-tasks`

AI generates:
- `SPEC.md`
- `ACCEPTANCE.md`
- Task breakdown

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

## Risk & Controls (Why This Is Safe for Citi)

A common concern with AI-assisted development is loss of control: unpredictable changes, undocumented decisions, and inconsistent behavior across teams. This workflow is explicitly designed to mitigate those risks.

By enforcing standards upfront, requiring written specifications, generating implementation plans before code, and verifying against acceptance criteria, we introduce **natural control points** into the AI workflow. Every decision is documented, every change is reviewable, and every output is traceable back to intent. AI is not allowed to “freestyle” — it operates within clearly defined constraints.

> **This turns AI from an uncontrolled actor into a governed participant in our SDLC.**

From a risk perspective, this model improves:
- Auditability
- Predictability
- Explainability
- Accountability

---

## Final Thought

This isn’t about process for the sake of process.  
And it’s not about chasing AI trends.

It’s about answering one simple question:

> **How do we scale AI safely in a highly regulated, highly complex environment?**

For me, Agent-OS (and this simplified adaptation) is the most compelling answer I’ve seen so far.
