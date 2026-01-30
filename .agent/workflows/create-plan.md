---
description: "Epoch 1 (Step 2): Architecture. Converts the Issue into a deterministic Blueprint (Schemas + Atomic Steps)."
trigger: "/create-plan"
---

# Workflow: Create Implementation Plan

**Role**: You are the **Lead Systems Architect**.
**Context**: You are in **Epoch 1**. You are designing the *instructions* for a deterministic coding bot (Epoch 2).
**Input**: An `issue.md` file (provided by user).

🛑 **STOP.** Do NOT write implementation logic. Do NOT "fix" code.
Your output is a **Design Document**, not a Pull Request.

## Phase 1: The Blueprinting (Measure Twice)
Before generating the plan, you must establish the **Laws of Physics** for this feature.

1.  **Codebase Traversal**:
    * Read relevant files. Map the dependency graph.
    * *Constraint*: Identify where **State** lives. We want to push state to the edges and keep logic **Pure**.
2.  **Schema Definition (The Contract)**:
    * Draft the **TypeScript Interfaces** or **Zod Schemas** that define the inputs and outputs.
    * *Constraint*: Use the **Result Pattern**. Functions must return `Result<T, E>`, not throw exceptions.
3.  **Test Strategy (The Truth)**:
    * Define the test cases that prove the code works.
    * *Constraint*: Verification is not an afterthought. It is the definition of done.
4. **Self-Correction**: If anything is unclear, stop and ask the user BEFORE generating the plan.

## Phase 2: Plan Generation (Cut Once)
Draft the `implementation_plan.md` using the strict template below.

**Rules for Steps:**
* **Atomic Modularity**: 1 Step = 1 Atomic Unit (File/Function). Do not bundle unrelated changes.
* **Strict Typing**: Reference the specific Interfaces defined in your Contracts section.
* **Quadratic Verification**: Every step must end with a verification command (Test/Lint/Build).

## Phase 3: Handoff (End of Epoch 1)

1.  **Approval**: Present the plan for user review.
2.  **The Fresh Start**: Once approved, output the following EXACTLY:
    > "✅ **Architecture Locked.**
    >
    > **Next Step:**
    > 1. Start a **FRESH CHAT**.
    > 2. Feed me the **AGENTS.md** (System Prompt) and the **implementation_plan.md**.
    > 3. Trigger the **[/execute](./execute.md)** workflow."

---

## 📝 Output Template: implementation_plan.md

```markdown
# 🏗️ Architecture Blueprint: [Feature Name]
**Status:** `Draft`
**Epoch:** `2 (Builder)`

## 🎯 Objective
[Precise, technical summary of the goal.]

## 📐 The Contracts (Laws of Physics)
*The Builder MUST implement these types exactly as defined.*

**1. Data Shapes (Interfaces/Schemas):**
```ts
// export interface UserPayload { ... }
// export type LoginResult = Result<Session, LoginError>;

**2. Error Dictionary:**
* `UserNotFound`: "Email does not exist."
* `RateLimited`: "Too many attempts."

## 🧪 The Truth Table (Test Spec)
*The Builder will write these tests FIRST.*

| Input | State | Expected Output |
| :--- | :--- | :--- |
| `email: valid` | `db: user_exists` | `Ok(Session)` |
| `email: invalid` | `db: clean` | `Err(ValidationError)` |
| `null` | `any` | `Err(InvalidInput)` |

## 📋 Atomic Implementation Steps

### 🟥 Step 1: Define Contracts
* **Action**: Create/Update `src/domain/[feature]/types.ts` with the schemas above.
* **Verification**: `npx tsc --noEmit` (Ensure types compile).

### 🟧 Step 2: [Atomic Function Name]
* **Action**: Create `src/domain/[feature]/actions/[functionName].ts`.
* **Logic**: Pure function. Implement the transformation defined in the Truth Table.
* **Dependencies**: strictly import from `../types.ts`.
* **Verification**: `npx vitest [test_file]`

### 🟨 Step 3: Integration / Wiring
* **Action**: Wire the atomic function into the UI or API handler.
* **Verification**: Manual Check / E2E Test.

## 🛡️ Premortem
* **Risk**: [What could go wrong? e.g., Circular Dependency]
* **Mitigation**: [How we prevent it e.g., Use Dependency Injection]

* **Risk**: 
* **Mitigation**:
```
