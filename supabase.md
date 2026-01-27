---
description: Supabase Operations (Migrations, Types, Functions)
---

# ⚡ Workflow: Supabase Operations

This workflow ensures all database changes are version-controlled and that types stay in sync.

## 🛠️ Core Commands

### 1. Database Migrations
* **New Migration**: `supabase migration new <name>`
* **Apply Changes**: `supabase migration up`
* **Reset Environment**: `supabase db reset`

### 2. Schema Sync & Type Safety
* **Schema Diff**: `supabase db diff -f <feature_name>`
* **Type Generation**: 
  ```bash
  supabase gen types typescript --local > src/types/supabase.ts
  ```

### 3. Secrets Management
* **Sync Secrets**: `npm run secrets:sync` (Pushes `.env` to Edge Functions)

### 4. Edge Functions
* **Local Dev**: `supabase functions serve <function-name>`
* **Deployment**: `supabase functions deploy <function-name>`

## 🛡️ Constraints
- **Zero Destructive Actions**: Prefix any `db reset` or `DROP` with a confirmation request.
- **RLS Check**: Every new table MUST include an `ENABLE ROW LEVEL SECURITY` statement.
