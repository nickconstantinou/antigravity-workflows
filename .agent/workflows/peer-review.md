---
description: 
---

---
description: Peer Review Synthesis & Validation
---

A different AI model has reviewed your code. You are the **Lead Engineer**. Your job is to act as a "Skeptic-in-Chief." Validate findings with code-based evidence before touching the implementation.

## 📥 Input
[PASTE FEEDBACK FROM OTHER MODEL]

## 🛠️ The Validation Protocol

1.  **Evidence Search**: For every "Issue" reported, use `grep` or `find` to see the actual code. 
    - *Critique*: If the reviewer says "missing error handling," look at the file. Is there a global error boundary the reviewer missed?
2.  **Architectural Alignment**: Ensure the reviewer’s "Fix" doesn't violate **AGENTS.md** (e.g., ensure they aren't suggesting a new library or an unnecessary microservice).
3.  **The "False Positive" Test**: Deliberately try to prove the reviewer wrong before agreeing with them.

## 📤 Output

### 🛡️ Validated Issues (Evidence-Backed)
* **Issue**: [Description]
* **Proof**: [Reference specific line numbers or test failures that confirm the bug]
* **Fix**: [Briefly state the refined approach]

### 🗑️ Dismissed Issues (Hallucinations/False Positives)
* **Issue**: [Description]
* **Evidence of Correctness**: [Why the current code is actually correct. e.g., "Line 42 already handles this via the X provider."]
* **Context**: [If the reviewer missed project-specific patterns from AGENTS.md]

### 📝 Execution Plan
1. **Prepare**: Update the **Verbose Header** to reflect any logic changes.
2. **Draft**: Implement validated fixes.
3. **Verify**: Re-run the **Quad Gate** (Test, Logic, Lint, Efficiency).

---
**Lead Engineer Note**: If the reviewer suggests a fix that is technically correct but "over-engineered," simplify it to the most minimal, readable version that satisfies the requirement.