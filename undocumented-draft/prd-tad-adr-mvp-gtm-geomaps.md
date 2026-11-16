---
title: "Geo map technology stack — grounding and verification companion"
doc_type: "Evidence Record"
version: "0.4.1"
date: "2026-11-16"
lang: "en-US"
frontmatter_contract: "required"
owner: "Solo Founder / AI Orchestrator"
continuity_id: "geostack"
parent_plan: "prd-tad-adr-mvp-gtm-geostack.md@0.4.1"
lifecycle_status: "active"
load_policy: "on-demand"
---
# Grounding and verification

This companion supports [the single geo map technology stack plan](prd-tad-adr-mvp-gtm-geostack.md), `geostack@0.4.1`. It owns observations only. `geomaps-poi@0.1.0` is absorbed; this filename no longer identifies a second plan, schema, release route or implementation. Source-owner contracts remain authoritative.

## Source closure update — 2026-11-16

The shared coordinate core is implemented under [AGENTIC-GEO-001@0.3.2](prd-tad-adr-mvp-gtm-agentic-geo.md); this integration plan creates no competing package contract. Graph's separate area-projection correction is protected source `2335267d9da9d77fb77b9df705f67927f9933931` through [PR #1974](https://github.com/huijoohwee/agentic-graph/pull/1974): 28 affected checks, linked builds/Canvas typecheck and required Integration Gate pass. Native END reports sourceComplete=true/workspaceClosed=true. Historical/local screenshots below remain scoped to their captured source; they do not prove deployment. Prior 0.4.0 authoring bytes are retained in the local evidence snapshots.

## Source snapshot — 2026-11-16

Local file inspection, not provider documentation or account verification. Exact pins keep observations bounded; recheck affected rows when bytes/dependencies change.

| Repository / inspected revision | Relevant source and observation | Reuse / limit |
|---|---|---|
| Graph `675d0ad10eea5d57fe101c1fb5d4318a804a7ff5` | `canvas/src/features/geospatial/localPoiDirectoryModel.ts`: input/output ≤500,000 bytes; stable `source:id`; exact Point/coarse region approvals; allowlisted metadata; deterministic SHA-256; ≤50 visible results | existing validator/search owner; not a proposed module |
| same Graph revision | `canvas/src/features/geospatial/localPoiDirectoryRuntime.ts`: subscribable approved dataset, cached GeoJSON graph projection, region area metadata without fake centroid | reuse; not durable/offline storage |
| same Graph revision | `canvas/src/features/maps/LocalPoiDirectory.tsx`, `canvas/src/lib/toolbar/ToolbarToolMenuGeoView.tsx`: local form/search, lazy shared dataset projection, source-feature ID selection; generation guards | one directory/shared map selection; synthetic preview only for the canonical approved fixture |
| same Graph revision | `geospatialOverlayGraphData.ts`, `InlineMarkdownGeoJsonLayerMap.tsx`, `gympgrph/src/maplibreLayers.ts`, `gympgrph/src/features/geospatial/graphFeatureAffordances.ts` | reuse current-source overlay, SVG, optional cluster layers and map affordances; no renderer added |
| same Graph revision | `scripts/geostack-local-geojson-build.mjs`: bounded race-checked read, shared validator, new directory/exclusive output files and partial-write cleanup | local command already implemented; no fetch or overwrite |
| same Graph revision | Local POI Directory plan `1.0.10`, Mapping Stack plan `1.0.3`, Geospatial Mode document | implementation/requirements/delivery owners; this docs repo consumes them |
| Design System `7fae5884f7024c1ddd029ef058a3e7758614f73b` | package `agentic-design-system`, `./react/panels` public export; exact Graph Canvas pin | canonical shared UI owner, direct upstream; no fork/override |
| Base local HEAD `9170a1de4ae290ad3a077af976813e70b3a7552d`; Graph consumes `5f5a76d8d1cb955c8d1ce2a6277bd21ed7dd065f` | `src/index.mjs` exports `createBaseEngine`, memory/IndexedDB adapters and table/matrix/kanban/calendar projectors; package exposes existing controls/table/settings APIs; Graph `SemanticSelect` imports pinned controls | reuse existing views only where needed; local HEAD is not Graph's dependency pin; shared control changes belong to Design System |
| Canvas OS `f6d61d582ac1121151bf0ba9b20365588435bb43` | package describes product tier calling Graph over MCP/embedding Graph; `src/agentic-graph-mcp-client.js` is an existing compatibility export from OS; `src/launch-copilot-contract.js` validates source/revision/graph joins | reuse product/contract seam when admitted; no direct Canvas OS dependency added to the geo path; do not copy its client or proposal validator |
| OS `45ea0e1f4a87976c4427a6a393dfffcbdb6c5a6a` | runtime prompt, START/ADLC/RELEASE and shared UI ownership contract | existing lifecycle and ownership owner; no local governance copy |
| Joohwee lane `0331abd2c662a247928caa14798f771286c6b0c2`, base `19de5d7e1431bdfb8000981877f5b650a28239a1` | requested docs were 69,188 B / 555 lines (Geostack) and 36,732 B / 478 lines (Geomaps); Geomaps was untracked | preserve existing listing commit and authored input; consolidate these paths only |

Graph currently pins Design System directly and Base at the revisions above. Local canonical repository HEADs are observations, not automatic upgrades. Canvas OS is a potential shell/contract consumer, not a second geo runtime. No claim of runtime linkage follows from listing all four repositories.

## Contract reconciliation

| Former conflict / duplicate | Current disposition | Proof or next check |
|---|---|---|
| Geomaps new `poi.schema.json`, UUIDv7 and 14-category records versus existing `source:id`/five-category validator | one existing Graph contract; richer schema deferred, not silently mapped | owner model + AC-POI-01…08 |
| unknown properties rejected vs dropped; unknown values universally null vs required fields/operator defaults | actual allowlist drops arbitrary properties and validates accepted required fields | focused validator checks; do not claim JSON Schema/country/postal validation |
| business phone and public contact publication vs public-field restriction | existing public allowlist retained; no contact fields added | owner validator + explicit public-field review |
| NDJSON master, detail shards, PMTiles, source-release archive, extra static host and range-deploy tests | deferred scale proposals; no such pipeline selected or required for local MVP | revisit only after measured cap breach and source/rights/$0 evidence |
| Overture/OSM/government source claims and unverified provider limits | no source/provider selected; former limits/pricing not carried forward as facts | obtain current primary evidence and exact provider/account proof before an effect |
| listing store as potential POI master | separate owners; no dual write or mutation | any listing reference requires a later owner-approved contract |
| Geostack claims validator/search missing, scratch code unintegrated and no delivery | superseded by Graph owner plan and historical release evidence | retain exact candidate boundary below; current live identity still separate |
| duplicate POI projection/approval/selection tests in active-source regression file and registry | remove three duplicate definitions/registrations; keep four canonical POI checks and independent source-replacement check | exact focused command below |
| coarse region interpreted as an invented centroid point; original active-source regression failed with four rather than three points | fix the existing GeoJSON graph builder to retain Polygon/MultiPolygon area metadata and omit coarse-region point coordinates | existing source-replacement regression now covers both area types and removal of a supplied centroid |
| canonical synthetic fixture treated as a historical nonfixture | assert six places + one region; reject unrelated report, wrong source path and altered provenance | canonical `localPoiDirectory.test.ts` |
| seed metadata claims old scratch draft SHA is current readiness | replace active cross-repo scratch binding with Graph owner-plan link; retain dated audit as history | two source seed companions updated; no digest-refresh loop |

No retired design is preserved as an alternate active specification. Historical source and receipts remain evidence for their original subjects only.

## Historical integration and delivery

The inspected Graph [Local POI Directory plan][poi] records accepted implementation PR [#1843](https://github.com/huijoohwee/agentic-graph/pull/1843), merge `dd842651c4f1888d2d4b161b389635b6be3162a1`, and synthetic-provenance guard PR [#1844](https://github.com/huijoohwee/agentic-graph/pull/1844), merge `768e794bcb7f61dfaeb7169a598cab82c9e67dce`.

Its retained [path-bound report][delivery] and `docs/reports/production-delivery-evidence-41021713269.json` record successful release run `41021713269`, source `f3c7816b2788d006dbf076009560eba18c2aa609`, candidate `2729de17d1e80b6d2c2676e0a86f3368bdbd97f0f6f2e7c67e896f1b9e82c317`, Pages deployment `d4bf1bde-c77b-4495-8085-0874d43450ca` and runtime receipt `28e88a4d6efec6f4948e777f386a6b30f4b865fc32f7310939cf42681bf7e838`. These are read from retained repository records, not reobserved provider state. They refute the old blanket “never integrated/deployed” draft claim but do not prove current public identity, a new release, today's billing state or this plan's VCCs. Rollback and no-deploy closeout remain owned by those exact Graph records.

## Admission and preservation

- Joohwee: explicit readmission reused `agent/device-0232231d4a19/listing-management-grounding` at `0331abd2c662a247928caa14798f771286c6b0c2`; workflow digest `ab3569d158704eb5be79b2b63b40491d339f2d435b7a4f90e107a85b04365ffc`; exact write digest `ec111412c9081076050b851d8ffaa8ebfc5c573b63a11609c0cf6fa605d15570`. Existing database plan remains the admitted mission root; this user request explicitly expands the local docs scope. No mission-root substitution is claimed.
- Graph: new scope `agent/device-0232231d4a19/geo-map-stack-grounding` based on `675d0ad10eea5d57fe101c1fb5d4318a804a7ff5`; final readmission digest `e69a444b4d41a7f88befa04a251458bd96c2f54816bf6d7bd6e7c4bd56bdde9b`, write digest `5b3d5ce9fcf03260f3b2878a1b5af503fd2753605d486e0da44e6281acb8509a`; seven existing files reserved. The readmitted seven-file scope includes one existing runtime owner, `canvas/src/lib/graph/io/geojsonToGraphData.ts`; no new runtime module or dependency.
- Early attempts used an invalid absolute planning path, then a competing scope and different mission plan; START rejected those safely. Exact-mission readmission resolved the scope without resetting or adopting unrelated work.
- Original tracked Geostack remains at Joohwee `0331abd2c662a247928caa14798f771286c6b0c2:undocumented-draft/prd-tad-adr-mvp-gtm-geostack.md`. Original untracked Geomaps was reconstructed from the two complete pre-edit tool-read slices and preserved at `/Users/huijoohwee/.codex/private-evidence/geo-map-stack-grounding/geomaps-poi-0.1.0.original.md`: 36,732 bytes, 478 lines, SHA-256 `58840ecc43560fac50cf299dc9a15b21f2d5145386fe14bca1979480f6705959`. This is a local retained input, not a committed predecessor or active variant.

## Verification — current task

| Check / criterion | Observed result | Scope / limitation |
|---|---|---|
| baseline `npm -C canvas run test:ci:unit -- geospatial.localPoi` | 5 pass, 2 fail of 7; stale synthetic expectation and duplicate selection source-string assertion | baseline Graph `675d0ad…`; runtime defect not established by these failures |
| repaired `npm -C canvas run test:ci:unit -- geospatial.localPoi geospatial.markdown.activeGeoJsonReplacesStaleMapFeatures geojson` | **28/28 passed** | four canonical POI checks, independent current-source replacement and GeoJSON import/preview coverage; synthetic only |
| normal canonical/session startup | blocked by unrelated untracked canonical sources; shared OS docs checkout also dirty | preserved unrelated bytes; no cleanup/stash or policy weakening |
| live browser | **scoped local observations below** | repository test `vite-runner` mode; not canonical Dev readiness, named-device or production proof |
| `npm run check` | **passed** after runtime owner change | linked package builds, Canvas typecheck and 3 smoke-runner contract checks; not full product/integration CI |
| conflict source compliance, doc identity/local links/size, and `git diff --check` | **passed** | one plan/companion identity; both <600 lines; final combined content <60 kB |
| `node --test scripts/__tests__/workspace-seed-authority.test.mjs` | **104/104 passed** | source-owned seed and projection contracts |
| final `npm exec -- tsc -b --noEmit` in Canvas | **passed** | incremental typecheck after strengthening Polygon/MultiPolygon regression |

### Live UI record

Route: `http://127.0.0.1:4177/?kgPath=%2Fagentic-graph%2F`; Graph admitted worktree based on `675d0ad10eea5d57fe101c1fb5d4318a804a7ff5` plus the reviewed local diff. Isolated Chrome context `geo-map-stack-verification`; Vite 6.4.5, repository-supported test `vite-runner` startup. Test harness selected the canonical `/docs/workspace-seeds/agentic-graph-maps-places.md` bytes through the existing active-document action; actual UI clicks/fills exercised the directory and category menu. This is not an independent evaluator or an end-to-end file-import trial.

- **1280×800, light:** one Local POI Directory heading, one MapLibre canvas, six native point-selection controls and a visible filled coarse region without a seventh centroid marker. Searching Central returned one result; clicking it displayed `Selected on the shared map` and highlighted Central. Source, synthetic licence and attribution were present in the directory. Screenshot: [desktop](/Users/huijoohwee/Documents/GitHub/.artifacts/geo-map-stack-grounding/geo-desktop-light.jpg).
- **360×800 mobile/touch emulation, dark:** category `store` plus query East returned one result and selected East through the shared callback. Directory bounds x=29…331 px fit the viewport; no document horizontal overflow. With the same page loaded, network Offline, query Central returned zero under the store filter and returning to East restored one result; selection/source/attribution stayed in memory. Screenshot: [mobile directory offline](/Users/huijoohwee/Documents/GitHub/.artifacts/geo-map-stack-grounding/geo-mobile-dark-offline.jpg). Before activation the mobile shell intentionally mounted no map. Closing the directory exposed the existing `Load map view` touch-device opt-in; clicking it mounted one MapLibre canvas and six point controls. Clicking Central on the map set shared selection source `canvas` and selected `geo:141864eb`; its highlight, the coarse region and loaded tiles remained visible after disconnecting network. Screenshot: [mobile map after opt-in, offline](/Users/huijoohwee/Documents/GitHub/.artifacts/geo-map-stack-grounding/geo-mobile-map-dark-offline.jpg). This confirms the existing mobile lazy-load boundary; SVG fallback and physical-device behavior were not exercised.
- Switching mobile emulation while offline triggered a navigation that failed with `ERR_INTERNET_DISCONNECTED`; after restoring network the local page recovered. **Offline reload is not supported by this Dev-preview observation** and was never an MVP guarantee. The valid screenshot above was captured after a successful online load and subsequent network disconnection.
- Console inspection included local 404/400 resource failures and the deliberate offline network failure; this is not a zero-console-error result. A bounded resource readback listed only loopback host entries, but no complete network/provider/account audit was retained; no zero-provider-effect or current cost claim follows. No provider configuration or production surface was changed.

VCC-GS-03 is **partial**: desktop/mobile map and directory behavior observed, including touch-device runtime opt-in; named-device, screen-reader, SVG fallback and full network/console acceptance remain open.

### Remaining conditions and next action

GS-05 real operator task/$1 result, named-device timing, screen-reader behavior, real data rights, provider cost/headroom, persistent offline reload and current production identity remain unproved. External wait: consenting operator plus permitted file; recheck when supplied, with no delivery ETA. Graph protected checks/publication and any production effect keep independent receipts and authority.

Resource accounting: no new dependency, runtime module, hosted resource or always-loaded data/prompt bytes. Initial 45-minute authoring estimate was refreshed when admission/local-runtime blockers and the projection regression changed scope; scope refreshed explicitly to seven Graph files and one runtime owner, with ≤8 kB added authored source. No completion-time or production ETA is inferred from that estimate. Active minutes, tool/model tokens, energy and provider spend are not measured by this document; no inference cost is fabricated as zero. Browser test data is synthetic. Consolidation final size and check outcomes are recorded at handoff.

[poi]: https://github.com/huijoohwee/agentic-graph/blob/675d0ad10eea5d57fe101c1fb5d4318a804a7ff5/docs/documents/agentic-graph-local-poi-directory-prd-tad-adr-mvp-gtm.md
[delivery]: https://github.com/huijoohwee/agentic-graph/blob/675d0ad10eea5d57fe101c1fb5d4318a804a7ff5/docs/reports/agentic-graph-delivery-evidence-geostack-pr1875.json

## Local handoff / END observation

Both source lanes remain local and uncommitted for review. Shared OS `complete-adlc --ref=<exact lane>` observed each exact lane and returned `requires-published-lane`; no merge, sync, cleanup or deployment effect was selected or inferred. Retain both registered worktrees and the original input snapshot. Protected publication/integration is the next lifecycle step if selected by the operator; do not label this task source-released or deployed. The Joohwee lane still includes its earlier listing-management commit, which was preserved.

The consolidation replaces 105,920 bytes of conflicting drafts with one plan and an evidence companion below 60,000 bytes in total. Graph removes duplicate checks and fixes one existing projection owner; it adds no package, provider, schema master, map host, scheduled job or always-loaded prompt content. Screenshots are local evidence under `/Users/huijoohwee/Documents/GitHub/.artifacts/geo-map-stack-grounding/`. The owned test Vite process is stopped after verification.
