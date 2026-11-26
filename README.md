# RemitNuru

Customer PWA and operator desk for CAD to East Africa transfers. Without Supabase keys the app runs in the browser and stores the session in localStorage. Sandbox FX rates match the edge functions: UGX 300, KES 90, ETB 40, SOS 75.

## Run

```bash
cd frontend/web
npm install
npm run dev
```

From the repo root, `npm run build` compiles the web app.

Operator sandbox login: `admin@remitnuru.ca` / `remitnuru`.

## Supabase

Apply `supabase/migrations/20261123000001_initial_schema.sql`, create the `remitnuru-assets` storage bucket, then deploy:

```bash
supabase functions deploy kyc-submit
supabase functions deploy kyc-status
supabase functions deploy remit-create
supabase functions deploy remit-status
supabase functions deploy fund-confirm
```

Copy `.env.example` and set the project URL, anon key, service role, and partner sandbox keys. Edge functions use the service role. The customer UI does not ship that key.

`transactions_audit.transaction_id` is nullable so a KYC submission can be logged before a transfer exists. Audit rows cannot be updated or deleted.
