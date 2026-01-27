# AGENTS.md

This file serves as the persistent memory for autonomous agents working on **Antigravity Workflows**.
It captures high-level context, architectural patterns, "gotchas," and lessons learned to ensure continuity between sessions.

## 🌟 The Golden Rules (Operational Constraints)

1.  **Workflows-Only**: This repository is a library of workflows. Do not add component or application logic here.
2.  **Flat Structure**: All workflows MUST reside in the root to support `.agent/workflows` direct installation.
3.  **Self-Contained**: Each workflow should contain its own procedural knowledge (no dependencies on external skill files).

## 🏗️ Architecture Patterns
- **Technology Layer**: Workflows assume a Supabase (Backend) + Expo (Frontend) stack unless otherwise specified.
- **Strictness**: Enforce the **Result Pattern**, **Atomic Modularity**, and **Strict Types** in all generated plans.

## 🔄 Available Workflows
- **[/init](file://./init.md)**: Project Initialization.
- **[/create-plan](file://./create-plan.md)**: Unified Research & Implementation Planning.
- **[/execute](file://./execute.md)**: Deterministic Code Generation.
- **[/refactor](file://./refactor.md)**: Migrate legacy code to the Atomic Blueprint.
- **[/review](file://./review.md)**: Senior Architect level audit.
- **[/supabase](file://./supabase.md)**: DB migrations, type safety, and secrets.
- **[/github](file://./github.md)**: Feature branches, atomic commits, and PRs.
- **[/deploy](file://./deploy.md)**: Multi-stage deployment (Supabase + Railway).
- **[/test](file://./test.md)**: Quad Gate verification suite.
- **[/guidelines](file://./guidelines.md)**: Structural & architectural standards.

## 🛡️ Security & Risks
- **Security**: Never include secrets in workflow files.
- **Persistence**: Multi-stage (Epoch) workflows MUST use artifacts in `~/.gemini/antigravity/brain/` for state management across sessions.
