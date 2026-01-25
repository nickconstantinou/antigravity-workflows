# AGENTS.md

This file serves as the persistent memory for autonomous agents working on **Antigravity Workflows**.
It captures high-level context, architectural patterns, "gotchas," and lessons learned to ensure continuity between sessions.

## 🌟 The Golden Rules (Operational Constraints)

1.  **Modular Monolith > Microservices**: Keep all logic within this repository. Do not suggest or create external microservices. Use internal modules in `src/lib/` to manage complexity.
2.  **The "Verbose Header" Rule**: Every new file (Logic, Component, or Function) **MUST** start with the following header block:
    ```typescript
    /**
     * PURPOSE: [One sentence: What does this file do?]
     * INPUTS: [What data does it consume?]
     * OUTPUTS: [The primary result/side-effect?]
     * NEIGHBORS: [Key files/modules it interacts with]
     * LOGIC: [Plain-English summary of the algorithm/intent]
     */
    ```
3.  **Test-First Scaffolding**: Before writing implementation logic for a new feature, you must create a `*.test.ts` file in `src/test/` to validate the logic.
4.  **No Ghost Dependencies**: Never install a new `npm` or `pip` package without explicit human confirmation. 
5.  **Proximity of Truth**: Define shared types in `src/types/` or `database.types.ts`. Avoid local re-declarations.

## 🧠 Core Context
- **Project**: Antigravity Workflows (Standard Agent Lifecycle & Skills)
- **Goal**: Provide a portable, high-fidelity agentic workflow system.
- **Current Sprint**: Generalizing for GitHub publication.

## 🏗️ Architecture Patterns
- **Frontend**: Expo Router, NativeWind (Tailwind), Reanimated.
- **Backend**: Supabase (Postgres, Edge Functions, Auth).
- **State**: Local React State (mostly), transitioning to Zustand for global.
- **Testing**:
  - `vitest` for Logic/Unit tests (Follow **Arrange-Act-Assert**).
  - `Playwright` for E2E (POMs in `tests/e2e/pom/`, Global Auth in `tests/e2e/utils/auth-setup.ts`).
  - `npx expo lint` for Style.
- **Observability**:
  - All automated tool actions should be wrapped in `GlassBoxLogger` (Standard pattern: `[Tool] => LOG => [Outcome]`).

## ⚠️ Gotchas & Lessons Learned
- **Web Compatibility**: Always wrap `Haptics` and other native-only modules in `Platform.OS !== 'web'` checks.
- **Supabase Types**: Do not use `any`. Use generated types from `database.types.ts` or create strict Interfaces.
- **Edge Functions**: Must complete within **400ms** for perceived latency targets. Use strict timeouts.
- **Artifacts**: Store temporary artifacts in `~/.gemini/antigravity/brain/...`.
- **Linting**: Pre-commit requirement: `npx expo lint` must be clean.
- **RPC & Views**: Avoid relying on `auth.uid()` in Views if accessed via `SECURITY DEFINER` RPCs with custom user context. Use direct table queries instead.
- **Daily Pulse**: Always filter node candidates by `total_questions > 0` to avoid targeting empty container nodes.
- **Playwright & RNW**: `testID` prop translates to `data-testid` on Web. Use `waitForFunction` with opacity checks for Reanimated animations, as strict visibility may fail.
- **Playwright Visual Snapshots**: First run will fail (no baseline). Re-run with `--update-snapshots` to establish baselines.
- **AppState Death Loop (Web)**: Avoid `AppState` listeners in the root `AuthProvider` on Web. It can trigger high-frequency re-renders if standard DOM events conflict with the RN polyfill.
- **Reanimated Ghost Form (Web)**: `Animated.View` entering animations can fail on Web if the parent re-renders within the first 16ms, leaving the container at `opacity: 0`. Disable `entering` props on Web for critical UI (Login, etc.) to ensure immediate visibility.
- **Environment Variables**: Use the Root `.env` as the Single Source of Truth. Symlink it to sub-projects (`ln -s ../.env .env`). Never use `CUSTOM_SERVICE_ROLE_KEY` or process-level double fallbacks.
- **Web Compatibility**: Always wrap `Haptics` and other native-only modules in `Platform.OS !== 'web'` checks.
- **Metro & ESM (`import.meta`)**: Modern libraries (e.g., `zustand`, `reactflow`) often ship raw ESM using `import.meta`, which crashes Metro Web. **Fix:** Use `metro.config.js` `resolver.resolveRequest` to force the package to resolve to its **CommonJS** build.
- **Supabase Types**: Do not use `any`. Use generated types from `database.types.ts` or create strict Interfaces.

## 🗺️ Key File Locations
- **Routes**: `app/`
- **Components**: `src/components/`
- **Logic/Utils**: `src/lib/`
- **Tests**: `src/test/`
- **Server**: `supabase/functions/`

## 🛠️ Available Skills (Procedural Memory)
- **[supabase-ops](file://./skills/supabase-ops/SKILL.md)**: Migrations, Edge Functions.
- **[mobile-app-dev](file://./skills/mobile-app-dev/SKILL.md)**: Expo, NativeWind, Platform checks.
- **[state-management](file://./skills/state-management/SKILL.md)**: Zustand Atomic Stores.
- **[ai-engineering](file://./skills/ai-engineering/SKILL.md)**: Edge Function Patterns, Gemini.
- **[refactoring](file://./skills/refactoring/SKILL.md)**: Monolith First, Proximity Test.
- **[testing](file://./skills/testing/SKILL.md)**: The Quad Gate.
- **[context-maintenance](file://./skills/context-maintenance/SKILL.md)**: "The Closing Ritual" and Housekeeping.

## 🔄 Available Workflows
*See the **[Agent Workflow Guide](file://./docs/AGENT_WORKFLOW_GUIDE.md)** for detailed lifecycle instructions.*
- **[/start-services](file://./workflows/start-services.md)**: Launch Expo, Supabase, and Dev Server.
- **[/create-plan](file://./workflows/create-plan.md)**: Unified Research & Implementation Planning.
- **The Epoch Protocol**: We divide development into three context-isolated stages: **Architect** (Plan), **Builder** (Code), and **Historian** (Sync).
- **Fresh Start Rule**: **Epoch 2** (Implementation) and **Epoch 3** (Cleanup) MUST begin in a fresh chat session to prevent "brain drain" and context poisoning.
- **[/create-issue](file://./workflows/create-issue.md)**: Capture bugs/features mid-flight.
- **[/close-issue](file://./workflows/close-issue.md)**: Verify, Sync Memory, and Push to GitHub.

## 🔄 The Ralph Loop (Quad Gate)
The agent MUST follow the [RALPH Protocol](file://./skills/ralph/SKILL.md).
Before marking a task as DONE, verify:
1. **Test**: `npm run test` (Unit) or `npx playwright test` (E2E).
2. **Logic**: `tsc --noEmit` passes (0 errors).
3. **Lint**: `npx expo lint` passes (0 warnings).
4. **Efficiency**: Check Edge Function latency < 400ms.

## 🛡️ Security & Risks
- **Accepted Risks**:
  - `markdown-it` (DoS Vulnerability): No fix available for `react-native-markdown-display`. Risk is low (client-side DoS).
  - `tar` (High Severity): Requires Expo SDK 54 upgrade. **STATUS: PARKED.** See `docs/PARKED_EXPO_54_UPGRADE.md` for the failed attempt log before re-opening.

## 🔒 Critical Data & Persistence
- **Migrations (`supabase/migrations/`)**: Contains vital schema logic.
    - `20260123000000_visual_entropy.sql`: Creates `user_node_unlocks` / `user_node_states`. **DO NOT DELETE**.
    - `20260222_unify_mastery_schema.sql`: Defines the unified `user_node_progress` view.
    - `20260223_fix_knowledge_map_rpc.sql`: Restores Knowledge Map RPC using direct table logic (bypassing view auth issues).
- **Seeding Script**: `exam-pulse-app/scripts/reseed_test_data.ts`.
    - Run via: `npx tsx scripts/reseed_test_data.ts`
    - Restores AQA Maths & Edexcel Psychology data from mocks.
- **Mock Data**: `tests/mocks/data/` - Source of truth for content.

## 📋 Post-MVP / Future Polish
- **Skia Web WASM Hosting**: The Skia WASM (`canvaskit.wasm`) must be served from a CDN (e.g., Unpkg, Cloudflare R2) with the correct `application/wasm` MIME type. Metro/Expo dev server cannot serve `.wasm` files directly with the correct headers. Until this is done, the `WithSkiaWeb` component uses a "Smart Fallback" pattern (CSS-only rendering on Web).
