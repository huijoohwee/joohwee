---
title: "SME Business Plan Workspace — E2E Pitch, Plan, and Financial Model"
doc_type: "PRD-TAD-ADR-MVP-GTM"
version: "1.4.3"
date: "2026-11-05"
lang: "en"
owner: "Product Manager function"
continuity_id: "sme-business-pack"
local_rung: "undocumented"
delivered_rung: "undocumented"
lane: "authoring"
universal_scope: true
lifecycle_status: "proposed"
source_docs: "prd-tad-adr-mvp-gtm-guidelines.md@3.4.0; pitch-deck-guidelines.md@1.2.0; business-plan-guidelines.md@1.1.0; financial-model-guidelines.md@1.1.0; prd-tad-adr-mvp-gtm-venture.md@2.1.3"
---

# SME Business Plan Workspace — E2E Pitch, Plan, and Financial Model

## Document control

Join key: `sme-business-pack@1.4.3`. This document is the sole current product, architecture, decision, MVP, and go-to-market contract for the SME planning workspace. It defines two selectable plan contracts inside one E2E workflow: a general business plan and an SME takeover checker. Both use one versioned protocol interface, tool registry, table, editor, evidence model, and worksheet flow; their declared fields and calculation models remain contract-owned. There are no duplicate workflow variants or parallel registries. Pitch, plan, and model requirements are consumed from the exact shared guideline revisions in `source_docs`; this PRD and the live schema link to those owners and report MVP support without copying their taxonomies or creating a second rules registry.

- **Status:** proposed. Source integration is recorded below; independent product acceptance and deployment remain open.
- **Audience:** people preparing or reviewing an early business or venture plan, including founders, operators, and advisers.
- **Scope:** organize user-entered information into a twelve-role pitch deck outline, business-plan starter prompts, single-period financial arithmetic, and a neutral acquisition cash-to-close check. This MVP is not a complete guideline-conformant deck, operating plan, or financial model.
- **No external source dependency:** the product neither searches nor fetches planning, market, pricing, company, or business data.
- **Canonical implementation:** existing local-first SME workspace and shared Multi-dimensional Table, protocol/evaluator, codebook, and dictionary in `agentic-commerce-os`.

## 1. Product requirements

### 1.1 User need

People preparing a business plan need one place to organize the venture narrative, assumptions, evidence notes, financial inputs, deterministic arithmetic, and open questions. Inputs are often incomplete and must remain distinguishable from calculated values and independently verified facts.

### 1.2 Product outcome

The workspace produces a reviewable planning draft from explicitly supplied information. It makes completeness, missing prerequisites, ranges, evidence context, formulas, and open checks visible without estimating demand or declaring viability.

### 1.3 Product principles

1. **Universal:** no country, currency, legal form, sector, business model, funding source, market size, or regulatory assumption is built into the active contract.
2. **Neutral:** no winner, score, ranking, recommendation, forecast, valuation, or viability judgment is produced.
3. **Agnostic:** users supply their own narrative, evidence, units, currency, and financial assumptions. Unknown remains unknown; no missing value becomes zero.
4. **Local-first:** calculations run on the device; form values and reports stay in memory and clear when leaving the workspace.
5. **One workflow owner:** the current E2E workflow is one native `agentic-base` Multi-dimensional Table. Its selected-row editor edits that same table's fields. Results are projected as table columns; a separate checklist or second calculation workflow is prohibited.
6. **Atomic columns and shared nesting:** field attributes are separate columns, never concatenated into one field label. Metadata orientation exposes record type, section, group, parameter, stable key, data type, unit, requirement, constraints, and definition independently. The host supplies protocol-derived row paths/depth; Base owns nested-row display and collapse/expand controls. No consumer duplicates collapse state or table rendering.
7. **Shared contracts:** reuse the existing table adapter, generated design tokens, and canonical shared dictionaries. A versioned alignment map points to the parent PRD and pitch, plan, model, and Venture Record owners; it reports partial and out-of-scope requirements without redefining them. No duplicate renderer, token set, tool registry, command, skill, or dictionary taxonomy is introduced.
8. **Free and portable:** MVP has no paid service, account, hosting requirement, added package, or new runtime dependency. It works in mobile browsers and remains usable offline after the local shell is available.

### 1.4 E2E workflow

The workspace starts with the general business plan contract and **Buy/Build** mode. The Plan contract selector also offers **SME takeover checker**; the mode selector offers **Scenario** for either contract. The user chooses one, two, or three plan options or scenarios; selects a row; enters that contract's fields; optionally records evidence context; builds a local draft; reviews each calculated and unknown output in the same table; pivots that table if useful; and prints, exports, or imports a local worksheet. Changing mode preserves entered rows and inputs while invalidating the previous report. Changing contract clears row inputs and evidence so incompatible fields cannot mix.

Scenario A/B/C order is entry order. A comparison requires the same protocol version and currency code. Values are never sorted, normalized, converted, scored, or selected as a winner. Any evidence entry remains user-recorded and unauthenticated.

The single workflow table includes:

- one row per plan option in Buy/Build mode or per scenario in Scenario mode, ordered A/B/C;
- a shared mode column and mode selector, defaulting to Buy/Build;
- every field from the active protocol as an input column;
- required-input completeness and input-validation state;
- separate evidence value, provenance, observer role, date, and authentication-status columns;
- every active contract's deterministic model output and its prerequisite coverage;
- pitch-role and projection-coverage columns when declared by the active contract;
- ordered next checks;
- the shared Base pivot over the same projection.

In metadata orientation, each record attribute has its own column: record type, section, group, parameter, stable key, data type, unit, requirement, allowed values, bounds, length, pattern, definition, and each option's value. Hierarchy is represented through row depth; Base provides row and bulk collapse/expand. Commerce may derive protocol-specific path and group-label rows, but it does not implement a second collapse controller. Graph's data-view host delegates nested-row collapse state to the same Base hook while retaining its existing owner-bound filter and group settings.

Coverage columns report mapped owner requirements and supplied inputs within each projection's declared MVP scope. They do not judge completeness of the full owner contract, quality, readiness, authentication, or conformance. Pitch roles trace only to declared input keys and model output keys; missing content remains explicit and roles may be combined in a final presentation. The general business plan's Buy/Build mode requires an explicit approach (`buy_existing`, `build_new`, or `undecided`). A purchase path requires user-entered acquisition and transition costs; build costs remain separate. The takeover checker records transfer structure and scope, acquisition and asset information, operating figures with a user-stated basis and period, location obligations and user-stated renewal/assignment information, handover, working capital, and available cash. Optional context fields do not silently alter cash-to-close arithmetic. Outputs show cash required, location exposure, shortfall, and monthly revenue less listed monthly costs as transparent arithmetic; they do not derive a transfer-price opinion. An unknown obligation is not treated as not applicable. Scenario mode uses the selected contract's same fields and calculation model without requiring a Buy/Build path.

The Data dictionary is a separate read-only route and table because it documents the contract, including projection owner revisions, requirement anchors, mapped input keys, and current support status. It does not run a second workflow or calculate a parallel report. It is generated from the live protocol and lists the canonical shared owners for invocation, `/`, `#`, `@`, skills, MCP, WebMCP, and AgenticRAG terms.

### 1.5 Data and financial model

The shared contract schema is `sme-business-plan/protocol/v3`; the selector resolves `sme.business-plan@2.3.0` or `sme.takeover-checker@1.1.0`. Both protocols declare Buy/Build as default and Scenario as selectable, with mode supplied to the same build and comparison entry points. The general plan declares exact source revisions and anchor references for the parent scope and pitch, plan, model, and Venture Record owners. It includes neutral venture narrative, user-selected currency and financial inputs, twelve pitch-role columns, nine shared workflow columns, and four scoped projection/evidence outputs. The takeover checker declares user-entered transfer details, assets, operating context, conditional location obligations, working capital, and available cash. Its outputs are cash required, location exposure, cash shortfall, and monthly revenue less listed costs; every input and evidence prompt remains in the same table. Optional descriptive fields do not enter cash-to-close arithmetic. Its explicit example bundle loads only after user action. Both contracts keep missing values unknown and never convert currency.

Money accepts a single nonnegative amount or a low/high range, up to four decimal places and a bounded maximum. Calculations propagate ranges. Currency is selected per row as a three-letter code; a comparison with mixed or absent codes is refused. Comparison also uses one shared workspace mode. The implementation does not look up, convert, or compare purchasing power.

The general-plan model exposes single-period revenue, variable cost, contribution, operating costs, operating result, break-even volume, cash runway, entered-runway funding need, and the difference between proposed funding and that modeled need. The takeover model exposes cash required to close and fund the selected period, remaining location payment exposure, shortfall against available cash, and user-entered monthly revenue less listed costs. The latter is arithmetic only and is not reported as profit. No calculation estimates a transfer amount from asset age, lease duration, earnings evidence, or a fixed assumption. Outputs are not forecasts, valuations, linked statements, price opinions, or guideline Headline Registers. An output stays unknown when prerequisites are missing or ambiguous. The formula, required inputs, model state, and owner alignment are available through the table and dictionary.

### 1.6 Evidence and privacy

Evidence is attached to a declared input field. Its provenance values describe how the user recorded context and are not authentication tiers. No name, contact, URL, document upload, or image is accepted as evidence. Short text fields reject URL, email, and phone patterns. Nothing is persisted or transmitted during a local plan build.

### 1.7 Non-goals

The MVP does not provide a market research feed, benchmarks, automated forecast, legal/tax/accounting/investment/financing advice, valuation, loan application, company registry, venture database, investor matching, public listing, payment, fundraising transaction, publishing, or agent-controlled execution. It also does not implement the guideline owners' full Variant Registers, Claim Manifest or Section Claim Record, two-method market sizing, structured business risk/review lifecycle, linked income/cash-flow/balance-sheet statements, Base/Downside/Upside model, Headline Register, actuals/variance, or ADLC Cost Ledger. The pitch output is a twelve-role structured outline and local worksheet, not a rendered slide file or investor endorsement. Each section shows its source field keys; missing text remains explicit and is not generated.

## 2. TAD — architecture

### 2.1 Reference implementation — components and ownership

The names in this table identify current reference implementations; the schema and user-facing contract remain neutral and portable.

| Concern | Owner | Contract |
|---|---|---|
| Both plan contracts, shared modes, fields, models, evidence tasks, artifact roles, and source alignment | `public/local-first/sme-pack-business-plan.js` | One field and mode definition source; takeover fields remain generic with no locale, sector, or currency defaults |
| Registry, validation, deterministic models, pitch outline, worksheets, and tool schemas | `public/local-first/sme-business-pack-core.js` | One protocol/tool entry point with the active contract's declared calculation model and bounded inputs |
| Table projection, route lifecycle, local worksheet actions | `public/local-first/sme-business-pack.js` | One E2E table, one selected-row editor, one local status channel |
| Evidence and generated field editor | `public/local-first/sme-workflow-editor.js` | Renders fields from protocol; does not maintain a second field list |
| Contract documentation | `public/local-first/sme-pack-dictionary.js` and `docs/sme-business-pack-codebook-and-data-dictionary.md` | Read-only projection from protocol, canonical owner references, and explicit MVP support boundaries |
| Grid, pivot, nested groups, and collapse/expand | `agentic-base` data-view adapter | `multiDimensional`; Commerce supplies protocol-derived paths/depth and Graph uses Base's nested-row hook; no duplicate renderer or collapse state |
| Theme | `agentic-design-system` generated tokens | Mapped to shared table theme slots |
| Shared token, command, skill, and invocation meanings | Existing Agentic OS/Canvas dictionaries and AgenticRAG schema | Link to owner; never fork or redefine meanings here |
| MCP and optional WebMCP | Existing Commerce service/browser adapters | Same core tool names, schemas, and evaluator; explicit argument input only |

### 2.2 Contract and tool surface

Canonical tools are `pack.list`, `pack.protocol`, `business.plan.build`, and `business.plan.compare`. The API schema contains no industry field list or market-data source. `business.plan.build` accepts `{ pack_id, mode?, inputs, evidence? }` and resolves its fields and calculation model from the selected contract; omitted mode uses that contract's Buy/Build default. Comparison accepts one shared optional mode and two or three ordered `plan_sets`, each with the same `pack_id`, `pack_version`, and user-selected currency. Unsupported keys and values fail closed. Maximum request is 32 KB, maximum response is 64 KB, text is bounded, and at most 40 evidence records are accepted per row.

MCP and WebMCP discovery do not imply connection, identity, authority, evidence verification, or persistence. The browser tool is optional. Local calculations work when MCP/WebMCP are absent and when offline.

### 2.3 Decisions (ADR)

- **ADR-001 — One neutral registry and evaluator entry point:** register the general business plan and SME takeover checker as separate versioned contracts; resolve their owned fields and calculations through one protocol/tool registry. Do not duplicate the workflow, editor, table, evidence system, tool schemas, or registry.
- **ADR-002 — One workflow table:** use the existing Base Multi-dimensional Table for user inputs and all E2E outputs. No separate results cards/table or transfer checklist is a current workflow surface.
- **ADR-010 — Contract and mode are orthogonal selectors:** start with the general business plan and Buy/Build; offer the SME takeover checker in the same contract selector and Scenario in the mode selector. Mode changes row meaning while preserving values; contract changes clear incompatible rows. Neither creates another table, evaluator entry point, or registry.
- **ADR-003 — User-selected currency:** preserve input currency and ranges; refuse comparisons without matching explicit currency codes; do not convert.
- **ADR-004 — No inferred market values:** keep all market and financial assumptions user-entered; do not retrieve or embed external values.
- **ADR-005 — Evidence is context:** retain source type, actor role, and date as user-recorded metadata; display unauthenticated status and avoid evidence scores.
- **ADR-006 — Explicitly unknown outputs:** disclose missing inputs and the formula prerequisites; never impute zero or produce a forecast.
- **ADR-007 — Shared owner reuse:** reuse Base, Design System, Agentic OS dictionaries, and existing adapters; do not duplicate shared definitions.
- **ADR-008 — Local privacy:** hold working state in memory, perform no network request for local calculation, and clear state when leaving the route.
- **ADR-009 — Guideline ownership:** map the four projection guidelines and their Venture Record owner by exact revision and anchor; show current support status in the shared dictionary, and leave unsupported full-lifecycle records to their canonical owners.

## 3. MVP scope and acceptance criteria

The MVP is the existing SME workspace, its contract- and mode-aware Multi-dimensional Table and generated editor, shared local evaluator entry point, contract-owned calculations, local worksheet actions, optional shared MCP/WebMCP calls, and protocol-backed dictionary table.

| ID | Acceptance criterion | Proof |
|---|---|---|
| MVP-01 | Workspace starts with General business plan and Buy/Build; the Plan contract selector offers SME takeover checker; Scenario is selectable for both. One, two, or three rows appear in entry order. Mode switching preserves inputs; contract switching clears incompatible inputs. | Live UI at mobile and desktop widths |
| MVP-02 | Every active protocol input, selected mode and contract, shared workflow column, evidence facet, coverage output, model output, and any declared pitch role is a column in the same table; selected-row editing updates that row. | Compare each protocol to table columns and editor controls |
| MVP-03 | Each contract's local build shows its declared outputs, applicable coverage, completeness, invalid fields, evidence value and attributes, and next checks in the same table. General-plan pitch roles appear only for that contract. Coverage is scoped and makes no quality or conformance claim. | Live UI with blank and illustrative entries for each contract |
| MVP-04 | Missing inputs remain unknown; amount ranges propagate; no benchmark, currency conversion, or ranking occurs. | Live UI and manual formula fixtures |
| MVP-05 | Each multi-row comparison uses one selected mode, refuses mismatched contract versions or currencies, and preserves entry order. | Live UI in both modes with matching and mismatched currency inputs |
| MVP-06 | Workflow pivot changes the same table orientation and preserves row values. | Live UI pivot in both orientations |
| MVP-07 | Data dictionary route is visible in SME navigation and renders a read-only Multi-dimensional Table from the active protocol, including all inputs, outputs, pitch artifact, evidence guidance, tools, and shared owner links. | Navigate to `#sme-dictionary`; inspect table and sidebar |
| MVP-08 | Print, JSON, CSV, and Markdown exports carry the selected mode and same plan input contract; imported worksheets validate mode and contract version. | Local round-trip in the running app |
| MVP-09 | Local build makes no service request, persists no report, and runs in offline-capable mobile browsers after shell load. | Browser request capture, storage inspection, and offline route check |
| MVP-10 | Same evaluator and schemas back local, worker/MCP, and optional WebMCP calls. Unsupported tools do not block local work. | Adapter parity against the shared protocol |
| MVP-11 | Existing `agentic-base` and `agentic-design-system` utilities are reused; no dependency, second renderer, duplicate token system, or parallel workflow is added. | Imports, build manifest, and source review |
| MVP-12 | A source change is published only after the applicable AOS release workflow records authority and green proof. Local UI verification is not treated as publication or deployment. | Release receipt |
| MVP-13 | Protocol v3 and the read-only dictionary expose both modes, conditional Buy/Build inputs, canonical guideline owner revision, anchor, projection join rule, mapped stable keys, explicit support status, each pitch-role column, and each scoped coverage output. Unsupported owner records are not represented as implemented. | Protocol inspection and live dictionary route |
| MVP-14 | SME takeover checker requires user-supplied acquisition amounts, currency, location-obligation state, working-capital assumptions, and available cash. It records transfer scope, asset context, operating figures and their stated basis, renewal/assignment context, and handover in the same table. It calculates cash required, location exposure, cash shortfall, and monthly revenue less listed costs; unknown values stay unknown, explicit not-applicable stays distinct, and numeric ranges propagate. | Protocol inspection, live table/dictionary, and deterministic single/range/missing-input fixtures |
| MVP-15 | Nested record type, section, and group rows collapse individually and in bulk through Base; pivoting preserves values and hierarchy. Graph's table continues to use the same Base collapse hook alongside its existing filters and grouping controls. | Live UI collapse/expand, pivot, and Graph settings interaction |

## 4. MVP boundary and operating requirements

- Free-tier and FOSS use only; no paid API, add-on, overage, or recurring account.
- Existing dependency graph only; 0 new packages and 0 new runtime services.
- Individual source modules remain below 600 lines; emitted chunks remain below 500 KB.
- Route-load only the existing SME feature modules; keep unrelated application surfaces lazy.
- Support keyboard, touch, narrow mobile widths, system zoom, and offline shell usage.
- Fail loudly on invalid contract identity, malformed ranges, unsupported field keys, oversized requests, and stale route results.
- Keep mutation scopes limited to the existing Commerce owner, its existing local adapter inventory, the codebook, and the corresponding PRD lane.

## 5. GTM and validation

### 5.1 Positioning

An open, local-first planning worksheet for assembling and reviewing a business pitch, operating plan, and explicit financial assumptions. It organizes user-provided information; it does not source or verify market data and does not judge the venture.

### 5.2 First-use path

Open the existing SME workspace; choose a plan contract and mode; use that contract's explicitly loaded neutral example or enter user-owned values; inspect unknowns and formulas; export or print a local worksheet; share it outside the tool only by the user's own action. No signup or publication flow is required.

### 5.3 Validation hypotheses

- People can assemble a coherent first draft without a guided sales call.
- Showing formula prerequisites and unknowns improves reviewability compared with a single headline estimate.
- Users understand the boundary between their assumptions, derived arithmetic, and unauthenticated evidence.

Validate with time-boxed, consented walkthroughs using user-owned or fictional inputs. Do not collect scenario data or infer financial performance. Record only task completion, confusion, and requested fields. Pause if users interpret the output as verification, a forecast, or financing advice.

### 5.4 Release and rollback

Follow `agentic-os/docs/RELEASE-WORKFLOW.md` and the repository's release/deploy/rollback procedures. Preserve source lane and artifact receipts. A green local preview does not grant publication, merge, or deployment authority. Rollback restores the last known-good route module and protocol atomically; do not leave a partial schema/UI mismatch live.

### 5.5 Source and verification record (2026-11-05)

- Commerce source `f593f33152550dd378dc1e736c585ee267ef0c1c` passed 233 local tests, the complete local-first browser suite, and Integration Gate run `42016964859`. PR #210 merged as `1d6977a61237c6554e6406a63315eee2c3f17a1f`; PR #209 was closed as superseded. Canonical main was synchronized and the completed task checkout was recoverably quarantined, with refs and objects retained.
- The browser proof at that exact source covers both plan contracts, Buy/Build and Scenario modes, contract-scoped values, pivot and atomic metadata headers, the live dictionary route, local worksheet round-trips, stale-result suppression, route-exit clearing, offline mobile journeys, and no SME service writes. Earlier candidate UI observation also exercised nested collapse/expand. These are bounded implementation checks, not independent product acceptance or full guideline parity.
- Graph's shared-collapse source `8a51ed828a9f7da0c7a5c58eaa873fb41462cdb7` passed its protected checks and merged through PR #1888 as `6e353ce3c1ec21872e9dd3a3c7abc4eefb2b216d`. Its canonical checkout was synchronized. The earlier isolated preview loaded without console errors, but its workspace data-view interaction was not reachable; no additional candidate table interaction is claimed.
- Carried local observations: the Base demo rendered its Multi-dimensional Table and bulk collapse/expand controls; the Design System registry rendered its owner catalog without console errors. These observations are not deployment receipts.
- Revision 1.4.3 consolidates the universal plan-contract draft and the older workflow draft into this single current PRD. Original authoring copies and patches are retained privately for recovery. Deployment, independent acceptance, user validation, and owner-guideline conformance remain unclaimed.

## 6. Risks and mitigations

| Risk | Mitigation |
|---|---|
| Users read derived arithmetic as a prediction | Label the draft and formula; show unknowns and caveat beside outputs |
| A changed field breaks editor, table, exports, or tools | Generate those views from the same protocol and version worksheet schemas |
| Narrow screens hide fields in a wide table | Reuse Base's touch-accessible scroll and pivot; avoid page-level horizontal overflow |
| Evidence labels appear to certify facts | Use descriptive provenance only and display “not authenticated” |
| Multiple surfaces drift | Single tool registry/evaluator and adapter parity; exact guideline revision/anchor map in the protocol-backed dictionary; no compatibility aliases for removed task-specific tools |
| Offline cache contains mixed versions | Include the protocol module, dictionary, and editor in the same release manifest and reject identity mismatch |

## 7. Traceability

| Requirement | Implementation owner |
|---|---|
| Both plan contracts, shared modes, fields, models, evidence tasks, examples, and workflow columns | `public/local-first/sme-pack-business-plan.js` |
| Protocol, tool schemas, validation, model, and exports | `public/local-first/sme-business-pack-core.js` |
| E2E table, route, compare, and worksheet UI | `public/local-first/sme-business-pack.js` |
| Protocol-driven input and evidence editor | `public/local-first/sme-workflow-editor.js` |
| Live dictionary projection | `public/local-first/sme-pack-dictionary.js` |
| Codebook and stable-key definitions | `docs/sme-business-pack-codebook-and-data-dictionary.md` |
| Local/MCP/WebMCP adapter | `src/local-first/sme-business-pack.ts` and existing browser registration |
| Grid and token reuse | Existing `agentic-base` adapter and generated Design System Commerce tokens |
