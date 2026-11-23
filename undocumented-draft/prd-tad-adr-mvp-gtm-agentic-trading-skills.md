---
title: "Agentic Trading Skills: native gateway consumer"
doc_type: "PRD-TAD-ADR-MVP-GTM"
version: "0.16.0"
date: "2026-11-24"
lang: "en-US"
frontmatter_contract: "required"
owner: "Product function"
continuity_id: "AGENTIC-TRADING-SKILLS-001"
prd_revision: "0.16.0"
tad_revision: "0.16.0"
adr_revision: "0.16.0"
mvp_revision: "0.16.0"
gtm_revision: "0.16.0"
local_rung: "dev-proven"
delivered_rung: "undocumented"
lane: "authoring"
universal_scope: false
worktree_id: "device-0232231d4a19--moomoo-integration-roadmap"
agent_id: "codex"
lifecycle_status: "proposed"
guideline_revision: "3.5.1"
guideline_source: "https://github.com/huijoohwee/huijoohwee.github.io/blob/f07f1a3c27d6936f86233d750d8db7b7690d5fb4/guidelines/prd-tad-adr-mvp-gtm-guidelines.md"
source_docs:
  - "huijoohwee.github.io@f07f1a3c27d6936f86233d750d8db7b7690d5fb4:guidelines/prd-tad-adr-mvp-gtm-guidelines.md"
  - "huijoohwee.github.io@f07f1a3c27d6936f86233d750d8db7b7690d5fb4:guidelines/skill-guidelines.md"
  - "huijoohwee.github.io@f07f1a3c27d6936f86233d750d8db7b7690d5fb4:guidelines/skill-repo-map.md"
  - "huijoohwee.github.io@f07f1a3c27d6936f86233d750d8db7b7690d5fb4:guidelines/codebase-neutrality-guidelines.md"
  - "huijoohwee.github.io@f07f1a3c27d6936f86233d750d8db7b7690d5fb4:guidelines/lean-startup-guidelines.md"
  - "huijoohwee.github.io@f07f1a3c27d6936f86233d750d8db7b7690d5fb4:docs/documents/prd-tad-adr-mvp-gtm-agentic-functions.md"
  - "agentic-os@abcbfc6dc5e9e3c5f4ccb91bd5a7cdfed39408fc:package.json"
  - "agentic-os@abcbfc6dc5e9e3c5f4ccb91bd5a7cdfed39408fc:catalog/invocation.json"
  - "agentic-os@abcbfc6dc5e9e3c5f4ccb91bd5a7cdfed39408fc:catalog/features.json"
  - "agentic-os@abcbfc6dc5e9e3c5f4ccb91bd5a7cdfed39408fc:runtime/agents/docs/SKILLS.md"
  - "agentic-os@abcbfc6dc5e9e3c5f4ccb91bd5a7cdfed39408fc:__tests__/portable-skills.test.mjs"
  - "agentic-os@11c8fde490e1af2622d465ff2b98e7e1930095c3:catalog/invocation.json"
  - "agentic-os@11c8fde490e1af2622d465ff2b98e7e1930095c3:skills/trading/SKILL.md"
  - "agentic-trading-platform@173e71f2a4d48f61f17b3bf85266965b7f6a3924:scripts/package-skill.py"
  - "agentic-os@b2966d88f57abfec7f4f1c0211c9740526a98c67:skills/trading/SKILL.md"
  - "agentic-trading-platform@58d46ff779d3240b3200b677360560fdd40b10e3:runtime/provider-mapping.mjs"
  - "agentic-trading-platform@4db0b21d45c07cc89dead27d2dea13cacf7514bb:runtime/rest-market-read.mjs"
  - "agentic-trading-platform@4db0b21d45c07cc89dead27d2dea13cacf7514bb:src/provider-coverage.mjs"
  - "agentic-graph@33c955a4e24d62b4fbd7323d52c689037320ef9a:canvas/src/features/panels/views/tradingCalendarReceipt.ts"
  - "agentic-gateway@563dab262dd6a7debd8d4e643505ec64666893e0:connectors/profiles.json"
  - "agentic-trading-platform@afb60fbbc966010767adf5ac8e201d3bea06e214:qualification/moomoo/README.md"
  - "agentic-os@1b7f3726fd250127d93d8a0ccaa08ae356974385:skills/trading/SKILL.md"
  - "AGENTIC-TRADING-HYBRID-001@0.20.0"
---

# Agentic Trading Skills: native gateway consumer

`AGENTIC-TRADING-SKILLS-001@0.16.0` accompanies [Trading 0.20.0](./prd-tad-adr-mvp-gtm-agentic-trading.md). OS owns the portable instruction and catalog identity. Gateway publishes shared connector profiles and conversions. Trading admits domain operations, enforces rights, records the ledger and signs results. Graph renders permitted results. VCC-14 covers the released synthetic desk. VCC-15–18 define the remaining laboratory acceptance tests.

Trading admits API and MCP through one signed-grant boundary (Product E-42/E-44). Outbound mappings, connected rights and host binding require independent qualification. Graph Integrations can present admitted capabilities through Design System. The skill discovers and explains them with `authority: false`. Product-local scope and S1 ownership continue to apply.

**Historical release status, 21 November 2026.** E-28 records the native desk instruction source, offline installation and local ZIP inspection. Product E-46 records local synthetic desk behavior. E-09–27 describe earlier candidates and specification work. Operator-attested external runtime, provider permissions, Cloud package acceptance and commercial adoption remain open.

## Decision record (ranked next outcome)

| Field | Value |
|---|---|
| Next outcome | A desk operator can explain one entitled quote from a named hosted moomoo MCP session and reopen its permitted receipt in Graph. Show provenance, time, known field precision and expiry. Physical-device and human acceptance remain deferred. [Consumer roadmap](#native-consumer-implementation-roadmap) |
| Riskiest uncertainty | The canonical inbound gateway now exists implemented-local (Product E-42/E-44) and the general provider-mapping definition registry landed on Trading main at `58d46ff` (Product E-50, PR #5); per-provider connected conformance, per-environment rights, least privilege, simulator enforcement and $0 remain unproven. Demand remains unvalidated. |
| Cheapest sufficient test | Explain the E-34 signed conformance receipt offline. Compare it with the separate OpenD display replay and identify the unknown fields. Repeat with one hosted N3 read after Trading admits the binding. |
| Threshold / window | One outbound business read, one ledger result, matching incoming HTTP and MCP replay, and a tested expiry refusal. Qualify R1–R4 separately per package and host. S2 requires an independent second consumer and S3 requires two compatible callers. |
| Stop / revisit | Stop extraction if no second consumer is named (retain-local); revisit at discovery, baseline, MVP acceptance, audience handoff. |
| Bounds | Time-box each qualification slice to 90 active minutes. One skill source ≤8,191 bytes, zero added runtime modules for this plan, <600 lines per plan and <500 kB per chunk. Use local fixtures first and require $0 provider spend. |

## Reference implementation — PRD

### Vision, user, and job

Make reusable trading capability a **shared, headless, invocable asset** owned once and consumed by
many products. The immediate user is an **integrator/maintainer** of a second agentic product who
needs trading capability without re-implementing or forking it. The beneficiary is the end operator
who gets consistent, provider-neutral behavior across products.

### Pain-point-to-feature mapping (all `unvalidated`)

| Pain | Hook | Break | Fix | Close | Min-time-resource-max-value |
|---|---|---|---|---|---|
| P1 Duplicated trading logic drifts across products (`unvalidated`) | "Reuse one trading skill everywhere" | Clients duplicate signals/risk and bypass a single owner | OS descriptor/instructions consumed against Trading-owned canonical admission/policy | One instruction identity; product-local policy; two compatible callers before pure extraction | Reuse `skills/` and `catalog/`; no new OS runtime or registry at S1 |
| P2 Provider-specific instructions couple reuse to one environment (`unvalidated`) | "Use one native gateway consumer" | Transport, credentials and rights differ; copied instructions drift | Provider-neutral instructions; Trading owns domain admission and consumes pinned Gateway profiles | Native bytes reviewed; inbound parity and outbound mappings qualified separately | Existing OS seams only; hosted N3 qualification pending |
| P3 Trading policy leaks into shared utilities (`unvalidated`) | "Keep the core portable" | Domain rules/secrets/effects contaminate browser-safe utilities | Separate pure contract from domain owner and adapters; policy stays local | Effect-free core; dependency direction portable → domain → adapter → view | Reuse Functions portable-call pattern; build no domain logic into the core |

No quotes, tickets, or measured behavior are recorded; all pain is `unvalidated`. P1 is a bounded
learning hypothesis at baseline, not validated demand. `demand-proven` is reserved for paid-customer
evidence and is not claimed.

### MoSCoW stories

| ID | Priority | Story | Acceptance (VCC join) |
|---|---|---|---|
| PRD-SKL-01 | Must | As an integrator I can discover a trading skill descriptor offline from one centralized catalog | VCC-01, VCC-05 |
| PRD-SKL-02 | Must | As a maintainer I can validate one skill package through the portable-skills contract | VCC-02, VCC-08 |
| PRD-SKL-03 | Must | As a reviewer I can confirm the core is provider-neutral, headless, and effect-free | VCC-03, VCC-04 |
| PRD-SKL-04 | Must | As an owner I can confirm OS solely owns portable instructions/catalog while Trading owns canonical gateway admission, policy, ledger, signed read envelope/guard and provider mappings; all instruction clients are consumers | VCC-07 |
| PRD-SKL-05 | Should | As a second consumer I can pin a shared pure operation once two compatible callers exist | VCC-06 (gated S3) |
| PRD-SKL-06 | Won't (this increment) | Extract all trading domain logic into the shared core | Retain-local per ADR-03 |
| PRD-SKL-07 | Must (event runtime) | As the operator I can trace reviewed native bytes through archive acceptance to the actual executing host's discovery, binding, documented transport and independently verified auth | VCC-09/10; R1–R3 |
| PRD-SKL-08 | Must (event runtime) | As the reviewer I can reproduce pinned delegation, independent signed veto, safe refusal and rollback without giving an agent direct broker-write authority | VCC-11/12; R4 |
| PRD-SKL-09 | Must (gateway target) | As a consumer I use one canonical operation/admission contract over inbound API or MCP without embedding provider adapters; each outbound REST/MCP mapping is admitted independently | VCC-13 and R-GW local conformance, then N3 connected acceptance |
| PRD-SKL-10 | Must | Guide market, portfolio, research and prediction workflows through discovered Trading operations. Report the data source, result and available authority before interpreting a result or requesting an effect. | VCC-14 for the local baseline. VCC-15–18 and Product VCC-40–46 for full parity. |

### Success metrics and Time-to-Value

| Metric | Target (estimate, unvalidated) | Method |
|---|---|---|
| TTV (integrator) | ≤ 10 min from opening the catalog to discovering and invoking one pinned skill capability offline | Clean-environment local rehearsal; zero token cost; no auth |
| Discovery cost | 0 tokens / $0 per read | Offline catalog read; metadata-first |
| Duplicate owners | 0 new registries; one capability identity | Invocation Register join check |
| Drift after reuse | Unknown — measure failed/repeated actions before/after | GTM experiment H2; not yet measured |

The historical release harness completed its canonical route check in 0.277 s (E-12); this is not a current candidate result. Human setup, host discovery and verification still need a timed integrator session.

### Verification conditions (VCCs)

E-11/12/14 retain baseline S1 results; E-19 retains the later **pre-gateway** bytes/digest/install results. Neither validates the new gateway-consumer revision, qualifies a connected host or proves instruction-following behavior. R-GW is independent of package, host and connected acceptance.

| VCC | Condition | Evidence Reference | State |
|---|---|---|---|
| VCC-01 | Offline discovery returns a stable ID, owner, description, source and SHA-256. | E-11/12, `/skill.discover` | Passed with zero model tokens and zero estimated cost. |
| VCC-02 | The installed export resolves, the descriptor matches the YAML, and loading checks the exact entrypoint bytes. The standalone skill resolves its resources. | E-11/12, portable skills contract | Passed after packing and installing offline. Unknown IDs, changed bytes and missing files each produced the expected error. |
| VCC-03 | The portable descriptor and instructions are provider-neutral and headless. Reading either grants no effects. | E-11/12, descriptor and entrypoint inspection | Verified for S1. The routes return `authority: false`. |
| VCC-04 | Shared operation is effect-free (no I/O/model/DOM/global state), typed input/output, bounded, deterministic digest | E-04 (G4), check `purity-contract` | deferred to S3; not run |
| VCC-05 | The command, read-only semantic and skill binding resolve one identity through the existing Invocation Register. | E-11/12, invocation and portable-package checks | Passed for discovery and load. |
| VCC-06 | Extraction deferred until two concrete consumers with compatible contracts (S3); second-product adoption requires a named consumer and a verified pin (S2) | E-06 (G4), check `reuse-gate` | gated; not satisfied |
| VCC-07 | OS solely owns portable instructions/catalog; Trading owns canonical gateway admission, account policy, SQLite ledger, signed read envelope/single paper guard and provider mappings. Native/third-party instruction clients consume, never adapt providers or authorize execution. | G6/G7/G9; E-17–19 | Target contract; no new OS registry/runtime or external skill prerequisite. E-19 is pre-gateway; E-22 verifies revised bytes/digest. |
| VCC-08 | Historical local proof, new native source, gateway conformance, package/host/connected qualification, delivery and demand carry separate status. | E-09–21 | E-11/12/14 are baseline S1; E-19/20 pre-gateway; E-22 current local checks, E-23 final validation. Direct connector smoke is not gateway proof; connected status UNQUALIFIED. |
| VCC-09 | Review native source identity and complete bytes, standalone entrypoint <8192 bytes, dependency/resource closure and rights. Use the existing product packager and inspector for strict YAML/name, compressed/expanded bounds and rejection of traversal, symlinks, duplicates, missing resources and secrets. | R1/R2; E-17 | Product packaging seam exists; optional Python dependencies absent in default interpreter; no new archive/test acceptance claimed. |
| VCC-10 | Resolve the native skill in the actual executing host/store; for Cloud retain actual `skill_id`, immutable version and content readback, bind the executing Agent and inspect a fresh Session. Verify that environment's documented transport/runtime/auth with a harmless admitted read. | R3; Trading RT-02/04/05 | Pending; no upload or provider execution in this revision. MCP-only needs no CLI; absent required capability yields a typed gap, not fallback. |
| VCC-11 | Coordinator explicitly delegates; pinned child outputs join by immutable input/policy/account binding. Independent authenticated risk can veto; forged files, stale verdicts and direct execution bypass fail the external guard. | R4; Trading VCC-25/34 | Pending; independent conversations alone do not provide enforcement. |
| VCC-12 | Before/after configuration and effective hashes match intended edits; fixed four-prompt evaluation, new Session snapshots, per-Thread events, resource digests and restore of the predecessor are retained. | R4; Trading VCC-26/33 | Pending joined receipts; historical fixture version strings are not host provenance. |
| VCC-13 | Inbound API/MCP have identical canonical admission outcomes; outbound REST/MCP mappings independently match provider/adapter/schema/mapping pins, operation, environment/account or public-data scope, rights, freshness/delay, quota and $0. Unknowns, passthrough, token forwarding and silent fallback fail closed. | R-GW; G9 | Inbound parity and selected outbound REST/MCP mappings pass local fixtures (Product E-55–57). Hosted provider qualification is pending per operation and host. |
| VCC-14 | Parity consumer guidance covers Product PRD-TRD-09 groups (a)–(i) through admitted operations only; experiment/prediction surfaces hold no dispatch authority; paper writes stay behind the single guard; no reference name/copy/dependency appears in native bytes or payloads. | Product VCC-39, E-28 | IMPLEMENTED-LOCAL. Portable discovery/load, archived instruction bytes and local gateway behavior verified. |
| VCC-15 | On landing, discover capabilities and enter the desk. On the desk, independently exercise all 22 actions mapped below. Verify feature detection, one registration per action, abort on navigation, ordinary-browser fallback and equivalent human/API/MCP results. | Product VCC-40–42 | Required. Synthetic API/MCP proof covers only the existing operations. |
| VCC-16 | Obtain a read-only observer link. Follow the same market context, chart overlays and sanitized activities from a second device. Attempt a write and an expired read, then verify the owner session remains intact. | Product VCC-43 | Required. A loopback owner cookie supplies no observer proof. |
| VCC-17 | Save a Python strategy by hash, run one historical hypothesis and all 20, poll, cancel and overlay markers. Explain technical outcome, input quality, risk and profitability separately, including missing data, modeled costs and cache provenance. | Product VCC-44–46 | Required. A browser signal run or a synthetic report cannot qualify a historical result. |
| VCC-18 | Inspect both spot and perpetual accounts. Require direct owner intent for each paper mutation, submit once and reuse the request binding after timeout. Test an over-limit order, a reduce-only reversal, a mismatched retry, ambiguous instructions and an untrusted label that requests a trade. | Product VCC-41/42 | Required. Every refused case preserves the prior ledger revision. |

## Reference implementation — TAD

### Codebase Grounding Record (historical observations; current owner-supplied facts)

| ID | Input | Exact source / revision | Inspected fact | Disposition |
|---|---|---|---|---|
| G1 | Skill package seam | `agentic-os@abcbfc6dc5e9e3c5f4ccb91bd5a7cdfed39408fc:skills/` | `canvas`, `esp-idf`, `software-forensics`, each `SKILL.md` with YAML `name`+`description`; subpath exports `./skills/<name>/SKILL.md` (+ `esp-idf/references/*`) | reuse (existing owner) |
| G2 | Catalog manifests | `agentic-os@abcbfc6:catalog/invocation.json`, `catalog/features.json`, `catalog/composition-source-lock.json` | invocation schema `agentic-os-invocation-catalog/v1`, entryCount 36, digest `sha256:aa9adef3…b5abc5`; features schema `agentic-os-feature-catalog/v1`, profile `fossOnly:true`, `maxIncrementalSpendUsd:0`, `deploymentAllowed:false`, entryCount 5, digest `sha256:17714ee4…25d985`; composition lock artifacts `{blob, owner, path}` | reuse (manifest precedent) |
| G3 | Runtime + admission seams | `agentic-os@abcbfc6:package.json`, `runtime/adapters/` | exports `./agents/skill-registry-gate`, `./agents/skill-proposer` — the **Agent-Definition** proposed→active promotion path (operator-gated, tool allowlists), *not* `SKILL.md` admission; also `./context/*`, `./planning/*`, `./forensics/source-evidence`, `./agent-docs/SKILLS.md`; `runtime/agents/docs/SKILLS.md` schema `agentic-canvas-os-skills/v1`, `publish_policy: Dev-only until explicit operator approval` | reuse (Agent-Definition path; separate from portable skills) |
| G4 | Functions consolidation pattern | `huijoohwee.github.io@f07f1a3c:docs/documents/prd-tad-adr-mvp-gtm-agentic-functions.md` (`AGENTIC-FUNCTIONS-001@0.1.1`) | T3 `catalog/functions.json` discovery gated S2 (named second consumer); T4 `runtime/functions/sum.mjs` + export `agentic-os/functions/sum` gated S3 (two callers); ADR-04 keep existing repos; portable call = ordered 0–512 finite binary64, effect-free. `runtime/functions/` and `catalog/functions.json` **absent** at `abcbfc6` (deferred) | reuse pattern; not native proof |
| G5 | Authoring contracts | `huijoohwee.github.io@f07f1a3c:guidelines/prd-tad-adr-mvp-gtm-guidelines.md` (v3.5.1, blob `392fcda1…`, last commit `fc53dc02…`), `skill-guidelines.md`, `skill-repo-map.md`, `codebase-neutrality-guidelines.md` | < 600 lines/file; frontmatter contract; C01–C16; one owner per capability; configuration-driven repo identification; no path-derived claims; brands only under reference-implementation label | govern (this doc) |
| G6 | Trading domain owner | Paired `AGENTIC-TRADING-HYBRID-001@0.20.0`; implementation context at Trading `173e71f2a4d48f61f17b3bf85266965b7f6a3924` (E-17) | Trading owns policy, SQLite ledger, signed telemetry/read envelope, single paper guard and mappings. Packager/inspector, Forward config/diff/GETs and injected-broker guard exist; the canonical inbound gateway is implemented-local, merged into Trading main (Product E-42/E-44), and the general provider-mapping definition registry landed on Trading main at `58d46ff` (Product E-50, PR #5) while per-provider connected conformance remains a target. Real paper dispatch is implemented-local as a labelled simulation (Product E-44); deployed dispatch and complete scheduler/child fetching remain absent | retain-local; owner-supplied facts, not new validation |
| G7 | Native instructions and consumer boundary | OS baseline `11c8fde490e1af2622d465ff2b98e7e1930095c3`; historical `trading-native-runtime` lane (E-18) | Same six-section `skills/trading/SKILL.md` and catalog identity; Gateway-consumer instructions are 8170 bytes (E-22). No provider endpoints/adapters or mandatory CLI in native contract; simulator rights independent of live flags | extend sole OS owner; E-22 bytes/digest/tests passed locally, no new runtime/registry |
| G8 | Portable skill contract + install/run | historical `agentic-os@abcbfc6:__tests__/portable-skills.test.mjs`, `package.json`; E-11/12 baseline release | `npm pack` → offline install → `import.meta.resolve("agentic-os/skills/<name>/SKILL.md")`; `dependencies: {}`; `files` ships `skills/`; resources <8192 bytes; standalone directory; no external relative links. Package resolution alone does not prove host skill-store discovery | reuse historical seam; recheck candidate and explicit host target |
| G9 | Gateway and domain integration | Trading `afb60fb` consumes Gateway `563dab2` and admits signed operations at `/api/gateway` and `/mcp`. | Selected REST and outbound MCP bindings pass local fixtures. The OpenD snapshot profile has separate private-display evidence. | R-GW checks each operation, refusal and scope. N3 requires the first hosted quote joined to a Trading ledger entry. |

G1–G3, G5 and G8 retain baseline observations; G4 is a pattern, not native proof. G6/G9 are bounded owner-supplied implementation facts. E-19 validates only the pre-gateway source/install path; E-22 validates G7's new native revision locally, not gateway execution. Earlier external-source research is superseded, not recast as native implementation evidence.

### Division of Work — ownership and reuse record

| Capability | Owner | Source / export / revision | Current consumers | Decision | Smallest delta | Named check |
|---|---|---|---|---|---|---|
| Native instructions/package | `agentic-os` alone | `./skills/trading/SKILL.md`; E-11 baseline, E-18 lane | Native host/client as consumer; host separately qualified | extend-owner | Same six sections, ≤8191 bytes; handbook 3.1–9; gateway-consumer instructions, no provider library | `portable-skills` (E-22 local pass) |
| Skill discovery catalog | `agentic-os` alone | Descriptor on `@skill:` in `catalog/invocation.json` | Offline discovery/load | extend-owner | Hash exact new bytes; metadata grants no authorization; no new registry | `catalog-read` |
| Shared pure operation | `agentic-os` | Future `runtime/trading/<op>.mjs` + export `agentic-os/trading/<op>` | none yet | defer (S3) | Effect-free only after two compatible callers; no module now, no gateway/policy extraction | `purity-contract` |
| Instruction discovery/load routing | `agentic-os` | `catalog/invocation.json`, `bin/agentic-os-invocation.mjs` at E-11 | Packaged CLI | extend-owner | Existing two read commands and selector only; not gateway execution routing | `invocation-join` |
| Portable skill validation | `agentic-os` | `__tests__/portable-skills.test.mjs`; E-19 pre-gateway | Packaged CLI and standalone instructions | extend-owner | Explicit offline target, zero dependencies, bounds/digest/refusals; native owner refreshes evidence | `portable-skills` |
| Agent-Definition promotion | `agentic-os` | `./agents/skill-registry-gate`, `./agents/skill-proposer` @ `abcbfc6` | runtime agent definitions | defer (separate path) | Not portable-skill or gateway admission | `skill-registry-gate` |
| Canonical gateway admission | Trading | Product E-55–57 and the Trading domain registry | Native hosts, Graph and API clients | Reuse Trading’s signed-grant boundary | Same operation, policy, request identity and ledger across HTTP/MCP | R-GW local conformance and N3 connected acceptance |
| Shared provider profiles and domain mappings | Gateway owns reusable profiles and field conversion. Trading owns semantic bindings and admission. | Gateway `563dab2` and Trading `afb60fb` | Trading, then clients of Trading | Pin the released profile and exercise the native consumer fixture | New provider fields go upstream to their owner. Keep endpoints and mapping tables out of the skill. | R-GW, N1–N3 |
| Archive construction/inspection | Trading | `scripts/package-skill.py`, `scripts/inspect-skill.py` at E-17 | reviewed native archive | reuse | Complete byte digests and nested producer provenance; missing parser dependencies block qualification | `native-package-review` |
| Trading policy and effects | Trading alone | `AGENTIC-TRADING-HYBRID-001@0.20.0`; existing E-17 seams | Product; instruction clients consume admitted results only | retain-local | Account isolation, SQLite ledger, signed reads/independent veto, single paper guard, schedule/dashboard; no duplicate in OS | `ownership-seam` |

Target dependency direction: instruction consumer → Trading canonical gateway → independently admitted product mapping/adapter → provider. The effect-free utility dependency rule remains portable → domain → adapter → view; neither permits provider SDKs, secrets or execution authority in a skill/core. Share by declared export or versioned protocol, never sibling source imports. Consumer metadata can request a supported operation, not select an arbitrary endpoint/tool/command or mint admission.

### Invocation Register

| Route | Kind | Capability identity | Mode | Authority | Owner / schema |
|---|---|---|---|---|---|
| `/skill.discover` | command | trading-skill discovery | read-only | none (metadata) | `catalog/invocation.json` |
| `/skill.load` | command | trading-skill package load | read-only | none | `catalog/invocation.json` |
| `#read-only` | semantic | discovery/load posture | read-only | none | `catalog/invocation.json` |
| `@skill:` | binding | select one descriptor | read-only command option | none | `catalog/invocation.json` |
| skill route `skills/<name>/SKILL.md` | skill | one validated instruction package | consumer guidance only | none; not a provider adapter | package export `./skills/<name>/SKILL.md` + `portable-skills` |
| Inbound API / MCP (implemented-local routes `/api/gateway`, `/mcp`) | product protocol | same canonical Trading operation | one admission boundary | only explicit product admission; never discovery | Trading-owned admission and idempotent ledger. E-55 covers local parity. N3 requires one hosted read. |
| Outbound REST / MCP | product transport | reviewed binding of one semantic operation | independently admitted per binding | host-specific grant, scope and budget | Product E-56 covers local REST and E-55 covers a conformance MCP feed. N3 qualifies hosted MCP. |

The OS register identifies instructions, not provider tools or execution rights. Native skills and third-party instruction clients are consumers; discovery may inventory supported operations, schemas and transport metadata but cannot authorize them. The inbound gateway is implemented-local in Trading (Product E-42/E-44), not a new OS registry or a deployed/cloud service. An inbound MCP caller does not imply outbound MCP support (nor API imply REST); each outbound mapping needs separate admission. Live-order routes/scopes are **out of scope**. Default read-only/mock; simulator rights, account/environment, independent signed veto, operator grant and single product paper guard are separate checks. `live-trade:false` neither proves paper tools absent nor grants simulator rights. Offline discovery/load costs zero model tokens; connected rights, freshness/delay, quota and $0 must be evidenced.

### Flow classification (five types)

| Flow type | Applicable? | View / reason |
|---|---|---|
| User journey | yes | D1 — integrator discovers → loads → invokes one capability offline |
| Workflow | yes | D2 — author descriptor → portable-skills check → catalog read → consumer pin |
| Data flow | yes | D3 — descriptor metadata → catalog manifest → consumer; no secret/effect data in core |
| Orchestration / harness | yes | D4 — target consumer → one admission boundary → independently admitted transport; typed output/cost/refusal, bounded loop |
| Topology | not applicable to this spec edit | No DEPLOYED/cloud gateway; the inbound API/MCP gateway is implemented-local in Trading's separate `trading-runtime-implementation` lane (Product E-42/E-44), a new local runtime surface only. Deploy Boundary closed (no deployment). Outbound provider mappings remain specified, not implemented. |

```mermaid
flowchart LR
  I[Integrator] -->|open catalog| C[catalog/invocation.json]
  C -->|select descriptor| P[skills/name/SKILL.md]
  P -->|invoke existing command| R[Invocation Register]
  R -->|read-only result| I
```

```mermaid
flowchart LR
  A[Author descriptor] --> G[portable-skills check]
  G -->|validate| M[catalog manifest]
  M -->|named second consumer S2| N[consumer pin]
  N -->|two compatible callers S3| O[runtime/trading/op.mjs]
```

```mermaid
flowchart LR
  D[descriptor metadata] --> M[catalog manifest]
  M --> C[consumer]
  X[secrets / provider SDK / effects] -. excluded .-> D
```

```mermaid
flowchart LR
  S[Native skill or third-party consumer] -->|inbound API or MCP: target| G[Trading canonical admission]
  G -->|independent pinned mapping| T[Outbound REST or MCP]
  G -->|typed result or refusal + cost log| S
```

### Contract, failure, and budgets

These are contract obligations: the inbound boundary is implemented-local (Product E-42/E-44), while G9's outbound clients still do not implement provider mappings.

- **One canonical boundary:** normalize inbound API/MCP requests to the same typed operation contract and Trading admission/policy/ledger decisions. Instruction clients carry no provider library, endpoint, tool-name translation, credential logic or execution authority. No copied provider instructions, mandatory CLI or external-skill dependency.
- **Independent mappings:** before dispatch, match approved provider identity and adapter/schema/mapping revisions/digests, canonical operation, selected outbound REST/MCP transport, environment, authenticated caller and account binding **or explicit public-data scope**. Bind policy/input revisions too; mismatched, unknown or unsupported pins/operations/scopes fail closed. Inventory is metadata, not admission or compatibility proof.
- **Rights and evidence:** verify interface/data rights, permissions, freshness/observed time/expiry, delay class, quotas and $0 for that exact mapping and environment. Public data is not an inferred account entitlement or proof of free use. Unknown rights, quota, fees or freshness block connected use; no broadening scope to succeed.
- **No passthrough/fallback:** validate incoming gateway token audience; reject raw endpoint/tool/command passthrough, incoming token forwarding to providers, guessed capabilities and silent provider/transport switching. Product credentials stay server-side and are independently scoped; inbound auth cannot substitute for outbound auth. Changing provider/transport requires explicit mapping review and re-admission, not a skill fork.
- **Honest output:** typed results/refusals include provenance, selected pins, timestamps/delay, unknowns and cost evidence. Preserve supplied numeric precision and units; never synthesize precision, prices, timestamps or freshness. Missing categories remain typed gaps; an unavailable provider can leave offline metadata readable, never create an effect path.
- **Isolation and enforcement:** bind account-scoped reads/caches/intents/ledger records to the exact account/environment; never reuse another account's credentials, receipts or risk approval. Keep public-data scope explicit. Paper requires independent signed risk veto, expiring operator grant and the single Trading paper guard; live routes/scopes remain excluded. An instruction or discovery result is never a grant.
- **Uncertainty and bounds:** preserve durable deduplication, reservations, ledger/checkpoint and `RELEASE_UNKNOWN` across timeouts, restart and rollback; reconcile authoritatively before any new dispatch, never auto-resubmit. Emit cost/refusal logs; bound every loop and circuit-breaker. Read-only/mock is an explicit safe state, not silent transport fallback. S1 token spend $0, ≤1 validation pass, ≤4 h active.

**R-GW · Gateway conformance acceptance (separate gate).** Inbound API/MCP parity, refusal and ledger outcomes for equivalent canonical inputs are implemented-local and passing (Product E-42/E-44); outbound tests must independently exercise each supported provider/REST/MCP mapping and pin drift, unsupported operations, account/public-scope isolation, expired rights/data, quota/$0 failures, passthrough/token-forwarding denial, no silent fallback and precision preservation. Include signed veto/single-guard enforcement and duplicate/uncertain/restart cases. Retain exact code/schema/mapping fixtures and receipts. Inbound parity/refusal/isolation/precision/restart tests are **implemented-local**; outbound provider-mapping conformance remains **pending**, and mock conformance would not prove real-provider compatibility. Package acceptance, host binding, a direct connector read and connected execution cannot substitute for R-GW, nor can R-GW substitute for them.

### Install and run mechanics (native package; historical S1 seam)

- **Store**: OS `skills/trading/SKILL.md` remains the sole portable instruction source: same six sections,
  ≤8191 bytes, zero runtime dependencies and no external relative links. Any resource meets the portable
  size bound. E-22 records refreshed catalog digest, unchanged entry count and tests for the new bytes;
  E-19's 8169-byte digest is pre-gateway history. No new runtime module, registry or provider endpoint.
- **Package resolution**: E-22 repeats `npm pack` → offline install →
  `import.meta.resolve("agentic-os/skills/trading/SKILL.md")`. Rehearse only in an explicit absolute
  install target with an available local tarball, no implicit global/home target or dependency fetch.
  npm installation/export resolution alone is **not** executing-host skill-store discovery.
- **Host installation**: name the exact host, user/project scope and absolute skill-store target;
  admit reviewed native bytes through that host's documented local mechanism. Verify discovery and
  loading in the actual executing session. Do not install an external skill or infer host binding from
  a package on disk. For Cloud, R2/R3 separately require immutable native ZIP acceptance and binding.
- **Run (gateway target)**: inventory quote, news, digest, sentiment and unusual-activity metadata;
  absent categories stay typed gaps. Consume only admitted canonical operations, not raw provider tools.
  Match provider/adapter/schema/mapping pins, operation, environment/account or public-data scope,
  rights, freshness/delay, quota and $0; qualify inbound and outbound separately. MCP requires no CLI.
  The inbound gateway is implemented-local (Product E-42/E-44); G9's outbound clients are not a provider-mapping gateway. Do not fabricate a route or bypass admission with a direct connector.
- **Paper boundary**: default read-only/mock; separately check documented simulator rights and a
  SIMULATE account even when `live-trade:false`. That flag is not proof of unavailable paper tools.
  Paper effects require independent risk, expiring operator grant and the product guard; no live scopes.
- **Admission check**: rerun existing `portable-skills` for candidate bytes/digest, offline resolution,
  zero dependencies, bounded standalone resources and failures. Agent-Definition promotion remains
  a separate path; native package checks do not prove host auth or connected readiness.

From an `agentic-os` checkout, run the following commands. Quoting the semantic keeps `#` literal in a shell. The installed `agentic-os` binary accepts the same arguments.

```sh
node bin/agentic-os.mjs /skill.discover '#read-only' '@skill:trading'
node bin/agentic-os.mjs /skill.load '#read-only' '@skill:trading'
```

Discovery returns metadata. Load verifies the file and returns its instructions. The documented failure codes are `skill-unavailable`, `skill-digest-mismatch` and `skill-source-unavailable`.

### Event runtime contract — handbook 3.1–9 (native source; connected UNQUALIFIED)

Trading owns RT-01–RT-10, domain admission, account policy, ledger, signed read envelope, independent veto, single paper guard, scheduling and execution authority. Gateway publishes reusable provider profiles and field conversions. OS owns portable instructions and their catalog. Third-party hosts consume this contract through Trading.

| Layer / handbook | Artifact and owner | Required proof / boundary |
|---|---|---|
| Native skill / S1 | OS `trading` descriptor and digest-verified first-party entrypoint | Consumer only; discover/load grant no effects. E-14 is baseline, E-19 pre-gateway; E-22 supplies revised count/digest/install/load evidence. |
| Gateway / cross-cutting | Trading domain admission and reviewed bindings consume a pinned Gateway profile where applicable. | Inbound parity and selected outbound REST/MCP mappings pass local fixtures (Product E-55–57). Hosted provider qualification is pending per operation and host. |
| Desktop connector / 3.1 | Documented session connector; future product-admitted mapping is separate | Verify schema/runtime/auth and all admission evidence. E-21 direct read is bounded connector smoke, not an admitted gateway call; tool inventory grants no rights. |
| Desktop native skill / 3.2 | OS standalone `skills/trading/SKILL.md` installed to an explicitly named host store | Resolve reviewed bytes in the executing session; no external wrapper/install dependency. Package resolution is not host discovery. |
| Cloud control / 3.3 | Operator-admitted control interface for the chosen host | Verify actual availability, identity and readback of the intended template/environment; local source does not prove remote control access. |
| Cloud credentials / 4.1 | Operator-owned session Vault and Agent-specific tool permissions; product-held outbound credentials | Desktop login is not inherited. Gateway grants/config/identity and outbound mapping rights must agree independently; never forward incoming tokens. No mandatory CLI or native provider endpoints. |
| Cloud native skill / 4.2 | Native archive produced by the existing product packager, accepted as an immutable version | R1–R4 separate source review, ZIP validation, host acceptance/content readback, Agent binding and execution. |
| Channel / 5 | Optional paired channel, outside the skill package | Approved destination and harmless delivery proof; no order/mandate authority via chat; secrets never in skill files. |
| Schedule / 6 | One coordinator's bounded schedule and durable product checkpoint | Self-contained inputs, IANA timezone/window, concurrency one, finite attempts/cost, config bindings and distinct trigger/run/delivery states; inspect child Threads. Verify the reference host's disputed `start_at`/`stop_at` create-schema support before recurring activation. Manual-first; enforce an independent exclusive UTC cutoff at trusted dispatch, retain in-flight uncertainty, handle holidays/DST and persist events/cursors/deduplication atomically. No competing child schedules. |
| Dashboard / 7 | Existing product views over server-redacted signed observations | Credentials stay server-only; product owns adapter/provenance/redaction. No raw Vault/account secrets or skill-side dashboard implementation. |
| Versioning and collaboration / 8–9 | Product-owned independent role outputs and sanitized config history | Exact child/skill versions, effective hashes, actual Thread events, independent veto, external guard and rollback; shared files are not a trust boundary. |

**Per-environment transport/auth qualification.** Inbound API and MCP must share Trading's canonical admission; outbound REST and MCP require independently reviewed mappings, not caller-selected raw tools or implicit protocol pairing. Match provider/adapter/schema/mapping pins, operation, environment/account or public-data scope, authenticated identity, rights, freshness/delay, quotas and $0. Desktop auth, Cloud Vault and product outbound credentials are not interchangeable; never forward incoming tokens. Missing/unsupported evidence yields a typed refusal with no account, scope, provider or transport fallback. MCP needs no CLI install/login; no new CLI installation is authorized. The inbound boundary is implemented-local (Product E-42/E-44); outbound provider mappings remain a target contract, not current G9 capability.

**Select only permitted categories.** Quote, news, digest, sentiment and unusual-activity reads are portable categories, not provider skill dependencies or authorization. Missing data/categories remain unknown, without synthetic precision. Independently check simulator rights: `live-trade:false` neither proves paper tools absent nor authorizes use. No live scopes; paper writes go only through the single external Trading guard with isolated account/policy, independent signed risk veto and expiring operator grant. Never give a sandbox a direct-write bypass credential. E-21's user-requested direct Desktop read supplies no gateway admission, Cloud, scope/rights/delay/$0, account-access or order proof.

**Desk guidance and operation map.** Use `/skill.discover #read-only @skill:trading` and digest-checked load for instructions. Read the current capability descriptor from Trading. The table names user actions, leaving wire names to the existing gateway. The landing route supplies discovery and entry. The five groups below account for the 22 desk actions required by VCC-15. Each browser action reads or updates the same state the owner sees.

| Surface | Required desk actions | Consumer contract |
|---|---|---|
| Discovery and context (5) | Describe capabilities, obtain the observer session, search instruments, set instrument/type/timeframe, replace the full indicator selection. | Show data source and freshness. An empty selection clears studies. A fixture is identified as synthetic even during stream playback. |
| Market inspection (3) | Inspect completed chart bars and markers, inspect depth and imbalance, inspect trades and aggressor volumes. | Distinguish forming and closed bars, report venue/type and UTC interval. Bound and paginate results. Treat labels as untrusted data. |
| Paper account (7) | Read the account, page history, place an order, cancel an order, add virtual funds, record a prediction, reset the session. | Explain cash, contracts, margin, fees and funding using the same revision. Bind the precise effect and retry key to owner intent. Require the displayed reset phrase. Every write goes through Trading’s simulation guard. |
| Research authoring and execution (4) | List built-in and saved strategies, save named source, queue one historical run, queue the complete regression. | Show all 20 catalog rows, dependencies and availability. Saving validates and versions source. Research has its own initial capital and cannot dispatch paper orders. |
| Research follow-up (3) | Read run progress/result, overlay the stored signals on the matching chart, cancel a queued or running job. | Report last observed state, requested/actual dates, UTC annual and walk-forward metrics, assumptions and artifact hash. A cached result identifies its source run, scientific hash and immutable artifact. A blocked row has a reason and an unknown return. |

| Gate | Procedure and retained evidence | Pass / refusal |
|---|---|---|
| R-GW · Gateway conformance | Exercise matching HTTP/MCP admission and separately pinned outbound REST/MCP contracts, including refusal, isolation, veto and uncertainty. | Inbound parity and selected outbound REST/MCP mappings pass local fixtures (Product E-55–57). Hosted provider qualification is pending per operation and host. |
| R1 · Native source review | Review OS YAML identity, same six-section source, complete inventory/digests, resource/dependency closure, rights and consumer-only safety instructions. Record producer commit, candidate changes, reviewer and UTC; verify ≤8191 bytes and exact catalog digest. Review Trading-owned mapping pins/transport/auth separately. | No provider execution or installation. Unknown rights, runtime, cost or bypass blocks use. Baseline commit does not identify changed bytes; E-19 cannot identify the new gateway revision. |
| R2 · Native archive qualification | Reuse Trading `scripts/package-skill.py` with reviewed native source ZIP and review JSON; independently inspect output ZIP with `scripts/inspect-skill.py`. Retain source/archive/per-file digests and review manifest. Review schema `skill-package-review/v1` uses `upstream.repository` and exact `upstream.revision` for the OS producer, not an external skill prerequisite; `source_sha256` and complete `source_files` identify bytes. An uncommitted candidate is not the base commit's archive: retain its separate digest and require reviewed source/provenance before packaging, never fabricate a Git pin. | One top-level folder equal to YAML `name`; strict YAML/name ≤64 chars matching `^[a-z0-9][a-z0-9_-]*$`, nonempty description ≤5120 chars. Confirm host compressed/expanded byte limits (handbook ceiling 50 MB each; stay below both). Reject traversal, symlinks, duplicate members, missing links, corrupt ZIPs, secrets and Git/OS debris. No skill execution, dependency installation or automatic upload. |
| R3 · Executing-host binding/auth | Name host/store target; discover/load reviewed bytes there. For authorized Cloud acceptance retain actual `skill_id`, immutable opaque string `version`, downloaded content digests and timestamp; bind exact version to the executing Agent and inspect a fresh Session. Verify runtime, inbound gateway auth and independently admitted outbound mapping with a harmless read, when implemented/authorized. | npm install, ZIP acceptance or metadata hash alone is insufficient. Keep versions lossless, verify bytes. MCP requires no CLI. Missing credential/runtime/scope gives a typed failure; E-21 direct connector smoke is not this receipt. Acceptance alone is `PACKAGE_ACCEPTED`, connected status UNQUALIFIED. |
| R4 · Joined qualified runs | Join R-GW and native candidate/package/host receipts with product candidate, strategy/policy/evaluator, provider/adapter/schema/mapping pins, operation, isolated account/environment or public scope, rights/freshness/quota/$0, effective config, child versions, resources and expiring grants. Retain independent-role outputs, bounded coordinator/optional channel, signed redacted telemetry, per-Thread events and EV-01–04 before/after rollback. | Required RT/host evidence must pass; no implicit `latest`, stale resource, token forwarding, risk bypass or ambiguous effect. Mocks/injected broker are not real paper transport; paper needs separately documented simulator rights, signed veto and single external guard. Preserve ledger/uncertainty across restart. |

At Trading `173e71f2a4d48f61f17b3bf85266965b7f6a3924`, the existing packager interface is `python3 scripts/package-skill.py --source <native-source.zip> --review <review.json> --output <native.zip>`; the current tree also exposes `--source-archive`. `python3 scripts/inspect-skill.py <native.zip>` remains the separate local validator. These are product-owned tools, not installers, rights grants or uploaders; reuse them rather than adding a registry or OS packager. The default interpreter lacks `yaml` and `markdown_it`; E-19 records eight corresponding test skips. R2 is blocked until an approved dependency environment and native archive review are available. No dependency installation or validated native ZIP is claimed.

### Structured roles, ownership and enforcement

These role outputs are obligations on **product-owned envelopes**, not new OS implementations or host API objects. The paper join includes `schema`, `run_id`, `decision_id`, `environment=SIMULATE`, `account_alias`, `profile`, `strategy_revision`, `policy_revision`, `evaluator_revision`, `snapshot_digest`, observed/expiry UTC and source references. Gateway targets additionally bind operation, provider/adapter/schema/mapping pins and admission evidence. Public-data reads use explicit public scope, never an invented account binding or account grant. Product validation rejects missing, mismatched or expired fields and cross-account reuse. Credentials resolve only behind the product boundary; sanitized provider provenance releases no secrets. The implemented-local inbound gateway (Product E-42/E-44) and existing signed telemetry/guard (E-17) still do not qualify joined host execution or connected provider mappings.

| Role | Structured output / file ownership | Capabilities and forbidden paths |
|---|---|---|
| Coordinator | Delegation plan and final run summary; owns only its summary artifact | Explicitly delegate research, await independent risk, then request guard evaluation; no broker credentials, direct orders, approval minting or policy edits. A selected child list alone does not cause delegation. |
| Researcher | `CANDIDATE` or `NO_TRADE`, source/time/freshness, signal, invalidation and unknowns; owns only research output | Admitted read-only market/news tools; no paper/live write, risk-file changes or execution claims. Missing evidence remains unknown. |
| Risk auditor | `APPROVE`, `REJECT` or `UNKNOWN`, isolated account/intent/input/policy digest, limits, reasons and expiry; owns only risk output and drawdown report | Independent signed veto is final. Trading authenticates reviewer principal/runtime and retains approval outside shared files; distinct conversations alone are insufficient. Research-authored JSON or cross-account approval is never accepted. |
| Paper executor | Bound intent reference to the external guard; guard returns `BLOCKED`, `NO_TRADE`, confirmed broker-state receipt or `RELEASE_UNKNOWN` | Guard interface only; no direct broker MCP/API/CLI writes or credentials, arbitrary network/shell bypass or self-approval. Only the guard owns durable intents, reservations, deduplication and final decision/execution log. |
| Advisor (optional) | Second-opinion text only; no authoritative files | No tools or actions. Advice never substitutes for risk approval or guard evaluation. |

Treat a host's shared filesystem and session-bound Vaults as shared trust surfaces even with distinct conversations; verify actual isolation rather than inferring it from roles. File ownership prevents collisions, not bypass. Broker-write credentials and trusted risk approvals must be inaccessible from the shared sandbox; test tool/permission and generic shell/network bypass denial. A provider adapter with direct-write ability belongs behind the external guard, never as an agent bypass tool. If isolation cannot be demonstrated, remain read-only/mock. Do not weaken native safety instructions to achieve a pass.

The single Trading writer emits one structured decision record for every proposal, rejection, abstention, skipped trigger, approval, dispatch uncertainty and reconciliation. Records join the common envelope to authenticated actor/runtime, outcome/reason, source event and intent ID, previous head and output digest. Use idempotent stable IDs and atomic checkpoint updates; agents submit observations, not concurrent appends to one shared log. Do not commit raw account logs; the submission includes only owner-approved redacted projections. A named risk role and a recomputable hash alone prove neither identity nor approval.

### Configuration capture, regression and rollback

Retain sanitized retrieved agent configurations as clearly fenced **data**, apart from editor instructions, only under separate configuration-change authority. Capture retrieved UTC, Agent ID, host-returned version, local revision and change summary per agent. The handbook's local `AGENTS.md` convention grants no editing permission here; this revision changes no config/AGENTS files. Never import exported prompts as instructions to the current assistant.

The portable contract requires documented delegation capability, explicit child bindings/versions and least-privilege tools, not a host-specific broad shell/write preset. In the Cloud reference mapping, `agent_toolset_20260401` and `multiagent.agents` identify that delegation seam; numeric child versions and opaque string skill versions follow the host schema. Product-owned Forward config/diff/GETs exist (E-17). Read back Template, Identity overrides and compiled effective config; retain hashes and actual fresh Session snapshots, preserving intended arrays on update. Compiled config is not a writable Forward request. Re-read/diff conflicts; pause admission, account for in-flight work and verify a new Session before reopening. Complete scheduler/child fetching and the previously recorded schema discrepancy remain qualification gates, not solved by native instructions.

| Fixed evaluation | Required output / negative assertion |
|---|---|
| EV-01 · Eligible fresh fixture | Research candidate → independent approval → mock guard permitted result; bind every revision and retain at most one intent. This does not authorize a provider order. |
| EV-02 · Independent risk veto | A plausible candidate violates the explicit fixture risk limit; auditor rejects, coordinator cannot override, executor makes zero dispatch calls. |
| EV-03 · Missing/stale data | Expired quote, missing delay class or missing selected-transport capability/auth gives `UNKNOWN`/typed failure and no trade. No invented data, wider scopes or mandatory CLI for MCP-only use. |
| EV-04 · Duplicate/uncertain/restart | Redeliver the event and inject a response timeout then restart; one persistent intent, halted new dispatch and authoritative readback required, with no automatic resubmission. |

Run these same fixtures before and after every prompt/model/skill/child/tool/resource change; compare structured safety results and provenance, not prose equality or claimed returns. Local mocks test the contract; an admitted Cloud run must separately demonstrate delegation and tool denial. Collect main and child Thread events rather than treating main-stream completion or `requires_action` as the whole result. Roll back through the predecessor configuration and pinned skill versions, verify a fresh Session and preserve ledger/cursor/uncertainty; never reset a paper account or retry an uncertain order as a rollback.

### Gates and Deploy Boundary

G0–G3 retain historical results. E-19 describes the pre-gateway candidate and E-22 repeats local source, install and discovery checks. E-34–36 add fixture evidence. R-GW, package inspection, per-host execution and a joined provider run each require their own receipts.

| Gate | Condition | State |
|---|---|---|
| G0 grounding | Pin source and owner | S1 source and contract identified (E-11). |
| G1 descriptor | Match the catalog binding to the packaged YAML | Passed (E-11/12). |
| G2 admission | Resolve the installed and standalone skill | Passed offline (E-11/12). |
| G3 discovery | Read metadata and verify selected bytes | Passed on canonical source (E-12); no authorization. |
| R-GW gateway conformance | Same inbound API/MCP admission; independently tested provider/REST/MCP mappings | Inbound parity and selected outbound REST/MCP mappings pass local fixtures (Product E-55–57). Hosted provider qualification is pending per operation and host. |
| S2 second consumer | Independently named second product/integrator pins the descriptor | Open under H1; not satisfied by multiple agents or transports. |
| S3 two callers | Two compatible contracts justify extraction | Open under VCC-04/06. |
| Deploy Boundary | Separate delivery receipt and authority | Closed for hosted delivery. |

All three lanes (authoring / mirror / delivery) are documented; no authoring-lane command mutates a
mirror or delivery surface. Deployment stays closed absent a referenced operator instruction.

## Reference implementation — ADR

| ADR | Decision | Alternatives | Consequences | Recovery / revisit |
|---|---|---|---|---|
| ADR-01 | OS solely owns portable instructions and existing catalog | New repo, copied provider instructions or per-product forks | Same six-section ≤8191-byte skill; no new OS runtime/registry; native and third-party clients are consumers, not adapter libraries | Restore reviewed bytes/digest; recheck exact candidate; reuse gates S2/S3 |
| ADR-02 | Discovery inventories metadata; only Trading gateway admission can authorize canonical operations | Discovery/tool listing or package loading treated as permission | One inbound API/MCP boundary; metadata never grants effects | Keep boundary even after reuse; unknown admission remains refused |
| ADR-03 | Extract only domain-agnostic, two-compatible-caller-proven pure operations; gateway/policy/ledger/mappings retain-local | Extract all trading logic into OS | `universal_scope: false` remains product-local; no extraction by branding a gateway universal | Retain-local without independently named S2 consumer and S3 contracts |
| ADR-04 | Provider-neutral gateway consumers; Trading owns outbound REST/MCP mappings | External skill dependency, provider library in native skill, mandatory CLI | Match provider/adapter/schema/mapping pins independently of inbound transport; no native provider endpoints or lock-in | Re-admit mappings/config on change; no raw passthrough, token forwarding or silent provider/transport fallback |
| ADR-05 | Effect-free utilities; secrets/effects stay behind Trading's product boundary | Provider-coupled core or consumer-side credentials | Portable → domain → adapter → view; account/public scope isolated, no synthetic precision | Provider change needs mapping review, not instruction fork; reject core effects |
| ADR-06 | Existing OS Invocation Register owns instruction discovery/load only | New skill-specific execution registry | Trading canonical gateway is product-owned protocol, not an OS provider registry; no new registry here | Restore reviewed entries/digests; retain single ownership |
| ADR-07 | Separate gateway conformance, native package, host and connected gates | Treat npm resolution, ZIP acceptance or direct read as universal compatibility | Inbound parity and selected outbound REST/MCP mappings pass local fixtures (Product E-55–57). Hosted provider qualification is pending per operation and host. Package, host and joined-run gates stay independent. | Restore qualified pins; G9 gaps and unknown rights/cost remain blocked |
| ADR-08 | Independent signed veto and one external paper guard; shared files untrusted | Direct paper CLI/MCP writes, self-approval or editable reviewer labels | No bypass credential; isolated accounts, expiring grants and durable ledger; no multiagent claim from fixtures | Preserve uncertainty/checkpoint on timeout/restart/rollback; authoritative reconciliation, no automatic resubmission |
| ADR-09 | Extend by a named semantic operation and transport | Inferring all-provider compatibility from discovery | E-34–36 identify which paths have local tests, desktop OpenD evidence and hosted qualification outstanding. | Qualify each proposed binding under R-GW and each host under R3/R4. Refuse unknown operations. |
| ADR-10 | Project discovered capabilities through the existing OS skill. Trading owns schemas, observer access, research jobs and guard. | Forked browser tools, research formulas in instructions or a skill-specific account | Use `agentic-design-system` controls, `agentic-base` record/activity views and `agentic-sheets` research workbooks. Reuse their existing contracts and extend the owning component for any missing primitive. |

## Reference implementation — MVP

### Smallest validated slice (S1 native extension)

The baseline proved one discoverable descriptor + one `SKILL.md`, read offline at zero model-token cost.
E-19's later 8169-byte install/discovery/load evidence is **pre-gateway**, not new-candidate acceptance.
OS's revised six-section 8170-byte gateway-consumer skill passed targeted install/load checks at E-22; E-23 records final affected validation.
Trading owns domain admission, policy and ledger. Local HTTP/MCP parity and selected outbound mappings have fixture evidence (E-34–36). The hosted moomoo read is the next N3 qualification.
S1 answers "can one instruction package be discovered and validated?", not gateway compatibility, host/connected readiness or demand.
No new OS runtime, registry, repo or deployment. Handbook 3.1–9 and independent S2/S3 gates remain intact.

### Criterion-to-evidence joins (baseline only; not current candidate acceptance)

| Criterion | VCC | Evidence | Local rung | Delivered rung | Gap |
|---|---|---|---|---|---|
| Descriptor discovery | VCC-01 | E-11/12 | runtime-ready | undocumented | Human TTV open |
| Package load and validation | VCC-02 | E-11/12 | runtime-ready | undocumented | Hosted delivery open |
| Neutral S1 instructions and read authority | VCC-03 | E-11/12 | dev-proven | undocumented | Pure operation gated separately under VCC-04 |
| One invocation identity | VCC-05 | E-11/12 | runtime-ready | undocumented | Second consumer open |
| Ownership and extraction | VCC-06/07 | E-07/11/13 (historical), E-17/18 (current owner reports) | dev-proven (baseline) | undocumented | Native ownership corrected; candidate checks, per-host qualification and compatible callers open |
| Evidence-derived status | VCC-08 | E-10–13 | dev-proven | undocumented | Demand and deployment open |

### Demo Skeleton (S1, time-boxed ≤ 10 min total)

**Full laboratory acceptance demo (target).** A human opens the desk, an agent selects a perpetual market and studies, and a second device follows the restricted observer view. Inspect completed bars, book and tape. Run a dated hypothesis on documented research capital, poll and overlay the result, then explain a blocked hypothesis. Repeat for cache provenance and verify the same account revision. Separately approve one paper order, replay its key and reconcile exactly one fill. Record the user’s time to reproduce the result and whether they would pay $1 for the report.

| Beat | Bound | Action | Anchor |
|---|---|---|---|
| Hook | ≤ 1 min | "One trading skill, owned once, reused everywhere" | P1 |
| Probe | ≤ 2 min | Open the centralized catalog offline; show one descriptor with exact pin | VCC-01 |
| Reveal | ≤ 2 min | Portable-skills check validates the matching `SKILL.md`; zero token cost | VCC-02 (Reveal = VCC) |
| [domain action] | ≤ 3 min | Invoke the skill's read-only discovery route through the existing Invocation Register | VCC-05 |
| Close | ≤ 2 min | Identify the OS instruction, shared Gateway connector and Trading admission owners. Show the tested local mappings and the remaining hosted qualification. | VCC-07/13 |

`[domain action]` is the product's own discovery invocation; no device or channel is hardcoded.

### Roadmap

| Phase / outcome | Pain evidence / rank | Reuse / new delta / owner | Prerequisite / exit VCC | Bounds / wait | Stop, recovery / next check |
|---|---|---|---|---|---|
| S1 native instructions + descriptor | P1/P2 | OS owner updates same six-section `skills/trading/SKILL.md`, existing digest and portable tests only | Baseline E-11/12; E-19/20 pre-gateway. E-22 revised count/hash/install/load pass; final affected validation at E-23 | Explicit offline target, zero runtime dependencies/model tokens, ≤8191 bytes | No new runtime/registry; skills and third-party instruction clients remain consumers only. |
| S2 independent adoption | P1 | Independently named second product pins reviewed descriptor/package | Named owner, compatible interface and working independent-consumer receipt | Not unlocked by R-GW or R1–R4 | Multiple roles/transports in Trading do not satisfy this gate. |
| S3 shared pure operation | P1/P3 (needs two callers) | Future effect-free operation/export only after compatible contracts | Two concrete compatible callers; VCC-04/06 independent of gateway/host qualification | Deferred; no module now | Retain-local without evidence; Trading gateway/policy/ledger/mappings never migrate by implication. |
| R-GW gateway conformance | Portability/safety target | Trading-owned canonical API/MCP admission (inbound implemented-local) and independently pinned outbound REST/MCP mappings | VCC-13, E-34–36 and R-GW. Repeat positive, refusal and expiry on each proposed binding. | Inbound parity and selected outbound REST/MCP mappings pass local fixtures (Product E-55–57). Hosted provider qualification is pending per operation and host. | Separate from package/host/connected; G9 outbound clients are not a gateway. Handbook 3.1–9 audit (Product E-43) recorded MOCK-only wiring, superseded by E-44's signed-grant admission and local paper transport; Graph MainPanel Integrations centralization landed via Graph PR #2049 (Product E-49), connected wiring pending. |
| R1 native source review | Safety/portability, not demand | OS owns reviewed instruction bytes/catalog; Trading owns gateway/mapping contract | VCC-07/09; inventory, actual producer/candidate digests, rights/runtime review | No provider effect | Unknown rights/runtime/cost blocks; no provider endpoints/copied instructions in native contract. |
| R2 native archive qualification | Package integrity | Existing Trading packager + inspector with review JSON; no new packager | VCC-09; approved Python environment, reviewed native ZIP and negative cases | Default interpreter lacks optional deps; gate, not success promise | Re-estimate after 90 active minutes; no install/upload; never fake a candidate Git pin. |
| R3 actual host qualification | Desktop/Cloud independence | Authorized native host binding; inbound auth and independent outbound mapping admission; immutable Cloud acceptance where used | VCC-10; exact bytes, fresh session, harmless admitted gateway read once available | Separate rights/cost/auth/upload authority; no ETA | npm install and E-21 direct smoke insufficient; no CLI prerequisite; restore binding on drift. |
| R4 joined qualification | Reproducible independent roles | Product signed reads, SQLite ledger and single guard; real dispatch/scheduler/child fetch remain gaps | R-GW plus VCC-11/12 and RT rows; EV-01–04, signed/redacted events and rollback | Bounded coordinator; optional channel; no activation here | Connected UNQUALIFIED; read-only/mock until qualified, preserving account isolation, ledger and uncertainty. |

### Native consumer implementation roadmap

A desk operator needs to decide whether a saved quote is fresh enough to explain a ticket. Start with one instrument and one named host. The product plan owns the provider inventory, operation dispositions and transport qualification. The steps below specify what a person or native client can verify. [Product integration roadmap](./prd-tad-adr-mvp-gtm-agentic-trading.md#moomoo-integration-roadmap)

| Step and owner | Action | Acceptance evidence |
|---|---|---|
| N1 · OS maintainer | From a pinned OS checkout run `/skill.discover #read-only @skill:trading` and `/skill.load #read-only @skill:trading`. Resolve the existing descriptor. OS’s stdio MCP interface routes harness operations. Trading’s API/MCP handles product operations. | Match the loaded content digest and `authority:false`. The slash verb, selector and tag may select a skill. Only Trading can admit a typed operation against a grant. Check an unknown selector and a missing grant. [OS instruction](https://github.com/huijoohwee/agentic-os/blob/1b7f3726fd250127d93d8a0ccaa08ae356974385/skills/trading/SKILL.md) |
| N2 · Trading and Graph maintainers | Start offline with the E-32 synthetic observation, E-34 signed ticker and E-35 earnings calendar. Separately run `npm run quote:moomoo -- replay HK.00700 qualification/moomoo/sdk-replay.json` in Trading. | Explain instrument, asserted currency, source and capture time, delay and retention expiry for each supported receipt. Preserve unknowns and independent null bid/ask. The OpenD snapshot has a binary-double price, unknown currency and delay. Its provider display supplies no ledger identity or per-quote Nasdaq Basic attribution. [OpenD qualification](https://github.com/huijoohwee/agentic-trading-platform/blob/afb60fbbc966010767adf5ac8e201d3bea06e214/qualification/moomoo/README.md) |
| N3 · Trading operator and host owner | Bind the named moomoo MCP service using that host’s OAuth and reviewed read-only descriptor. Trading checks `quote:read`, the signed grant, symbol rights and $0 budget. Use one semantic `read.ticker` for a single entitled symbol. | Reserve discovery calls and one business read. Replay the same request at the second inbound surface. Both results must have one request ID, observation and ledger revision. Expired grants, tool drift and absent entitlements surface a refusal. Keep credentials with the host. Retry when the missing binding or rights receipt is supplied. [Hosted setup](https://open.moomoo.com/mcp-docs/quick-start) · [Scopes](https://open.moomoo.com/mcp-docs/authentication) |
| N2 expansion / N4 · Trading integration owner | Consume Trading’s family inventory and evidence per transport. Present REST-only calendar dates, sessions and null estimates faithfully. Distinguish private account reads, watchlist maintenance, market subscriptions and simulation. | An absent MCP tool stays unavailable on that route. Scope `trade:read` to the account alias and `quote:write` to the approved watchlist task. Label stale or disconnected streams. In a separate paper rehearsal require simulator identity, independent veto and reconciliation. Live securities/crypto orders and transfers are excluded from this release. [Coverage register](https://github.com/huijoohwee/agentic-trading-platform/blob/afb60fbbc966010767adf5ac8e201d3bea06e214/src/provider-coverage.mjs) |
| N5 · Browser and Graph owners | Import the signed ticker under MainPanel → Integrations. Project the same admitted action in WebMCP when available. Provide the visible read-only action on other browsers. Distinguish available operations from the current grant. | Verify the independently trusted signer, provider, mapping, candidate and expiry. Reopen a rights-permitted result on a primed offline desktop with zero host requests. Reject tampering or wrong signer and purge at expiry and cold reopen. Remove the WebMCP action on navigation. A physical-phone replay remains deferred. |
| N6 · OS package and host owners | R1 checks source and digest. R2 inspects one portable skill in the ZIP. R3 loads it in fresh Desktop and Cloud sessions independently. R4 joins the host receipt to the exact Trading and Gateway candidates, grant, result and policy. | Record host version, installed digest, granted scope, positive read and denial after expiry separately for each host. Revoke the binding and restore the previous reviewed pin on drift. OS's 8,177-byte instruction has an 8,191-byte ceiling. Load provider references on demand. |
| N7 · Product owner | When the human trial reopens, give one uncoached desk operator the saved ticket. Ask them to identify its age and reopen a permitted quote in ≤10 minutes. Offer the $1 walkthrough only when the buyer pilot resumes. | Record elapsed time, failures and buyer response separately. Both human gates remain deferred. S2 still requires named independent adoption and S3 requires two compatible callers. |

**Host handoff.** Record the host and version, instruction digest, Trading candidate, Gateway pin, mapping/schema digests, scope, private alias reference, source and observation times, precision, rights expiry, result digest or refusal, ledger revision and predecessor binding. Keep private market data within its retention grant. Refresh discovery when a descriptor changes. Re-run the fixture before seeking a new external observation.

**Packaging for R2.** From Trading, use the reviewed OS checkout, revision, independent review manifest and a fresh output directory. E-46's historical archive baseline is OS `a5d8f7a`. For a new candidate, verify the manifest's exact producer, file inventory, dependencies and any relocation edits. Require the approved local PyYAML and markdown-it-py parsers and retain their inspection result.

```sh
git -C "$OS" archive --format=zip --output="$OUT/native-trading-source.zip" "$OS_REV" skills/trading
python3 scripts/package-skill.py --source "$OUT/native-trading-source.zip" --review "$REVIEW" --output "$OUT/trading.zip"
python3 scripts/inspect-skill.py "$OUT/trading.zip"
shasum -a 256 "$OUT/native-trading-source.zip" "$OUT/trading.zip" "$OUT/trading.zip.manifest.json"
```

**Release evidence.** Local affected checks in Trading include `npm run check`, `check:runtime`, `check:browser`, `check:runtime-browser` and `package:replay` via npm scripts. R1 uses the OS portable skill test and offline discover/load. R3 needs executing-host readback. Source integration, Dev/Prod deployment, predecessor rollback and commercial acceptance have separate owners and receipts.

## Reference implementation — GTM

### Buyer hypothesis and experiments (all unvalidated)

Buyer hypothesis: an integrator/maintainer of a second agentic product values a centralized,
provider-neutral trading skill enough to adopt and pin it. No payment, demand, or revenue is claimed.

| ID | Hypothesis | Cheapest test | Threshold | Window | Stop / revisit |
|---|---|---|---|---|---|
| H1 | A second product will consume a centralized descriptor | name one concrete second consumer; admit its pin | one named consumer with compatible contract | discovery → S2 | no consumer → retain-local |
| H2 | Reuse reduces integration time / failed actions | measure before/after on the same buyer journey | measurable reduction (value unknown) | S2 → S3 | no reduction → reconsider extraction |
| H3 | Integrators will pay for maintained trading skills | interview / pre-order signal (no charge) | explicit WTP signal | post-S3 | no signal → monetization stays deferred |

### Monetization

`mechanism-proven`: not applicable yet (no payment mechanism built). `demand-validated`: unvalidated
(no experiment result). **Monetization is explicitly deferred.** Recognized revenue and collected
payment are both $0 and unclaimed. Stream ordering by distance to a real first dollar: (1) maintained
skill subscription, (2) integration support — both hypothetical, neither validated. Under the $0/FOSS
scope, unknown fees, sponsorship, or paid infrastructure cannot silently enter the MVP; sponsored
credits require terms confirmation and remain unclaimed.

### Economics

Unit economics, TCO per deployment model, and cash timing are **unknown** and labelled unknown. No
serving-token cost is incurred at S1 (offline, zero token). The Financial Model ADLC Cost Ledger
consumes execution receipts by exact reference; E-11/12 record engineering outcomes. Revenue, collected cash and human time savings remain unmeasured. Utility counts, shared imports and passing checks prove neither payment, demand nor revenue.

## Reference implementation — coverage and evidence

### C01–C16 coverage record

| ID | Domain | Disposition | Evidence / reason | Owner | Revisit |
|---|---|---|---|---|---|
| C01 | Purpose, customer, pain | covered | PRD vision + P1–P3 (unvalidated) | Product | MVP acceptance |
| C02 | Market and timing | deferred | no sizing yet; hypothesis only; two methods pending | GTM | H1 result |
| C03 | Offer and alternatives | covered | offer = centralized skill; alternatives = fork/copy/retain-local (ADR-01/04) | Product+ADR | S2 |
| C04 | Product and experience | covered | journeys D1, Must stories, offline reach, TTV row, VCCs | Product | Phase 3 |
| C05 | Architecture and data | covered | TAD owners, flows D1–D4, dependency direction, boundaries | TAD | S3 |
| C06 | Quality, security, AI | covered | failure cases, secrets excluded, purity, fallback, license/quota | TAD | S3 |
| C07 | Decisions and tradeoffs | covered | ADR-01–09 with alternatives/consequences/recovery; universal target vs implemented gateway separated | ADR | material change |
| C08 | Smallest validated slice | covered | MVP S1 + criterion-to-evidence + demo skeleton | MVP | acceptance |
| C09 | Acquisition–retention | deferred | channel/activation unvalidated; H1–H3 defined | GTM | H1/H2 |
| C10 | Business operations | deferred | support/incident process not yet needed at S1 | TAD+GTM | S2 |
| C11 | Organization and obligations | covered | one native instruction owner; package rights and documented provider-interface/data terms; no entity/IP change | TAD+ADR | adoption |
| C12 | Financial viability | deferred | economics unknown; $0 scope; no statements yet | GTM+TAD | H3 |
| C13 | Capital and milestones | not-applicable | bootstrap $0/FOSS; no funding ask; reviewer: Product | GTM+ADR | if funding sought |
| C14 | ADLC execution | covered | Historical S1 integration E-11/12 is separate from native lanes E-18; Product E-49/E-50 record landed Graph/Trading integration and the provider-mapping registry landing. This 0.16.0 draft updates the admitted authoring lane. Hosted delivery remains unqualified. | ADLC | current validation/handoff |
| C15 | Audience projections | deferred | deck/BP/FM not needed for an integrator decision yet | Venture | audience handoff |
| C16 | Learning and next increment | covered | N1 landed (E-50); N2–N7 roadmap toward full moomoo OpenAPI coverage; separate R-GW conformance, R1–R4 package/host/run and S1→S3 adoption gates; risk register/stop thresholds | MVP+GTM | each increment |

Counts: dispositioned **16 / 16**; covered **10** (C01, C03, C04, C05, C06, C07, C08, C11, C14, C16);
deferred **5** (C02, C09, C10, C12, C15); not-applicable **1** (C13). Covered applicable domains:
**10 / 15** (C13 not applicable). Each deferral carries a reason, dependency, owner, and revisit trigger;
C13 inapplicability carries a rationale and reviewer (Product).

### Evidence register

E-01–30 refer to earlier candidates. E-31 verifies the current audit-lane source and portable package locally.

| ID | Kind | Source / identity | State |
|---|---|---|---|
| E-01 | grounding | G1/G2 `agentic-os@abcbfc6` skills + catalog manifests | observed |
| E-02 | grounding | G1/G3/G8 `SKILL.md` shape + `portable-skills` contract test | observed |
| E-03 | grounding | G5 neutrality guideline @ `f07f1a3c` | observed |
| E-04 | pattern | G4 Functions portable-call pattern (not native proof) | documented; deferred S3 |
| E-05 | grounding | G2 `catalog/invocation.json` entryCount 36 | observed |
| E-06 | gate | G4 S2/S3 reuse gates | gated; unsatisfied |
| E-07 | historical grounding | Original domain ownership and external-source review | Historical only; current native ownership supersedes external dependencies under G6/G7 and ADR-04. |
| E-08 | self | this specification's status honesty | covered |
| E-09–10 | Historical OS package and suite | Offline install/load was exercised. A full run timed out after 220 passing suites. | Partial suite result. |
| E-11–14 | Native source release and offline rehearsal | OS PR #708 at `11c8fde` exported the 3,346-byte skill. Discovery and load returned the reviewed digest offline. Trading separately exposed product entry points. | Local release baseline. |
| E-15–18 | Earlier runtime and authoring lanes | Trading `0d5a4db` and `173e71f` grounded package, host and gateway requirements. The prior START receipts identify those candidates. | Historical authoring and source context. |
| E-19–23 | Pre-gateway validation and native revision | E-19/20 concern an 8,169-byte candidate. E-21 was a direct Desktop diagnostic. E-22 reviewed 8,170 bytes, and E-23 records its final affected suite and retry. | Runtime access and deployment remained separate gates. |
| E-24–27 | Product source, CLI observation and parity requirements | Product E-42–45 record the local inbound gateway, historical diagnostic, signed admission, local paper transport, roles/consent and the parity target. | Product-local scope. |
| E-28 | Native desk source and package | Reviewed candidate `72218f2` and release `a5d8f7a` establish the synthetic-consumer baseline. | Host acceptance open. |
| E-29 | Graph and Trading source integration | Graph #2049 and Trading #4 landed setup metadata and operation-shaped reads. | Discoverable local contracts. |
| E-30 | Provider definition registry | Trading #5 at `58d46ff` completed N1 (Product E-50). | No per-operation connected receipt. |
| E-31 | Historical OS audit worktree, 23 November 2026 | `device-0232231d4a19--mcp-integration-audit` at `f5cca6b1cd0d7bd16a0dd57abba35996262c481f` recorded the harness, invocation catalog and native skill before the lane was retired. The 8,177-byte instruction matched catalog SHA-256 `5a10ce4fb2af9382569c8c53eb2534491fcdf054ff2932a6f9e0dcf15a32ec5c`. The portable skill suite passed 1/1 locally. | Reused for source review and offline verification. Paired drafts belong to `device-0232231d4a19--moomoo-integration-roadmap`. Host qualification is open. |
| E-32 | Synthetic ticker consumer, 23 November 2026 | Trading `bc0e7ce` returned matching HTTP/MCP results on one request, revision 2. Graph `8ba385196` reopened digest `d2961deca48422bee134b87110f2c2c85cf61a62c3a1b85496c13e4cb4666b46` offline at 360 × 780 after tab closure, with zero host requests. A tampered price left the saved receipt intact. | The OS audit at `f5cca6b` passed 24/24 portable and MCP checks. Executing-host qualification, provider rights and the physical-phone exercise are open. [Product evidence](./prd-tad-adr-mvp-gtm-agentic-trading.md#moomoo-integration-roadmap) · [Local verification record](/Users/huijoohwee/Documents/GitHub/.workspace/.artifacts/trading-ticker-fixture/20261123-8ba385196/verification.json) |
| E-33 | Live dashboard and read-only qualification, 23 November 2026 | On Trading `70e37de`, the 300 s R01 pass became a 301 s failure and saved as revision 1. Browser discovery exposed desk actions. Run B reopened offline with 26 synthetic events. An older journal lacked the toolbar until reopened in a new tab. The localhost alias fell back to sealed replay and the toolbar overlapped the replay heading. | Trading HTTP/MCP agreed on synthetic digest `508d452e90132668e374c769c904c924c4c932ca12a48629c91d4926e4c7ff23`, revision 2. Graph restored it offline on desktop with zero host requests. The unbound gateway refused both transports with `UNQUALIFIED`. Provider quote calls: 0. Physical-phone handoff deferred. [Verification record](/Users/huijoohwee/Documents/GitHub/.workspace/.artifacts/trading-ticker-fixture/20261123-qualification-oabHwF/verification.json) · [Dashboard capture](/Users/huijoohwee/Documents/GitHub/.workspace/.artifacts/trading-dashboard-ui/replay-dashboard-70e37de.jpg) |
| E-34 | Trusted `read.ticker` receipt, 23 November 2026 (Product E-55) | Trading `78d4fec` made one conformance quote dispatch. HTTP and MCP returned the same request, result and ledger revision 2. Graph `209f2e04f` verified the 830-byte Ed25519 receipt. Desktop Chrome reopened it via the service worker with zero host requests and the exact decimal price. | Graph refused a changed price, purged expired provider data while open and on cold reopen, and preserved the separate synthetic receipt. The run used zero live moomoo calls. Phone handoff deferred. [Provider receipt tests](https://github.com/huijoohwee/agentic-graph/blob/209f2e04f2294ddf3a6a5fb23a93ffcddb446b60/canvas/src/__tests__/tradingProviderTickerReceipt.test.ts) · [Desktop verification](/Users/huijoohwee/Documents/GitHub/.workspace/.artifacts/trading-ticker-fixture/20261123-provider-npcLi9/verification.json) |
| E-35 | REST-only calendar consumer and coverage inventory, 23 November 2026 (Product E-56) | Trading `4db0b21` admitted REST protocol `1.0` and mapped `read.calendar`; the loopback gateway returned three synthetic rows (null EPS preserved) and refused an over-window request. Graph `33c955a4e` replays the 532-byte receipt under MainPanel → Integrations, re-verifies its SHA-256 in browser and restores it after reload. The 25-family inventory (305 sources) renders in both surfaces. | Live Chrome on desktop, 360 px and 390 px showed no overflow and zero non-loopback requests; live moomoo calls numbered zero. Connected reads still require N3 operator receipts; the inventory states mapping readiness, not connected readiness. [Calendar fixture tests](https://github.com/huijoohwee/agentic-trading-platform/blob/4db0b21d45c07cc89dead27d2dea13cacf7514bb/test/runtime-calendar-fixture.test.mjs) · [Graph receipt tests](https://github.com/huijoohwee/agentic-graph/blob/33c955a4e24d62b4fbd7323d52c689037320ef9a/canvas/src/__tests__/tradingCalendarReceipt.test.ts) |
| E-36 | Connector and consumer review, 24 November 2026 (Product E-57) | The Trading owner pins Gateway `563dab2`. Selected Trading fixtures passed 41 tests and Gateway connectors passed five. Existing local qualification records HK and US single-symbol OpenD display reads. | Hosted MCP was unavailable in this review. The desktop OpenD evidence, signed conformance ticker and REST calendar each qualify only the documented path. The next external test is N3. [Trading baseline](https://github.com/huijoohwee/agentic-trading-platform/blob/afb60fbbc966010767adf5ac8e201d3bea06e214/qualification/moomoo/README.md) · [Gateway profile](https://github.com/huijoohwee/agentic-gateway/blob/563dab262dd6a7debd8d4e643505ec64666893e0/connectors/profiles.json) |

[Previous Trading owner edition](https://github.com/huijoohwee/agentic-trading-platform/blob/afb60fbbc966010767adf5ac8e201d3bea06e214/undocumented-draft/prd-tad-adr-mvp-gtm-agentic-trading-skills.md) preserves the earlier owner text. The prior register retains exact commands, hashes, skipped tests, owner-supplied observations and historical lane dispositions for E-01–29. Product E-50 holds the N1 release evidence. [Archived skills register](https://github.com/huijoohwee/joohwee/blob/4bad2d7e0c0ce4cb753a108f62176fdb19d4d567/undocumented-draft/prd-tad-adr-mvp-gtm-agentic-trading-skills.md#evidence-register) · [Audited native instruction](https://github.com/huijoohwee/agentic-os/blob/f5cca6b1cd0d7bd16a0dd57abba35996262c481f/skills/trading/SKILL.md)

### Risk register

| Risk | Likelihood | Impact | Mitigation | Owner |
|---|---|---|---|---|
| No second consumer materializes | medium | extraction wasted | gate S2/S3; retain-local default | Product |
| Provider interface/auth drifts per host | medium | stale mapping or privilege mismatch | Trading-owned provider/adapter/schema/mapping pins; independent operation/environment/scope/rights/freshness/quota/$0 admission; no silent fallback | TAD |
| Universal gateway mistaken for implemented compatibility | high | bypass or unsupported execution | Disclose operation, transport, host and evidence type. Product E-55–57 record local coverage and N3 specifies hosted evidence. | TAD |
| Domain policy leaks into core | medium | portability lost | purity contract; dependency direction | TAD |
| Second registry created | low | duplicate-owner | extend `invocation.json` only | TAD |
| Overclaimed readiness | medium | unproven-claim | evidence-derived rungs; proposed labels | Product |

### Historical planning record (`AGENTIC-TRADING-SKILLS-001@0.8.0`)

| PRD-TAD-ADR-MVP-GTM | CID | RAO | Updated Date |
|---|---|---|---|
| PRD | Context: inbound gateway implemented-local (Product E-42/E-44), connected UNQUALIFIED, parity workspace specified (Product E-45); Intent: OS instruction consumers, Trading authority; Directive: VCC-01–14 | Role: Product; Action: neutralize provider coupling and specify parity consumer guidance; Outcome: discovery never authorizes, universal not proven compatibility, parity a specified target | 2026-11-21 |
| TAD | Context: G9 outbound clients plus implemented-local inbound gateway; Intent: canonical API/MCP admission with independent REST/MCP mappings; Directive: G1–G9, handbook 3.1–9 | Role: TAD; Action: specify pins/refusals/isolation and separate R-GW; Outcome: no new OS runtime/registry, passthrough or mandatory CLI | 2026-11-21 |
| ADR | Context: consumer vs authority boundary; Intent: one OS instruction/catalog owner, Trading gateway/policy/ledger/mappings owner; Directive: ADR-01–09 | Role: ADR; Action: preserve signed veto/single guard and uncertainty; Outcome: product-local rule and explicit re-admission | 2026-11-21 |
| MVP | Context: E-19/20 pre-gateway, E-22 native pass, E-23 final validation, E-24/26 inbound gateway + local paper transport implemented-local, E-27 parity review, Python gate; Intent: bounded honest qualification; Directive: R-GW, R1–R4, EV-01–04, independent S2/S3 | Role: MVP; Action: separate conformance/package/host/connected evidence; Outcome: inbound parity implemented-local; outbound mapping/connected tests and parity implementation not claimed | 2026-11-21 |
| GTM | Context: buyer hypothesis; Intent: learn before extraction; Directive: H1–H3, monetization deferred | Role: GTM; Action: seek a timed named independent adoption; Outcome: demand and cash remain open | 2026-11-21 |

### Git handoff and provenance

**Historical 0.8.0 handoff.** The original lane, candidate pins and receipt boundaries remain recorded in the 0.8.0 revision of this document at Trading `94ee095`. E-19–27 retain the historical validation results.

**0.16.0 handoff.** Start from the E-34 signed ticker and E-35 REST calendar. Use E-36 to explain the bounded OpenD evidence and N3 to qualify the first hosted quote through Trading’s ledger. Record the resulting operation, host and expiry before expanding coverage. [Product roadmap](./prd-tad-adr-mvp-gtm-agentic-trading.md#moomoo-integration-roadmap)
