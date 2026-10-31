---
title: "SME Business-Pack Service — Takeover Cash-to-Close Check (Buyer Side)"
doc_type: "PRD-TAD-ADR-MVP-GTM"
version: "0.9.1"
date: "2026-10-31"
lang: "en-US"
owner: "Product Manager function"
continuity_id: "sme-business-pack"
local_rung: "undocumented"
delivered_rung: "undocumented"
lane: "authoring"
universal_scope: false
lifecycle_status: "proposed"
source_docs: "prd-tad-adr-mvp-gtm-guidelines.md@3.4.0"
---

# SME Business-Pack Service — Takeover Cash-to-Close Check (Buyer Side)
## Document Control
Join key: `sme-business-pack@0.9.1`. PRD, TAD, ADR, MVP and GTM are addressable here, with the evidence register and open findings at the end. **Clean slate**: rewritten from one wedge. Version 0.7.0 is consumed only for document conventions and for observations carried into the [Evidence register](#evidence-register) (marked *carried*); every fact carries its own source join (S-ids).

- **Revision 0.8.0** (2026-10-27): rewritten around one buyer-side offer, **the takeover cash-to-close check**: before an offer on a small Singapore F&B outlet, the buyer learns (1) the total cash needed to take over and open, (2) the lease exposure, and (3) how much of that cash rests on claims nobody has checked. The service analyses the buyer's own claims. It does not list, host, introduce, match, route, negotiate, reveal contacts, value, hold funds or charge anything tied to a deal (green zone, ADR-007). Introduces PP-01..PP-05, US-01..US-13, VCC-01..VCC-19, ADR-001..ADR-009, HG-01..HG-07, VH-01..VH-05, A01..A12, F-01..F-11, S-01..S-16.
- **Revision 0.9.0** (2026-10-31): adds a gated, fixed-row comparison of two or three buyer-entered claim sets in the existing SME workspace; it reuses the same pack and evaluator and does not rank or recommend. Adds PP-06, US-14..US-15, VCC-20..VCC-25, ADR-010, VH-06, F-12, S-17. **Revision 0.9.1** (2026-10-31): merges the Singapore cash-to-close integration plan and local candidate evidence; reserves VCC-20..VCC-23 for shell identity, surface parity, Singapore-only discovery and legacy compatibility, and renumbers comparison VCCs to VCC-24..VCC-29. Adds S-18; neither candidate checks nor this draft constitute acceptance or delivery proof.
- **Changed from 0.7.0**: the money question becomes the product (budget engine, lease exposure, unchecked share); the plan is ordered by cash at risk; pilot narrows to Singapore F&B (`sg.fnb.takeover`), Malaysia follows after its own legal review (R3); land-bearing packs leave this document; seller and adviser exports become gated later stories; the teaser, stealth and pay-to-reveal ideas are parked behind a legal gate (ADR-008).
- **Status**: draft, **not baselinable** (see [Findings](#findings-and-open-items)). Rungs stay `undocumented`. Alignment cycles used: 0 of 3.
- **Neutrality**: capabilities are named by function; `agentic-commerce-os` is the target host and code-evidence source only. No external asset, service or package is a build or runtime dependency. **The product itself never searches or fetches**.
- **Limitation**: companion guideline modules (templates, verification, readiness, diagram, venture, maturity, lean-startup) were not supplied; their joins follow the index text and are `source=unverified` (F-07).
- **Vocabulary**: pain status `unvalidated` | `demand-proven`; `H` = hypothesis target; `source=unverified` = not checked against a primary source; **claim** = a closed-field assertion about the takeover, taken from any listing source or conversation; **evidence entry** = a closed-field observation or document sighting gathered by a person offline; **provenance** = how an evidence entry was obtained; **tier** = evidence strength T0..T3 (Evidence model); **line** = one cash item in the budget; **retiring tier** = the tier at which a claim counts as checked for its line; **unchecked share** = the share of the planned cash whose lines still rest on claims below their retiring tier (a plain ratio, not a score); **status** = `discrepancy`, `conflicting_evidence`, `no_discrepancy_found` or `unsupported`; **protocol** = reviewer-approved tasks that gather evidence for one claim kind; **plan** = protocol tasks selected and ordered for one claim set.
- **Not advice**: every output is information, never legal, tax, valuation, financing or licensing advice, and never an opinion on whether a price is fair.

### Scope declaration
| | Statement |
|---|---|
| Vision | An agent-callable, offline-capable, zero-spend service that tells a first-time buyer, before an offer, what a small F&B takeover will really cost in cash, what the lease commits them to, and which parts of that cash rest on unchecked claims, then plans the ground checks that retire the largest unchecked amounts first |
| Pitch | **Know your real cash to close, and how much of it nobody has checked.** Works on a listing from any source; needs none of their data |
| Pack | Claim kinds, required fields, budget lines and parameters, evidence protocols with retiring tiers, tolerances, ratio parameters, red-flag rules, checklists and glossary, as versioned data carrying `as_of`, sources and `review_status` |
| Target host | Reuse the existing `agentic-commerce-os` SME workspace route and module owners; S-17 records the inspected revision and the limits of the as-built surface |
| Pilot launch | `sg.fnb.takeover` (Singapore): takeovers of F&B units (cafe, restaurant, coffee-shop or hawker stall) with or without a lease transfer |
| Later | `my.fnb.takeover` (R3, after its own legal review, HG-07); retail packs on demand evidence |
| Evidence rule | Human-gathered and offline: site observation, measurement on foot, documents sighted, written confirmation from a third party. No web search, fetching, scraping or third-party data lookup exists in the service (ADR-004) |
| Green-zone rule | The service analyses the user's own claims and plans the user's own checks. It never introduces, matches, relays, negotiates, hosts, publishes or reveals counterparties; never charges a fee tied to a deal or an introduction; never values, advises or holds funds (ADR-007, VCC-10) |
| 0 (opportunity) | Listings show asking price and sometimes rent or sales; the cash to take over and open is spread across deposits, fit-out and equipment, legal and licence costs, reinstatement and working capital, and the lease commitment is not shown as a number (S-01..S-05). Uncertainty: whether first-time buyers recognise the gap and will pay to close it |
| 1 (target outcome) | One Singapore F&B takeover buyer or adviser pays for an evidence pack or adviser seat, collected, within 60 days of first deploy. Evidence: payment record. Observation: 60 days |
| Won't (this increment) | a directory, marketplace, showcase, teaser, stealth listing or pay-to-reveal feature; hosting or republishing listing text; introductions, matching, contact reveals or message relay; negotiation or any act for a counterparty; fees contingent on a deal or tied to an introduction; sponsored slots; crawling, scraping, web search, URL fetching or third-party data lookup; map, traffic or open-data layers; valuation or price-fairness opinions; legal, tax or financing advice; escrow, deposits or fund-holding; land-bearing packs; China and other Southeast Asian packs; accounting, P&L or payments composition; credential custody; composite scores, sorting, ranking, recommendations or a winner; verdict wording about a listing or a person; storing claims, evidence, images, names, contacts or personal data |

Delivery, first collected dollar and repeat demand each need separate evidence — `blended-status`.

## PRD
### Problem and pain-point mapping
Every pain is `unvalidated` until interviews or payments exist (F-01). Ranked by hypothesised pain × willingness to pay: the buyer carries the cash risk; the adviser repeats the work; the seller's interest is secondary and gated.

| ID | Pain | Who | Today's workaround | Our response |
|---|---|---|---|---|
| PP-01 | The cash needed to take over and open is not stated anywhere: asking price and rent are shown, while fit-out and equipment, deposits, reinstatement, legal and licence costs and opening working capital are not | First-time buyer of a cafe, restaurant or stall | Own spreadsheet, adviser hours, generic checklists (S-05) | A budget engine: claims in, cash-to-close range and the gap above the asking price out |
| PP-02 | The lease is a multi-year commitment that listings do not total, and assignability, landlord consent, remaining term and reinstatement are unchecked | Same buyer | Verbal assurance, lawyer review late in the process | Lease-exposure line (remaining months × rent, with reinstatement) and a landlord written-confirmation task |
| PP-03 | The buyer cannot tell which claims have been checked or how much cash depends on the ones that have not; a portal's "Verified" stamp concerns the listing, not the claims (S-04) | Same buyer | Trust, gut feel | Evidence tiers per claim and the **unchecked share** of the planned cash |
| PP-04 | The buyer does not know what to check first, in what order or with what sampling | Same buyer | Own judgment; consultant feasibility spend (S-05, S-06) | A plan ordered by cash at risk, with a printable worksheet |
| PP-05 | Advisers repeat the same budget and diligence questions by hand deal after deal, and honest sellers cannot show what supports their claims | Fit-out contractor, F&B consultant, accountant; seller | Own checklists; verbal assurances | Same protocol and exports under the adviser's name; a summary the seller shares themselves (Could, R2, gated) |
| PP-06 | A buyer cannot compare two or three takeover options on consistent cash, lease and evidence rows | First-time buyer considering multiple outlets | Separate notes and inconsistent spreadsheets | Compare buyer-entered claim sets against the same pack and evaluator, with unknowns visible and no winner (Should, R1 only after VH-06) |

PP-05 backs Could stories only, so no feature exists without a named pain (`pain-pointless-feature`).

### User stories (MoSCoW)
| ID | Story | Priority | Pain |
|---|---|---|---|
| US-01 | As a buyer, adviser or agent, I list the packs and see the required fields, budget lines, claim kinds and evidence protocol for the right country and asset | Must | PP-01 |
| US-02 | As a buyer, I submit a closed-field claim set from any listing source or conversation and receive missing fields and arithmetic flags | Must | PP-01 |
| US-03 | As a buyer, I receive the cash-to-close range, the gap above the asking price, the opening runway and the lease exposure, each with its lines | Must | PP-01, PP-02 |
| US-04 | As a buyer, I see the unchecked share and which lines rest on unchecked claims | Must | PP-03 |
| US-05 | As a buyer, I receive a plan that orders the ground tasks and documents to request by the cash each would retire, as a worksheet I can print or fill offline | Must | PP-04 |
| US-06 | As a buyer, I enter what I gathered and receive per-claim statuses with tiers, and the budget and unchecked share recomputed | Must | PP-03, PP-04 |
| US-07 | As a buyer, I receive a transfer checklist, only from a reviewed pack | Should | PP-02, PP-04 |
| US-08 | As a non-agent user, I run the same checks in a browser page that works offline and sends nothing | Should | PP-04 |
| US-09 | As an agent, I call the tools on any surface and get identical typed results at zero token cost | Should | PP-01 |
| US-10 | As a bilingual user, I read the same record in en or zh (ms with the Malaysia pack) | Should | PP-01 |
| US-11 | As an adviser, I run the protocol on a client's deal and export the result under my own name, labelled | Could (R2) | PP-05 |
| US-12 | As a seller, I generate a summary of which of my claims have evidence at which tier, and share it myself; the service does not publish, route or reveal it | Could (R2, after HG-07) | PP-05 |
| US-13 | A directory, showcase, teaser, stealth listing, pay-to-reveal, introduction, matching, contact reveal, success fee, scraping, web search, score, ranking, recommendation, winner, valuation or price opinion, escrow, or legal advice | Won't (this increment) | — |
| US-14 | As a buyer, I compare exactly two or three claim sets with the same pack, version, currency and fixed report rows; missing data stays visibly unknown | Should (R1 after VH-06) | PP-06 |
| US-15 | As a buyer on mobile or offline, I use comparison in the existing SME workspace; inputs stay in memory and clear when I leave the route | Should (R1 after VH-06) | PP-06 |

PRD stops at criteria; implementation is in [TAD](#tad).

### Success metrics
Every user-facing feature carries a TTV row (`missing-economics-metric`).

| Metric | Target `H` | Check |
|---|---|---|
| **TTV F1** (budget check): connect to first report, clean environment | ≤ 5 min | VCC-14 |
| **TTV F2** (plan): first report to worksheet | ≤ 2 min | VCC-15 |
| **TTV F3** (evidence): worksheet entries to recomputed budget | ≤ 3 min | VCC-07 |
| **TTV F4** (reviewed checklist) and **TTV F5** (comparison): first report to checklist or fixed-row comparison | ≤ 2 min each | VCC-13, VCC-24, VCC-28 |
| Mapping: pilot users who turn a listing into a claim set unaided | ≥ [60]% | VH-04 |
| Field effort: protocol completed on site by a practitioner | ≤ [3] h | VH-04 |
| Pain recognition: buyers who describe a past takeover where the cash needed exceeded the advertised price materially | ≥ 5 of 10 | VH-01 |
| Willingness to pay: buyers who pre-commit after seeing the free output; advisers who pre-commit | ≥ 3 of 10; ≥ 2 of 10 | VH-02, VH-03 |
| Server-side inference tokens per check | 0 | VCC-01 |

### Verifiable Completion Conditions
The Evaluator is a mechanism separate from the implementer and from every work tree or agent it judges. No VCC is satisfied; each needs an Evidence Reference (invocable check, recorded result, surface).

| VCC | End state | Check | Constraints | Status |
|---|---|---|---|---|
| VCC-01 | `pack.list`, `pack.protocol`, `takeover.budget` and `takeover.plan` consume 0 inference tokens and return pack id, version, `as_of`, `review_status` | invocation log | no server-side model | unsatisfied |
| VCC-02 | `takeover.check` and `takeover.budget` return typed reports in ≤ 2 s p95 on [30] labelled fixtures | fixture suite | zero spend | unsatisfied |
| VCC-03 | Every omitted required claim in the fixtures is reported (recall 100%) | deterministic diff vs labels | schema pinned | unsatisfied |
| VCC-04 | Every planted arithmetic inconsistency (implied sales vs band, rent share, payroll share, break-even above claimed sales) is flagged; in-range figures raise 0 flags | fixture assertions | parameters from the pack only | unsatisfied |
| VCC-05 | **Budget integrity**: the lines sum exactly to the total on every fixture; low ≤ high; an independent re-implementation in C-EVAL matches the engine to the dollar on [30] fixtures; a missing required line yields `incomplete` and a range, never a zero | oracle comparison | ADR-002, ADR-006 | unsatisfied |
| VCC-06 | **Unchecked share**: 100% with no evidence; computed only from lines and retiring tiers; never rises when retiring evidence is added; shown with the lines behind it | fixture suite, monotonicity test | ADR-006 | unsatisfied |
| VCC-07 | Planted discrepancies and conflicts between claims and evidence are all reported (recall 100%); within-tolerance evidence raises 0 discrepancies; a claim with only T0 evidence returns `unsupported`, never `no_discrepancy_found`; the budget recomputes after entries | fixture suite | ADR-004, ADR-006 | unsatisfied |
| VCC-08 | Every report carries "indicative, not verified", pack version, `as_of` and claim counts by tier, including reports with no flag; no composite score, no verdict word and no price-opinion word (for example "fair", "overpriced", "good deal") appears in any output string; documents are labelled "sighted, not authenticated" | wording lint over all outputs | ADR-006 | unsatisfied |
| VCC-09 | Claims and evidence validate against closed vocabularies and numeric bounds; unknown fields are dropped; free text, images, names, addresses, contacts and any URL are rejected: [20] negative fixtures | schema and negative fixtures | ADR-004, ADR-005 | unsatisfied |
| VCC-10 | **Green zone**: no route, field or output string introduces, matches, relays or discloses a counterparty; no field accepts a counterparty's name or contact; no field or flow carries a fee tied to a deal or an introduction | static scan and negative fixtures | ADR-007 | unsatisfied |
| VCC-11 | The local package and the static page complete a full check with 0 network requests; no code path fetches a URL, uses credentials or drives a browser | static scan, egress test | ADR-001, ADR-004 | unsatisfied |
| VCC-12 | No claim, evidence or worksheet content persists on any service surface; counters only in logs | storage and log audit | no accounts | unsatisfied |
| VCC-13 | A pack not `reviewed` returns only completeness, arithmetic and raw differences, with no budget parameters presented as reviewed, no tolerance and no checklist; a pack mismatch is flagged | negative fixtures | gate in C-ENDPOINT | unsatisfied |
| VCC-14 | First report ≤ 5 min from a clean environment | timed run | guest client, no account | unsatisfied |
| VCC-15 | A worksheet exported as Markdown, CSV or JSON re-imports to the identical claim and evidence set (0 lost rows, 0 column drift); the printable worksheet is ≤ [4] pages | round-trip fixtures | one schema | unsatisfied |
| VCC-16 | [3] practitioners run the worksheet on real or mock outlets: ≥ [80]% of tasks completed unaided and median effort within ±[30]% of the estimate | pilot record | HG-06 | unsatisfied |
| VCC-17 | One query fixture returns identical typed results from the local, static-page and remote surfaces; the in-page surface matches where the browser supports it | parity fixtures | adapters generated from C-SCHEMA | unsatisfied |
| VCC-18 | [20] mixed-language fixtures (en, zh) map to the same enums; unmappable values become `unknown` | fixture suite | closed vocabulary | unsatisfied |
| VCC-19 | Simulated [200] remote checks/day stay ≥ [30]% under the runtime's free quota | load script vs current quota | quota re-verified at run date (HG-05) | unsatisfied |
| VCC-20 | Opening `#sme` keeps the existing Commerce document and shell mounted while only the SME workspace slot changes | browser shell-identity check | no second page, router or shell | unsatisfied |
| VCC-21 | Local, WebMCP and optional Worker/MCP calls return the same typed result for identical inputs; local check and budget work offline with zero service requests | cross-surface fixtures and offline browser check | all adapters call one core; no claim/evidence persistence | unsatisfied |
| VCC-22 | R1 discovery and all six tools expose only the Singapore pack; Malaysia remains unavailable until R3 review gates pass | REST, MCP, WebMCP and negative fixtures | no inference about Malaysian legality or readiness | unsatisfied |
| VCC-23 | Existing `pack.required_fields` and `takeover.check_listing` clients receive a parity-tested adapter over the shared core or keep their current contract until migration is reviewed | pinned-client inventory and compatibility fixtures | no duplicate calculations or silent breaking change | unsatisfied |
| VCC-24 | `takeover.compare_claim_sets` accepts exactly 2 or 3 buyer-entered claim sets and returns the same deterministic report for each as an individual check on [30] labelled fixtures | oracle and parity fixtures | same pack evaluator; no inference | unsatisfied |
| VCC-25 | Comparison uses fixed slot order A/B/C and fixed report-row order; unknowns remain explicit; no sort, weight, score, recommendation, rank or winner is emitted | schema, wording and render checks | ADR-010 | unsatisfied |
| VCC-26 | Mixed pack id, pack version or currency is rejected before evaluation; all reports carry the common pack id, version and `as_of` | negative fixtures | no cross-pack conversion | unsatisfied |
| VCC-27 | Comparison accepts no free text, candidate name, URL, contact or address; content is memory-only and clears on leaving the SME route | negative fixtures, storage audit | no persistence or network fetch | unsatisfied |
| VCC-28 | Comparison opens within the existing SME workspace on direct entry, mobile, offline and back/forward navigation; cancelled or late results cannot replace the active route | browser route and race checks | reuse current shell and lazy SME module | unsatisfied |
| VCC-29 | F5 local comparison completes ≤ 2 s; request ≤ 32 KB and response ≤ 64 KB if the existing service adapter is used; 0 inference, 0 new modules/dependencies, ≤ 3 existing feature modules changed, each emitted chunk < 500 KB | bounded local and adapter checks | $0 cap; fail closed on quota or size | unsatisfied |

### Traceability
`PRD-[Epic]-[Story] ↔ TAD-[Component]-[Interface] ↔ VCC ↔ Evidence Reference` — closes in both directions; refinement bounded at 3 cycles.

| PRD | TAD | VCC | Evidence Reference |
|---|---|---|---|
| PRD-Packs-US-01 | TAD-C-ENDPOINT-pack.list, -pack.protocol | VCC-01 | none yet (invocation log) |
| PRD-Check-US-02 | TAD-C-CHECKS-takeover.check | VCC-02..04, VCC-08, VCC-09 | none yet (fixture suite) |
| PRD-Budget-US-03, US-04 | TAD-C-CHECKS-takeover.budget | VCC-01, VCC-05, VCC-06, VCC-08 | none yet (oracle, fixtures) |
| PRD-Plan-US-05 | TAD-C-CHECKS-takeover.plan; C-UI worksheet | VCC-01, VCC-15, VCC-16 | none yet |
| PRD-Evidence-US-06 | TAD-C-CHECKS (comparators, recompute) | VCC-06, VCC-07 | none yet |
| PRD-Check-US-07 | TAD-C-ENDPOINT-takeover.transfer_checklist | VCC-13 | none yet (negative fixtures) |
| PRD-Check-US-08 | TAD-C-UI, C-LOCAL; ADR-009 integration | VCC-11, VCC-14, VCC-15, VCC-20..VCC-23 | S-18 local candidate; evaluator acceptance pending |
| PRD-Check-US-09, US-10 | TAD-C-SCHEMA adapters; C-PACKS glossary | VCC-17, VCC-18, VCC-19 | none yet |
| PRD-Adviser-US-11, PRD-Seller-US-12 | TAD-C-UI exports; C-CHECKS | VCC-07, VCC-08, VCC-10, VCC-15 | none yet; R2 only, US-12 after HG-07 |
| PRD-Boundary-US-13 | TAD-C-EVAL scans | VCC-10, VCC-11 | none yet |
| PRD-Compare-US-14, US-15 | TAD-C-CHECKS-compare; existing Commerce SME route and view | VCC-24..VCC-29 | none yet; VH-06 first |

## TAD
### Component inventory and division of work
One owner per capability — `duplicate-capability-owner`. Reuse decision per component — `component-origin-unstated`.

| Component | Capability owned | Origin | Note |
|---|---|---|---|
| C-SCHEMA | Claim, evidence, budget, report and comparison schemas; pack schema; generated adapters | extend existing contracts | pure, browser-safe, no secrets; comparison slots are A/B/C only |
| C-PACKS | Versioned pack data: required fields, budget lines and parameters, claim kinds, evidence protocols with retiring tiers, tolerances, ratio parameters, red flags, checklists, glossary (en, zh) per jurisdiction × asset family | new (content) | each pack declares `pack_id`, `version`, `as_of`, `sources[]`, `review_status`, `reviewer`; parameters, not constants |
| C-CHECKS | Rule evaluator: completeness, ratio and driver arithmetic, **budget engine**, claim-vs-evidence comparators, unchecked-share computation, plan generator and fixed-row comparison assembly | extend existing SME core in `agentic-commerce-os` | pure and offline; compare outputs from the same evaluator; no ranking logic |
| C-LOCAL | Local stdio package serving the same routes offline | new adapter | primary surface; no network code |
| C-ENDPOINT | Optional stateless routes, input validation, budgets and review-status gate | extend `src/local-first/sme-business-pack.ts` | reuse current MCP/API handler, 32 KB/64 KB/2 s bounds and tool descriptor owner |
| C-UI | Claim form, budget view, worksheet, export/import and comparison view | reuse `agentic-commerce-os` SME workspace route and lazy view | no second document or shell; local inputs clear on route leave |
| C-EVAL | Fixtures, budget oracle (independent re-implementation), wording lint, green-zone scan, egress and static scans | new | held outside the implementer lane |
| C-LEDGER | Usage counters only | new | no content; no second ledger |

### Flows
Notation: Mermaid (`source=unverified` against Diagram Guidelines; class and canvas-projection check names unresolved — F-07). Features: **F1 Budget Check** (`takeover.check` + `takeover.budget`; Must), **F2 Plan and Worksheet** (`takeover.plan`; Must), **F3 Evidence Re-run** (Must), **F4 Transfer Checklist** (Should), **F5 Comparison** (`takeover.compare_claim_sets`; Should, gated by VH-06 and core report VCCs).

**D-01 Journey** (F1–F3)
```mermaid
flowchart LR; A[Find a listing from any source] --> B[Map its claims to closed fields]; B --> C[Get cash-to-close range, lease exposure, unchecked share]; C --> D[Get plan ordered by cash at risk]; D --> E[Gather evidence on the ground, offline]; E --> F[Enter evidence entries]; F --> G[Read statuses, tiers and the recomputed budget]; G --> H{Unchecked share still large?}; H -->|yes| I[Repeat tasks or ask seller, landlord, adviser]; H -->|no| J[Take report to adviser, then decide]
```

**D-02 Workflow** (check and budget)
```mermaid
flowchart TD; A[Validate vs schema, reject free text and URLs] --> B[Completeness]; B --> C[Ratio and driver arithmetic]; C --> D[Budget lines from claims and pack parameters]; D --> E[Sum to range, mark incomplete if a line is missing]; E --> F{Evidence entries present?}; F -->|no| G[All claims unsupported, unchecked share 100%]; F -->|yes| H[Comparators with pack tolerance, assign status and tier]; H --> I[Recompute unchecked share from retiring tiers]; G --> J[Plan generator ordered by cash retired]; I --> J; J --> K[Label indicative, add pack version and as_of]; K --> L[Typed report, budget and worksheet]
```

**D-03 Data flow**
```mermaid
flowchart LR; U[Claims and evidence, on device] --> V[Validator] --> K[Checks and budget]; P[(Packs, read-only)] --> K; K --> O[Report, budget, plan, worksheet]; K -.counters only, remote path.-> L[(Usage log)]
```

**D-04 Topology**
```mermaid
flowchart LR; S[Listing source or conversation, any, out of band] -.read by the user or their agent.-> U[User or agent]; U --> LP[Local package]; U --> PG[Static page, offline]; U -.optional.-> EP[Edge endpoint, stateless]; PK[(Pack files)] --> LP; PK --> PG; PK --> EP
```
**D-05 Comparison (F5)**: accept two or three options, each with pack id/version/currency and closed claims → reject any mismatch → run each through the same evaluator → render fixed A/B/C slots in entry order, with identical rows and explicit unknowns; no sorting, ranking or winner.

### Budget model
All amounts are whole currency units (SGD in the pilot). Each line is a range `[low, high]`: a number the user enters gives `low = high`; a band code gives the band's bounds; a pack parameter gives the parameter's reviewed range. Every parameter carries `as_of`, source and `review_status`. A user may override a parameter with their own quote, which then counts as T0 (stated) or T2 (document sighted).

| Line | Source | Retiring tier |
|---|---|---|
| L1 Takeover price (consideration for the business) | claim `price` | T2 (written offer or agreement terms sighted) |
| L2 Equipment and fit-out purchase | claim `equipment_included`, `equipment_price`; else pack parameter, marked incomplete | T1 (inventory counted on site) |
| L3 Landlord deposit | claim `deposit_months` × monthly rent; else pack parameter | T2 (lease or deposit receipt sighted) |
| L4 Utilities and other deposits | pack parameter | T2 |
| L5 Transfer, legal, licence and registration costs | pack parameter, reviewed | T2 (quote sighted) |
| L6 Immediate repairs and reinstatement provision | pack parameter by fit-out age and handover condition | T1 (condition observed) |
| L7 Opening working capital | `runway_months` (buyer-set, default `[3]`) × monthly fixed cost | T3 for rent, T2 for payroll, per component |

Derived: **monthly fixed cost** = rent + payroll (staff-count band × wage parameter) + utilities parameter. **Break-even monthly sales** = monthly fixed cost ÷ (1 − variable-cost share parameter). **Cash to close** = L1 + L2 + L3 + L4 + L5 + L6 + L7. **Gap above asking price** = cash to close − L1. **Lease exposure** = remaining lease months × monthly rent, shown beside the reinstatement provision. **Opening runway** = working capital ÷ monthly shortfall, where shortfall = fixed cost − contribution at claimed sales; shown only when claimed sales are present, otherwise "not computable".

**Unchecked share** = Σ(midpoint of lines whose claim is below its retiring tier) ÷ Σ(midpoint of all lines), shown with the lines behind it. It is a plain ratio of cash, not a score: it makes no statement about any person or listing and has no threshold. Reports always show the cash-to-close range first and the unchecked share second.

### Green-zone boundary
The service performs analysis for the person using it. The Singapore Estate Agents Act defines estate agency work as work for a client, in the course of business or for a fee, that introduces a third person who wishes to acquire or dispose of a property or that negotiates such an acquisition or disposition; property includes interests in land and "lease" includes subleases and tenancies (S-11). Licensing of agents covers residential, commercial and industrial property (S-12), and acting without a licence is an offence (S-11). A takeover that transfers a lease may therefore engage that regime if the service introduces or negotiates. The boundary below keeps the service on the analysis side; it is a design position for counsel to confirm (HG-07), not a legal conclusion.

| Boundary | Rule | Check |
|---|---|---|
| Introduction and matching | no route, field or output introduces, matches, ranks or recommends a counterparty | VCC-10 |
| Contact and identity | no counterparty name, contact or address is accepted, stored, revealed or relayed | VCC-09, VCC-10 |
| Negotiation | no message drafting, relay or act for a counterparty; outputs are the user's own questions and worksheets | VCC-10 |
| Fees | charged only for software access or an evidence pack; never contingent on a deal, never tied to an introduction, never a commission or referral flowing from a counterparty | VCC-10, HG-03 |
| Listings | the service does not host, publish, mirror or republish listings; the source is an enum | VCC-09 |
| Valuation and price opinion | none; the budget is arithmetic on stated claims and parameters, and wording is linted | VCC-08 |
| Legal, tax, financing advice | none; lease and licence items are raised as questions for a qualified adviser | VCC-08 |
| Funds | none held, escrowed or routed | VCC-10 |
| Personal data | none stored; observation tasks use counts and enums only; reviewer sets privacy rules (PDPA scope unresearched) | VCC-12, HG-02 |
| Malaysia | separate legal review of Act 242 and board guidance before `my.fnb.takeover`; this document makes no claim about it (S-14) | HG-07 |

### Invocation Register
One register for every route. Tool discovery grants no mutation authority; every route is read-only or compute-only. No command-token or alias is bound in the MVP — `orphan-route`, `ambiguous-route`.

| Capability identity | Agent-tool (local, remote) | In-page tool (if supported) | Browser | Mode | Owner |
|---|---|---|---|---|---|
| `pack.list` | yes | yes | yes | read-only, 0 tokens | C-ENDPOINT, C-LOCAL |
| `pack.protocol` | yes | yes | yes | read-only, 0 tokens: required fields, budget lines, parameters, claim kinds, tasks, tolerances | C-ENDPOINT, C-LOCAL |
| `takeover.check` | yes | yes | yes | compute-only: claims and optional evidence in, completeness, flags and statuses out | C-CHECKS |
| `takeover.budget` | yes | yes | yes | compute-only: claims and optional evidence in, cash-to-close range, gap, lease exposure, runway and unchecked share out | C-CHECKS |
| `takeover.plan` | yes | yes | yes | compute-only: claim set in, tasks ordered by cash retired and worksheet out (Markdown, CSV, JSON) | C-CHECKS |
| `takeover.compare_claim_sets` | yes | yes | yes | compute-only: 2–3 compatible buyer-entered sets in, fixed-row reports out; no ranking or recommendation | C-CHECKS |
| `takeover.transfer_checklist` | yes | yes | yes | read-only, review-gated | C-ENDPOINT, C-LOCAL |

### Agent-native surfaces, one schema
C-SCHEMA is the sole schema owner; every adapter is generated from it, never hand-written (`duplicate-owner`).

| Surface | Serves | Network use | Status |
|---|---|---|---|
| Local package (stdio) | agent hosts, offline users | 0 requests | baseline, primary |
| Static files: pack data, worksheet templates, API description, `llms.txt` | any client or agent | 0 outbound from the service | baseline |
| Static page (single file) | people | 0 requests after load | baseline |
| Remote agent-tool server (stateless edge function) | hosts without a local package | 1 per call `H` | optional, hard-capped |
| In-page tools | in-browser agents | 0 | optional: draft standard with limited support (S-16); feature-detect first; never required |

Rules: same capability identities and typed outputs on every surface (VCC-17); default response ≤ 64 KB with pack version, `as_of` and provenance; fields come from closed vocabularies, so no free text reaches an agent as instructions. Comparison preserves A/B/C input order and the common fixed report rows. The client agent that maps a listing into claims does so on the user's side; its inference is outside this service's COGS (ADR-002, ADR-005).

### Evidence model
Evidence is what a person on the ground collects. The service never collects it and never authenticates it.

| Tier | Provenance values | Meaning | Counts toward `no_discrepancy_found`? |
|---|---|---|---|
| T0 | `seller_stated`, `buyer_assumed` | the claim itself, or the buyer's own assumption | no |
| T1 | `observed_on_site`, `measured_on_foot`, `counted_on_site` | one person saw, counted or measured it | yes, if the protocol's coverage rule is met |
| T2 | `document_sighted` | a document was seen, not authenticated | yes |
| T3 | `third_party_confirmed` | written confirmation from the landlord, an accountant, an authority or a supplier | yes |

Rules: a claim's status uses its independent entries (T1 and above). Entries within tolerance give `no_discrepancy_found`; outside tolerance give `discrepancy`; independent entries that disagree give `conflicting_evidence`; none give `unsupported`. A claim counts as checked for its budget line only at or above that line's retiring tier. The report counts claims by highest tier reached and never sums them into a number. Protocols carry a coverage rule (for customer counts: at least `[3]` windows including a weekday peak, a weekday off-peak and a weekend window), so one staged hour cannot clear a claim. Observer role (`buyer`, `adviser`, `field_checker`) is recorded; observer bias and seasonality are stated limits, not corrected.

### Quality, security and AI
| Case | Mitigation | Check |
|---|---|---|
| Oversized or malformed input | schema validation, byte cap `[32 KB]`, numeric bounds, timeouts | VCC-02, VCC-09 |
| Instructions hidden in pasted text steering the client agent | closed fields only; free text rejected; output returns user values as escaped data | VCC-09 |
| A low cash-to-close or "no flags" read as safe | range shown first, `incomplete` marking, unchecked share beside it, mandatory "indicative, not verified" label, unsupported claims counted | VCC-05, VCC-06, VCC-08 |
| Budget parameters stale or invented | `as_of`, sources, `review_status`; stale after `[180]` days flagged; unreviewed packs show arithmetic on user inputs only | VCC-13 |
| Output read as a price opinion or advice | no valuation or fairness wording; lint | VCC-08 |
| Output read as an accusation | statuses name claims, never persons; lint | VCC-08 |
| A staged week, observer effect or seasonality | coverage rule per protocol; tiers; T3 tasks (written landlord or accountant confirmation) | VCC-07, VCC-16 |
| A sighted document treated as authentic | label "sighted, not authenticated" | VCC-08 |
| Observation captures personal data | counts and enums only; no images, names or free text | VCC-09, HG-02 |
| Online evidence creeps in | no fetch code path; URL-bearing input rejected | VCC-09, VCC-11 |
| Drift toward introductions or deal-linked fees | green-zone scan in C-EVAL; HG-07 before any new module | VCC-10 |
| An impractical or unsafe protocol task (for example entering premises uninvited) | tasks limited to public vantage points or seller-consented access; reviewer approves every task | HG-02, HG-06, VCC-16 |
| Persistence of listing or evidence content | no storage; counters only | VCC-12 |
| A comparison looks like endorsement or mixes incompatible offers | neutral A/B/C slots, fixed rows, unknowns shown; reject pack/version/currency mismatch | VCC-25, VCC-26 |
| Quota exhaustion or abuse (remote) | per-client rate cap; breaker; fall back to local package | VCC-19 |

**AI components**: none server-side (ADR-002). Any future AI component needs typed input, typed output, an emitted cost log and a stated fallback. Every agentic loop is bounded: session cap 10 tool calls, per-call wall clock 10 s, breaker after 3 consecutive errors — `unbounded-loop`.

| Feature | Server inference tokens | Max response | Session ceilings |
|---|---|---|---|
| F1 Budget Check | 0 | 64 KB (≈ `[3k]` tokens typical `H`) | 10 calls, 10 s per call |
| F2 Plan and Worksheet | 0 | 64 KB | same |
| F3 Evidence Re-run | 0 | 64 KB | same |
| F4 Transfer Checklist | 0 | 64 KB | same |
| F5 Comparison | 0 | 64 KB | same; reuse the report evaluator |

**TCO per deployment model** (kept separate — `blended-deployment-tco`):

| Model | Operator spend | Operator active time | Limit / risk | Exit |
|---|---|---|---|---|
| Local package and saved static page | 0 | docs and pack releases | user's machine | n/a |
| Optional shared remote endpoint | 0 within free quota (`unverified`, F-06) | monitoring | quota and CPU limits | use local package |
| Self-hosted on the user's own free account | 0 | user setup | user effort | fork and run |

Zero-spend scope: unknown fees, paid infrastructure, paid reviewers and proprietary dependencies cannot silently enter the MVP — `constraint-gate-skipped`. Reviewer cost and budget-parameter sourcing are the main hidden costs (A08, F-10): until reviewers are named, packs stay provisional.

### Data schema and formats (SSOT)
Plain text in Git, validated by JSON Schema (2020-12, `additionalProperties: false`); canonical form (UTF-8, LF, sorted keys, 2-space indent) checked in CI. Everything generated is rebuildable and never edited.
```text
packs/{pack_id}/pack.json        fields, budget lines and parameters, claim kinds, protocols, tolerances, flag rules, glossary (en, zh), as_of, review_status
schema/*.schema.json             claim, evidence, budget, report and comparison schemas; schema_version semver
fixtures/{pack_id}/*.json        labelled check, comparison, budget and status fixtures
worksheets/{pack_id}/ (generated) Markdown, CSV and printable HTML worksheets
mcp/descriptors/ (generated)     one descriptor per tool, generated from C-SCHEMA
```
Pack budget parameter and claim kind with protocol (examples; `[..]` values are reviewed parameters not yet sourced, F-10):
```json
{"param":"legal_transfer_cost_sgd","low":"[..]","high":"[..]","as_of":"[..]","sources":[],"review_status":"provisional"}
{"claim_kind":"lease.remaining_months","unit":"months","retiring_tier":"T2","comparator":"exact_or_within_months","tolerance":"[..]",
 "protocol":[{"provenance":"document_sighted","task":"sight_lease_term_and_assignment_clause","effort_min":30,"tier":"T2"},
             {"provenance":"third_party_confirmed","task":"request_landlord_written_confirmation_of_term_deposit_consent","effort_min":20,"tier":"T3"}],
 "review_status":"provisional"}
```
Claim set, evidence entry and report (illustrative only; money fields are whole SGD integers or band codes; nothing is free text; no name, address or contact):
```json
{"pack_id":"sg.fnb.takeover","listing_source":"classifieds","claims":{"subtype":"cafe","price":150000,"equipment_included":true,"rent_monthly":6000,"lease_remaining_months":24,"deposit_months":3,"sales_band":"b4","staff_band":"b2","licence":"held","fit_out_age_band":"b2","runway_months":3}}
{"claim_kind":"lease.remaining_months","provenance":"document_sighted","observer_role":"buyer","date":"2026-11-03","value":18}
{"pack_id":"sg.fnb.takeover","pack_version":"0.1.0","as_of":"2026-10-27","review_status":"provisional","label":"indicative, not verified","budget":{"incomplete":true,"cash_to_close":{"low":"[..]","high":"[..]"},"gap_above_price":{"low":"[..]","high":"[..]"},"lease_exposure":{"low":108000,"high":108000},"unchecked_share":0.86,"lines":[{"line":"L3","low":18000,"high":18000,"checked":false}]},"coverage":{"claims":11,"by_tier":{"T0":10,"T2":1},"discrepancy":1,"conflicting_evidence":0,"no_discrepancy_found":0,"unsupported":10},"results":[{"claim_kind":"lease.remaining_months","claimed":24,"status":"discrepancy","tier":"T2","next":"request landlord written confirmation"}]}
```
`listing_source` is an enum (`portal`, `classifieds`, `broker_brochure`, `social_post`, `word_of_mouth`, `direct`, `other`); no URL, name, address or contact is accepted or stored. Where a band replaces a number, ratios use band bounds and the output is a range marked indicative. The report example shows 24 months claimed at 6,000 a month against 18 months sighted: the lease exposure shown uses the sighted value (18 × 6,000 = 108,000), and the entry also changes the `lease.remaining_months` status.

### Operations and obligations
- **Delivery and support**: solo operator; issues via the source host; no SLA. Incident path: pin back the pack or endpoint to the prior revision.
- **Pack release**: draft pack → sources attached → practitioner pilot (HG-06) → reviewer sign-off (HG-02) → `review_status: reviewed` → publish. Each pack revision is one release with its own rollback pin.
- **Obligations**: information only; no legal, tax, valuation, financing or licensing advice. Open questions for named reviewers, not assertions: whether the analytic-only role stays outside Singapore estate-agency licensing, including for lease-bearing takeovers and for any paid evidence pack (HG-07); whether and how a person may lawfully observe and count customers at an outlet and whether the seller's consent is required; confidentiality owed when documents are sighted; whether `discrepancy` wording about a listing creates defamation or misleading-statement exposure; whether referral fees to legal or accounting professionals are permitted; personal-data rules for any future stored record. Jurisdiction: Singapore (Malaysia at R3). Reviewers: unnamed (F-02).
- **Licences and IP**: no copied listing text or assets; the service stores nothing from any listing.

### Human gates
No silent gate — `human-gate-unstated`.

| Gate | When | Evidence | Rollback |
|---|---|---|---|
| HG-01 operator opens a Deploy Boundary | before any promotion | operator instruction reference | revert to prior protected revision |
| HG-02 qualified reviewer per pack (Singapore F&B practitioner for budget parameters and protocols; Malaysia at R3) approves budget parameters, claim kinds, protocol tasks, retiring tiers, tolerances, checklists, observation and privacy rules, wording and disclaimers | before a pack is marked `reviewed` | signed review record | revert pack to `provisional` |
| HG-03 operator approves payment-mechanism terms | before any collection | recorded fee terms | stop collection |
| HG-04 founder conducts interviews | R0 | quotes on record | none (observation only) |
| HG-05 operator re-verifies free-tier limits and terms | before any hosted route and every `[90]` days | dated record | disable hosted route |
| HG-06 founder runs a practitioner pilot: ≥ 3 practitioners execute the protocol on real or mock outlets | before HG-02 sign-off of any protocol | pilot record: tasks completed, time, errors | protocol reverts to `provisional` |
| HG-07 **legal review** by a qualified Singapore lawyer (and, before R3, a Malaysian one) confirms the green-zone boundary, fee structure and wording; written clarification from the regulator is optional | before any collection, before any seller-facing output (US-12), and before any module parked in ADR-008 | written opinion | stop collection; remove the module |

### Lanes and Deploy Boundary Register
| Lane | Contents | Boundary to next | Gate | Evidence | Rollback | State |
|---|---|---|---|---|---|---|
| authoring | this document, source, packs, fixtures | → mirror | CI pass + zero `blocker` | Integration Receipt | revert to prior SHA | closed |
| mirror | read-only public copy | → delivery | exact protected SHA named | deployment receipt | redeploy rollback predecessor | closed |
| delivery | optional deployed endpoint | — | HG-01 | live identity | prior revision | closed |

No authoring-lane command may mutate a mirror or delivery surface — `deploy-boundary-breach`.

### Ecosystem
| Participant / job | Value exchange / payer | Native owner | Interface / authority | Evidence / gap | Cost, privacy, exit |
|---|---|---|---|---|---|
| Buyer: budget, check claims, plan and gather evidence | free open checks; pays for an evidence pack (hypothesis) | C-CHECKS | local or tool route, compute-only | none / VH-01, VH-02 | no retention |
| Adviser (fit-out contractor, F&B consultant, accountant) | seat or exports (hypothesis) | C-UI exports | same routes, adviser label | none / VH-03 | no client data stored |
| Seller | shares a summary they generate (R2, gated) | C-UI exports | same routes | none / HG-07 | no retention |
| Listing venues (classifieds, marketplaces, portals, brokers) | none; the service reads nothing from them and sends them nothing | external | none; no integration | observed (S-01..S-04, S-08) | untouched |
| Agent host | none | C-LOCAL, C-ENDPOINT | discovery grants no mutation | none / VCC-14 | 0-token read path |
| Qualified reviewers (SG practitioner, SG lawyer) | approve pack content and the boundary | HG-02, HG-07 | review record | gap: unnamed (F-02) | unknown cost (A08) |
| Referral partners (incorporation, accounting, lending) | referral fee (hypothesis) | external | link-out only; never from a counterparty | none / outreach | no data shared |

Coverage here is not certification, availability, revenue or a production claim.

### Shared utilities and reuse
| Candidate | Source / revision | Consumers | Decision | Smallest delta | Check |
|---|---|---|---|---|---|
| Pure schema, checks and budget engine package | this repo | local package, endpoint, browser | `reuse` internally | share by declared export, not sibling imports | VCC-17 |
| Same six tools for every pack | this repo | SG and later MY packs | `reuse` | add pack data; add line kinds or comparators only when needed | VCC-17 |
| Existing MCP tool-server harness patterns | revision **unresolved** | C-LOCAL, C-ENDPOINT | `defer` until a specific codebase is pinned and inspected (F-08) | pattern only; no copied code without licence check | VCC-11 |

## ADR
### ADR-001 — Local-first, offline-capable delivery with an optional stateless remote (proposed)
Requirements: zero spend, no retention of inputs, usable with no network, solo-operable, agent-callable.

| Candidate | Disposition |
|---|---|
| A. Local package plus static files, with an optional free-tier stateless endpoint | pass |
| B. Hosted service only | fail-offline and fail-no-retention-by-construction |
| C. Static page only | fail-remote-agent-route (kept as baseline surface) |
| D. Paid container hosting | fail-zero-spend |

**Decision**: A. The local package is primary; the remote is optional, hard-capped and fails closed to the local package when quota is reached (VCC-19). Free-tier terms are `unverified` and re-checked at HG-05. **Consequences**: users install or save a file; vendor coupling is contained by a pure package behind thin adapters. **Recovery**: disable the hosted route. **Reversibility**: high. **Revisit trigger**: evidence that most users cannot or will not run a local package.

### ADR-002 — Deterministic checks and budget arithmetic, no server-side model (proposed)
Alternatives: server-side model (fail-zero-spend: inference cost; fail-reproducible: money outputs must be identical on re-run); client-agent reasoning with no service (fails the need for sourced, versioned, reviewable parameters); deterministic engine (pass). **Decision**: deterministic, with an independent oracle in C-EVAL (VCC-05). **Consequences**: reproducible, 0 serving tokens; mapping a listing's prose into closed claims is the client agent's job. **Revisit trigger**: evidenced demand for unstructured parsing and a zero-cost inference path.

### ADR-003 — Packs as versioned data with budget parameters and evidence protocols (proposed)
Requirements: reviewable by a non-engineer, provenance per parameter and rule, separate review per jurisdiction, protocols checkable on the ground, zero spend, portable.

| Candidate | Disposition |
|---|---|
| A. Data packs with schema; budget parameters, claim kinds, protocols, retiring tiers and tolerances in data; line kinds and comparators implemented in C-CHECKS | pass |
| B. Rules and parameters hard-coded per jurisdiction | fail-reviewer-readable |
| C. One regional pack with country parameters | fail-separate-review |
| D. Hosted rules-engine service | fail-zero-spend |

**Decision**: A. **Consequences**: a new line kind or comparator is a code change; pack and schema versions must be compatible (validator in CI); rollback by pack pin; parameters without sources stay `provisional` (F-10). **Revisit trigger**: three or more packs needing the same new comparator (extract a shared kind, with an ADR).

### ADR-004 — Evidence is human-gathered and offline; no web search or data fetch (proposed)
Requirements: the pitch (sits on top of any source, needs none of their data), evidence about this unit rather than an area, no automated collection, zero spend, no retention.

| Candidate | Disposition |
|---|---|
| A. Web or open-data lookups (maps, footfall, registries) at build or run time | fail-pitch and fail-this-unit (area proxies do not measure the outlet); deferred |
| B. Scrape listing platforms or third-party sites | fail-no-automated-collection |
| C. Structured evidence entered by a person: observations, counts, documents sighted, written confirmations, each with provenance and tier | pass |
| D. Vendor footfall, mobility or point-of-sale data | fail-zero-spend |
| E. The service ingests uploaded documents (OCR) | fail-no-retention and fail-cost; deferred |

**Decision**: C, with tiers T0..T3. **Consequences**: effort sits with the user, so the plan must make the work small, specific and ordered by cash retired; quality depends on protocol design and reviewer approval; a sighted document is not authenticated; observer bias, staged periods and seasonality remain. **Recovery**: drop a protocol task by pack release. **Reversibility**: high. **Revisit trigger**: buyers say area context would change a decision (VH-01) and a source passes a new ADR on licence, cost and independence.

### ADR-005 — Source-agnostic input: closed-field claim sets with numeric money (proposed)
Requirements: works for any source, no URL fetching, no retention, no per-platform parsers, one schema, exact buyer figures where the buyer has them.

| Candidate | Disposition |
|---|---|
| A. Per-venue connector or URL fetcher | fail-no-automated-collection |
| B. Server-side extraction of pasted listing text with a model | fail-zero-spend (ADR-002) |
| C. Closed-field claim set mapped by the user or their client agent; money as bounded whole numbers or band codes; the source is an enum | pass |

**Decision**: C. Input containing a URL, name, address or contact is rejected (VCC-09). Money amounts are not personal data, so exact figures are accepted and give point values; bands give ranges. **Consequences**: mapping effort on the client side; claims the schema has no field for are dropped. **Revisit trigger**: fewer than `[60]`% of pilot users complete mapping unaided (VH-04).

### ADR-006 — Report semantics: budget range, unchecked share, per-claim status; no score, verdict or price opinion (proposed)
| Candidate | Disposition |
|---|---|
| A. A composite honesty, trust or deal score | fail-false-precision and fail-no-verdict (unreviewable weights, defamation exposure, invites gaming) |
| B. A single cash-to-close number | fail-false-precision (hides incompleteness and parameter ranges) |
| C. Binary pass or fail per claim | fail-false-reassurance |
| D. A range with its lines and an `incomplete` flag, the unchecked share of cash as a plain ratio, status per claim (`discrepancy`, `conflicting_evidence`, `no_discrepancy_found`, `unsupported`), highest tier reached, counts by tier, next task | pass |

**Decision**: D. `no_discrepancy_found` requires independent evidence of T1 or above and never means true or verified. The unchecked share has no threshold and no label. Wording is linted against a pack-listed verdict-word list and a price-opinion list (VCC-08). **Consequences**: reports look unfinished when little evidence exists, which is accurate. **Revisit trigger**: a reviewer finds any label or ratio unsafe.

### ADR-007 — Green zone: analytic role only (proposed)
Requirements: stay outside introducing, matching, negotiating and brokerage; no regulated advice; no deal-linked revenue; solo-operable.

| Candidate | Disposition |
|---|---|
| A. Analysis of the user's own claims and plans for the user's own checks; fees for software or evidence packs only; no counterparty handling | pass |
| B. A listings showcase with introductions or contact reveals | fail-green-zone (introduction for a fee where a lease is involved; S-11) |
| C. A listings showcase with no contacts, relying on the publishing carve-out | defer: the carve-out applies only to someone who does no other estate agency work (S-11); needs HG-07 and ADR-008 |
| D. Partnership with a licensed agency for the introduction step | defer: needs HG-07, a partner and a fee structure reviewed by counsel |

**Decision**: A, enforced by VCC-10 and the Green-zone boundary table. **Consequences**: no marketplace revenue and no network effects in this increment; distribution depends on free outputs, advisers and worksheets passed between people. **Revisit trigger**: HG-07 opinion that a defined showcase module is outside the regime and evidence that sellers would publish (VH-05).

### ADR-008 — Parked modules: showcase, teaser, stealth listing, pay-to-reveal (proposed)
These are valuable ideas that are not part of this increment. Condition to unpark any of them: (1) HG-07 written opinion; (2) a new ADR covering stored records, privacy, fee structure and the re-identification risk of bands in thin markets (suppress or merge any cell with fewer than `k` listings; no coordinates or exact figures in the page before payment); (3) VH-05 evidence that sellers or agents would publish; (4) the core check at R1 exit. Design intent if unparked: only listings that have passed through the check are shown; a free teaser shows asset type, area-level region, bands for cash-to-close, rent share and runway, and tier counts; paid reveal unlocks figures and the gap list, never a counterparty contact. **Reversibility**: n/a, nothing is built.

### ADR-009 — Placement: reuse the existing SME workspace (proposed)
Requirements: one owner per capability, no second app or shell, smallest delta. **Decision**: target the existing SME route and feature modules in `agentic-commerce-os` (S-17); S-18 records a local cash-to-close candidate on that route, with no integration or deployment claim. Its owner retains source release, deployment and rollback authority. Add no central MCP server or separate repository for this increment. **Revisit trigger**: two proven duplicate consumers justify a shared library.

### ADR-010 — Buyer-entered fixed-row comparison (proposed)
**Decision**: compare 2–3 closed claim sets only when pack id, version and currency match, through the same deterministic report evaluator; show A/B/C in entry order, preserve unknowns, and emit no sort, score, recommendation or winner. Browser/local-package use computes in memory and offline; an optional existing edge tool uses the same stateless handler. No comparison content persists. Revisit only after VH-06 and core report VCC-05..08 pass.

## MVP
**Scope**: US-01..US-06 (Must), plus US-07..US-10 where the pack is reviewed; six planned base capabilities; one pilot pack (`sg.fnb.takeover`); `[30]` fixtures; local-first operation; existing Commerce SME route. F5 adds one comparison capability only after VH-06 and VCC-05..08 pass, within 3 existing feature modules and with no new module or dependency. S-17 records four baseline tool identities; S-18 records a six-tool cash-to-close candidate, not integration or evaluator acceptance. Pack data version `1.0.0` is separate from PRD revision `0.9.1`. Until HG-02 passes, the pack remains `provisional`; R2 exports and the Malaysia pack (R3) stay out of scope.

### Demo Skeleton (F1–F3)
Budget 5 min; beats sum to 5 min: **Hook** 0:30 — "The listing says SGD 150,000. How much cash do you actually need?"; **Probe** 0:45 — agent lists packs, budget lines and protocol; **Run budget check** 1:00 — cash-to-close range, lease exposure and unchecked share (**VCC-05**, **VCC-06** holding); **Plan** 0:45 — tasks ordered by cash retired; **Reveal** 1:00 — mock evidence changes one status and narrows the range (**VCC-07**, **VCC-08** holding); **Compare** 0:30 — if VH-06 passes, show two same-pack options on the fixed rows, with unknowns and no winner; **Close** 0:30 — hand open items to an adviser.

### Rubric and readiness
- **Domain object**: the takeover cash-to-close report. The Agent Experience Maturity matrix was not supplied; claimed level: none; blocking component: matrix definitions — `unresolved-rubric-gap` (F-07).
- **Readiness** (separate): local `undocumented`; delivered `undocumented`. Dimensions in scope: discovery, zero-token read routes, offline operation, single Invocation Register.

### ADLC seam
Handoff needs zero open `blocker`, VCCs decomposable into bounded RAO Steps, a named reviewer path for HG-02 and an HG-07 plan. Ceilings `H` per feature: 1.5 M tokens, 20 iterations, 4 h wall clock; per-task budgets may narrow, never exceed. Operator path: START one lane → RELEASE one exact candidate → DEPLOY one exact protected revision. Cost lines (active minutes, tokens, CI minutes, provider fees, avoidable-block cost) come from receipts only. Before ending any implementing turn, update this document (criteria implemented, evidence recorded).

## GTM
### Offer and alternatives
**Pitch**: know your real cash to close, and how much of it nobody has checked. **Offer**: free open budget checks, plans, worksheets and any gated comparison (zero spend); a paid evidence pack for buyers and adviser seats or branded exports remain hypotheses. Comparison is an activation aid, not a new fee or a claim of willingness to pay. No marketplace, ads, listing, introduction or success fees.

**Whitespace claim (hypothesis, `source=unverified`)**: from search snippets only, no player was found that totals the cash to take over a small F&B outlet, totals the lease exposure, and shows how much of that rests on unchecked claims, for Singapore. Adjacent players cover listings, listing authenticity, generic checklists, bespoke professional diligence or large-deal AI tooling.

| Alternative | What it does | Overlap | Our difference | Evidence |
|---|---|---|---|---|
| Classifieds (SG) | Free-text takeover ads with price, rent, size and claims | Source of the claims we check | Any source accepted; never hosted or read by us | S-01 |
| Structured marketplace | Profiles with sales, EBITDA and asking price; screens against a basic requirement; diligence left to the user | Nearest structured rival; could add a cash calculator | Budget lines, lease exposure and ground evidence; no listing, no score | S-02 |
| Property portals | Rent, psf, size, MRT distance and agent tags for spaces; "Verified" stamp and agent registration checks concern the listing | Source of space and rent claims | We total the takeover cash and the lease, and tier the claims; portal verification does not address claim accuracy | S-03, S-04 |
| Free checklists and guides | Generic financial, legal and operational checklists (accounting software vendor, law firms, POS vendor, food blog) | The real free substitute | Numeric budget, tiers, plan ordered by cash at risk, reviewed parameters | S-05 |
| Professional diligence (accountants, lawyers, consultants) | Bespoke human diligence aimed at M&A scale | Same job, by hand, at prices unsuited to a small stall | Structured protocol they can reuse; not a substitute for them | S-06 |
| AI diligence tools | Data-room and document analysis for SMB acquirers; US-centric | Same buyer concern, different market and input | No seller documents needed up front; ground evidence; SG pack; zero tokens | S-07 |
| Brokers | Human intermediaries, mostly sell side | Adjacent channel | Buyer-side, no introductions | S-08 |
| Scraping due-diligence agent tool | Scrapes US listing sites and returns a 0–100 risk score | Closest in form (agent tool) | No scraping, no score, SG pack, human evidence | S-10 |
| General AI assistants with a prompt | Ask what is missing from seller documents | The real free substitute | Versioned, sourced, reviewer-gated parameters; reproducible money output; zero tokens | S-05 |

Differentiation is a hypothesis, not demonstrated value. Main threats: a free assistant plus a generic checklist is enough; a marketplace adds a cash calculator; buyers will not do ground work; and the unreviewed budget parameters may be wrong. Do-nothing: rely on a broker, an adviser late in the process, or the venue's disclaimer.

Lease scale, for orientation only (arithmetic on rents shown on one portal for spaces, not takeovers, S-03): a monthly rent of SGD 6,000 over 1 to 3 years is SGD 72,000 to 216,000; SGD 22,800 over the same terms is about SGD 273,600 to 820,800.

### Market sizing (draft)
Reduced discovery sketch — labelled **incomplete** (F-01). No TAM/SAM/SOM figure is asserted.
- Method A (top-down): annual SG F&B unit transfers `[n]` × share by first-time or small buyers `[q]` × share seeking a structured check `[r]` × price `[A01]`.
- Method B (bottom-up): active SG F&B takeover postings across channels `[m]` × monthly turnover `[t]` × conversion `[c]` × price.
- Observed anecdotes, not sizing: one SG cafe takeover advertised near SGD 150,000 (S-01, carried); structured profiles for cafes and restaurants with run-rate sales and asking prices (S-02).

### Acquisition through retention
Channel hypotheses, all human and offline-first: advisers who already meet buyers (fit-out contractors, F&B consultants, accountants); F&B community groups and associations; saved and printed worksheets passed between people; open pack pages findable by search; agent-tool registries. No automated outreach and no collection from any venue. Activation = first budget report. Paid conversion = buyer buys an evidence pack or an adviser takes a seat. Repeat use = re-run after evidence entries. Support = source-host issues. Sales cycle unknown. All hypotheses.

### Monetization
Mechanism-proven: **no**. Demand-validated: **no**. Recognized revenue: **0**. Collected payment: **0** — `monetization-demand-unvalidated` (F-01).

| Order | Stream | Distance to a real first dollar | Wait / unblock |
|---|---|---|---|
| 1 | Buyer evidence pack: one-off fee (SGD) for the printable protocol, evidence entry and recomputed budget | short: concierge-testable by hand before any build | HG-02, HG-03, HG-07; VH-02 pass |
| 2 | Adviser seat or branded exports: flat annual or per-engagement fee (R2) | medium: needs adviser trials | HG-03, HG-07; VH-03 pass |
| 3 | Seller-generated evidence summary, shared by the seller (R2, gated) | needs a seller who wants proof | HG-07; VH-05 |
| 4 | Referral fees from accounting, incorporation and lending partners | needs partner agreement; legality unknown; never from a counterparty | reviewer answer; partner response |
| 5 | Subscription | deferred: low deal volume | revisit if repeat use ≥ `[3]`/month |

Success fee, introduction fee, listing and sponsor revenue are `Won't (this increment)`. The free budget check stays free; a paid stream must charge for the evidence pack or the adviser workflow, not for access to the check and never for a deal.

**Experiment VH-01** (pain, buyers; format `source=unverified` against Lean Startup Guidelines): *Hypothesis*: ≥ 5 of 10 recent or active SG F&B takeover buyers describe a takeover where the cash needed exceeded the advertised price by a material amount, and ≥ 6 of 10 quantify a workaround. *Method*: 10 interviews reached by personal introduction, adviser referral or public postings seen by hand, no automated collection; 14-day window; owner founder; the interview also asks what total cash they needed against what was advertised and whether they would filter by it. *Continue* ≥ 5/10; *pivot* to the adviser channel only at 3–4/10; *stop* the buyer-side wedge at ≤ 2/10.

**Experiment VH-02** (buyer WTP): *Hypothesis*: ≥ 3 of 10 buyers who see the free budget output on their own listing pre-commit in writing to pay ≥ [A01] for an evidence pack. *Method*: concierge test with manual worksheets, after VH-01 and after HG-07 confirms the fee structure; 14 days; owner founder. *Continue* ≥ 3/10; *pivot* to adviser-only at 1–2/10; *stop* paid buyer streams at 0/10.

**Experiment VH-03** (adviser WTP): *Hypothesis*: ≥ 3 of 10 fit-out contractors, F&B consultants or accountants use the protocol on a live or recent deal and ≥ 2 pre-commit in writing to ≥ [A02]. *Method*: 10 conversations and a supervised 14-day trial, owner founder. *Continue* at the thresholds; *pivot* to buyer-only at 1; *stop* adviser streams at 0.

**Experiment VH-04** (R1 gate, with HG-06): *Hypothesis*: (a) ≥ 3 practitioners complete the protocol on site, ≥ [80]% of tasks unaided, effort within ±[30]% of the estimate; (b) ≥ [60]% of pilot users map a listing to claims unaided; (c) of `[5]` real outlets checked with the seller's permission, ≥ `[2]` show a gap above the asking price or a material discrepancy that changes the cash plan. *Method*: stage-0 manual worksheets, no build, 14 days, owner founder. *Continue* at (a), (b) and (c); *pivot* to checklist-only at (a) without (c); *stop* R1 at none.

**Experiment VH-05** (parked modules gate): *Hypothesis*: ≥ 3 of 10 sellers or agents would publish a teaser with stealth identity and pre-commit to a listing fee. *Method*: 10 conversations after R1 exit and HG-07, no build, 14 days. *Continue* ≥ 3/10 and a favourable opinion; *stop* at ≤ 1/10.

**Experiment VH-06** (buyer comparison gate): *Hypothesis*: recent or active buyers need to compare two or three options using consistent cash, lease and evidence rows, and understand the output as neutral. *Method*: 10 buyer interviews plus a paper prototype, no build, 14 days; *continue* only if ≥ 6/10 describe a recent comparison workaround and ≥ 8/10 identify unknowns without reading a winner; *revise* at 3–5 workaround cases or 6–7 neutral readings; *drop F5* at ≤ 2 workarounds or if users require ranking. Owner: founder. F5 also waits for VCC-05..08.

### Financial sketch
| ID | Assumption | Value | Source | Disposition | Date |
|---|---|---|---|---|---|
| A01 | Buyer evidence pack price | SGD [..] | hypothesis | to-validate (VH-02) | 2026-10-27 |
| A02 | Adviser seat or export price | SGD [..] | hypothesis | to-validate (VH-03) | 2026-10-27 |
| A03 | Interview → commit conversion | 30% | hypothesis | to-validate | 2026-10-27 |
| A04 | Infra cost per check | 0 within quota | design + unverified quota | verify (VCC-19, HG-05) | 2026-10-27 |
| A05 | Server-side serving-token cost per check | 0 | ADR-002 | design fact | 2026-10-27 |
| A06 | Payment fee | unknown | none | gap (HG-03) | 2026-10-27 |
| A07 | Referral fee rate | unknown | none | gap | 2026-10-27 |
| A08 | Reviewer cost per pack (practitioner and lawyer) | unknown | none | gap; main hidden cost | 2026-10-27 |
| A09 | Field effort per outlet check | `[3]` h `H` | hypothesis | to-validate (VH-04) | 2026-10-27 |
| A10 | Outlets with a material gap above the asking price | `[..]` of 5 | none | gap (VH-04) | 2026-10-27 |
| A11 | Operator support minutes per month | `[..]` | none | gap | 2026-10-27 |
| A12 | Seller-generated summary price (R2) | SGD [..] | hypothesis | to-validate (VH-05) | 2026-10-27 |

Unit economics: contribution per paid pack = A01 − A06 − support minutes × `[rate]` − amortised A08; infrastructure = 0 within quota. Break-even packs = A08 ÷ contribution. All inputs open.

### Capital
Zero external capital sought. Cost = operator time, then reviewer fees (A08, unknown). No spend before HG-03.

### Roadmap
| Phase | Pain | Reuse / owner | Prerequisite | Cost / time | Stop / recovery | Next |
|---|---|---|---|---|---|---|
| R0 Validate | PP-01..PP-04; PP-06 | founder | none | interviews and stage-0 worksheets ≈ `[30]` h `H`; spend 0 | stop per VH-01, VH-04, VH-06 | R1 on pass |
| R1 Pilot: `sg.fnb.takeover`, six base capabilities, local-first in existing Commerce SME route | PP-01..PP-04; PP-06 | C-SCHEMA, C-PACKS, C-CHECKS, C-LOCAL, C-UI / founder | R0 pass; HG-06; HG-02 for `reviewed`; HG-07 before collection; HG-05 for hosted route; F5 only after VH-06 and VCC-05..08 | base ≈ `[60]` active h `H`; F5 ETA/cap ≤12 active h, ≤20 KB added source, ≤3 existing SME feature modules, 0 new modules/deps; spend $0; chunks <500 KB | revert F5 only; keep base check | R2 |
| R2 Buyer evidence pack, adviser exports, seller-generated summary | PP-05 | C-UI, C-CHECKS | VH-02 or VH-03 pass; HG-03; HG-07 | ≈ `[20]` h `H` | stop collection | R3 |
| R3 `my.fnb.takeover` | PP-01..PP-04 (MY) | C-PACKS | R1 exit; Malaysian legal review (HG-07); MY practitioner reviewer | ≈ `[40]` h `H` | unpublish pack | R4 |
| R4 Parked modules (ADR-008): showcase, teaser, stealth, pay-to-reveal | PP-05 | new | R1 exit; HG-07 opinion; new ADR; VH-05 pass | `[..]` | remove the module | — |
| Later (new ADR and evidence required) | — | — | evidenced demand | — | — | retail packs, land-bearing packs, area context, data lookups |

### Learning and next increment
Actual versus target is recorded per VCC and per experiment. Continue, pivot and stop thresholds sit in VH-01..VH-06 and the roadmap stop column. R1 measures re-run use, movement in unchecked share, and whether buyers understand F5 as a neutral comparison; no additional ranking is inferred. Decide R2 on VH-02 and VH-03 evidence.

## Evidence register
Market entries S-01..S-16 remain `source=unverified`: observed 2026-10-26 and 2026-10-27 through web-search snippets (and, for S-11, a fetched copy of the statute); most pages were not opened in full, and informal channels are not observable this way (F-04). S-17 is a read-only baseline observation; S-18 records local candidate checks, neither is integration or release proof. *Carried* = from version 0.7.0, not re-observed.

| ID | Observation | Source |
|---|---|---|
| S-01 | *Carried.* Singapore classifieds search "cafe takeover": free-text ads with rent, takeover price, size and claims such as SFA-approved premises; one cafe takeover near SGD 150,000 | https://www.carousell.sg/cafe-takeover/q/ |
| S-02 | *Carried.* Structured marketplace profiles for SG and MY F&B: years established, employees, reported and run-rate sales, EBITDA margin, asking price; disclaimers that completeness is not guaranteed; screens profiles against a basic requirement and leaves thorough diligence to users | https://www.smergers.com/business/restaurant-for-sale-in-singapore/76dro/ ; https://www.smergers.com/business/na/3y1xl/ |
| S-03 | A Singapore property portal's commercial and F&B pages show monthly rent, psf, size, unit type, MRT distance and agent-chosen tags such as "High Tourist Footfall"; example rents SGD 6,000 (619 sqft) and SGD 22,800 (1,560 sqft) a month | https://www.99.co/singapore/rent/commercial/retail/with-multi-purpose-hall ; https://www.99.co/singapore/rent/commercial/retail/with-bbq?page_num=4 |
| S-04 | The same portal states that most listings come from CEA-registered agents, that it checks phone and registration details, that authenticated "Must See" listings carry a "Verified" stamp, that not all listings are verified, and that it is free for seekers | https://www.99.co/singapore/sale/commercial/with-no-column?page_num=16 ; https://www.99.co/singapore/sale/commercial/with-bbq?page_num=38 |
| S-05 | Free checklists and guides on taking over or buying a business: accounting-software vendor, POS vendor, law firms, a food blog (the last carried); the same blog notes consultant feasibility spend; an AI-prompt newsletter suggests asking an assistant what is missing from seller documents (carried) | https://www.xero.com/sg/guides/buying-a-business/ ; https://www.ichefpos.com/en-sg/blog/take-over-an-foodandbeverage-business ; https://irblaw.com.sg/learning-centre/due-diligence-checklist-buying-businesses/ ; https://yuenlaw.com.sg/singapore-law/how-to-buy-a-business-in-singapore/ ; https://sethlui.com/taking-over-food-beverage-business/ ; https://nikolas-newsletter-241a64.beehiiv.com/p/newsletter-0007-how-to-buy-your-first-business-with-ai-in-7-steps |
| S-06 | Professional due-diligence services by accounting and consultancy firms; due diligence described as handled by the buyer or investor with legal and financial advisers | https://sg.ecovis.com/?p=4880 ; https://intuitconsultancy.com/sg/due-diligence-services-in-singapore/ |
| S-07 | AI due-diligence tools and posts aimed at small-business and search-fund acquirers, built around data rooms and documents; largely US-centric | https://searchfunder.com/post/we-built-an-ai-agent-that-interrogates-your-data-room-not-just-reads-it-looking-for-beta-testers-with-active-deals ; https://searchfunder.com/post/looking-for-due-diligence-support-aitools-for-smb-roll-ups |
| S-08 | Broker offices and other business-for-sale channels in SG and MY (Sunbelt, a listicle of sites; not inspected in depth) | https://www.sunbeltnetwork.com/international/malaysia/ ; https://www.axial.net/company/sunbelt-business-brokers-singapore-and-malaysia ; https://sbo.sg/?p=71168 |
| S-09 | Pattern reference from a verified-revenue directory for software startups: verified figures, stealth listings that hide identity, a broker fee tied to completed sales, and public pages scraped by third-party tools | https://www.trustmrr.com/faq ; https://trustmrr.com/startup/posture-icu.md ; https://apify.com/memo23/trustmrr-scraper |
| S-10 | *Carried.* An agent-callable due-diligence server that scrapes US listing sites and owner profiles and returns a 0–100 risk score | https://apify.com/warui09/due-diligence-mcp |
| S-11 | Singapore Estate Agents Act 2010 (2020 Rev Ed): definition of estate agency work (introduction or negotiation for a client for a fee), "property" and "lease", exclusions (publishing advertisements or disseminating information by someone doing no other such work; a party acting as vendor or purchaser; valuation or survey only), licensing requirement and offence | https://www.cea.gov.sg/docs/default-source/default-document-library/estate-agents-act-2010.pdf |
| S-12 | Regulator material: the Act covers residential, commercial and industrial property; agents must be registered through a licensed agency | https://www.cea.gov.sg/consumers/engaging-a-property-agent/check-if-your-property-agent-is-registered/ ; https://www.cea.gov.sg/docs/default-source/default-document-library/cea_brochure_englisha30f3033f22f6eceb9b0ff0000fcc945.pdf |
| S-13 | The portal's glossary states that an entity must hold an estate agent licence to perform estate agency work through a traditional or digital platform | https://www.99.co/singapore/glossary/estate-agent-licence/ |
| S-14 | Malaysia: estate agency governed by Act 242 and a board (BOVAEP); acting without a licence reported as punishable by a fine up to RM300,000 and/or three years' jail; the board has flagged online portals and web applications marketing properties | https://www.malaymail.com/news/malaysia/2019/07/31/real-estate-agents-group-raises-alarm-over-unlicensed-reps/1776217 ; https://www.starproperty.my/news/featured-news/-use-only-registered-property-agents-/75212 ; https://nst.com.my/amp/property/2018/04/353373/know-your-real-estate-practitioner |
| S-15 | *Carried.* A Johor cafe listing claims roughly 200 customers a day at peak and 15–20 at the low end | https://www.smergers.com/business/cafe-for-sale-in-johor-bahru-malaysia/az906/ |
| S-16 | *Carried.* In-page agent tools are a draft browser standard with limited support; not verified here | none gathered (F-07) |
| S-17 | At `agentic-commerce-os` revision `2fb00defb2f9a057eaaa659338500c2b6b07aafc`, `public/local-first/workspace.js` lazy-loads the SME view into `#sme`; `sme-business-pack.js`, `sme-business-pack-core.js` and `src/local-first/sme-business-pack.ts` expose four tools: `pack.list`, `pack.required_fields`, `takeover.check_listing`, `takeover.transfer_checklist`. No comparison tool exists; pack data is version `1.0.0` | local read-only code inspection; no live or deploy claim |
| S-18 | Candidate `f0f0f072f3ae5065c9eaa9433f2331a1c0527583` adds Singapore cash-to-close, evidence re-runs, unchecked share and cash-ranked worksheet to the existing workspace and exposes six canonical tools; `check:named`, `check:plan`, `check:evidence-contract`, `check:adlc` and `typecheck` passed locally. Comparison remains absent; lane closeout is continuable with no remote tracking ref or deployment receipt | local branch and check output observed 2026-10-31; candidate evidence only |

## Findings and open items
| ID | Finding | Effect |
|---|---|---|
| F-01 | No interview or willingness-to-pay evidence exists | all pains `unvalidated`; monetization unvalidated |
| F-02 | No qualified reviewer named (SG F&B practitioner, SG lawyer; MY at R3); reviewer cost unknown | packs stay `provisional`; HG-02 and HG-07 open |
| F-03 | Protocols and effort estimates are untested in the field | VH-04 and HG-06 open |
| F-04 | Competitor evidence is search snippets only; informal channels not observable | whitespace and differentiation are hypotheses |
| F-05 | Lawfulness and consent for observing and counting customers are unreviewed; the green-zone boundary rests on a reading of the statute, not on an opinion | tasks may change or drop at HG-02; collection blocked at HG-07 |
| F-06 | Free-tier limits and terms for any hosted route are unverified | remote route stays optional (HG-05) |
| F-07 | Companion guideline modules and the maturity matrix were not supplied; the in-page tool standard is unverified | rubric and diagram checks unresolved |
| F-08 | No reuse source is pinned or inspected for the tool-server harness | reuse deferred |
| F-09 | Payment fees and mechanism are unknown | collection blocked at HG-03 |
| F-10 | Budget parameters (legal and transfer costs, reinstatement provisions, utilities deposits, wage and variable-cost shares) have no sources yet | budget stays `provisional`; arithmetic on the user's own inputs only until HG-02 |
| F-11 | Personal-data rules (PDPA), payments or escrow regimes, and the limits of lease-related information versus legal advice are unresearched | reviewer questions at HG-02 and HG-07 |
| F-12 | Comparison demand and neutral interpretation are unvalidated; S-17 is the baseline and S-18 is a local cash-to-close candidate. Comparison remains unimplemented and no VCC has evaluator acceptance. The shell PRD is pinned to older source `88bd730c8f35da249fb23349c50820cc1932a95c` | reconcile `docs/prd-tad-adr-mvp-gtm-agentic-commerce-os.md` with the current route before delivery evidence; VH-06 gates F5 |

## Checkpoint
**Checkpoint (2026-10-31)**: revision 0.9.1 merges the fixed-row comparison plan with the cash-to-close integration plan. S-18 records a local, unintegrated candidate and green local checks for the cash-to-close flow; this is not evaluator acceptance, delivery or deployment proof. Comparison remains unimplemented and VH-06-gated. All VCCs remain unsatisfied; no buyer interview, willingness-to-pay, field pilot or reviewer decision is evidenced, and all pains remain `unvalidated`. R0 remains the gate to R1; HG-07 gates collection.
