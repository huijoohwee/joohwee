---
title: "Knowgrph Storage Sync - Cloudflare D1"
owner: "knowgrph"
status: "implemented"
updated: "2026-05-08"
---

# Knowgrph Storage Sync - Cloudflare D1

## Authoring Contract

- The opening YAML frontmatter block remains the first-block machine SSOT for storage-handoff metadata, ownership, and runtime sync configuration.
- This document is a canonical authored runtime handoff doc, not a typed normalization fixture.
- Frontmatter stays in plain YAML so the file demonstrates the default authoring path for storage, deployment, and sync guidance.
- If typed `{key, type, value}` envelopes are needed for ingestion-regression coverage, that validation should live in a dedicated fixture doc rather than replacing the canonical storage handoff example.
- Runtime behavior must still be derived from parsed frontmatter and document content only, never from file path assumptions or hardcoded demo fallbacks.

This document is the runtime handoff for the storage ladder:

1. Canonical markdown authoring source: `huijoohwee/docs/**`
2. Per-device working store: RxDB (browser IndexedDB)
3. Shared cloud store: Cloudflare Worker + Cloudflare D1

## Seed Source Of Truth

The workspace initialization seed family is sourced from this directory:

- `knowgrph-maps-readme.md`
- `knowgrph-video-demo.md`
- `knowgrph-maps-places.md`

The app reads these files through:

- `VITE_WORKSPACE_INITIALIZATION_DOCS_ABS_ROOT`

Example local value:

```bash
VITE_WORKSPACE_INITIALIZATION_DOCS_ABS_ROOT=<repo>/huijoohwee/docs
```

## Cloudflare D1 And Worker

Worker config path:

- `knowgrph/cloudflare/workers/knowgrph-storage/wrangler.toml`

Migration path:

- `knowgrph/cloudflare/d1/migrations/0001_knowgrph_storage.sql`

Run from `knowgrph/`:

```bash
npm run storage:d1:migrate:remote
npm run storage:worker:deploy
npm run storage:d1:seed:docs
```

Or one-step deploy:

```bash
npm run storage:deploy
```

Dry-run (no remote write):

```bash
npm run storage:d1:seed:docs:dry-run
```

## Production Base URL

If storage API is not served on the same origin as the SPA, set:

```bash
VITE_KNOWGRPH_STORAGE_BASE_URL=https://<your-worker-domain>
```

For `airvio.co/knowgrph`, keep this empty when `/api/storage/*` is same-origin; set it only when API lives on a separate Worker domain.
