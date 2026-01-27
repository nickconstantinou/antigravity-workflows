---
description: Comprehensive Code Review
---

---
description: "Epoch 2 (Final Gate): Peer Review. Enforces architectural strictness before code is merged."
trigger: "/review"
---

# 🕵️ Workflow: The Gatekeeper (Peer Review)

This workflow triggers a **Senior Staff Engineer** level audit. It is the final defense against entropy.

## 📋 Strict Compliance Checklist

### 1. 📐 The Contract (Type Safety)
- [ ] **Zero `any`**: Are there any explicit or implicit `any` types? (Reject if yes).
- [ ] **Exhaustiveness**: Are all union types handled in switch statements?

### 2. 🛡️ The Flow (Result Pattern)
- [ ] **Death to Exceptions**: Does the code use `return Result.err()` instead of `throw new Error()`?
- [ ] **Error Handling**: Are errors treated as typed values?

### 3. ⚛️ The Structure (Atomic Modularity)
- [ ] **Single Purpose**: Does the file do exactly one thing?
- [ ] **Dependency Hygiene**: Are imports explicit? (No circular dependencies).

### 4. 🧪 The Truth (Verification)
- [ ] **Test as Spec**: Do the tests cover the "Truth Table"?
- [ ] **Deterministic Replay**: Can the tests run without external network calls?

## 📤 Output Format
1. **Verdict**: [APPROVED / REQUEST CHANGES]
2. **Analysis Matrix**: (Atomic, Types, Pattern, Tests)
3. **Violations**: List specific file/line and required fix.

## 🛑 The "No-LGTM" Rule
Do not simply say "Looks good." You must prove you analyzed the logic.