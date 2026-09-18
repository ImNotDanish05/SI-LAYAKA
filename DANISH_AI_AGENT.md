# DANISH_AI_AGENT.md
> This file is for AI agents, not humans. Update after finishing every task. Read this BEFORE exploring other files.

## Overview
SI-LAYAKA is an Indonesian personnel-administration system for Universitas Diponegoro. It runs a Vercel serverless/Supabase deployment while retaining Google Apps Script source files and deployment configuration.

## Stack
Node.js >=18; Vercel Serverless Functions; Supabase Postgres via `@supabase/supabase-js`; legacy/parallel Google Apps Script V8 web app. The frontend is static HTML/CSS/JS assembled from source `.txt` files by PowerShell.

## Commands
- Build frontend: `powershell -ExecutionPolicy Bypass -File build.ps1`
- Package scripts: none defined in `package.json`.
- Tests: none defined; `check_encoding.js` is an ad-hoc utility.

## Structure map
- `api/` — Vercel endpoints; `rpc.js` is the primary POST RPC dispatcher.
- `public/` — deployed static assets, including generated `index.html`.
- `supabase/` — incremental database migrations.
- `supabase_schema.sql` — database schema reference.
- `templates/` — DOCX templates.
- `*.gs v2.txt`, `*.txt` — Google Apps Script and frontend source fragments.
- `build.ps1` — merges source fragments into `public/index.html`.
- `appsscript.json` — Apps Script deployment configuration.

## Conventions that differ from defaults / can't be inferred
- Browser calls use a `google.script.run` compatibility polyfill that POSTs `{ method, params }` to `/api/rpc`.
- `api/rpc.js` supports environment-variable aliases for Supabase credentials; never put credentials in source.
- Document-related backend code can call `GOOGLE_SCRIPT_URL` and uses local DOCX tooling (`pizzip`/`docxtemplater`).
- Database changes should be additive migrations in `supabase/migrations/`.
- The source frontend is not `public/index.html`; edit its fragments then rebuild.

## DO NOT touch
- `.env` — local secrets.
- `node_modules/`, `.vercel/`, and `scratch/` — ignored/generated local state.
- Existing generated files or database schema destructively without explicit approval.

## Known gotchas
- No README, package scripts, linter, formatter, or automated tests are currently present.
- `api/rpc.js` and frontend source fragments are large: search for the relevant function before reading.
- `RENCANA_OPTIMASI.md` describes a proposed concurrency plan; do not treat it as implemented behavior without code verification.

## Changelog (newest first, 1 line per entry, NOT a diff)
- 2026-09-18: Added initial agent context from a high-level first scan; awaiting user review.
