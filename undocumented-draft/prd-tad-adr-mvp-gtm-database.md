---
title: "Native Listing Entry Management — PRD, TAD, ADR, MVP, GTM"
doc_type: "PRD-TAD-ADR-MVP-GTM"
version: "0.5.0"
revision: "0.5.0"
prd_revision: "0.5.0"
tad_revision: "0.5.0"
adr_revision: "0.5.0"
mvp_revision: "0.5.0"
gtm_revision: "0.5.0"
date: "2026-11-13"
lang: "en-US"
frontmatter_contract: "required"
owner: "Commerce product architecture / Solo Founder"
continuity_id: "listing-db-admin"
local_rung: "dev-proven"
delivered_rung: "undocumented"
lane: "authoring"
universal_scope: true
load_policy: "on-demand"
runtime_readiness_policy: "fail-closed"
lifecycle_status: "proposed"
---

# Native listing entry management

Join: **`listing-db-admin@0.5.0`** across PRD, TAD, ADR, MVP and GTM. Enhance the existing private offer editor, library and review table with optional listing facts, safe changes, archive and restore. Keep one record owner, one editor, one writable store and one release path. The product is country, category, device and storage neutral; concrete source paths below identify this implementation.

Revision 0.4.0 proposed a new file-backed admin without inspecting the native runtime. That proposal is superseded by the grounding below. Existing browser storage is the MVP master; a file is a portable export, never an independently writable replica. A reviewed file-backed or relational master remains a triggered later decision. No new CMS, store, registry, provider or UI variant is authorized by this document.

## Scope and evidence status

| Item | Current disposition |
|---|---|
| Product owner | Existing Commerce offer workspace; parent `edge-commerce-agent-mvp` and its native workspace companion retain launch, checkout and deployment ownership |
| Local readiness | `dev-proven` for the bounded native listing slice; local browser/contract results are recorded below; future migration conditions remain deferred |
| Delivery readiness | `undocumented`; source inspection and local preview do not establish delivery |
| Baseline | Commerce `ac61bee799e223fcf24e0418305a09db693c1f6e`, inspected 2026-11-13; refresh changed paths at the admitted candidate |
| Directive | User authorizes native CRUD enhancement, shared utility reuse, draft update and live UI verification; a new lane is explicitly authorized |
| Execution | START admitted the document lane and the explicitly authorized new Commerce lane; four exact reservation-release receipts preserve the existing shared UI lane |
| Spend | USD 0; no packages, paid plans, addons, overages or external runtime dependency |
| Provenance | External reading informs generic management behavior only; no reference code, assets, schema, prose, branding or dependency enters the product |

## PRD: buyer pain and smallest useful outcome

**Operator.** A person maintaining private location-bound listings needs to enter facts once, find the right entry, distinguish missing information, and reverse a retirement without losing work. **Buyer.** A prospective buyer needs clear asking terms and evidence gaps before spending time on due diligence. The MVP serves the operator; it does not publish or certify seller claims.

| ID / rank | Pain and evidence | Existing capability → smallest change | Commercial connection |
|---|---|---|---|
| PP-01 / 1 | Price notes and free text cannot reliably distinguish unknown rent, revenue or asking price. Observed native schema gap; willingness to pay unvalidated | Existing title/notes and editor → optional structured listing facts with nullable numbers and inline errors | Less operator rework before one manually delivered listing review |
| PP-02 / 2 | Removing an entry must be reversible and must not silently overwrite another tab. Observed revision fence exists; archive controls absent | Reuse atomic revision check → archive/restore in the same record | Preserve operator work and buyer context |
| PP-03 / 3 | An admin should not reconstruct a database or UI to manage an existing listing | Reuse native library, search, shared table and export → extend their projections | Shortest route to a usable operator workflow; no infrastructure bill |

**Use case.** A business acquisition entry needs identity, category/location, asking amount, recurring financial declarations, lease date and source context. The supplied [business listing](https://listings.sg/businesses/established-interior-design-business-for-sale-in-singapore-f) was inspected on 2026-11-13 as a workflow example. It is not an imported record, verified financial evidence, an asset source or a dependency. Demo records use invented values and wording. Unknown is not zero; seller supplied is not independently checked.

### Stories and conditions

| Story | Priority | Outcome / completion condition |
|---|---|---|
| PRD-LST-01 | Must | Create a private listing from the existing editor; VCC-LST-01 |
| PRD-LST-02 | Must | Edit only the current saved revision; VCC-LST-02 |
| PRD-LST-03 | Must | Archive and restore the same ID without hard deletion; VCC-LST-03 |
| PRD-LST-04 | Must | Search identity, category and location; filter archived entries in the existing library/table; VCC-LST-04 |
| PRD-LST-07 | Must | Saved facts survive reload and offline use; VCC-LST-05 |
| PRD-ADM-01 | Must | Private projections exclude listing notes, sources and financial facts from agent/public launch payloads; VCC-ADM-01 |
| PRD-OPS-01 | Must | Export/import and rollback preserve old and new records; VCC-OPS-01 |
| PRD-PUB-01 | Must | Archived entries stay out of shopper and launch review projections; VCC-PUB-01 |
| PRD-DBR-01 | Should / later | Define and prove a database-ready import before changing the writable master; VCC-DBR-01 |
| PRD-DBR-02 | Later | One storage adapter conforms to the existing semantics; VCC-DBR-02 |
| PRD-MIG-01 | Later | Count, canonical bytes, revisions and lifecycle survive a separately approved migration; VCC-MIG-01 |

| VCC | Observable end state and check | Constraint / bound |
|---|---|---|
| VCC-LST-01 | Live UI creates a listing; malformed dates, unsafe URLs, negative or overprecision money and unknown fields fail validation | Same editor and store; nothing saved on invalid input |
| VCC-LST-02 | Two tabs edit the same revision; the second save is refused with recoverable text | No last-write-wins; revision increments exactly once per accepted write |
| VCC-LST-03 | Archive hides a saved listing from active views; archive filter finds it; restore retains ID, facts and creation time | No hard delete; stale archive/restore refused; explicit saved revision required |
| VCC-LST-04 | Search category/location and filter archived records in native vendor/admin views at 360 and 1280 px | Existing 100-record ceiling; no fabricated 5,000-record or two-second claim |
| VCC-LST-05 | Save, reload, switch offline and reopen: values unchanged; storage failure shows an error and preserves editor text | Saved records only; unsaved text is not claimed durable |
| VCC-ADM-01 | Native launch pack and workspace snapshot omit the optional listing block; archived records cannot be reviewed/exported for launch | Browser-local has no authenticated multiuser access guarantee; no new mutating MCP/WebMCP tool |
| VCC-OPS-01 | Old v1/v2/v3 backups import unchanged; new export retains listing state; conflicting import is atomic and changes nothing | Backward reads; old clients may fail closed on new records; never drop unknown data |
| VCC-PUB-01 | Archived entries are absent from shopper preview, active counts and launch queue; direct archive review fails | Restore is a private draft transition and grants no publication authority |
| VCC-DBR-01 | Deferred: exact-schema importer produces matching row count and canonical per-record checksum in a disposable store | No migration or relational persistence claimed by JSON export |
| VCC-DBR-02 | Deferred: port conformance proves same validation, revision and failure semantics | Reuse the owner, no dual write |
| VCC-MIG-01 | Deferred: freeze, import, compare and rollback rehearsal recorded before master cutover | Separate target-specific authorization and USD 0 provider proof |

**Metrics.** TTV-01: fresh browser → first saved listing → searchable → archive → restore. Record actual time after the UI drill; target ≤5 minutes is a hypothesis. Record edit time, validation escapes and stale-save refusals. No measured demand, revenue, cost saving or scale claim exists yet. Touch and keyboard editing must work on mobile browsers; all controls are labelled and focus/error recovery remains usable.

## TAD: extend native owners

### Codebase grounding record

All paths are relative to the named repository. These observations identify source mechanisms, not readiness receipts.

| Owner / source | Observed behavior | Reuse and delta |
|---|---|---|
| Commerce `public/local-first/drafts.js` | IndexedDB `agentic-commerce-local-drafts` / `drafts`; exact record keys; v1/v2/v3 import; revision CAS in readwrite transaction; atomic conflict refusal; 100 records / 8 MB transfer | Sole data owner; add an optional validated listing block and compatible next export version |
| Commerce `public/local-first/app.js` | Existing create/edit form, dirty navigation guard, save errors, source revision review and JSON backup controls | Extend this form; render listing errors; archive/restore through the same revision-fenced save |
| Commerce `public/local-first/workspace.js` | Native routes, paged vendor library, admin queue, local search and cross-tab refresh | Extend matching/filtering; keep archive state independent from commercial readiness |
| Commerce `public/local-first/workspace-graph.js` | Commerce projects rows; lazy-loads portable Base table and Graph guide; shared CSS via shadow-root surfaces | Extend detail rows and actions; no table/form renderer fork |
| Commerce `public/local-first/launch.js`, `workspace-capabilities.js` | Integer money parser, exact reviewed launch terms; allowlisted workspace snapshots and read-only tools | Reuse money parsing; exclude listing facts and archive state from launch authority; reject archived review |
| Commerce `public/local-first/sw.js`, `scripts/local-first-release/artifact.mjs`, `src/local-first/worker.ts` | Offline cache, exact asset inventory, release identity and serving route | Existing modules need no parallel route or launcher; add no undeclared asset |
| Design System `site/tokens/shared-ui-profile.json`, `site/vendor/shared-ui-profile.css` → installed Commerce projections | Shared tokens, density and control styling; Commerce pins source/output digests | Reuse existing tokens, form layout classes and controls unchanged; no local token overrides |
| Base `config/agentic-base-data-view.json` / browser `mountDataView` | Commerce pins portable table browser export and styles; installed artifact is below 500 KB | Reuse the current table through `workspace-graph.js`; do not import a sibling checkout |
| Graph `config/graph-data-view.json` / `mountSequenceGuide` | Existing setup guide and shared view artifacts carry source revision/digests | Retain existing guide and presentation ownership; listing actions use native editor |
| Canvas `src/agentic-graph-mcp-contract-utils.js`, `scripts/invocation-resolve.mjs` | Contract-only re-exports and invocation parsing delegate to the portable OS owner | Reuse the existing shared contract path; no copied parser or cyclic Commerce → Canvas UI import |
| Commerce `src/invocation/catalog.ts` | Imports `serializeInvocationCatalogForDigest` and `serializeInvocationRoutingForDigest` from `agentic-os/invocation`; consumes the Canvas docs routing contract | Keep the shared exports and existing `/`, `@`, `#` resolver; no competing listing registry |

Inspected canonical source identities: Design System `94c61815db7a4c7ec067161386df6364aa7a8909`; Base `1a756dc933cafb2b9590bb5ed7c84042aaed61ed`; Canvas `f6d61d582ac1121151bf0ba9b20365588435bb43`. Source observations are distinct from consumed artifact pins; use the actual lane configuration before checks. The existing shared UI lane owns pending pin refreshes; this increment must preserve them and keep disjoint reservations.

### Division of work and dependency order

| Element | Sole responsibility / extension owner |
|---|---|
| TAD-SCH / TAD-VAL | Listing field contract and pure validation in existing draft owner; both UI and backup reader consume it |
| TAD-UI | Existing editor fields, local lifecycle controls, accessible errors and saved-state display |
| TAD-STG / TAD-ADP | Existing IndexedDB record transaction; saved draft is the device-local master; editor text remains memory only |
| TAD-EXP | Existing JSON backup owner with explicit schema version; launch export remains separately allowlisted |
| TAD-AUTH / TAD-AUD | Existing local device boundary and record revisions; no server identity, permanent change history or publication audit is invented |
| TAD-CI | Focused contract/browser checks, exact asset inventory and required repository gates |
| TAD-ADP-VCS / TAD-ADP-SQL / TAD-GEN | Deferred: only introduce on a named trigger, with conformance and removal of the old writable adapter |

Dependency order: portable draft contract → transaction/import → editor → native list/detail projections → local/browser proof → existing release controller. No lower-level module imports a UI, secrets or effectful provider client. Shared UI source changes precede consumer pin refreshes under their existing owner; this listing slice consumes compatible pins only.

### Listing contract

The existing top-level `id`, `title`, `description`, `price`, `launch`, `workflow`, `revision`, `createdAt` and `updatedAt` retain their meaning. Listing facts are optional. Existing records remain readable without a write or schema migration. New listing records use one optional block; fields are neutral and derived from operator decisions in PP-01…03.

| Field family | Semantics / validation |
|---|---|
| Identity and lifecycle | Existing immutable UUID; optional listing `status` is `draft` or `archived`; restore returns to private draft |
| Classification | Free bounded category, ISO-shaped country code and bounded region; no hardcoded country or category catalog |
| Asking and recurring figures | Currency plus nullable whole minor-unit asking amount, monthly revenue, profit and rent; blank remains null; no implicit conversion or arithmetic certification |
| Tenure and operating facts | Optional established year, lease-end calendar date, premises area and staff count, each bounded and correctly typed |
| Source context | Optional safe HTTP(S) source URL and as-of calendar date; refuse credentials and executable schemes; dates are real calendar days |
| Evidence semantics | Supplied facts only; no automatic verified flag, profitability endorsement or external fetch; review notes remain private |
| Strict shape | Listing block `schemaVersion: 1`; full exports use `commerce.local-drafts/v4`. Exact supported keys and version, bounded strings, finite safe numbers; reject unknown fields rather than silently stripping them |

The UI must not combine an acquisition asking price with per-sale launch economics. Listing values stay in their block; launch terms keep their current domain and parser. Category/location and source dates are optional, so legacy offers and non-location services remain usable. An explicitly archived listing is never made active by saving ordinary form edits; restoration is explicit.

### Changes, conflicts and duplicate prevention

1. Read a saved record and its revision. Edit only through the existing form; show unsaved/saved state.
2. Validate all fields before submission. Keep field errors associated with controls and focus the first error.
3. In one existing readwrite transaction, compare expected revision and check any new listing uniqueness rule before `put`.
4. Increment revision exactly once, retain ID/creation time and preserve existing workflow/launch compatibility. A changed revision invalidates prior launch review.
5. Notify the existing draft update channel; refresh tables without treating stale editor text as current.

A normalized nonempty source URL can identify an accidental second entry. If introduced, compare it within the same transaction, include archived entries and reject a duplicate import atomically. Do not claim fuzzy duplicate detection or unique real-world business identity. Similar titles alone are not proof of duplication. No duplicate database, route, source-specific schema, parallel admin, copied shared renderer or local token variant is allowed.

### Persistence and interchange

| Representation | Authority / support |
|---|---|
| Existing browser draft store | One writable device-local master; current 100-record ceiling unchanged |
| Editor text | Unsaved memory; no autosave or eviction recovery promise |
| JSON backup | Versioned full export; supports old schemas and preserves listing metadata; import conflicts refuse the complete transaction |
| Launch pack / read-only workspace snapshot | Existing allowlist only; listing facts are excluded; no publication/payment authority |
| CSV/XLSX, per-record files, relational rows | Deferred optional exchange/adapters; no package or second writable store in MVP |

DBR-01: IDs and revision meaning remain stable. DBR-02: explicit nulls represent unknowns. DBR-03: schema changes are versioned; unknown properties fail closed. DBR-04: future tables must preserve all authored fields, including lifecycle/source context. DBR-05: one writable master; no dual write. DBR-06: bulk work stays bounded and fails at resource limits. DBR-07: canonical serialization/checksums are migration acceptance, not an unimplemented current guarantee.

### Human, agent and failure surfaces

| Surface | Existing owner and support |
|---|---|
| Human UI | Existing vendor editor, vendor library, admin shared table and private JSON backup controls |
| WebMCP / MCP | Existing workspace reads remain supported through their common handler; no new listing mutation or bulk write registration |
| `/`, `@`, `#` | Existing invocation resolver only; discoverable metadata never grants execution, publication or payment authority |
| Offline | Existing cached modules and IndexedDB; local CRUD after assets are available; external reads and deployment unavailable |
| Storage denied/full | Fail save visibly; preserve form text; retain saved data; copy/export recovery when available |
| Cross-tab stale save | Refuse at the store owner; reopen current record; never overwrite silently |
| Old client / new record | Fail closed if incompatible; retain raw stored bytes and backup; no downgrade stripping |
| Untrusted text or URL | Render as text, validate URLs, no automatic fetch, raw HTML or seller script execution |

Browser-local storage is not multiuser authentication, a remote database, encrypted-at-rest assurance or durable backup against browser data clearing. Those are explicit later product decisions. Native publication/authentication and operational audit stay with their existing backend owners.

## ADR: decisions

**Constraints.** K1 USD 0 with fail-closed effect costs; K2 mobile/browser/offline; K3 one owner and no duplicate variants; K4 strict validation/revision fences; K5 provenance restrictions; K6 under 600 lines per authored file and under 500 KB per executable chunk; K7 no drift in shared UI ownership.

| Decision | Alternatives and disposition | Result / revisit |
|---|---|---|
| ADR-001 native master | Existing IndexedDB extension passes K1…K7; a new file-backed admin fails K3 for this increment; immediate remote master lacks K1 evidence and increases scope | Extend draft owner. The former file-master-first assumption is superseded |
| ADR-002 UI ownership | Existing editor/table passes; separate admin app or cloned shared table fails K3/K7; reference package adoption fails K5 | Extend existing owner; no fallback CMS variant |
| ADR-003 phase change | Keep device master now; later single adapter cutover; simultaneous masters fail K3/K4 | Revisit only for validated multiuser writes, shared persistence or scale need |
| ADR-004 schema and export | One pure validation owner consumed by UI/store/import; parallel schema definitions fail K3 | Extend owner; defer SQL/type/form generators until there are real consumers |
| ADR-005 evidence | Unknown remains null; supplied facts remain unverified; automatic source scraping/certification has no authorization or proof | Manual private facts only; revisit with evidence source, legal owner and cost gate |

The admitted native extension is the sole constraint-passing candidate. No fabricated ranking score is needed. Argument for a new database: eventual shared editing may need one. Counter-evidence: the existing atomic local owner already meets this private MVP and no shared-writing demand is established. Independent architecture verdict: pending; this authoring decision is not a fabricated independent review.

## MVP and bounded execution

**Slice.** Add optional structured facts to the existing record; create/edit/find; archive/restore; preserve backup compatibility; verify strict/atomic/stale behavior and live responsive UI. Existing launch review and shared utility paths remain native. Hard delete, bulk actions, scraped imports, attachments, live publication, payment, public submissions, verification services, authenticated collaboration and new database adapters are outside this slice.

| Sprint / owner | Work and dependency | Time / bytes / modules | Exit / recovery |
|---|---|---|---|
| S0 grounding | Inspect owners, START, bind draft and exact path reservations | 10-minute initial estimate; refresh on observed admission blocker | Source joins and safe lane; no overwrite of retained work |
| S1 native increment | Schema/store → existing editor → list/detail → compatibility and live UI | ETA 45 active minutes after admission; cap 60 KB source delta, 8 runtime modules, 0 packages/services; no always-load guidance delta | VCC-LST-01…05, VCC-ADM-01, VCC-OPS-01, VCC-PUB-01; stop and refresh bounds on drift |
| S2 future store | Only after validated shared write/scale need | New scoped plan and USD 0 proof; no current ETA | VCC-DBR-01/02 and VCC-MIG-01 before cutover |

External admission/provider waits are blockers, not ETAs. Recheck on an ownership handoff, current remote ref observation or required provider event. One owner/candidate per effect. Reuse matching check receipts; refresh only invalidated inputs. No background workers or always-load module is added. Extend existing modules within their caps; lazy shared renderers remain lazy.

**Demo.** In a clean browser, enter an invented business record, omit revenue, save and reload. Find it by category/region. Edit in two tabs and show stale refusal. Archive, find with archive filter, restore and compare ID/facts. Export/import unchanged and attempt a conflicting import. Repeat essential actions at 360 px offline. Show a legacy offer still works and listing details never enter a launch pack.

## GTM and economics

Ranked path to the first dollar is a hypothesis: **one manually delivered listing preparation/review** using the existing export → reusable operator workflow → broader listing platform only after demand. Ask one reachable operator to try the actual saved-entry drill and state whether one usable handoff is worth USD 1 (or a declared local-currency equivalent). Record a real offer and payment evidence before claiming a first dollar. This task authorizes neither outreach nor collection.

EXP-01: compare a 20-edit planted-error drill against free text; proceed if structured input prevents at least one error without blocking valid editing. EXP-02: five operator conversations, only when outreach is separately authorized; two independently stated willingness-to-pay responses justify a pricing test. Failure leads to fewer fields or a validator-only slice, not more infrastructure. Market size, channel conversion, operator time saving and recurring revenue remain unmeasured.

Local runtime uses already-installed FOSS/browser facilities and performs no model inference. Active minutes, model/token cost, CI usage and actual transfer bytes remain measured separately; they are not assumed zero. Remove the previous paid-tier alternative and unverified quota claims. Any later hosted effect requires current provider-owned hard USD 0/deny-at-quota evidence. Free allowance or an alert alone grants no authority.

## Verification, release and rollback

| Effect | Required evidence and authority | Current state |
|---|---|---|
| Local source work | START reservation; exact files; preserved existing edits | New code lane admitted; clean local candidate `42f118e1192733e5bba6869350d08f3c2de47441`; no remote publication |
| Local verification | Focused contracts, live UI with viewport/offline/revision/backup checks; record candidate and results | Browser drill and focused tests pass; final repository gate result below |
| Protected source integration | Existing land/required-check/review path; exact green Integration Gate and authorized merge | Pending; local checks do not replace it |
| Delivery | Existing Commerce release controller, exact-candidate promotion instruction, cost proof and rollback disposition | Closed; not implied by this enhancement request |
| Cleanup/sync | Exact target/effect authority and independent receipts | No inferred cleanup or canonical overwrite |

Rollback source via reviewed revert using the existing release owner. Preserve all browser records and a full export before downgrading; old clients may reject listing-aware records. Do not erase fields to make an old reader pass. A future schema downgrade needs a lossless tested conversion and its own authorization. Production rollback uses the existing Commerce deployment runbook and predecessor artifact; source rollback is separate.

### Gaps and findings

| ID | Evidence / owner / next check |
|---|---|
| G-01 closed for source grounding | Native Commerce workspace parent and concrete owners inspected; no inferred runtime readiness |
| G-02 narrowed | Readiness/verification/selection companion semantics inspected; full authoring baseline and independent evaluation remain pending |
| G-03 superseded | Old third-party quota/price/region evidence removed from decision basis; no hosted effect selected |
| G-04 open | Operator pain/demand and actual TTV unvalidated; Solo Founder owns EXP-01/02 |
| G-05 closed for source inspection | Native store/editor/table/shared contracts inspected; implementation and browser evidence remain distinct |
| G-06 open | Independent evaluator verdict absent; no independent approval claim |
| G-07 open | Legal/privacy reviewer for future published business data unassigned; no reference content imported or published |
| G-08 closed for local admission | Four native exact-path releases, distinct listing lane and clean local candidate; committed peer merge preview has no conflicts. Pending shared UI dirty edits retain their original owner |

### Planning record and handover

| ID / join | CID: context → intent → directive | RAO / check |
|---|---|---|
| T-01 PRD-LST-01/02 ↔ TAD-SCH/ADP ↔ ADR-001/004 | Existing strict draft contract → structured facts without a second store → extend validator and CAS transaction | Commerce owner implements; schema/import/stale checks |
| T-02 PRD-LST-03/04 ↔ TAD-UI ↔ ADR-002 | Native editor/table exist → reversible management → extend editor, filtering and detail projection | Commerce owner; live create/edit/search/archive/restore at both viewports |
| T-03 PRD-LST-07/OPS-01 ↔ TAD-EXP ↔ ADR-003 | Existing offline master/backups → preserve work → version export and retain old-reader failure safety | Commerce owner; reload/offline/legacy/conflicting-import proof |
| T-04 PRD-ADM-01/PUB-01 ↔ native invocation/launch owners ↔ ADR-005 | Shared read-only tools and review exist → prevent accidental publication → retain allowlists and exclude archived drafts | Commerce owner; privacy and launch refusal checks |
| T-05 PRD-DBR-01/02/MIG-01 ↔ future adapter ↔ ADR-003 | No shared-writing need validated → defer new infrastructure → reopen only on named trigger | Product owner; new scoped plan and migration evidence |

Revision 0.5.0 replaces the ungrounded greenfield/file-master proposal with inspected native owners, measurable local acceptance, a shared utility reuse map, explicit future-store boundaries and a first-dollar experiment. Historical v0.4.0 intent remains in the prior authored bytes; no previous implementation or evaluator receipt is invented. Next action: complete the existing required source/evidence gate, then request only the exact uncovered release effect; no publication or deployment is inferred from local proof. No parallel product document or variant is introduced.

## Local implementation evidence — 2026-11-13

Candidate: Commerce `42f118e1192733e5bba6869350d08f3c2de47441`, branch `agent/device-0232231d4a19/listing-entry-management`, worktree `.worktrees/agentic-commerce-os/device-0232231d4a19--listing-entry-management`. Prior shared UI work remains at `d4eb1ccb036d2af01b04c8e4d78a1fcc4bf551bb` with its dirty files untouched. Native scope-release receipts cover only `app.js`, `index.html`, `workspace.js` and `workspace-graph.js`. A read-only committed-peer merge preview passes with no conflict; it does not certify future dirty edits or grant integration authority.

| Evidence reference | Observed result / subject | Limits |
|---|---|---|
| ER-LIVE-01 | `node test/local-first/listing-entry-browser.mjs --base-url=<isolated-loopback>/agentic-commerce-os/ --output=<evidence-root>` exits 0 on the clean candidate. Real local Worker/browser at 1280 and 360 px: create/edit/reload, nullable amounts, negative profit, inline validation/focus, stale-tab refusal, archive/restore/search/detail, offline reload/edit, JSON import/export, atomic conflict and duplicate-source race, storage-denied recovery; zero page errors | Local UI, not the delivered route; no native WebMCP support or live publication claim |
| ER-CONTRACT-01 | Focused listing/shared table/invocation tests pass 16/16; actual durable-host build tests pass 2/2 after metadata is made tree-shakeable | No relaxed size bound, paid service, new module or copied utility; later full-gate results supersede these only for their coverage |
| ER-REUSE-01 | Existing Design System theme owner, Base browser artifact and Graph artifact checks pass; Canvas/OS contract imports remain the existing source | No pin upgrades, sibling source imports or duplicate shared renderer |
| ER-BOUNDS-01 | Nine changed files: six JavaScript runtime modules, one existing HTML page and two test modules. Largest authored file 591 lines; no dependency or asset-inventory additions | Total runtime-file sizes are not the source delta; all touched authored files stay below 600 lines |
| ER-MERGE-01 | Native Git merge preview of candidate and committed shared UI peer returns no conflict | Does not merge branches, modify peer source or prove the peer's future dirty state |

**ER-REPO-01 — exact candidate repository check.** `npm run check` ran against clean `42f118e1192733e5bba6869350d08f3c2de47441`. ADLC, evidence-contract and TypeScript pass. The named stage passes 52 admission tests, all 257 local tests, all existing local browser journeys (including offline, review, merchant export, imports, checkout fixture, program pack, Housing and durable listing), shared owner/bundle/line checks, source guards and task bounds. It then fails at the separate container browser preflight: `podman_workerd_override_required:see docs/container-runtime.md`. Podman is installed; `MINIFLARE_WORKERD_PATH` is unset and no matching verified binary receipt was selected. No bundled binary substitution, machine provisioning, threshold relaxation or external runtime execution was attempted. The terminal `check:evidence` stage was not reached. This is a blocked full gate, not green integration or production proof. Recheck condition: provide the documented matching-platform compatible binary with verified build/checksum evidence, then rerun the owning browser gate and terminal evidence gate for the same candidate.

Protected integration, independent evaluator evidence, authority, deployment and cleanup remain pending. Local source work and this draft update are complete; no new approval is needed for the work already covered. Evidence root: `.workspace/.artifacts/listing-entry-management/42f118e/` relative to the shared GitHub workspace; contains exact candidate manifest, browser result, desktop/mobile images and gate output. Serving tokens are zero for this deterministic local slice; model usage, user value, operator time saving and first-dollar demand remain unmeasured. The local preview is stopped after verification. Keep the full v4 backup before downgrade; retain both existing lanes until their owners authorize source integration and cleanup.
