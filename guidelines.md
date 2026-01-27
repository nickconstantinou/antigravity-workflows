---
description: Architectural Guidelines (AI, State, Mobile)
---

# 📐 Workflow: Architectural Guidelines

This workflow provides standard patterns for specific technology layers in Antigravity projects.

## 🧠 AI Engineering
- **The Dispatcher**: Use a single Entrypoint switching on an `action` param.
- **Async Reliability**: Use `EdgeRuntime.waitUntil` or fire-and-forget for heavy loops.
- **Structured JSON**: Request JSON from Gemini and validate with Zod.

## ⚛️ State Management (Zustand)
- **Atomic Stores**: Separate stores for distinct features (e.g., `useAuthStore`).
- **Strict Selectors**: Never export the whole state hook.
- **Encapsulation**: State mutations happen *inside* the store via Actions.

## 📱 Mobile & Web App Dev
- **Expo Router**: Use file-based routing in `app/`.
- **NativeWind**: Use `className` for all styling.
- **Web Compatibility**: Always check `Platform.OS === 'web'` for DOM-only libraries.

## 🛡️ The Laws of Physics
- **Result Pattern**: Functions return `Result<T, E>` values.
- **Atomic Units**: Files and functions have a single responsibility.
- **Strict Typing**: No `any` allowed.
