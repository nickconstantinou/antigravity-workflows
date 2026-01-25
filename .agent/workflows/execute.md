---
description: 
---

---
description: Execution Mode
---

Implement the current step from the plan. You are now in **Epoch 2 (The Builder)**.

## 🛡️ Epoch 2 Scope & Rules
1.  **Fresh Context**: You must be in a fresh chat session. Read ONLY **GEMINI.md** and the approved **implementation_plan.md**. Ignore all historical brainstorming noise.
2.  **Strict Adherence**: Follow the plan. If the plan is wrong, **STOP** and ask to update the plan.

2.  **Code Style**:
    - DRY (Don't Repeat Yourself).
    - Strong Typing (No `any` unless absolutely necessary).
    - Comments explaining *why*, not *what*.

3.  **Docs**: Update JSDoc/comments/headers as you write the functions.

## Workflow per Prompt

For every single step in the plan, perform this cycle:

[R]ead: Re-read the specific step from the "Feature Implementation Plan".
[C]ode: Output the minimal, clean, production-ready code for that step.
[Q]uad Gate: Verify the code meets the criteria:
- Test: Does it pass the relevant tests?
- Logic: Is it type-safe (tsc compliant)?
- Lint: Is it clean?
- Efficiency: Is it performant?
[U]pdate: Reprint the "Feature Implementation Plan" with the current step marked as 🟩 Done and update the overall progress percentage.

## 🏁 End of Epoch 2
Once all steps are marked as **Done**:
1. Verify the **Quad Gate** one last time.
2. Instruct the user: 
   > "🛠️ **Epoch 2 (Builder) Complete.** To finalize documentation and sync memory, please start a **FRESH CHAT**. Feed me the **git diff** of these changes and **AGENTS.md**, then trigger the **[/close-issue](file://./close-issue.md)** workflow."