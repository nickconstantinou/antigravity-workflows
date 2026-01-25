---
description: Unified Research & Plan Creation Stage
---

# Workflow: Create Implementation Plan

🛑 **STOP.** Do NOT write any implementation code until the plan is approved.
This workflow combines deep exploration with structured planning to ensure architectural rigor.

## Phase 1: Exploration (Measure Twice)
Before drafting the plan, you MUST achieve a complete mental model of the solution.

1.  **Codebase Analysis**:
    - Read relevant files and trace data flow.
    - Identify dependencies, types, and potential side effects (RLS, state drift).
2.  **Architecture Check**:
    - Align with **AGENTS.md** Golden Rules (Modular Monolith, Verbose Headers).
    - Reuse existing patterns/helpers. Identify necessary DB schema changes.
3.  **Ambiguity Hunting**:
    - Identify edge cases (empty states, errors).
    - **Self-Correction**: If anything is unclear, stop and ask the user BEFORE generating the plan.

## Phase 2: Plan Generation (Cut Once)
Draft the `implementation_plan.md` using the following requirements:

- **Atomic Steps**: Steps must be small enough for a single commit.
- **No Hallucinations**: Only reference existing or planned files.
- **Quadratic Verification**: Every step must include a verification plan (Unit, E2E, or Manual).

## Phase 3: Handoff (End of Epoch 1)
To prevent context poisoning and token fatigue, we enforce a "Fresh Start" for the implementation phase.

1.  **Approval**: Request user approval for the plan.
2.  **The Fresh Start Instruction**: Once approved, output the following exactly:
    > "✅ **Epoch 1 (Architect) Complete.** To begin implementation, please start a **FRESH CHAT**. Feed me ONLY **GEMINI.md** and this **implementation_plan.md**, then trigger the **[/execute](file://./execute.md)** workflow."

## Markdown Template

```markdown
# 🏗️ Feature Implementation Plan
**Status:** `0%`

## 🎯 Objective
One sentence on what we are building.

## 🧠 Critical Decisions
* **Architecture:** [e.g., "Using Zustand for global state"]
* **Trade-offs:** [e.g., "Simplifying UI to meet latency targets"]
* **Security:** [RLS impact or Auth requirements]

## 📋 Execution Tasks

- [ ] 🟥 **Step 1: [Name]**
  - **Action:** [Brief description of code changes]
  - **Files:** `[file_list]`
  - **Verification:** [e.g., "npx vitest tests/unit/logic.test.ts"]

...

## 🛡️ Premortum
* **Risk:** [What could go wrong?]
* **Mitigation:** [How we prevent it]
```