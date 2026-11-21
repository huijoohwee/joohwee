---
title: "Reference implementation: Agentic Trading Skills"
doc_type: "PRD-TAD-ADR-MVP-GTM"
version: "0.2.0"
date: "2026-11-20"
lang: "en-US"
frontmatter_contract: "required"
owner: "Product function"
continuity_id: "AGENTIC-TRADING-SKILLS-001"
prd_revision: "0.2.0"
tad_revision: "0.2.0"
adr_revision: "0.2.0"
mvp_revision: "0.2.0"
gtm_revision: "0.2.0"
local_rung: "dev-proven"
delivered_rung: "undocumented"
lane: "authoring"
universal_scope: false
worktree_id: "device-0232231d4a19--trading-runtime-readiness"
agent_id: "qoder"
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
  - "AGENTIC-TRADING-HYBRID-001@0.6.0"
---

# Reference implementation: Agentic Trading Skills

One joined specification at `AGENTIC-TRADING-SKILLS-001@0.2.0`. The job: make a reusable,
domain-agnostic agentic trading capability **discoverable and invocable across products from one
centralized owner**, without forking provider skills, duplicating trading policy, or creating a second
execution registry. This document is a labelled reference implementation; the portable contract it
specifies is domain-agnostic. No provider brand is named or copied in native artifacts; the upstream
reference is held only in private operator evidence.

**Release status, 20 November 2026.** The two S1 CLI routes are runtime-ready only for local, read-only discovery and loading; E-14 rechecked the 3,346-byte entrypoint and its existing digest. This 0.2.0 revision adds the provider-adapter, packaging, role and qualification contract for handbook **3.1–9** in [Trading 0.6.0](./prd-tad-adr-mvp-gtm-agentic-trading.md). It does not implement, install, upload or authorize those capabilities. The plan remains `dev-proven` locally and `undocumented` for delivery; connected event runtime is **NOT READY**. Native S1, official provider skills and Cloud runtime bindings are three different artifacts. Neither a loaded Markdown skill nor a Cloud ZIP acceptance grants trading authority.

## Decision record (ranked next outcome)

| Field | Value |
|---|---|
| Next outcome | Qualify the selected event skills and runtime bindings for `agentic-trading-platform` through R1–R4 below; keep S1 unchanged. H1 remains a separate second-product experiment. |
| Riskiest uncertainty | Whether each selected upstream skill can run with the admitted runtime, least privilege and $0 boundary in both Desktop and Cloud; a portable descriptor cannot answer this. Demand for consolidation remains unvalidated. |
| Cheapest sufficient test | Inventory exact skill bytes and required runtime without running them; validate one selected ZIP locally, then obtain separately authorized Cloud acceptance and a harmless read-only execution receipt. |
| Threshold / window | S1 route checks pass (E-11/12/14). Event R1–R4 need actual environment-specific evidence; S2 still requires a named consumer and S3 two compatible callers. |
| Stop / revisit | Stop extraction if no second consumer is named (retain-local); revisit at discovery, baseline, MVP acceptance, audience handoff. |
| Bounds | Active time ≤ 4 h; one Markdown file < 600 lines and ≤ 90 KiB; zero new runtime modules at S1; token spend $0; no deployment; FOSS-only. |

## Reference implementation — PRD

### Vision, user, and job

Make reusable trading capability a **shared, headless, invocable asset** owned once and consumed by
many products. The immediate user is an **integrator/maintainer** of a second agentic product who
needs trading capability without re-implementing or forking it. The beneficiary is the end operator
who gets consistent, provider-neutral behavior across products.

### Pain-point-to-feature mapping (all `unvalidated`)

| Pain | Hook | Break | Fix | Close | Min-time-resource-max-value |
|---|---|---|---|---|---|
| P1 Duplicated trading logic drifts across products (`unvalidated`) | "Reuse one trading skill everywhere" | Each product re-implements signals/risk; behavior drifts; no single owner | Centralized descriptor + gated shared operation in existing `agentic-os` seams | One pinned capability identity, two-caller-proven before extraction | Reuse existing `skills/`, `catalog/`, `runtime/` seams; build only one descriptor + package at S1 |
| P2 Provider skills forked or vendored lose upstream fixes (`unvalidated`) | "Stay current with the provider" | Forks diverge; upgrades break; vendor lock-in | External exact-pin reference to upstream provider skills; no fork | Pinned upstream revision; neutrality preserved | Reuse upstream pin; build a reference block, not a copy |
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
| PRD-SKL-04 | Must | As an owner I can confirm provider skills stay external and trading policy stays local | VCC-07 |
| PRD-SKL-05 | Should | As a second consumer I can pin a shared pure operation once two compatible callers exist | VCC-06 (gated S3) |
| PRD-SKL-06 | Won't (this increment) | Extract all trading domain logic into the shared core | Retain-local per ADR-03 |
| PRD-SKL-07 | Must (event runtime) | As the operator I can trace each selected skill from upstream bytes through package acceptance to a tested, exact environment-specific binding | VCC-09/10; R1–R3 |
| PRD-SKL-08 | Must (event runtime) | As the reviewer I can reproduce pinned delegation, independent veto, safe refusal and rollback without giving an agent direct broker-write authority | VCC-11/12; R4 |

### Success metrics and Time-to-Value

| Metric | Target (estimate, unvalidated) | Method |
|---|---|---|
| TTV (integrator) | ≤ 10 min from opening the catalog to discovering and invoking one pinned skill capability offline | Clean-environment local rehearsal; zero token cost; no auth |
| Discovery cost | 0 tokens / $0 per read | Offline catalog read; metadata-first |
| Duplicate owners | 0 new registries; one capability identity | Invocation Register join check |
| Drift after reuse | Unknown — measure failed/repeated actions before/after | GTM experiment H2; not yet measured |

The release harness completed its canonical route check in 0.277 s. Human setup, discovery and verification time still need a timed integrator session (E-12).

### Verification conditions (VCCs)

| VCC | Condition | Evidence Reference | State |
|---|---|---|---|
| VCC-01 | Offline discovery returns a stable ID, owner, description, source and SHA-256. | E-11/12, `/skill.discover` | Passed with zero model tokens and zero estimated cost. |
| VCC-02 | The installed export resolves, the descriptor matches the YAML, and loading checks the exact entrypoint bytes. The standalone skill resolves its resources. | E-11/12, portable skills contract | Passed after packing and installing offline. Unknown IDs, changed bytes and missing files each produced the expected error. |
| VCC-03 | The portable descriptor and instructions are provider-neutral and headless. Reading either grants no effects. | E-11/12, descriptor and entrypoint inspection | Verified for S1. The routes return `authority: false`. |
| VCC-04 | Shared operation is effect-free (no I/O/model/DOM/global state), typed input/output, bounded, deterministic digest | E-04 (G4), check `purity-contract` | deferred to S3; not run |
| VCC-05 | The command, read-only semantic and skill binding resolve one identity through the existing Invocation Register. | E-11/12, invocation and portable-package checks | Passed for discovery and load. |
| VCC-06 | Extraction deferred until two concrete consumers with compatible contracts (S3); second-product adoption requires a named consumer and a verified pin (S2) | E-06 (G4), check `reuse-gate` | gated; not satisfied |
| VCC-07 | Provider skills retain their upstream owner and exact pin. Trading policy stays in the product. | E-07/11/13 | Native release and policy ownership verified. The provider pin and rights require independent private verification before use. |
| VCC-08 | Local runtime evidence, source integration, hosted delivery and demand carry separate status. | E-10–14 | Earlier interrupted validation is history; E-11/12/14 establish only local S1. |
| VCC-09 | For each selected upstream skill, inspect exact revision, runtime/dependency closure and rights; validate one ZIP's compressed/expanded bounds, strict YAML/name, included links and preserved safety text. Reject traversal, symlinks, duplicate members, missing resources and secrets. | R1/R2; E-15 | Existing local inspector is a starting seam, not proof of all negative cases. Actual provider archives pending. |
| VCC-10 | Retrieve actual Cloud `skill_id` and immutable version/content, bind it to the executing Agent, and complete a harmless permitted read with the correct runtime/auth in a clean Session. Missing runtime, Vault, CLI login or scope yields a typed failure with no fallback. | R3; Trading RT-02/04/05 | Pending; no upload or provider execution occurred. |
| VCC-11 | Coordinator explicitly delegates; pinned child outputs join by immutable input/policy/account binding. Independent authenticated risk can veto; forged files, stale verdicts and direct execution bypass fail the external guard. | R4; Trading VCC-25/34 | Pending; independent conversations alone do not provide enforcement. |
| VCC-12 | Before/after configuration and effective hashes match intended edits; fixed four-prompt evaluation, new Session snapshots, per-Thread events, resource digests and restore of the predecessor are retained. | R4; Trading VCC-26/33 | Pending; current fixture version strings are not provider provenance. |

## Reference implementation — TAD

### Codebase Grounding Record (observed)

| ID | Input | Exact source / revision | Inspected fact | Disposition |
|---|---|---|---|---|
| G1 | Skill package seam | `agentic-os@abcbfc6dc5e9e3c5f4ccb91bd5a7cdfed39408fc:skills/` | `canvas`, `esp-idf`, `software-forensics`, each `SKILL.md` with YAML `name`+`description`; subpath exports `./skills/<name>/SKILL.md` (+ `esp-idf/references/*`) | reuse (existing owner) |
| G2 | Catalog manifests | `agentic-os@abcbfc6:catalog/invocation.json`, `catalog/features.json`, `catalog/composition-source-lock.json` | invocation schema `agentic-os-invocation-catalog/v1`, entryCount 36, digest `sha256:aa9adef3…b5abc5`; features schema `agentic-os-feature-catalog/v1`, profile `fossOnly:true`, `maxIncrementalSpendUsd:0`, `deploymentAllowed:false`, entryCount 5, digest `sha256:17714ee4…25d985`; composition lock artifacts `{blob, owner, path}` | reuse (manifest precedent) |
| G3 | Runtime + admission seams | `agentic-os@abcbfc6:package.json`, `runtime/adapters/` | exports `./agents/skill-registry-gate`, `./agents/skill-proposer` — the **Agent-Definition** proposed→active promotion path (operator-gated, tool allowlists), *not* `SKILL.md` admission; also `./context/*`, `./planning/*`, `./forensics/source-evidence`, `./agent-docs/SKILLS.md`; `runtime/agents/docs/SKILLS.md` schema `agentic-canvas-os-skills/v1`, `publish_policy: Dev-only until explicit operator approval` | reuse (Agent-Definition path; separate from portable skills) |
| G4 | Functions consolidation pattern | `huijoohwee.github.io@f07f1a3c:docs/documents/prd-tad-adr-mvp-gtm-agentic-functions.md` (`AGENTIC-FUNCTIONS-001@0.1.1`) | T3 `catalog/functions.json` discovery gated S2 (named second consumer); T4 `runtime/functions/sum.mjs` + export `agentic-os/functions/sum` gated S3 (two callers); ADR-04 keep existing repos; portable call = ordered 0–512 finite binary64, effect-free. `runtime/functions/` and `catalog/functions.json` **absent** at `abcbfc6` (deferred) | reuse pattern; not native proof |
| G5 | Authoring contracts | `huijoohwee.github.io@f07f1a3c:guidelines/prd-tad-adr-mvp-gtm-guidelines.md` (v3.5.1, blob `392fcda1…`, last commit `fc53dc02…`), `skill-guidelines.md`, `skill-repo-map.md`, `codebase-neutrality-guidelines.md` | < 600 lines/file; frontmatter contract; C01–C16; one owner per capability; configuration-driven repo identification; no path-derived claims; brands only under reference-implementation label | govern (this doc) |
| G6 | Trading domain owner | `AGENTIC-TRADING-HYBRID-001@0.6.0`, Trading `0d5a4dbc` (E-13) | Product owns replay fixtures, account policy and calculations | retain-local |
| G7 | Upstream provider skill hub (reference implementation) | historical adoption evidence is private; the public research candidate below is `ec092d2b4c21868ae285f65d9b30f7adb44f860e`, not an adopted runtime pin | upstream-owned provider skills covering market data, news, sentiment, unusual activity, and paper trading; installed into the executing agent's own skill store via the `skills` CLI; provider CLI/API stay external | external exact-pin; no fork; no brand or copy in native artifacts |
| G8 | Portable skill contract + install/run | `agentic-os@abcbfc6:__tests__/portable-skills.test.mjs`, `package.json` | `npm pack` → offline install → `import.meta.resolve("agentic-os/skills/<name>/SKILL.md")`; `dependencies: {}`; `files` ships `skills/`; each selected resource < 8 KiB; standalone dir distributable; no external relative links; GitHub remote `huijoohwee/agentic-os` enables `skills`-CLI install | reuse (proven installable/runnable seam) |

G1–G3, G5, G8 are observed from inspected checkouts for the original baseline. G4 is a documented pattern, not native
implementation proof. G6 is a sibling specification. G7 is an upstream reference held in private
evidence, not adopted code; native artifacts forbid mentioning or copying it.

### Division of Work — ownership and reuse record

| Capability | Owner | Source / export / revision | Current consumers | Decision | Smallest delta | Named check |
|---|---|---|---|---|---|---|
| Skill package shape | `agentic-os` | `./skills/trading/SKILL.md` at the E-11 release | Installed CLI and standalone skill | reuse | One bounded Markdown entrypoint | `portable-skills` |
| Skill discovery catalog | `agentic-os` | Descriptor on the `@skill:` binding in `catalog/invocation.json` at E-11 | CLI discovery and load | extend-owner | A second product can pin this descriptor when H1 passes | `catalog-read` |
| Shared pure operation | `agentic-os` | new `runtime/trading/<op>.mjs` + export `agentic-os/trading/<op>` | none yet | defer (S3) | one effect-free op, gated on two compatible callers | `purity-contract` |
| Invocation routing | `agentic-os` | `catalog/invocation.json` and `bin/agentic-os-invocation.mjs` at E-11 | Packaged CLI | extend-owner | Two read commands and one selector in the same register | `invocation-join` |
| Portable skill validation | `agentic-os` | `__tests__/portable-skills.test.mjs` at E-11 | Packaged CLI and standalone instructions | reuse | Pack, install offline, resolve, compare metadata and digest, exercise failure paths | `portable-skills` |
| Agent-Definition promotion | `agentic-os` | `./agents/skill-registry-gate`, `./agents/skill-proposer` @ `abcbfc6` | runtime agent definitions | defer (separate path) | none at S1; operator-gated, not `SKILL.md` admission | `skill-registry-gate` |
| Provider trading skills | upstream (reference implementation) | exact pin in private evidence (G7) | executing agent's skill store | retain-local (external pin) | generic reference; no brand/copy in native bytes; no fork | `ownership-seam` |
| Trading domain policy | trading domain owner | `AGENTIC-TRADING-HYBRID-001@0.6.0` | trading product | retain-local | none extracted | `ownership-seam` |

Dependency direction: portable contract → domain owner → adapter → view. Share by declared export or
versioned protocol, never sibling source imports. Secrets, provider SDKs, filesystem access, and effect
authority stay out of browser-safe utilities.

### Invocation Register

| Route | Kind | Capability identity | Mode | Authority | Owner / schema |
|---|---|---|---|---|---|
| `/skill.discover` | command | trading-skill discovery | read-only | none (metadata) | `catalog/invocation.json` |
| `/skill.load` | command | trading-skill package load | read-only | none | `catalog/invocation.json` |
| `#read-only` | semantic | discovery/load posture | read-only | none | `catalog/invocation.json` |
| `@skill:` | binding | select one descriptor | read-only command option | none | `catalog/invocation.json` |
| skill route `skills/<name>/SKILL.md` | skill | one validated package | orchestrate existing commands | no new authority | package export `./skills/<name>/SKILL.md` + `portable-skills` |

Skills orchestrate existing commands and never create a second registry or grant mutation authority.
Provider live-order routes are **unsupported** in this scope (paper-only; live requires explicit
operator intent and confirmation, owned by the trading domain, not this skill core). Discovery and read
routes stay at zero token cost.

### Flow classification (five types)

| Flow type | Applicable? | View / reason |
|---|---|---|
| User journey | yes | D1 — integrator discovers → loads → invokes one capability offline |
| Workflow | yes | D2 — author descriptor → portable-skills check → catalog read → consumer pin |
| Data flow | yes | D3 — descriptor metadata → catalog manifest → consumer; no secret/effect data in core |
| Orchestration / harness | yes | D4 — skill orchestrates existing commands; typed input/output, cost log, fallback, bounded loop |
| Topology | not applicable | no new deployment surface; Deploy Boundary closed; existing lane topology unchanged (reason: S1 adds metadata + one package only) |

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
  S[SKILL.md] -->|typed input| H[harness: existing command]
  H -->|typed output + cost log| S
  H -->|fallback / circuit-breaker| S
```

### Contract, failure, and budgets

- Typed input/output for every operation; emitted cost log; stated fallback; max-iteration bound and
  circuit-breaker on every agentic loop (`unbounded-loop` avoided).
- Failure cases: missing descriptor → typed gap, not silent fallback; invalid package → portable-skills
  rejection; provider unavailable → read-only metadata still resolves, live effect refused.
- Per-feature ceilings: token $0 at S1; iterations ≤ 1 validation pass; wall-clock ≤ 4 h active.
- External seam cost/license/quota/exit: provider skills carry upstream license and reference-use
  restrictions; none are copied into native OS artifacts. Upstream-preserving staging packages require R1 rights acceptance; unknown fees block adoption under $0 scope.

### Install and run mechanics (S1, proven seam)

- **Store**: `skills/trading/SKILL.md` in `agentic-os`; zero runtime dependencies; self-contained
  entrypoint < 8 KiB (any reference resource also < 8 KiB); no external relative links.
- **Install into an environment**: `npm pack` → `npm install --offline <tarball>` →
  `import.meta.resolve("agentic-os/skills/trading/SKILL.md")`; or `npx skills add
  huijoohwee/agentic-os#<rev> -a <agent> -s trading` (GitHub remote, same layout); or copy the skill
  directory standalone. The `portable-skills` contract test proves these resolve without repository or
  SDK dependencies.
- **Run**: the agent reads `SKILL.md` and discovers a market-data/trading capability from the current
  environment's documented interface (the canvas pattern); provider-specific execution stays in an
  environment adapter, never in the skill. With no such capability present, the skill reports the gap
  rather than guessing a provider. The skill defaults to paper rehearsal. A paper effect needs a separate domain grant. Live placement is outside this skill.
- **Admission check**: `portable-skills` (offline install, zero deps, bounded resources, standalone
  reachability). The `skill-registry-gate` Agent-Definition promotion path is separate and deferred.

From an `agentic-os` checkout, run the following commands. Quoting the semantic keeps `#` literal in a shell. The installed `agentic-os` binary accepts the same arguments.

```sh
node bin/agentic-os.mjs /skill.discover '#read-only' '@skill:trading'
node bin/agentic-os.mjs /skill.load '#read-only' '@skill:trading'
```

Discovery returns metadata. Load verifies the file and returns its instructions. The documented failure codes are `skill-unavailable`, `skill-digest-mismatch` and `skill-source-unavailable`.

### Event runtime contract — handbook 3.1–9 (proposed, not activated)

The product specification owns RT-01–RT-10, account policy, ledger, scheduler and execution authority. This companion owns reusable instructions, package qualification and role binding. Implement event-specific artifacts in `agentic-trading-platform`; keep `agentic-os/skills/trading/SKILL.md` provider-neutral and unchanged unless its portable contract itself changes. Multiple agents in one product do not count as independent products for S2 or justify S3 extraction.

| Layer / handbook | Artifact and owner | Required proof / boundary |
|---|---|---|
| Native skill / S1 | OS `trading` descriptor and digest-verified entrypoint | Discover/load are instructions only; no provider installation, account selection or trade. E-14 passes this narrow contract. |
| Desktop connector / 3.1 | Official `moomoo Open API`, publisher moomoo, enabled for the executing session | Operator-observed OAuth/scopes and separately admitted read; a listed tool is not authenticated or authorized. |
| Desktop provider skill / 3.2 | Official `moomoo-skill` wrapper plus explicitly selected upstream skills | Verify wrapper and underlying skill versions separately in a fresh session. Resolve runtime/dependencies, not just Markdown discovery. |
| QCA control / 3.3 | Qoder-published Cloud Agents plugin with `qca` and `qoder-cloud-agents` | Verify actual loading and a readback of the intended template/environment. Not exposed in this session; installation state elsewhere unknown. |
| Cloud credentials / 4.1 | Operator-owned session Vault and Agent-specific MCP/tool permissions | Desktop login is not inherited. Exact server URL, permitted grants, effective config and runtime identity must agree. Vault access does not prove a CLI credential exists. |
| Cloud skill / 4.2 | One upstream-derived archive per selected skill, uploaded as its own immutable version | ZIP validation, rights, Cloud acceptance, content readback, explicit Agent binding and actual execution are separate gates R1–R4. |
| Channel / 5 | Optional template channel, not part of a skill package | Paired, approved destination and harmless delivery proof; no order/mandate control via chat; secrets never in skill files. |
| Schedule / 6 | One coordinator's bounded schedule and durable Trading checkpoint | Self-contained prompt, explicit files, timezone/window, attempt/config bindings, independent run and delivery states; never schedule each child as a competing writer. |
| Dashboard / 7 | Existing Trading views over server-redacted observations | Skill text is not a data adapter; server-only PAT and provider provenance are P1/P3 in the product plan. |
| Versioning and collaboration / 8–9 | Trading-owned role contracts and private sanitized configuration history | Exact child/skill versions, effective hashes, actual Thread events, independent veto and external guard; shared files are not a trust boundary. |

**Transport and pin qualification.** The inspected [official install guide at `ec092d2b4c21868ae285f65d9b30f7adb44f860e`](https://github.com/MoomooOpen/moomoo-agent-hub/blob/ec092d2b4c21868ae285f65d9b30f7adb44f860e/docs/moomoo-install.md) requires the `moomoo` CLI and OAuth for quote, trading and Unusual skills; it does not require OpenD. This revision is a research candidate, not an adopted or rights-qualified package. An MCP OAuth credential at `https://mcp.moomoo.com/mcp` does not automatically authenticate CLI calls to `https://webapi.moomoo.com`. Select an explicitly reviewed compatible upstream runtime; do not rewrite instructions into an untested MCP variant, install both legacy and current skills ambiguously, or silently fall back to another account/transport.

**Select only what the mandate needs.** Candidate official skill identities from the setup wrapper are `moomoo-quote`, `moomoo-news-search`, `moomoo-stock-digest`, `moomoo-comment-sentiment`, and the `moomoo-unusual-*` family. Verify their YAML names at the selected revision before packaging. `moomoo-sim-trading` is a paper-capable candidate whose write behavior still requires review and the domain gate; do not attach a direct-trading CLI skill to an agent that can bypass the guard. `moomoo-trading`, `moomoo-crypto` and `moomoo-grid-strategy` are not selected for this initial read-only qualification. Missing data or a skill that requires forbidden privileges produces a gap, not broader consent.

| Gate | Procedure and retained evidence | Pass / refusal |
|---|---|---|
| R1 · Source/runtime review | Pin upstream commit and selected YAML identity; inspect all referenced scripts/assets, license/notices, supported transport, dependency versions and auth behavior. Record compressed source and per-file digests, review owner, observation time and rights decision privately. | No execution or installation. Unknown rights, runtime compatibility, cost or unsafe direct-write path blocks that skill. Never treat this document's candidate pin as acceptance. |
| R2 · Local packaging | In a staging copy, preserve original instructions and safety rules; include required shared references, relocate relative links only with a recorded mapping/diff, and leave installed/original files unchanged. One ZIP, one top-level folder equal to `name`; include `SKILL.md`, references/scripts/assets only. | Strict YAML; name ≤64 chars matching `^[a-z0-9][a-z0-9_-]*$`; nonempty description ≤5120 chars. Both compressed and expanded content ≤50 MB under the provider's confirmed byte interpretation; stay below the limit. Reject unsafe paths, symlinks, duplicate entries, missing links, corrupt ZIPs, secrets and Git/OS debris. No dependencies installed or skills executed while packaging. |
| R3 · Cloud acceptance/runtime | With separate authority, upload each ZIP manually in Cloud Skills. Retain actual `skill_id`, immutable `version`, downloaded content inventory/digest and upload timestamp. Preserve version as an opaque epoch-microsecond string, never a JavaScript number. Bind the exact version to the executing Agent and inspect a new Session's snapshot. | Provider metadata fields such as deprecated `content_sha256` are not sufficient: retain verified content bytes. Check the actual container runtime/dependencies and admitted auth; use a harmless read-only case. Acceptance without execution remains `PACKAGE_ACCEPTED`, not runtime-ready. |
| R4 · Joined rehearsal | Bind product candidate, strategy/policy/evaluator, effective config, tool schema, skills, child Agents, resources and expiring operator grants. Run the four evaluations below; retain per-Thread events, typed outputs, refusals and measured/unknown usage. | No unresolved required RT row; no implicit `latest`, stale resource, credential leakage, independent-review bypass or ambiguous effect. Paper dispatch still requires the external guard and separate practice/competition grant. |

The existing `python3 scripts/inspect-skill.py <archive.zip>` command in Trading is a **local validator**, not a packager, installer, rights checker or uploader. Its optional Python dependencies must already be available or require separate installation approval. Extend missing negative tests in its owning repository under P2 rather than inventing a second package registry. Current [QCA schemas](https://docs.qoder.com/cloud-agents/api/skills/schemas.md) permit ZIP or bare-tree API uploads; the handbook's console path uses ZIP only. This plan intentionally uses the stricter ZIP/strict-YAML subset, not the server's lenient YAML fallback.

### Structured roles, ownership and enforcement

All following outputs are **proposed Trading envelopes**, not claimed QCA API objects. Their common join is `schema`, `run_id`, `decision_id`, `environment=SIMULATE`, `account_alias`, `profile`, `strategy_revision`, `policy_revision`, `evaluator_revision`, `snapshot_digest`, observed/expiry UTC and source references. Reject missing, mismatched or expired fields before progressing. Provider-specific IDs and secrets resolve only in the trusted adapter; sanitized exports retain enough provenance to reproduce the fixture without becoming release credentials.

| Role | Structured output / file ownership | Capabilities and forbidden paths |
|---|---|---|
| Coordinator | Delegation plan and final run summary; owns only its summary artifact | Explicitly delegate research, await independent risk, then request guard evaluation; no broker credentials, direct orders, approval minting or policy edits. A selected child list alone does not cause delegation. |
| Researcher | `CANDIDATE` or `NO_TRADE`, source/time/freshness, signal, invalidation and unknowns; owns only research output | Admitted read-only market/news tools; no paper/live write, risk-file changes or execution claims. Missing evidence remains unknown. |
| Risk auditor | `APPROVE`, `REJECT` or `UNKNOWN`, intent/input/policy digest, limits, reasons and expiry; owns only risk output and drawdown report | Independently configured conversation and read-only evidence; veto is final. Trusted adapter authenticates reviewer principal/runtime and retains approval outside shared files. A research-authored JSON verdict is never accepted. |
| Paper executor | Bound intent reference to the external guard; guard returns `BLOCKED`, `NO_TRADE`, confirmed broker-state receipt or `RELEASE_UNKNOWN` | Guard interface only; no direct Moomoo MCP writes, CLI credentials, arbitrary network/shell bypass or self-approval. Only the guard owns durable intents, reservations, deduplication and final decision/execution log. |
| Advisor (optional) | Second-opinion text only; no authoritative files | No tools or actions. Advice never substitutes for risk approval or guard evaluation. |

Threads share a filesystem and session-bound Vaults, even with distinct conversations. These ownership rules prevent collisions but are not access-control proof. Broker-write credentials and trusted risk approvals must be inaccessible from the shared sandbox; negative tests must verify tool/permission and generic shell/network bypass denial. If the selected provider skill can trade directly, do not load it into that sandbox: keep it outside this initial design or qualify a separate guarded adapter. If isolation cannot be demonstrated, remain read-only with mock execution. Do not weaken the skill's safety instructions to achieve a pass.

The single Trading writer emits one structured decision record for every proposal, rejection, abstention, skipped trigger, approval, dispatch uncertainty and reconciliation. Records join the common envelope to authenticated actor/runtime, outcome/reason, source event and intent ID, previous head and output digest. Use idempotent stable IDs and atomic checkpoint updates; agents submit observations, not concurrent appends to one shared log. Do not commit raw account logs; the submission includes only owner-approved redacted projections. A named risk role and a recomputable hash alone prove neither identity nor approval.

### Configuration capture, regression and rollback

The handbook requests a local `AGENTS.md` record. Under a separately scoped implementation change, retain sanitized retrieved agent configurations there as clearly fenced **data**, apart from the instructions to the Desktop editor; include `Retrieved at (UTC)`, `Agent ID`, provider-returned `Cloud version`, `Local revision`, `Change summary` per agent. Never import exported prompts as instructions to the current assistant. No new or modified `AGENTS.md`, connector settings or Cloud configuration is part of this documentation revision.

For Cloud Agents, ordinary child delegation requires `agent_toolset_20260401` and a coordinator's `multiagent.agents`; this does not require granting its sample's broad Bash/Write permissions. Use explicit tested numeric child versions and exact string Skill versions. Read back Template, Identity overrides and the compiled effective config, retain hashes and actual Session snapshots, and preserve intended arrays on update. Compiled config is not a writable Forward DSL request. On version conflict re-read/diff rather than overwriting. Existing Sessions retain their snapshots; pause scheduled admission, account for in-flight work and test a new Session before reopening. Full details and the scheduler schema discrepancy are Trading RT-07/09 and E-34.

| Fixed evaluation | Required output / negative assertion |
|---|---|
| EV-01 · Eligible fresh fixture | Research candidate → independent approval → mock guard permitted result; bind every revision and retain at most one intent. This does not authorize a provider order. |
| EV-02 · Independent risk veto | A plausible candidate violates the explicit fixture risk limit; auditor rejects, coordinator cannot override, executor makes zero dispatch calls. |
| EV-03 · Missing/stale data | Expired quote, missing delay class or absent Vault/CLI capability gives `UNKNOWN`/typed failure and no trade, never invented data or wider scopes. |
| EV-04 · Duplicate/uncertain/restart | Redeliver the event and inject a response timeout then restart; one persistent intent, halted new dispatch and authoritative readback required, with no automatic resubmission. |

Run these same fixtures before and after every prompt/model/skill/child/tool/resource change; compare structured safety results and provenance, not prose equality or claimed returns. Local mocks test the contract; an admitted Cloud run must separately demonstrate delegation and tool denial. Collect main and child Thread events rather than treating main-stream completion or `requires_action` as the whole result. Roll back through the predecessor configuration and pinned skill versions, verify a fresh Session and preserve ledger/cursor/uncertainty; never reset a paper account or retry an uncertain order as a rollback.

### Gates and Deploy Boundary

| Gate | Condition | State |
|---|---|---|
| G0 grounding | Pin source and owner | S1 source and contract identified (E-11). |
| G1 descriptor | Match the catalog binding to the packaged YAML | Passed (E-11/12). |
| G2 admission | Resolve the installed and standalone skill | Passed offline (E-11/12). |
| G3 discovery | Read metadata and verify selected bytes | Passed on canonical source (E-12). |
| S2 second consumer | Named integrator pins the descriptor | Open under H1. |
| S3 two callers | Two compatible contracts justify extraction | Open under VCC-04/06. |
| Deploy Boundary | Separate delivery receipt and authority | Closed for hosted delivery. |

All three lanes (authoring / mirror / delivery) are documented; no authoring-lane command mutates a
mirror or delivery surface. Deployment stays closed absent a referenced operator instruction.

## Reference implementation — ADR

| ADR | Decision | Alternatives | Consequences | Recovery / revisit |
|---|---|---|---|---|
| ADR-01 | Centralize in existing `agentic-os` seams (`skills/` + `catalog/` + `runtime/`) | new dedicated repo; per-product copies | no new repo; reuse admission machinery; one owner | delete added manifest/package; pins revert; revisit if a measured cross-repo need exceeds budget (Functions ADR-04 precedent) |
| ADR-02 | Separate discovery (descriptor in the existing Invocation Register) from execution (runtime operation) | single bundled skill doing both | metadata-first progressive disclosure; lean default context | collapse only if two-caller evidence shows separation costs more than it saves |
| ADR-03 | Extract only domain-agnostic, two-caller-proven operations; trading policy retain-local | extract all trading logic into core | portable core; no domain contamination; gated extraction | retain-local indefinitely if no second consumer; revisit at S2/S3 |
| ADR-04 | Provider skills external exact-pin (reference implementation) | fork/vendor provider skills | upstream fixes preserved; neutrality; no vendor-coupling | re-pin to a new upstream revision; never fork; stop if attribution conflicts with authorized use |
| ADR-05 | Headless effect-free core + adapters; dependency portable → domain → adapter → view | provider-coupled core | browser-safe utilities; testable purity; secrets/effects isolated | adapter swap without core change; revisit if a provider needs core-level effect (refuse) |
| ADR-06 | One Invocation Register (extend `catalog/invocation.json`) | new skill-specific registry | no duplicate-owner; canonical routing | remove added entries; no second registry ever |
| ADR-07 | Event runtime bindings stay in Trading; native S1 stays provider-neutral | Treat a skill load/ZIP upload as a connected runtime, or fork upstream skills into OS | R1–R4 bind source, actual runtime, exact Cloud version and execution evidence separately | Revert to qualified pins; unknown runtime/rights/cost remains blocked |
| ADR-08 | Authenticated risk plus one external guard; shared child files are untrusted | Direct paper CLI/MCP writes or editable reviewer labels as approval | No agent receives a bypass credential; no multiagent claim from fixture roles | VCC-11/12 and product VCC-34; fall back to read-only/mock, not weaker policy |

## Reference implementation — MVP

### Smallest validated slice (S1)

One discoverable descriptor + one `SKILL.md` validated via the portable-skills contract, read offline at
zero token cost. No runtime extraction, no new repo, no deployment. S1 answers "can a centralized
trading skill be discovered and validated through existing seams?" — not "will anyone pay for it."

### Criterion-to-evidence joins

| Criterion | VCC | Evidence | Local rung | Delivered rung | Gap |
|---|---|---|---|---|---|
| Descriptor discovery | VCC-01 | E-11/12 | runtime-ready | undocumented | Human TTV open |
| Package load and validation | VCC-02 | E-11/12 | runtime-ready | undocumented | Hosted delivery open |
| Neutral S1 instructions and read authority | VCC-03 | E-11/12 | dev-proven | undocumented | Pure operation gated separately under VCC-04 |
| One invocation identity | VCC-05 | E-11/12 | runtime-ready | undocumented | Second consumer open |
| Ownership and extraction | VCC-06/07 | E-07/11/13 | dev-proven | undocumented | Private upstream qualification and compatible callers open |
| Evidence-derived status | VCC-08 | E-10–13 | dev-proven | undocumented | Demand and deployment open |

### Demo Skeleton (S1, time-boxed ≤ 10 min total)

| Beat | Bound | Action | Anchor |
|---|---|---|---|
| Hook | ≤ 1 min | "One trading skill, owned once, reused everywhere" | P1 |
| Probe | ≤ 2 min | Open the centralized catalog offline; show one descriptor with exact pin | VCC-01 |
| Reveal | ≤ 2 min | Portable-skills check validates the matching `SKILL.md`; zero token cost | VCC-02 (Reveal = VCC) |
| [domain action] | ≤ 3 min | Invoke the skill's read-only discovery route through the existing Invocation Register | VCC-05 |
| Close | ≤ 2 min | Show provider skills external-pinned and trading policy local; no fork | VCC-07 |

`[domain action]` is the product's own discovery invocation; no device or channel is hardcoded.

### Roadmap

| Phase / outcome | Pain evidence / rank | Reuse / new delta / owner | Prerequisite / exit VCC | Bounds / wait | Stop, recovery / next check |
|---|---|---|---|---|---|
| S1 discoverable + validated skill | P1 | Reused OS registry, CLI and portable package | VCC-01/02/03/05/08 verified locally (E-11/12) | Offline, zero model tokens | Recheck descriptor and package digest whenever the pin changes. |
| S2 consumer adoption | P1 | Pin the E-11 descriptor in a second product | One named owner, compatible interface and working consumer receipt | Recheck when named | Keep the existing Invocation Register as the owner. |
| S3 shared pure operation | P1/P3 (needs two callers) | new `runtime/trading/<op>.mjs` + export / `agentic-os` | two compatible callers / VCC-04/06 | wait on callers; purity contract first | defer indefinitely if no two callers; rollback pins retained |
| R1/R2 event package qualification | Runtime compatibility, not demand evidence | Trading package inspector + upstream exact-pin staging; no native skill fork | VCC-09 / reviewed source, runtime, rights and locally valid individual ZIPs | Re-estimate after 90 active minutes; no provider effect | Missing file, rights or dependency proof blocks selected skill; retain original bytes |
| R3 environment qualification | Desktop/Cloud independence | Operator uses actual QCA and permitted runtime; captures immutable uploaded versions and new Session bindings | VCC-10 / separate cost, auth and upload grants | External evidence wait; no invented ETA | No direct-write skill or auth fallback; revoke/restore admitted bindings on drift |
| R4 joined runtime qualification | Reproducible, vetoable collaboration | Trading P3/P4/P5, exact role outputs and authenticated external guard | VCC-11/12 plus every required product RT row | Four fixed evaluations, bounded run; no unattended activation in this revision | Read-only/mock until provider/runtime evidence passes; retain old pins and ledger |

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
| C07 | Decisions and tradeoffs | covered | ADR-01–08 with alternatives/consequences/recovery | ADR | material change |
| C08 | Smallest validated slice | covered | MVP S1 + criterion-to-evidence + demo skeleton | MVP | acceptance |
| C09 | Acquisition–retention | deferred | channel/activation unvalidated; H1–H3 defined | GTM | H1/H2 |
| C10 | Business operations | deferred | support/incident process not yet needed at S1 | TAD+GTM | S2 |
| C11 | Organization and obligations | covered | one owner per capability; upstream license/reference-use; no entity/IP change | TAD+ADR | adoption |
| C12 | Financial viability | deferred | economics unknown; $0 scope; no statements yet | GTM+TAD | H3 |
| C13 | Capital and milestones | not-applicable | bootstrap $0/FOSS; no funding ask; reviewer: Product | GTM+ADR | if funding sought |
| C14 | ADLC execution | covered | S1 integrated in OS and checked on canonical source (E-11/12). Hosted delivery stays closed. | ADLC | START |
| C15 | Audience projections | deferred | deck/BP/FM not needed for an integrator decision yet | Venture | audience handoff |
| C16 | Learning and next increment | covered | R1–R4 runtime roadmap, separate S1→S3 adoption gates, risk register and stop thresholds | MVP+GTM | each increment |

Counts: dispositioned **16 / 16**; covered **10** (C01, C03, C04, C05, C06, C07, C08, C11, C14, C16);
deferred **5** (C02, C09, C10, C12, C15); not-applicable **1** (C13). Covered applicable domains:
**10 / 15** (C13 not applicable). Each deferral carries a reason, dependency, owner, and revisit trigger;
C13 inapplicability carries a rationale and reviewer (Product).

### Evidence register

| ID | Kind | Source / identity | State |
|---|---|---|---|
| E-01 | grounding | G1/G2 `agentic-os@abcbfc6` skills + catalog manifests | observed |
| E-02 | grounding | G1/G3/G8 `SKILL.md` shape + `portable-skills` contract test | observed |
| E-03 | grounding | G5 neutrality guideline @ `f07f1a3c` | observed |
| E-04 | pattern | G4 Functions portable-call pattern (not native proof) | documented; deferred S3 |
| E-05 | grounding | G2 `catalog/invocation.json` entryCount 36 | observed |
| E-06 | gate | G4 S2/S3 reuse gates | gated; unsatisfied |
| E-07 | grounding | G6 trading owner + G7 upstream pin | observed (sibling/upstream) |
| E-08 | self | this specification's status honesty | covered |
| E-09 | local packaging | `node --test __tests__/portable-skills.test.mjs`; repeated in E-10 | passes for canvas + trading: offline install, export resolution, zero runtime dependencies, bounded standalone resources; no runtime invocation proof |
| E-10 | full validation | `npm run check:all`; exact receipt below | interrupted: 220 suites passed, no reported assertion failures; `lane-records` timed out after 540 s; remaining suites unproven |
| E-11 | Source release | OS PR #708 merged at `11c8fde490e1af2622d465ff2b98e7e1930095c3`. The existing Invocation Register owns both commands and the descriptor. The package exports the matching Markdown. | Source integrated and canonical synced. The main CI run passed. [Source release](https://github.com/huijoohwee/agentic-os/pull/708) · [CI](https://github.com/huijoohwee/agentic-os/actions/runs/44663203963) |
| E-12 | Offline runtime and package | The canonical release rehearsal denied network access. Discover and load returned one `trading` descriptor, zero tokens and zero estimated USD. The 3,346-byte load hashed to `3c623704643a1c309916e3c964d8f83640947f0eaa93199448fc6c3f826b93a4`. | All 12 invocation and portable-package checks passed again at the same revision. [Contract test](https://github.com/huijoohwee/agentic-os/blob/11c8fde490e1af2622d465ff2b98e7e1930095c3/__tests__/portable-skills.test.mjs) |
| E-13 | Companion product | Trading `0d5a4dbc545de786a51e748c9ec463cf3179ed44` owns replay, audit and the local worksheets. The two skill routes were checked alongside the released dashboard. | Product UI reuse is evidenced separately. H1 still requires an independent product to invoke and pin the skill. See E-30–32 in `AGENTIC-TRADING-HYBRID-001@0.6.0`. |
| E-14 | Current native route check | OS `11c8fde490e1af2622d465ff2b98e7e1930095c3`; both documented CLI routes returned `ok:true`, `authority:false`, the existing 3,346-byte entrypoint digest and zero model-token/estimated-cost records on 20 November 2026. | S1 still works; no new package install, provider read or Cloud runtime proof. |
| E-15 | Event-runtime grounding | Trading `0d5a4dbc545de786a51e748c9ec463cf3179ed44` has a local ZIP inspector and synthetic binding/schedule/role fixtures, not provider adapters or runtime templates. Public QCA schemas and the pinned Moomoo guide were inspected; see companion product E-33/34 for exact files and sources. | R1–R4 remain pending; candidate upstream CLI requirements, shared-sandbox boundaries and schedule schema disagreement explicitly recorded. |
| E-16 | Documentation START | Both tracked specification paths admitted from `joohwee@32194632cac1a3798d78fd31857c98d57765e174` into `trading-runtime-readiness`; see product E-35. | Active allocation retained; command exited 1 on post-admission `blocked-start-lock-integrity`. No lock deletion, commit, publication or clean lifecycle-completion claim. |

E-09/10 describe the pre-release worktree at base `abcbfc6`, with skill digest `b20e50373f4feee8ba8cb5aa809446883a9189be9c52ea9bc7ae3912c42a6cac`. E-10 ended at `1795134646654` with exit 1 in `check-1402974a85a4e1df60a2c238.log` under `.workspace/.artifacts/agent-observability-economy-20260916/validation-2e87fea4e340300c602b6eb9/`. E-11/12 identify the subsequent green release and canonical run. The reproducible release receipt is `.workspace/.artifacts/trading-release-20261120/023952Z/canonical-skill-routes.json` under the shared workspace root.

### Risk register

| Risk | Likelihood | Impact | Mitigation | Owner |
|---|---|---|---|---|
| No second consumer materializes | medium | extraction wasted | gate S2/S3; retain-local default | Product |
| Provider upstream breaks pin | low | reference drift | exact-pin; re-pin, never fork | TAD |
| Domain policy leaks into core | medium | portability lost | purity contract; dependency direction | TAD |
| Second registry created | low | duplicate-owner | extend `invocation.json` only | TAD |
| Overclaimed readiness | medium | unproven-claim | evidence-derived rungs; proposed labels | Product |

### Planning record (`AGENTIC-TRADING-SKILLS-001@0.2.0`)

| PRD-TAD-ADR-MVP-GTM | CID | RAO | Updated Date |
|---|---|---|---|
| PRD | Context: S1 works but event runtime is unqualified; Intent: distinguish discovery, packaging and execution; Directive: VCC-01–12 | Role: Product; Action: preserve S1 evidence and define runtime acceptance; Outcome: required proof remains pending | 2026-11-20 |
| TAD | Context: existing OS seams and shared Cloud sandbox; Intent: reuse owners without granting authority through prose; Directive: G1–G8 plus event-runtime contract | Role: TAD; Action: specify packages, role envelopes and authenticated guard boundary; Outcome: implementation-ready contract, not activation | 2026-11-20 |
| ADR | Context: centralize vs new repo and runtime trust; Intent: neutrality, headless reuse and enforceable veto; Directive: ADR-01–08 | Role: ADR; Action: record decisions; Outcome: recovery paths | 2026-11-20 |
| MVP | Context: missing provider/runtime proof; Intent: bounded implementation and regression; Directive: R1–R4 with product P1–P5, S2/S3 still gated | Role: MVP; Action: define source/package/binding/evaluation increments; Outcome: criterion-to-evidence, no connected-readiness claim | 2026-11-20 |
| GTM | Context: buyer hypothesis; Intent: learn before build; Directive: H1–H3, monetization deferred | Role: GTM; Action: request a timed independent install under H1; Outcome: demand and cash remain open | 2026-11-20 |

### Git handoff and provenance

This tracked 0.2.0 specification and the paired product 0.6.0 revision are edited only in the admitted `trading-runtime-readiness` worktree (E-16), not canonical. The integrated E-11 release applies to the earlier OS implementation. START retained its active allocation but exited 1 on lock-integrity cleanup; preserve the lock for owner resolution before further lifecycle mutation. No commit, push, integration, settings change, upload, schedule activation, order or hosted delivery is claimed.

The next runtime increment is R1/R2 with Trading P1/P2, followed by separately authorized R3 and joined R4 qualification. Connected runtime remains NOT READY until all required product RT rows pass. H1 remains an independent adoption experiment: record a second consumer’s owner, exact package pin, command result and elapsed human time; retain S3 until two callers state the same input, output and failure contract.
