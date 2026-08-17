---
title: "Knowgrph SME Care Agent Runtime Proof — Protection-Gap Evidence"
graphId: "md:knowgrph-sme-care-agent-runtime-proof"
doc_type: "SME Care Agent Runtime Proof"
date: "2026-07-13"
lang: "en-US"
schema: "kgc-sme-care-agent-runtime-proof/v1"
status: "runtime-ready-in-dev"
related_demo: "./knowgrph-sme-care-agent-demo.md"
invocation: "/sme-care-agent"
agent_definition: "agent.sme-care"
skill_variant: "agent.sme"
skill_id: "sme.risk.profile"
runtime_kernel: "sme.risk.profile"
input_schema: "knowgrph-sme-profile/v1"
output_schema: "knowgrph-sme-risk-run/v1"
runtime_source: "../../knowgrph/mcp/sme-risk-coverage/core.js"
runtime_contract: "../../knowgrph/docs/runtime-readiness-contract.md"
runtime_evidence: "../../knowgrph/sme-agent/demo/sme-care-agent-canvas-evidence.md"
runtime_status: "All audited SME Dev-runtime gaps are closed and focused proof passes; the repository-wide gate waits only for the separate healthcare canonical-authority commit and exact pin."
runtime_claim: "Local profile normalization, persisted growth-state deltas, caller run identity, complete output validation, canonical approval-token enforcement, three-domain risk analysis, coverage-gap and unknown-risk surfacing, provider-neutral guidance, cost evidence, atomic Source Files projection, and Canvas evidence are implemented."
publish_scope: "local-only"
publish_policy: "No quote, bind, purchase, policy mutation, third-party contact, Prod mirror, Cloudflare deploy, or regulated-advice claim."
kgCanvasSurfaceMode: "2d"
kgCanvasRenderMode: "2d"
kgCanvas2dRenderer: "storyboard"
kgDocumentSemanticMode: "document"
kgFrontmatterModeEnabled: true
kgMultiDimTableModeEnabled: true
kgDocumentStructureBaselineLock: false
kgBottomPanelOpen: true
kgBottomPanelTab: "flowchart"
kgFloatingPanelOpen: true
kgFloatingPanelView: "storyboard"
runtime_bounds:
  topology: "fan-out/fan-in"
  domains: ["cyber", "supply_chain", "asset_physical"]
  max_iterations: 1
  timeout_seconds: 300
  token_budget: 100000
  deterministic_tokens_used: 0
  deterministic_paid_calls: 0
  deterministic_estimated_cost_usd: 0
readiness_gaps:
  global_promotion_gate: "The separate /healthcare-agent authority row must be operator-reviewed, committed, and pinned before the repository-wide runtime:check can pass clean-source governance."
  deployed_runtime: "Cloudflare remains unverified for the typed deterministic SME kernel and is not authorized by this document."
socket_types:
  sme_profile_signal: {color: "#0ea5e9", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [sme_profile_signal]}
  sme_risk_signal: {color: "#f59e0b", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [sme_risk_signal]}
  sme_guidance_signal: {color: "#14b8a6", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [sme_guidance_signal]}
  sme_proof_signal: {color: "#22c55e", edgeWidthPx: 3, handleStrokeWidthPx: 3, accepts: [sme_proof_signal]}
flow:
  direction: {key: direction, type: string, value: "LR"}
  edgeType: {key: edgeType, type: string, value: "smoothstep"}
  balancedViewportPreset: {key: balancedViewportPreset, type: string, value: "widgetFrontmatter"}
  computed: {key: computed, type: boolean, value: true}
  snapToGrid: {key: snapToGrid, type: boolean, value: true}
  nodes:
    - id: {key: id, type: string, value: "sme_profile"}
      type: {key: type, type: string, value: "InputWidget"}
      label: {key: label, type: string, value: "/sme-care-agent Profile"}
      lane: {key: lane, type: string, value: "Profile"}
      position: {key: position, type: object, value: {"x":0,"y":0}}
      handles: {key: handles, type: object, value: {"source":["profile"]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"out":{"profile":"sme_profile_signal"}}}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Accepts a typed synthetic or operator-controlled SME profile and preserves undeclared fields as unknowns."}
    - id: {key: id, type: string, value: "sme_exposure_fanout"}
      type: {key: type, type: string, value: "ProcessWidget"}
      label: {key: label, type: string, value: "Three-Domain Exposure Fan-Out"}
      lane: {key: lane, type: string, value: "Exposure"}
      position: {key: position, type: object, value: {"x":300,"y":0}}
      handles: {key: handles, type: object, value: {"target":["profile"],"source":["exposures"]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"profile":"sme_profile_signal"},"out":{"risk":"sme_risk_signal"}}}
      domains: {key: domains, type: array, value: ["cyber","supply_chain","asset_physical"]}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Computes one deterministic exposure for each supported risk domain."}
    - id: {key: id, type: string, value: "sme_gap_analysis"}
      type: {key: type, type: string, value: "AnalysisWidget"}
      label: {key: label, type: string, value: "Coverage Gaps and Unknown Risks"}
      lane: {key: lane, type: string, value: "Analysis"}
      position: {key: position, type: object, value: {"x":600,"y":0}}
      handles: {key: handles, type: object, value: {"target":["risk"],"source":["gaps","unknowns"]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"risk":"sme_risk_signal"},"out":{"guidance":"sme_guidance_signal"}}}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Separates covered, partially covered, uncovered, and insufficient-input outcomes without treating missing information as safe."}
    - id: {key: id, type: string, value: "sme_protection_guidance"}
      type: {key: type, type: string, value: "OutputWidget"}
      label: {key: label, type: string, value: "Provider-Neutral Protection Guidance"}
      lane: {key: lane, type: string, value: "Guidance"}
      position: {key: position, type: object, value: {"x":900,"y":0}}
      handles: {key: handles, type: object, value: {"target":["guidance"],"source":["protections","rationales"]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"guidance":"sme_guidance_signal"},"out":{"proof":"sme_proof_signal"}}}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Emits provider-neutral review guidance with a traceable rationale for each visible gap, unknown, and protection item."}
    - id: {key: id, type: string, value: "sme_source_files"}
      type: {key: type, type: string, value: "ArtifactWidget"}
      label: {key: label, type: string, value: "Source Files and Canvas Evidence"}
      lane: {key: lane, type: string, value: "Artifacts"}
      position: {key: position, type: object, value: {"x":1200,"y":0}}
      handles: {key: handles, type: object, value: {"target":["proof"],"source":["artifacts"]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"proof":"sme_proof_signal"},"out":{"proof":"sme_proof_signal"}}}
      artifact_count: {key: artifact_count, type: number, value: 7}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Projects the profile, exposures, gaps, guidance, rationales, delta, and Storyboard evidence into a bounded local batch."}
    - id: {key: id, type: string, value: "sme_readiness_boundary"}
      type: {key: type, type: string, value: "ProofWidget"}
      label: {key: label, type: string, value: "Verified Dev Runtime Readiness"}
      lane: {key: lane, type: string, value: "Proof"}
      position: {key: position, type: object, value: {"x":1500,"y":0}}
      handles: {key: handles, type: object, value: {"target":["proof"]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"proof":"sme_proof_signal"}}}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Records closed SME Dev-readiness proof while keeping the global authority pin, regulated actions, Prod, and Cloudflare separately gated."}
  edges:
    - {id: "edge_sme_profile_exposure", source: "sme_profile", target: "sme_exposure_fanout", type: "sme_profile_signal"}
    - {id: "edge_sme_exposure_analysis", source: "sme_exposure_fanout", target: "sme_gap_analysis", type: "sme_risk_signal"}
    - {id: "edge_sme_analysis_guidance", source: "sme_gap_analysis", target: "sme_protection_guidance", type: "sme_guidance_signal"}
    - {id: "edge_sme_guidance_artifacts", source: "sme_protection_guidance", target: "sme_source_files", type: "sme_proof_signal"}
    - {id: "edge_sme_artifacts_readiness", source: "sme_source_files", target: "sme_readiness_boundary", type: "sme_proof_signal"}
flow_diagrams:
  sme_care_agent_flow:
    key: "sme_care_agent_flow"
    type: "mermaid_flowchart"
    value: |-
      flowchart LR
        profile["/sme-care-agent typed profile"] --> fanout["Cyber · supply chain · physical asset"]
        fanout --> analysis["Coverage gaps + unknown risks"]
        analysis --> guidance["Provider-neutral guidance + rationales"]
        guidance --> artifacts["Seven Source Files + Canvas evidence"]
        artifacts --> proof["Verified SME Dev readiness"]
---

# Knowgrph SME Care Agent Runtime Proof

This companion document preserves the original deterministic SME care-agent runtime proof that existed locally before the upstream risk-copilot demo claimed the `knowgrph-sme-care-agent-demo.md` path.

`/sme-care-agent` gives an SME a deterministic, traceable view of declared cyber, supply-chain, and physical-asset exposure; apparent protection gaps; unresolved unknowns; and provider-neutral guidance for qualified review.

It is decision support, not an insurer, broker, underwriter, legal adviser, or automated insurance seller.

## Invocation

Call the local `knowgrph.superagent.run` tool with:

```json
{
  "invocation": "/sme-care-agent",
  "inputPath": "sme-agent/fixtures/pre-seed.md",
  "outputDir": "data/outputs/sme-care-agent-demo",
  "mode": "dry-run",
  "runId": "sme-care-demo-01",
  "tokenBudget": 100000,
  "timeoutMs": 300000
}
```

Use `live` only for local Source Files persistence. The deterministic SME kernel still records zero model tokens, zero paid calls, and zero estimated provider cost.

## Demo Journey

| Stage | Observable output | Bound |
|---|---|---|
| Profile validation | Normalized `knowgrph-sme-profile/v1` or a typed field error | Fail before spend |
| Exposure fan-out | Cyber, supply-chain, and physical-asset exposure records | Exactly three domains |
| Coverage fan-in | Matches, ranked gaps, and explicit unknown risks | Missing coverage is never treated as safe |
| Guidance | One provider-neutral protection outcome per visible gap | No insurer or product selection |
| Rationale | Source-field trace for every visible gap, unknown, and protection item | Untraceable output is blocked |
| Artifacts | Seven local Source Files, including Canvas evidence in live mode | Roll back on write failure |
| Cost and boundary | Canonical zero-cost logs and Dev-only deployment status | No paid or deployment mutation |
| Growth update | Previous persisted profile is loaded for the same profile id | Second changed run emits a non-`initial_run` delta |
| Approval boundary | Canonical gate id, verified signature marker, 15-minute TTL, and unconsumed token | Forged, expired, mismatched, or reused token fails closed |

## Typed Profile

```yaml
schema: "knowgrph-sme-profile/v1"
profile_id: "synthetic-logistics-01"
industry: "logistics"
size: 48
growth_stage: "growth"
assets: ["warehouse equipment"]
digital_footprint: "online booking portal and staff email"
suppliers: ["packaging supplier", "fleet maintenance supplier"]
declared_coverage:
  - category: "asset_physical"
    scope: "limited"
```

Use `undeclared` for information that is not known. The runtime must preserve it as an unknown rather than inferring safety or coverage.

## Artifacts

A successful local live run writes:

```text
sme-agent/profiles/<profileId>/profile.md
sme-agent/runs/<runId>/exposures.md
sme-agent/runs/<runId>/gaps.md
sme-agent/runs/<runId>/protection.md
sme-agent/runs/<runId>/rationale.md
sme-agent/runs/<runId>/delta.md
sme-agent/runs/<runId>/canvas-evidence.md
```

## Verification

Run from `$KNOWGRPH_ROOT` after installing and building workspace dependencies:

```bash
npm run sme-risk-copilot:check
```

`npm run runtime:check` builds `grph-shared` and `gympgrph` before the repository runtime and Canvas proof. `npm run sme-risk-copilot:check` is the bounded Dev-local SME readiness gate; production, Cloudflare, and regulated actions remain separately unauthorized.

## Readiness Decision

| Scope | Decision |
|---|---|
| Deterministic local demo | Go |
| Internal Dev evaluation | Go |
| Adviser review workflow using synthetic or operator-controlled SME inputs | Go as decision support with qualified review |
| Quote, bind, purchase, or third-party contact | No-go |
| Cloudflare or production deployment | No-go without separate implementation, approval, and live proof |

## Promotion VCC

Given a clean checkout and two sequential versions of the same SME profile, when `/sme-care-agent` runs, then one documented command builds dependencies and passes all focused checks, the second run produces a verified non-`initial_run` growth delta, malformed output fails complete schema validation, forged or reused approvals fail closed, caller run identity follows its declared contract, cost remains exact zero on the deterministic path, and no Prod or Cloudflare mutation occurs.

The SME-specific VCC is now satisfied by focused proof. Repository-wide promotion remains separately gated by the healthcare authority pin and is not implied by this document.

## Guardrails

- Do not claim complete coverage, eligibility, premium, underwriting outcome, or claim outcome.
- Do not select an insurer, carrier, policy, or product.
- Do not quote, apply, purchase, bind, renew, cancel, or alter a policy.
- Do not contact a third party without exact canonical approval.
- Do not present the output as legal, financial, insurance, or regulated advice.
- Do not mutate Prod, Cloudflare, payment, DNS, remote storage, or a production mirror from this document.
