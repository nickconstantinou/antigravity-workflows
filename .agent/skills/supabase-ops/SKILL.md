---
name: supabase-ops
description: Manages local Supabase development including migrations, schema diffing, type generation, and edge function deployment. Use this when the user mentions "migration", "db reset", "edge function", or "syncing types".
---

# Supabase Operations Skill

This skill ensures all database changes are version-controlled via migrations and that the frontend types stay in sync.

## Core Workflows

### 1. Database Migrations
- **New Migration**: When creating a table/column, run `supabase migration new <name>`.
- **Apply Changes**: Use `supabase migration up`.
- **Reset Environment**: Use `supabase db reset` to wipe local data and restart from migration zero. 
- **Reset Environment**: Use `supabase db reset --no-seed` followed by explicit `seed.sql` loading if needed.
- **!! WARNING !!**: Never use the Supabase Dashboard to modify schema. Always use `db diff`.

### 2. Robust Reset Strategy (The "Nuclear Option")
Use this when the database state is corrupt or containers are out of sync with `.env`.
1.  **Sync Env Vars**: `ln -sf ../../.env supabase/functions/.env` (SSOT Strategy)
2.  **Reset without Seed**: `sudo npx supabase db reset --no-seed --yes`
3.  **Restart Services**: `sudo npx supabase stop && sudo npx supabase start`
4.  **Load Seed Data**: Execute directly into the container:
    ```bash
    sudo docker exec -i supabase_db psql -U postgres -d postgres < supabase/seed.sql
    ```
5.  **Gen Types**: `sudo npx supabase gen types typescript --local > src/types/supabase.ts`

### 3. Secrets Management (Single Source of Truth)
- **Local -> Cloud**: We treat the local `.env` as the SSOT.
- **Sync Command**: Run `npm run secrets:sync` to push `.env` changes to Supabase Edge Functions.
  - Automatically filters securely (only `GEMINI_`, `EXA_`, `SUPABASE_`).
  - Strips `EXPO_PUBLIC_` prefixes for backend cleanliness.
  - Requires `supabase login`.

### 4. Schema Sync & Type Safety
- **Schema Diff**: After making manual local changes for testing, run `supabase db diff -f <feature_name>` to capture them.
- **Type Generation**: After any schema change, run:
  `supabase gen types typescript --local > src/types/supabase.ts`

### 5. Edge Functions
- **Local Dev**: Use `supabase functions serve <function-name>`.
- **Deployment**: Use `supabase functions deploy <function-name>`. Ensure shared logic stays in `supabase/functions/_shared`.

## How to execute commands
1. Verify Docker is running.
2. Run `supabase status` to confirm local endpoint health.
3. Execute the specific command based on the user's intent.

### 5. Auth & JWT Troubleshooting
Use this when the user faces "Invalid JWT" errors or env var mismatches between CLI and Edge Runtime.
1.  **Generate HS256 Key**: `node scripts/generate_valid_key.js` (Fixes ES256 vs HS256 mismatch).
2.  **Verify Env**: `ls -l .env` (Ensure file exists).
3.  **Sync Secrets**: `ln -sf ../../.env supabase/functions/.env` (Ensure SSOT Link). (Explicitly provide secrets to runtime).
4.  **Restart**: `sudo npx supabase stop && sudo npx supabase start` (Force inject variables).
5.  **Verify**: `npx tsx scripts/debug_auth_discovery.ts` (Confirm fix).

## Constraints
- **Zero Destructive Actions**: Prefix any `db reset` or `DROP` with a confirmation request to the user.
- **RLS Check**: Every new table migration MUST include a `ALTER TABLE ... ENABLE ROW LEVEL SECURITY;` statement.
