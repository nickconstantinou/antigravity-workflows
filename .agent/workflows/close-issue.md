---
description: Close Issue
---

# Workflow: Close Issue (Epoch 3: The Historian)

You are now in **Epoch 3**. Your goal is cleanup and memory consolidation.
**Context Rule**: You should be in a fresh chat. Read ONLY **AGENTS.md** and the **git diff** of the final changes.

This workflow ensures that every completed task adheres to the **Antigravity Golden Rules**, updates persistent memory, and maintains a clean repository state.

## 1. Final Quality Audit (The Quad Gate) ✅
Before closing, the agent must verify:
- [ ] **Headers**: Every new/modified file contains an accurate **Verbose Header**.
- [ ] **Tests**: New logic is validated by passing unit or E2E tests.
- [ ] **Rules**: Code adheres to the "Monolith First" and "Proximity" principles in `AGENTS.md`.
- [ ] **Progress**: Update `REFACTOR_PROGRESS.md` if this task contributed to the long-term migration.

## 2. Documentation Sync 📝
*The map must match the territory. Update truth sources.*
- [ ] **Audit**: Scan git diffs for new Env Vars, Dependencies, or Schema changes.
- [ ] **CHANGELOG.md**: Add entry under `## Unreleased` describing user-facing changes.
- [ ] **README.md**: Update "Setup" or "Usage" if dependencies or signatures changed.
- [ ] **AGENTS.md (Persistent Memory)**:
    - Update "Gotchas & Lessons Learned" with any unique fixes (e.g., "Reanimated Web Ghost Form").
    - Ensure `NEIGHBORS` lists in file headers are accurate.
- [ ] **Inline Docs**: Add JSDoc to complex functions if missing.

## 3. Issue Closure & Cleanup 📂
- **Resolution Summary**: Append a "Resolution" section to the issue file.
  - *Format*: Briefly state the fix and architectural changes.
  - **IMPORTANT**: You must **EMBED THE FULL TEXT** of the `walkthrough.md` directly into the issue resolution section. Do not just link to it. Provide clear "Before/After" or "Verification Evidence" headers within the embedded text.
- **Move to Complete**: Move the issue file from `docs/issues/open` to `docs/issues/closed`.
  - *Tip*: Ensure the target directory exists (e.g., `mkdir -p docs/issues/closed/tech-debt`) before moving.
- **Workspace Cleanup**: Delete temporary files and test artifacts.
  - *Targets*: `implementation_plan.md`, `test_scratchpad.ts`, `exam-pulse-app/test-results/`, `exam-pulse-app/playwright-report/`.

## 4. Long-Term Memory Sync (The Closing Ritual) 🧠
*Ensure the next agent starts with the wisdom of this task.*
- [ ] **Consolidate**: Add any new "Gotchas" or pattern discoveries to `AGENTS.md`.
- [ ] **Verify**: Ensure all file links in `AGENTS.md` and `SKILL.md` are still valid.
- [ ] **Trash**: Delete the `task.md` and `implementation_plan.md` in the artifacts folder as they are now captured in the issue's resolution.

## 5. Git Synchronization 🚀
- **Atomic Commits**: Ensure all changes are committed with clear, descriptive prefixes (`feat:`, `fix:`, `refactor:`, `docs:`).
- **Push**: Push the validated branch to GitHub.
- **Branch Management**: If the task is fully merged, delete the local feature branch.

---
**Note for Agents**: Do not mark a task as "Done" until the documentation is verified and the workspace is clean.