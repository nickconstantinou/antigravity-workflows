---
description: Run the full test suite including unit, integration, and browser verification flows.
---

---
description: Robust Test Suite Execution
---

## 1. Quality Gate
Execute the full verification suite as defined in `skills/testing/SKILL.md`.

### Unit & Logic
// turbo
```bash
npm run test
```

### End-to-End (Browser)
// turbo
```bash
npx playwright test
```