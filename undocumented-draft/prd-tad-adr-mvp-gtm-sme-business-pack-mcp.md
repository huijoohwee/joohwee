---
title: "SME Business Plan Workspace — E2E Pitch, Plan, and Financial Model"
doc_type: "PRD-TAD-ADR-MVP-GTM"
version: "1.5.1"
date: "2026-11-06"
lang: "en"
owner: "Product Manager function"
continuity_id: "sme-business-pack"
local_rung: "undocumented"
delivered_rung: "undocumented"
lane: "authoring"
universal_scope: true
lifecycle_status: "in-progress"
prd_revision: "1.5.1"
tad_revision: "1.5.1"
adr_revision: "1.5.1"
mvp_revision: "1.5.1"
gtm_revision: "1.5.1"
load_policy: "on-demand"
source_docs: "prd-tad-adr-mvp-gtm-guidelines.md@3.4.0; pitch-deck-guidelines.md@1.2.0; business-plan-guidelines.md@1.1.0; financial-model-guidelines.md@1.1.0; prd-tad-adr-mvp-gtm-venture.md@2.1.3"
---

# SME Business Plan Workspace — E2E Pitch, Plan, and Financial Model

## Document control

Join key: `sme-business-pack@1.5.1`. This document is the sole current product, architecture, decision, MVP, and go-to-market contract for the SME planning workspace. It defines two selectable plan contracts inside one E2E workflow: a general business plan and an SME takeover checker. Both use one versioned protocol interface, tool registry, table, editor, evidence model, and worksheet flow; their declared fields and calculation models remain contract-owned. There are no duplicate workflow variants or parallel registries. Pitch, plan, and model requirements are consumed from the exact shared guideline revisions in `source_docs`; this PRD and the live schema link to those owners and report MVP support without copying their taxonomies or creating a second rules registry.

- **Status:** implementation integrated and locally verified; production delivery and independent product acceptance remain open. Commerce PR #212 implements §1.8 in the existing owners. This document records the current evidence and remaining gates in §5.6; it does not claim 100% runtime readiness. PRD, TAD, ADR, MVP, and GTM all consume `sme-business-pack@1.5.1`.
- **Audience:** people preparing or reviewing an early business or venture plan, including founders, operators, and advisers.
- **Scope:** organize user-entered information into a twelve-role pitch outline, business-plan prompts, single-period arithmetic, and a neutral acquisition review from opportunity context through questions and handover preparation. Extend the existing takeover contract in the same table; retain the general plan. This is a planning workspace, with no transaction execution or complete guideline-conformance claim.
- **No external source dependency:** the product neither searches nor fetches planning, market, pricing, company, or business data.
- **Canonical implementation:** existing local-first SME workspace and shared Multi-dimensional Table, protocol/evaluator, codebook, and dictionary in `agentic-commerce-os`.

## 1. Product requirements

### 1.1 User need

People preparing a business plan need one place to organize the venture narrative, assumptions, evidence notes, financial inputs, deterministic arithmetic, and open questions. Inputs are often incomplete and must remain distinguishable from calculated values and independently verified facts.

### 1.1a Buyer pain, reuse, and priority

Priority is a product hypothesis from the requested workflow, not measured demand or a recommendation between businesses. Each row joins the same enhancement in §1.8.

| Priority / pain | Hook → break → native fix → close | Minimum change / value hypothesis |
|---|---|---|
| P1 — Buyer cannot tell what an acquisition amount includes | Enter an opportunity → price lacks scope and obligations → reuse transfer structure, included/excluded items, location and cash inputs → review unknowns before preparing questions | Existing takeover model plus context fields; avoid repeated copying and double-counting |
| P2 — Buyer cannot compare the basis of supplied figures | Place two options side by side → estimates and historical periods appear comparable → retain currency checks and expose basis/period differences in existing coverage and next checks → export an explicit clarification list | Reuse one ordered comparison and evaluator; no valuation, ranking or inferred normalization |
| P3 — Buyer loses the next action between review and handover | Prepare a discussion → permission, accounts access, team continuity and support are unstructured → record user-stated states and one next action in the same row → export the worksheet for the user's own follow-up | Thirteen optional fields, existing editor and exports; no messaging, CRM or second checklist |

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

Coverage describes mapped requirements and supplied inputs within each projection's MVP scope, not full conformance, quality or authentication. Pitch roles trace to declared input/output keys; missing content stays explicit and roles may be combined in a final presentation. General-plan Buy/Build requires `buy_existing`, `build_new` or `undecided`; acquisition/transition costs stay separate from build costs. Takeover uses the scope, operating, location and handover fields and four arithmetic outputs in §1.5. Unknown obligations remain distinct from not applicable. Scenario mode keeps the selected contract's fields/model without requiring a Buy/Build path.

The Data dictionary is a separate read-only route and table because it documents the contract, including projection owner revisions, requirement anchors, mapped input keys, and current support status. It does not run a second workflow or calculate a parallel report. It is generated from the live protocol and lists the canonical shared owners for invocation, `/`, `#`, `@`, skills, MCP, WebMCP, and AgenticRAG terms.

### 1.5 Data and financial model

The integrated protocol is `sme-business-plan/protocol/v3`, selecting `sme.business-plan@2.3.0` or `sme.takeover-checker@1.2.0`. Both declare Buy/Build as default and Scenario as selectable. General plan maps exact owner revisions/anchors and declares twelve pitch roles, nine shared workflow columns and four scoped coverage outputs. Takeover declares acquisition, operating and location context, working capital, cash and four calculated outputs. Both retain unknowns and explicit user-loaded examples. Section 1.8 records the implemented takeover delta. The last observed public deployment still serves `1.1.0`; source integration and production identity are distinguished in §5.6.

Money accepts a single nonnegative amount or a low/high range, up to four decimal places and a bounded maximum. Calculations propagate ranges. Currency is selected per row as a three-letter code; a comparison with mixed or absent codes is refused. Comparison also uses one shared workspace mode. The implementation does not look up, convert, or compare purchasing power.

The general-plan model exposes single-period revenue, variable cost, contribution, operating costs, operating result, break-even volume, cash runway, entered-runway funding need, and the difference between proposed funding and that modeled need. The takeover model exposes cash required to close and fund the selected period, remaining location payment exposure, shortfall against available cash, and user-entered monthly revenue less listed costs. The latter is arithmetic only and is not reported as profit. No calculation estimates a transfer amount from asset age, lease duration, earnings evidence, or a fixed assumption. Outputs are not forecasts, valuations, linked statements, price opinions, or guideline Headline Registers. An output stays unknown when prerequisites are missing or ambiguous. The formula, required inputs, model state, and owner alignment are available through the table and dictionary.

### 1.6 Evidence and privacy

Evidence is attached to a declared input field. Its provenance values describe how the user recorded context and are not authentication tiers. No name, contact, URL, document upload, or image is accepted as evidence. Short text fields reject URL, email, and phone patterns. Nothing is persisted or transmitted during a local plan build.

### 1.7 Non-goals

The MVP does not provide a market research feed, benchmarks, automated forecast, legal/tax/accounting/investment/financing advice, valuation, loan application, company registry, venture database, investor matching, public listing, payment, fundraising transaction, publishing, or agent-controlled execution. It also does not implement the guideline owners' full Variant Registers, Claim Manifest or Section Claim Record, two-method market sizing, structured business risk/review lifecycle, linked income/cash-flow/balance-sheet statements, Base/Downside/Upside model, Headline Register, actuals/variance, or ADLC Cost Ledger. The pitch output is a twelve-role structured outline and local worksheet, not a rendered slide file or investor endorsement. Each section shows its source field keys; missing text remains explicit and is not generated.

### 1.8 Native acquisition review enhancement — implemented in source

**DIR-SME-16:** Context: the prior takeover table lacked structured review context; §5.6 records the implemented candidate and remaining delivery/acceptance gates. Intent: a prospective owner can prepare one reviewable acquisition worksheet without re-entering the same facts elsewhere. Product Manager function specifies the native enhancement; Commerce owns implementation; the outcome is MVP-16–21. This directive does not grant publication, outreach, payment or runtime deployment effects.

The implemented E2E path is **capture user-owned opportunity context → describe transfer scope → enter amounts and their basis → inspect cash and unknowns → prepare questions → record the user's review stage and handover context → export/read back**. These are field groups and states of the existing table, not routes, wizard steps, new contracts or workflow variants. The default general plan, Buy/Build and Scenario remain as defined in §1.4. No automated discovery, public catalog or seller contact is introduced.

The implementation extends `sme.takeover-checker` from `1.1.0` to `1.2.0` and retains protocol envelope `sme-business-plan/protocol/v3`, model `takeover-cash/v1`, general contract `2.3.0`, the four tool names, and both modes. The thirteen additions below are optional. Blank is unknown; all text retains current privacy-pattern validation. Enum states are user assertions, never verification. These keys extend the existing protocol; the protocol/codebook owns their descriptions. Whitespace-only text is unknown after length and privacy validation; imports normalize it identically, and blank evidence values are refused. Inherited object-property names are unsupported field keys.

| Group | Stable key / existing type | Bounds or values / meaning |
|---|---|---|
| Opportunity | `opportunity_label` / text | ≤80 characters; private alias, not an identity or public business name |
| Opportunity | `business_activity` / text | ≤120; user-described activity, no fixed sector taxonomy |
| Opportunity | `operating_area` / text | ≤120; broad user-described area or remote operation, no address or geolocation lookup |
| Opportunity | `transfer_reason` / text | ≤280; user-recorded reason, no inference about the seller |
| Buyer context | `buyer_budget` / money | Existing single/range limits and row currency; stated spending ceiling, distinct from `available_cash`; never enters cash-to-close or shortfall |
| Buyer context | `target_handover_months` / integer | 0–120 months from the user's review; desired timing, distinct from existing `handover_months` support duration |
| Buyer context | `operator_experience` / enum | `none_reported`, `related_reported`, `direct_reported`, `unknown`; no buyer score or eligibility decision |
| Review | `accounts_access` / enum | `not_requested`, `requested`, `reported_available`, `reviewed_by_user`, `reported_unavailable`, `unknown`; no documents ingested or authenticated |
| Review | `permission_transfer_status` / enum | `not_applicable`, `not_checked`, `reported_transferable`, `reported_new_application`, `conditional`, `unknown`; user-stated operating permission context, not legal clearance |
| Transition | `team_continuity` / enum | `not_applicable`, `not_discussed`, `reported_continuing`, `reported_changing`, `unknown`; no person/contact records |
| Transition | `support_scope` / text | ≤280; what the user reports is included in existing `handover_months`; no contract generation |
| Review | `review_stage` / enum | `captured`, `clarifying`, `reviewing`, `handover_planning`, `paused`, `closed_by_user`, `unknown`; manually selected, reversible, no automatic progression or acquired/paid state |
| Review | `next_action` / text | ≤280; one user-authored follow-up note, preserved separately from generated `next-checks`; no reminder or outbound action |

Reuse `transaction_structure`, `purchase_price`, `included_items`, `excluded_items`, `financial_basis`, `financial_period_months`, `location_obligation`, `location_assignment_status`, `location_renewal_months`, and `handover_months` unchanged. A premises-only case uses `asset_transfer` plus the user's scope description; do not create an assignment pack or alias price field. Unknown business revenue remains unknown. Renewal is context and does not extend the arithmetic term automatically. Explicit zero purchase price is permitted; it does not zero transition, deposit, location or working-capital costs. Additional outlays must exclude amounts already included in the purchase price.

Extend the contract's current evidence prompts and next-check field mapping for accounts, operating permissions, team and support. The existing `next-checks` output names missing context and asks the user to clarify it; it must not instruct a legal conclusion, declare diligence complete or duplicate `next_action`. Evidence stays attached to field keys and within the existing 40-record cap. Show the user-recorded basis and period beside each operating result; when comparing different, missing or `unknown` bases/periods, the existing coverage/next-check output says that operating figures are not comparable on the supplied basis. Retain each row's arithmetic and cash checks, A/B/C order, and the current currency/version refusal. Do not refuse unrelated cash checks, annualize figures, manufacture profit, or add a ratio/valuation engine.

Changing any input or evidence invalidates the report. Rebuilding must recompute checks from the current row, not a stale selection or earlier contract. A review-stage edit never satisfies a missing prerequisite. Exports carry the same field keys, mode, contract version, evidence and visible unknowns; an explicit import validates all rows before replacing current state. Existing strict version refusal remains: a `1.1.0` worksheet cannot silently become `1.2.0`. Explain the mismatch and retain the current worksheet; any later migration requires one explicit tested owner path, not parallel evaluators or compatibility aliases.

## 2. TAD — architecture

### 2.1 Reference implementation — components and ownership

Current reference implementations; user-facing contracts remain neutral and portable.

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

### 2.2a Grounded reuse, dependency direction, and size gate

Baseline Commerce source is `45d8803fc13cb66d1fbce482bae491bab5ad1b10`; source paths in this document resolve there unless a different owner/revision is named. Read source at the pinned commit before implementation; refresh only changed ownership or contracts.

| Owner / inspected contract | Existing consumer / decision | Smallest delta / check |
|---|---|---|
| Commerce `public/local-first/sme-pack-business-plan.js`: `TAKEOVER_PACK` | Core, generated editor, workflow and dictionary / **extend-owner** | Add §1.8 fields and prompts once; no general-plan schema growth; inspect protocol and field-key uniqueness |
| Commerce `sme-business-pack-core.js`: `loadPack`, `TOOL_NAMES`, `invokeSmePackTool` | Browser, `scripts/sme-business-pack-local.mjs`, `src/local-first/sme-business-pack.ts` / **extend-owner** | One contract version update and basis-aware next checks; same limits, errors, local evaluator and transport schemas |
| Base `0cd7602d0b968bf27ecdaee0d8726138bf7997df`: `packages/views-react/src/browser/DataViewBrowserAdapter.tsx`, `mountDataView`, `DATA_VIEW_BROWSER_LIMITS`; `table/MultiDimTableView.tsx` | Commerce pinned `config/agentic-base-data-view.json`; shared table family used by Graph / **reuse** | No renderer edit or consumer fork; `verifyAgenticBaseDataView()` validates pinned artifact hashes and offline boundary |
| Design System `c18253b35e8bcc0bed548cfb717ec31909422dbe`: `site/tokens/commerce-profile.json`, `scripts/commerce-profile.mjs` | Generated `commerce-theme.css`, existing shell and Base theme slots / **reuse** | No hardcoded alternate theme; `verifySharedThemeOwner()` and narrow-screen inspection |
| Commerce `sme-business-pack.js`, `sme-workflow-editor.js`, `sme-pack-dictionary.js` | Existing `#sme-workflow` and `#sme-dictionary` / **reuse**, minimal owner edits only if needed | Protocol-derived field editor, table, exports and read-only documentation; existing `test/local-first/sme-comparison-browser.mjs` |
| OS runtime and dictionary owners already linked by the protocol | Existing invocation surfaces and release path / **reuse** | No new `/` command, `@` resolver, `#` route, skill, MCP server or WebMCP tool; unsupported optional transport remains explicit |

Dependency direction remains portable protocol/model → existing transport adapters or browser projection → Base renderer and Design System tokens. Browser-safe modules import no CLI, filesystem, provider SDK or sibling-repository source. Reuse exact generated artifacts; future generic fixes belong in their shared owner and arrive through reviewed pins. No extraction is needed for this domain delta.

The integrated workflow module is 578 lines; its protocol-generated projection remains the owner and every edited source module stays below 600 lines. Do not add a replacement renderer to bypass that limit.

**Capacity gate:** the current general plan uses all **64** columns: row label + 28 inputs + mode + 9 workflow + 4 coverage + 9 model + 12 pitch. Takeover now uses **54**: row label + 38 inputs + mode + 9 workflow + 1 coverage + 4 model, leaving ten under the existing ceiling. Retain Base's 1,000-row, 4,096-character-cell, 196,608-byte payload and depth 1–8 limits, plus Commerce's one-to-three options and 32/64 KB tool bounds. Check worst-case Unicode, three rows and 40 evidence entries per row against every bound; if they do not fit, fail clearly with retained input and an actionable limit. Do not silently truncate, raise caps, duplicate the renderer or hide required fields to make a check pass.

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

- **ADR-011 — Extend the current takeover contract:** choose thirteen optional protocol fields and reuse the current table/editor/export path. A third contract, marketplace, CRM and parallel checklist are rejected because they duplicate workflow ownership and exceed the local planning scope. Consequence: implemented `1.2.0` is not readable as `1.1.0`; strict import refusal preserves existing data. Recovery uses the prior compatible artifact and its worksheet version.
- **ADR-012 — Context does not authorize or price a deal:** keep buyer budget, stages, access and handover context separate from available cash and deterministic formulas. Reuse coverage/next checks for comparability warnings. Automated screening, scoring, valuation and stage-driven execution are rejected; uncertainty remains visible. Roll back the whole protocol/model/UI artifact if these semantics diverge.

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

MVP-01–15 retain their existing scope and evidence limits. MVP-16–21 have candidate-bound engineering evidence in §5.6, including local rollback compatibility. This closes the observed implementation gaps; it does not substitute for exact production readback, a production rollback receipt, full accessibility evaluation, native WebMCP availability, or the independent walkthroughs in §5.3a.

| ID / pain / design / decision | Given → when → then; required proof |
|---|---|
| MVP-16 / P1,P3 / §1.8, §2.2a / ADR-011 | Given the takeover contract, when loaded, then all thirteen optional fields appear once in the same editor, table, dictionary and four existing tool surfaces; general plan stays unchanged and no third contract/route appears. Inspect protocol, unique keys, imports, desktop and 360-pixel UI. |
| MVP-17 / P1 / §1.8 / ADR-003,006,012 | Given zero purchase price, ranges, missing amounts, unknown or not-applicable location, when built, then current formulas preserve explicit zero, uncertainty and conditional prerequisites without double-counting. Altering context/budget/stage alone leaves numeric outputs identical. Deterministic fixtures plus UI readback. |
| MVP-18 / P2 / §1.8 / ADR-012 | Given two or three rows with differing/missing bases or periods, when compared, then each operating figure retains its basis and a non-comparability check; cash checks remain usable and entry order stays fixed. Mixed/missing currency or version still refuses comparison. Browser plus local/MCP adapter parity fixtures. |
| MVP-19 / P3 / §1.8 / ADR-005,008,012 | Given user-stated accounts/permission/team/support states, when rebuilding or changing stage, then next checks update without authentication or automated progression. Manual next action survives pivot, collapse and exports; contact/URL patterns fail and no service request occurs. UI, network and storage inspection. |
| MVP-20 / P1–P3 / §2.2a / ADR-007,011 | Given three bounded rows and maximum evidence, when rendering/exporting, then takeover has 54 unique columns, general plan 64, all adapter/tool byte limits hold or fail explicitly without losing inputs, and only the table scrolls at 360×780 and 1440×1000. Keyboard, touch, pivot, nested/bulk collapse and offline checks must pass on the same candidate. |
| MVP-21 / P1–P3 / §1.8, §5.4 / ADR-008,011 | Given a versioned worksheet, when round-tripping JSON/CSV/Markdown or printing, then current fields/mode/evidence match; malformed/older input leaves current state intact. Delayed results cannot overwrite contract changes or route exit; cached reload uses one artifact version. Validate import negatives, exports, reload, route races and rollback compatibility. |

## 4. MVP boundary and operating requirements

- Free-tier and FOSS use only; no paid API, add-on, overage, or recurring account.
- Existing dependency graph only; 0 new packages and 0 new runtime services.
- Individual source modules remain below 600 lines; emitted chunks remain below 500 KB.
- Route-load only the existing SME feature modules; keep unrelated application surfaces lazy.
- Support keyboard, touch, narrow mobile widths, system zoom, and offline shell usage.
- Fail loudly on invalid contract identity, malformed ranges, unsupported field keys, oversized requests, and stale route results.
- Implementation measured against baseline `45d8803`: +43,980 net bytes across six existing Commerce source/test/document files; 0 new modules, packages, services or always-load bytes. This replaces the earlier ≤20 KB planning estimate; the largest edited source module is 578 lines and the verified Worker bundle is 458,500 bytes.
- Final reconciliation sprint: one existing PRD, ≤8 KB net growth, <600 lines, 0 runtime modules/dependencies; target 15 active minutes after preflight. The initial implementation and audit remediation were bounded separately; refresh scope/time on drift.
- Runtime delivery has no ETA while a required effect approval or current provider $0/headroom proof is missing. Preserve the current checkout profile, prepared candidate and rollback predecessor; recheck the missing condition rather than claiming delivery.

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

### 5.3a First-dollar validation — hypothesis only

Buyer: an owner-operator reviewing one to three supplied opportunities. Channel hypothesis: an opt-in operator walkthrough; no outreach is performed here. Demo: capture → unknown cash inputs → basis mismatch → next action → export in under five minutes. Automated fixture timing is recorded in §5.6; human completion time and the five-session target remain unmeasured.

Proposed experiment: five consented sessions using fictional or participant-owned inputs; success requires at least four participants to export a worksheet, identify an unresolved obligation, and distinguish an estimate from a historical figure without assistance. Record only opt-in aggregate completion/time/confusion, no worksheet contents. If fewer than four succeed or anyone interprets a stage as clearance, simplify the owner projection before adding features.

Price hypothesis: optional one-time **USD 1 assisted worksheet setup**, separate from the free tool, advice and transaction fees. No payment is taken or revenue established. A later first-dollar claim needs an actual receipt plus observed delivery effort; no paid infrastructure, addons or overages are needed.

### 5.4 Release and rollback

Follow `agentic-os/docs/RELEASE-WORKFLOW.md` and the repository's release/deploy/rollback procedures. Preserve source lane and artifact receipts. A green local preview does not grant publication, merge, or deployment authority. The integrated runtime change uses Commerce `scripts/local-first-release/{artifact,authorization,deployment,rollback-browser}.mjs` and `docs/production-runtime.md`, with the selected deployment workflow loaded on demand. Source PR #212 is merged; production remains a separate protected effect on its exact merged revision. Retain the existing live checkout configuration and its authenticated nonsecret provisioning/reader receipts; the SME change neither creates a payment nor changes checkout policy. Rollback restores the exact last known-good complete artifact (protocol, model, UI, styles, manifest and service worker) and verifies route/assets/offline readback; do not leave a partial schema/UI mismatch live. Preserve both worksheet versions as user-owned files and reject unsupported imports; do not rewrite them during rollback.

### 5.5 Retained source history (2026-11-05)

Revision 1.4.3 consolidated the plan/workflow drafts. Its Commerce candidate `f593f33152550dd378dc1e736c585ee267ef0c1c` recorded 233 local tests and Integration Gate `42016964859`, then merged through PR #210 as `1d6977a61237c6554e6406a63315eee2c3f17a1f`. Graph shared-collapse merged through PR #1888 as `6e353ce3c1ec21872e9dd3a3c7abc4eefb2b216d`. Earlier Base/Design System demos rendered; Graph table interaction was not reached. These retained observations establish no fresh check, deployment or independent acceptance.

### 5.6 Current implementation, runtime evidence and open gates (2026-11-06, Asia/Singapore)

**Development:** Commerce candidate `7d8b97b4db8774aeb6b8fe220e7620097c22dd4a` passed its applicable local integration gate and hosted [Integration Gate 42136769853](https://github.com/huijoohwee/agentic-commerce-os/actions/runs/42136769853). [PR #212](https://github.com/huijoohwee/agentic-commerce-os/pull/212) is merged as protected main `6d0693f03ac16b5d99e5c6c897ad9625b322187d` and canonically synced. It extends the existing protocol, evaluator and workflow, updates their codebook and two existing test owners, and introduces no additional workflow variant.

| Check / acceptance | Observed result and boundary |
|---|---|
| Applicable integration checks / MVP-10–12 | All five selected groups passed: ADLC, evidence contract, typecheck, unit and named checks. The named checks include 233 local-first tests and the browser suites; six unaffected groups were not selected. Seventeen focused shared SME tests passed, including local/worker/MCP parity. This is affected-scope proof, not every repository task or production proof. |
| Protocol, arithmetic and context / MVP-16–19 | All thirteen fields appear through the existing protocol, editor, table, dictionary and exports. General plan stays `2.3.0`; takeover is `1.2.0`. Fixtures cover zero/ranges/unknowns, context-invariant arithmetic, basis/period warnings, currencies, user-stated stages and current next checks. Empty/whitespace text stays unknown across direct calls and JSON/CSV/Markdown imports; invalid evidence and unknown/inherited keys fail without replacing current state. |
| Browser and capacity / MVP-01–09,13–14,20 | Desktop 1440×1000 and mobile 360×780 preserve inputs and have no page-level horizontal overflow. General plan has 64 unique columns and takeover 54. Three-row/40-evidence-per-row checks, explicit byte-limit refusals, keyboard, touch, pivot, individual/bulk collapse, dictionary and all worksheet formats passed. First fixture report: 1,934 ms; zero SME service calls. Fixture timing is not human time-to-value. |
| Native zoom and shared owners / MVP-11,15,20 | Actual Chrome 200% zoom retained table access without page overflow; viewport became 600×458. Base artifact integrity/offline checks and Design System token/icon ownership passed. Live Graph table individual collapse changed 266 rows to 261 and back; grouping changed L2 to None, filtering to eight rows cleared back to 266, and bulk collapse changed 266 to 28 and back. No Base, Design System or Graph source changed; Graph interaction is a separate live-surface observation, not candidate-SHA proof. |
| Race, offline and rollback compatibility / MVP-09,21 | Contract/mode changes, delayed results, route exits, strict version refusal, atomic imports, cached reload and offline rebuilding passed. Local complete-artifact rehearsal on one origin switched takeover `1.2.0` → retained `1.1.0` → exact `1.2.0`; both exported worksheets retained their digests and cross-version imports left existing input intact. This is local compatibility evidence, not a production rollback activation/receipt. |

Evidence: workspace `output/sme-runtime-readiness-implementation-20261106/` contains `validation.json`, `candidate-7d8b97b/`, `native-zoom.json`, `graph-proof.json`, `rollback-local.json`, retained worksheet files/screenshots, the build artifact, source closeout and exact release inputs. The earlier audit under `output/sme-runtime-readiness-audit-20261106/` remains the historical before-state. The implementation fixes its blank-text and inherited-key findings and closes its local Graph, zoom and rollback evidence gaps. Native WebMCP was unavailable in the inspected browser; shared-adapter parity and graceful local fallback were verified without claiming a native registration run.

**Production Release:** [preparation run 42138564108](https://github.com/huijoohwee/agentic-commerce-os/actions/runs/42138564108) targets exact main `6d0693f03ac16b5d99e5c6c897ad9625b322187d` with the existing live checkout selection and retained reader. The nonsecret provisioning receipt recovered from the prior successful run matches its retained digest. Production approval is a separate actual repository-owner environment review. Current provider Free-plan, hard-cap and headroom proof is still required: the available local token returned 403 for account subscriptions/settings. Do not approve or activate the release on that missing proof; no paid plan/add-on/overage is permitted.

**Runtime:** the last observed public source remains `45d8803fc13cb66d1fbce482bae491bab5ad1b10`, Worker version `e6125f69-5df5-4fb2-a75c-21ed49e27024`, takeover `1.1.0`, from prior release `42123513258`. No production activation, payment, production rollback or new-version public readback is claimed by this checkpoint. Reobserve source/version/assets and run the owner browser checks after any authorized promotion; retain its exact completion and rollback predecessor.

**Remaining work / next owner action:** complete candidate preparation, supply current $0/headroom proof and the actual protected environment approval, then verify exact public identity and SME behavior. Separately conduct the five consented sessions in §5.3a; no participant outcome, revenue or independent product acceptance is fabricated. The sole planning successor is this section in this existing continuity record; no alternate PRD or runtime variant is created. Full delivery remains open until these applicable gates have evidence.

## 6. Risks and mitigations

| Risk | Mitigation |
|---|---|
| Users read derived arithmetic as a prediction | Label the draft and formula; show unknowns and caveat beside outputs |
| A changed field breaks editor, table, exports, or tools | Generate those views from the same protocol and version worksheet schemas |
| Narrow screens hide fields in a wide table | Reuse Base's touch-accessible scroll and pivot; avoid page-level horizontal overflow |
| Evidence labels appear to certify facts | Use descriptive provenance only and display “not authenticated” |
| Multiple surfaces drift | Single tool registry/evaluator and adapter parity; exact guideline revision/anchor map in the protocol-backed dictionary; no compatibility aliases for removed task-specific tools |
| Offline cache contains mixed versions | Include the protocol module, dictionary, and editor in the same release manifest and reject identity mismatch |
| Added fields overflow Base or tool limits | Apply the explicit 64/54-column budget and worst-case byte checks; retain input on refusal |
| A review stage or permission label is mistaken for clearance | Keep user-stated status and missing prerequisites visible; stages never authorize an effect |
| Conflicting plan copies or parallel registries reappear | Amend this continuity record in place; extend the existing protocol/codebook once; no alternate PRD, route, pack, evaluator or token inventory |

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
