# N8N-Public-Templates
N8N flows and documentations

## Supabase Enrichment SQL Function

This repository includes an **optional Supabase SQL function** that enables **safe, production-ready enrichment updates** for creator records.

The function is designed to work with n8n workflows and enrichment APIs by **filling only missing fields** in your database — without overwriting existing data.

---

### What this function does

- ✅ Updates **only NULL fields** using `COALESCE`
- ✅ Matches rows using `(creator_handle, platform)`
- ✅ Preserves all existing data
- ✅ Does **not** modify primary keys
- ✅ Safe to re-run multiple times
- ✅ Contains **no secrets or credentials**

This makes it ideal for enrichment workflows where data may arrive incrementally or partially.

---

### When should you use this?

Use this function if you want:

- A **non-destructive** update strategy
- Protection against accidental overwrites
- A safer alternative to direct `UPDATE` operations in n8n
- A production-friendly enrichment pipeline

If you prefer a simpler setup or are just experimenting, you can skip this function and use direct updates instead.

---

### Installation (one-time setup)

1. Open your **Supabase Dashboard**
2. Go to **SQL Editor**
3. Copy the contents of:
supabase/Enrich creator contacts with social platform data from influencers.club - Supabase.sql
4. Paste it into the SQL editor
5. Click **Run**

That’s it — the function is now available in your database.

---

### Function signature

```sql
public.enrich_lead(
  p_creator_handle TEXT,
  p_platform TEXT,
  p_payload JSONB
)


