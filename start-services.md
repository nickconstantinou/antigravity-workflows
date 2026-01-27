---
description: Start all local development services (Supabase and Expo).
---

---
Service Startup Workflow
---

This workflow automates the process of bringing up the local development environment.

## 1. Kill Existing Expo/Supabase Process
Stop any Expo/Supabase server already running on port 8081 to avoid conflicts.
// turbo
```bash
kill $(lsof -t -i:8081) 2>/dev/null || echo "No process on 8081"
sudo npx supabase stop
```

## 2. Start Supabase
Ensure the local Supabase stack (Postgres, Auth, Edge Functions) is running.
// turbo
```bash
sudo npx supabase start
```

## 3. Start Expo Web
Launch the frontend application in web mode.
// turbo
```bash
cd exam-pulse-app && npm run web
```

## 4. Verify Services
Check that everything is operational.
// turbo
```bash
sudo npx supabase status
```