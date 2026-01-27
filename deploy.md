---
description: Deploy
---

# Workflow: Deploy
1. **Pre-flight:** - Run `npm run lint`.
   - Execute Unit & end to end tests
   - Verify `railway.json` and `supabase/config.toml` exist.

2. **Infrastructure & Backend:** - **Database:** Run `supabase migration push` to sync remote schema.
   - **Edge Functions:** Run `supabase functions deploy` to push all functions.
   - **Env Vars:** Sync Railway environment variables (`railway variables --set ...`).

3. **Push & Build:** - Execute `git push origin main`.
   - Trigger `railway up` and monitor the build logs.

4. **Verify:** - Use the browser tool to visit the Railway URL.
   - Confirm the build is live and run a smoke test on a core Edge Function endpoint.