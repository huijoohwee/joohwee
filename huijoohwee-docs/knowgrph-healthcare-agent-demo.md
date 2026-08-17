---
title: "Knowgrph Care Agent Demo - Multilingual Care Plan Coach"
graphId: "md:knowgrph-care-agent-demo"
doc_type: "Care Agent Demo"
date: "2026-07-07"
lang: "en-US"
schema: "kgc-computing-flow/v1"
demo_schema: "kgc-care-agent-demo/v1"
implementation_contract: "../../agentic-canvas-os/docs/PRD-TAD.md"
template_policy: "Minimum viable runnable care-agent seed for local-first patient engagement ideation, harness definition, Canvas projection, and validation; authored source payload owns graph data; local runtime proof is surfaced in runtime_proof; live outputs remain blank until operator-approved returned evidence exists."
validation_input_forbid_hardcode_in_repo: "true"
deployed_api_claim: "false"
runtime_status: "runtime-ready"
publish_scope: "local-only"
publish_policy: "No Prod mirror, Cloudflare deploy, external publication, PHI upload, fabricated provider IDs, generated media URLs, or clinical outcome claims."
kgCanvasSurfaceMode: "2d"
kgCanvasRenderMode: "2d"
kgCanvas2dRenderer: "storyboard"
kgDocumentSemanticMode: "document"
kgFrontmatterModeEnabled: true
kgMultiDimTableModeEnabled: true
kgDocumentStructureBaselineLock: false
kgWorkflowManagerModeEnabled: true
kgAutoSaveEnabled: true
kgAutoSaveDebounceMs: 1500
kgAutoSaveOn: ["nodeEdit", "runComplete", "approval", "assetReady"]
kgBottomPanelOpen: true
kgBottomPanelTab: "eventModeling"
kgFloatingPanelOpen: true
kgFloatingPanelView: "storyboard"
kgSharedRendererContract:
  version: "shared-renderer-contract/v1"
  semanticIdentity: "buildScopedGraphSemanticKey"
  cardPreview: "CardMediaPreview + CardMarkdownPreview"
  widgetCard: "canvas:widgetCard"
  richMediaPanel: "RichMediaPanel"
  storyboardDisplay: "2D Renderer: Storyboard Card (default) and Widget variants"
  storyboardSurfaces: ["Cards", "Widgets", "Rich Media Panels"]
  edgeModel: "active graph edges derive from this frontmatter-owned care-agent graph"
  rendererPolicy: "frontmatter and source payloads own data; renderers project view state only"
credential_policy:
  phi: "Use synthetic or operator-redacted source notes only; never commit PHI, credentials, browser sessions, or generated patient media."
  providers: "Server-managed environment names only; no browser-stored keys, repo-stored keys, or client-side signing."
  live_generation: "Human approval required before paid, mutating, provider, browser-auth, Prod, or Cloudflare action."
safety_policy:
  clinical_role: "Patient engagement coach and explanation aid; not diagnosis, prescribing, emergency triage, or clinician replacement."
  escalation: "Emergency, red-flag, medication-dose, diagnosis, and conflicting-instruction cases route to clinician or emergency care guidance."
  source_policy: "Use operator-owned care-plan notes, discharge instructions, appointment tasks, lab explanations, and approved paraphrases only."
  data_minimization: "Prefer synthetic examples, local redaction, and source hashes over raw PHI."
runtime_defaults:
  provider: "knowgrph-local-care-dry-run"
  model: "care-agent-local-dry-run-v1"
  status: "runtime-ready"
  paid_call_count: 0
  prompt_tokens: 0
  completion_tokens: 0
  cache_hits: 0
  estimated_cost_usd: 0
  runtime_proof_path: ""
  provider_job_id: ""
  live_result_url: ""
run_ready_demo:
  id: "care-agent"
  env_selector: "VITE_KNOWGRPH_RUN_READY_DEMO=care-agent"
  command: "npm run demo:care-agent -- --port <free-port>"
  source_root: "huijoohwee/docs"
  source_path: "../huijoohwee/docs/knowgrph-care-agent-demo.md"
  validation_seed_path: "/knowgrph-care-agent-demo.md"
  clean_canvas_recommended: true
  source_backed: true
probe_tree_runtime:
  version: "knowgrph-probe-tree/v0.1"
  status: "runtime-ready"
  owner: "knowgrph/mcp/probe-tree-runtime.js"
  contract_owner: "knowgrph/canvas/src/features/agent-ready/probeTreeContract.mjs"
  graph_store_dir: "data/probe-tree"
  memory_scope: "knowgrph-probe-tree"
  tools:
    generate: "knowgrph.probe.generate"
    select: "knowgrph.probe.select"
    evolve: "knowgrph.probe.evolve"
  local_model_adapter:
    provider: "ollama"
    model_env: "KNOWGRPH_PROBE_TREE_MODEL"
    url_env: "KNOWGRPH_PROBE_TREE_MODEL_URL"
    allow_remote_env: "KNOWGRPH_PROBE_TREE_MODEL_ALLOW_REMOTE"
    timeout_env: "KNOWGRPH_PROBE_TREE_MODEL_TIMEOUT_MS"
    stream: false
    structured_output: true
    default_state: "disabled until host-owned model env is configured; heuristic fallback stays local-zero-cost"
  care_agent_thread:
    thread_root_id: "care-agent-demo"
    current_node_id: "care_source"
    context_text: "Synthetic or operator-redacted care-plan coach intake; ask for missing context, language, caregiver handoff, or safety boundary."
    option_count: 3
    token_budget: 1200
  proof:
    generate_mutates_graph: false
    explicit_zero_recall_verified: true
    select_writes_type_probe_node: true
    select_edge_type: "branches-to"
    select_frontmatter_flow_canvas_sync: true
    select_cost_log_verified: true
    evolve_writes_memory_exemplar: true
    evolve_reports_incomplete_parent_path: true
    evolve_cost_log_verified: true
    process_descriptors_non_idempotent: true
    semantic_frontmatter_keys_verified: true
    clean_room_generate_select_evolve_verified: true
    token_budget_ceiling_enforced: true
    native_checkpointer_datastore: false
    paid_call_count: 0
starter_inputs:
  patient_context: "Synthetic older-adult patient managing a new care plan after a clinic visit."
  source_url: ""
  source_title: "Operator-supplied care-plan notes"
  source_author: ""
  target_brief: "Create a multilingual, low-spec, phone-camera-friendly care-plan coach that explains tasks, checks comprehension, prepares caregiver handoff, and fails closed before clinical or deployment risk."
  approval_state: "draft"
agentic_os_care_agent_pipeline:
  version: "agentic-care-agent-pipeline/v1"
  status: "runtime-ready"
  autonomy_mode: "local-dry-run-first"
  source_docs:
    - "../../agentic-canvas-os/docs/MEMORY.md"
    - "../../agentic-canvas-os/docs/AGENTS.md"
    - "../../agentic-canvas-os/docs/DICTIONARY-COMMAND.md"
    - "../../agentic-canvas-os/docs/DICTIONARY-SEMANTIC.md"
    - "../../agentic-canvas-os/docs/DICTIONARY-BINDING.md"
    - "../../agentic-canvas-os/docs/HARNESS-CONTRACTS.md"
    - "../../agentic-canvas-os/docs/RUNTIME-READINESS.md"
    - "../../huijoohwee.github.io/guidelines/prd-tad-guidelines.md"
  invocation_routes:
    slash:
      - "/source.normalize"
      - "/memory.seed"
      - "/prd-tad.create"
      - "/harness.define"
      - "/mcp.capabilities"
      - "/cost.audit"
      - "/canvas.project"
      - "/runtime-ready.check"
      - "/validation.run"
      - "/deploy.guard"
    semantic:
      - "#frontmatter"
      - "#harness"
      - "#token-economics"
      - "#tco"
      - "#ttv"
      - "#vcc"
      - "#foss"
      - "#canvas"
      - "#runtime-ready"
      - "#approval-gate"
      - "#dev-only"
      - "#no-hardcode"
      - "#no-legacy"
    binding:
      - "@source.frontmatter"
      - "@source.body"
      - "@operator"
      - "@local-harness"
      - "@cost-log"
      - "@mcp-gateway"
      - "@canvas"
      - "@runtime-proof"
      - "@approval-gate"
      - "@dev-only"
  stages:
    - id: "care-source-normalization"
      lane: "Source"
      command: "/source.normalize"
      bindings: ["@source.frontmatter", "@source.body", "@operator"]
      semantics: ["#frontmatter", "#no-hardcode", "#no-legacy"]
      output: "redacted source summary, missing-field list, and safety boundary"
      paid_call_count: 0
    - id: "care-plan-ideation"
      lane: "Ideation"
      command: "/memory.seed"
      bindings: ["@source.frontmatter", "@source.body", "@operator"]
      semantics: ["#frontmatter", "#ttv", "#vcc"]
      output: "minimum viable care-coach journey and patient value hypothesis"
      paid_call_count: 0
    - id: "care-probe-branching"
      lane: "Probe"
      command: "/mcp.capabilities"
      bindings: ["@mcp-gateway", "@runtime-proof", "@source.body"]
      semantics: ["#mcp", "#runtime-ready", "#ttv"]
      output: "probe.generate options, user-selected branch path, checkpoint fork metadata, and resolved-path exemplar"
      paid_call_count: 0
    - id: "care-harness-definition"
      lane: "Harness"
      command: "/harness.define"
      bindings: ["@local-harness", "@cost-log", "@mcp-gateway"]
      semantics: ["#harness", "#token-economics", "#approval-gate"]
      output: "typed care-agent manifest with schemas, bounds, fallback, and cost ledger"
      paid_call_count: 0
    - id: "care-canvas-projection"
      lane: "Canvas"
      command: "/canvas.project"
      bindings: ["@canvas", "@runtime-proof", "@approval-gate"]
      semantics: ["#canvas", "#runtime-ready", "#dev-only"]
      output: "Storyboard cards and Rich Media proof surfaces from source-owned frontmatter"
      paid_call_count: 0
    - id: "care-validation"
      lane: "Validation"
      command: "/validation.run"
      bindings: ["@runtime-proof", "@dev-only"]
      semantics: ["#vcc", "#no-hardcode", "#runtime-ready"]
      output: "parse, route, schema, cost, approval, and deploy-boundary proof"
      paid_call_count: 0
  gates:
    clinical_decision: "blocked; route to clinician or emergency instruction"
    phi_upload: "blocked until explicit operator-owned redaction and approval"
    live_provider_calls: "blocked until @operator approves @approval-gate"
    prod_mirror: "blocked by /deploy.guard and @dev-only"
    cloudflare: "blocked by /deploy.guard and @dev-only"
runtime_proof:
  version: "care-agent-runtime-proof/v1"
  status: "runtime-ready"
  proven_at: "2026-07-07"
  proof_scope: "Dev-local Markdown/frontmatter/runtime contract only"
  proof_owner: "knowgrph/canvas focused post-parser test registry"
  validation_cwd: "knowgrph repo root"
  focused_checks:
    - "docs.careAgentDemo.runtimeReady"
    - "docs.careAgentDemo.runReadyMode"
    - "mcp.probeTree.runtime"
    - "probeTree.select.frontmatterFlowCanvasSync"
    - "markdown.frontmatterFlowGraph.fidelity.publishedFlowDiagramDocs.dynamicPanels"
  validation_commands:
    - "npm --prefix canvas run test:ci:unit -- docs.careAgentDemo.runtimeReady"
    - "npm --prefix canvas run test:ci:unit -- docs.careAgentDemo.runReadyMode"
    - "node --test mcp/__tests__/probe-tree-runtime.test.mjs"
    - "npm --prefix canvas run test:ci:unit -- probeTree.select.frontmatterFlowCanvasSync"
    - "FLOW_DIAGRAM_SAMPLE_PATHS=../../huijoohwee/docs/knowgrph-care-agent-demo.md npm --prefix canvas run test:ci:unit -- markdown.frontmatterFlowGraph.fidelity.publishedFlowDiagramDocs.dynamicPanels"
  parsed_frontmatter_flow: true
  computed_frontmatter_flow: true
  probe_tree_canvas_sync_verified: true
  probe_tree_token_budget_verified: true
  probe_tree_zero_recall_verified: true
  probe_tree_cost_logs_verified: true
  probe_tree_non_idempotent_descriptors_verified: true
  probe_tree_semantic_frontmatter_keys_verified: true
  probe_tree_clean_room_smoke_verified: true
  dictionary_routes_verified: true
  semantic_html_verified: true
  zero_cost_local_harness_verified: true
  safety_gates_verified: true
  prod_mirror_mutated: false
  cloudflare_deploy_mutated: false
  live_provider_fields_blank: true
care_agent_harness:
  id: "care-agent-local-harness"
  owner: "existing shared Agentic OS harness utilities"
  mode: "local-dry-run-first"
  input_schema:
    fields: ["redactedCarePlan", "language", "literacyLevel", "caregiverMode", "cameraHint", "probeThreadRootId", "approvals"]
    rejects: ["rawPhi", "credential", "unboundedLoop", "missingApprovalForClinicalRisk"]
  output_schema:
    fields: ["probeOptions", "selectedProbeNode", "taskCards", "plainLanguageExplanation", "teachBackQuestions", "caregiverHandoff", "safetyEscalations", "costLog", "validationStatus"]
  fallback:
    schema_error: "reject before token spend"
    safety_risk: "return escalation card and stop"
    approval_missing: "blocked with zero paid calls"
    budget_breach: "blocked with cost summary"
  bounds:
    max_iterations: 1
    circuit_breaker: "schema error, safety risk, missing approval, budget breach, or validation failure"
socket_types:
  care_source_signal: {color: "#0ea5e9", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [care_source_signal]}
  care_task_signal: {color: "#14b8a6", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [care_task_signal]}
  care_safety_signal: {color: "#ef4444", edgeWidthPx: 3, handleStrokeWidthPx: 3, accepts: [care_safety_signal]}
  care_cost_signal: {color: "#f59e0b", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [care_cost_signal]}
  care_proof_signal: {color: "#22c55e", edgeWidthPx: 3, handleStrokeWidthPx: 3, accepts: [care_proof_signal]}
flow_diagrams:
  key: "flow_diagrams"
  type: "object"
  value:
    care_agent_flowchart:
      key: "care_agent_flowchart"
      type: "mermaid_flowchart"
      floatingPanelView: "flowchart"
      floatingPanelOpen: true
      bottomPanelTab: "flowchart"
      bottomPanelOpen: true
      value: |-
        flowchart LR
          source["Redacted care-plan source"]
          normalize["/source.normalize #frontmatter @source.frontmatter"]
          ideate["/memory.seed #ttv #vcc @source.body"]
          harness["/harness.define #harness @local-harness"]
          cost["/cost.audit #token-economics #tco @cost-log"]
          canvas["/canvas.project #canvas @canvas"]
          validate["/validation.run #vcc @runtime-proof"]
          guard["/deploy.guard #dev-only @operator"]
          source --> normalize --> ideate --> harness --> cost --> canvas --> validate --> guard
    care_agent_event_model:
      key: "care_agent_event_model"
      type: "mermaid_eventmodeling"
      floatingPanelView: "eventModeling"
      floatingPanelOpen: true
      bottomPanelTab: "eventModeling"
      bottomPanelOpen: true
      value: |-
        eventmodeling
        tf 01 ui RedactedCarePlanSubmitted
        tf 02 cmd NormalizeCarePlanSource
        tf 03 evt SourceSafetyBoundaryReady
        tf 04 cmd DefineCareAgentHarness
        tf 05 evt HarnessContractReady
        tf 06 cmd BuildTaskCards
        tf 07 evt TaskCardsReady
        tf 08 cmd RunTeachBackCheck
        tf 09 evt ComprehensionSignalsReady
        tf 10 cmd PrepareCaregiverHandoff
        tf 11 evt HandoffReady
        tf 12 cmd ValidateLocalProof
        tf 13 evt RuntimeProofOrGateReady
flow:
  direction: {key: direction, type: string, value: "LR"}
  edgeType: {key: edgeType, type: string, value: "smoothstep"}
  balancedViewportPreset: {key: balancedViewportPreset, type: string, value: "widgetFrontmatter"}
  computed: {key: computed, type: boolean, value: true}
  snapToGrid: {key: snapToGrid, type: boolean, value: true}
  nodes:
    - id: {key: id, type: string, value: "care_source"}
      type: {key: type, type: string, value: "InputWidget"}
      label: {key: label, type: string, value: "Care Source"}
      position: {key: position, type: object, value: {"x":-522.8889524019576,"y":-836.9403955453596}}
      handles: {key: handles, type: object, value: {"source":["redactedCarePlan","language","literacyLevel"]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{},"out":{"care_source_signal_out":"care_source_signal"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:care_source"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 3}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 2}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      image: {key: image, type: string, value: "http://localhost:5185/api/storage/media/airvio/runs/upload-088c7665f3bdba06/image/image-088c7665f3bdba06.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC0wODhjNzY2NWYzYmRiYTA2IiwiZXhwaXJlc0F0IjoxNzgzNTE2ODA0MTA2fQ"}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Source-owned redacted care-plan intake. It carries synthetic or operator-redacted notes only and rejects PHI or credentials."}
      lane: {key: lane, type: string, value: "Source"}
      language: {key: language, type: string, value: "multilingual"}
      lastRunAt: {key: lastRunAt, type: string, value: "2026-07-08T13:32:01.439Z"}
      literacyLevel: {key: literacyLevel, type: string, value: "plain-language"}
      media: {key: media, type: string, value: "http://localhost:5185/api/storage/media/airvio/runs/upload-088c7665f3bdba06/image/image-088c7665f3bdba06.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC0wODhjNzY2NWYzYmRiYTA2IiwiZXhwaXJlc0F0IjoxNzgzNTE2ODA0MTA2fQ"}
      media_kind: {key: media_kind, type: string, value: "image"}
      media_url: {key: media_url, type: string, value: "http://localhost:5185/api/storage/media/airvio/runs/upload-088c7665f3bdba06/image/image-088c7665f3bdba06.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC0wODhjNzY2NWYzYmRiYTA2IiwiZXhwaXJlc0F0IjoxNzgzNTE2ODA0MTA2fQ"}
      mediaKind: {key: mediaKind, type: string, value: "image"}
      mediaUrl: {key: mediaUrl, type: string, value: "http://localhost:5185/api/storage/media/airvio/runs/upload-088c7665f3bdba06/image/image-088c7665f3bdba06.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC0wODhjNzY2NWYzYmRiYTA2IiwiZXhwaXJlc0F0IjoxNzgzNTE2ODA0MTA2fQ"}
      output:
        key: output
        type: string
        value: |
          # Care Source

          Run-ready card output generated from the selected InputWidget node without a provider call.

          | Field | Source-backed value |
          | --- | --- |
          | lane | Source |
          | summary | check my hand, numb...<br>![空武.jpg](http://localhost:5185/api/storage/media/airvio/runs/upload-088c7665f3bdba06/image/image-088c7665f3bdba06.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC0wODhjNzY2NWYzYmRiYTA2IiwiZXhwaXJlc0F0IjoxNzgzNTE2ODA0MTA2fQ) |
          | output | # Care Source<br>Run-ready card output generated from the selected InputWidget node without a provider call.<br>\| Field \| Source-backed value \|<br>\| --- \| --- \|<br>\| lane \| Source \|<br>\| summary \| check my hand, numb...<br>![空武.jpg](http://localhost:5185/api/storage/media/airvio/runs/upload-088c7665f3bdba06/image/image-088c7665f3bdba06.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC0wODhjNzY2NWYzYmRiYTA2IiwiZXhwaXJlc0F0IjoxNzgzNTE2ODA0MTA2fQ) \|<br>\| output \| # Care Source<br>Run-ready card output generated from the selected InputWidget node without a provider call.<br>\\| Field \\| Source-backed value \\|<br>\\| --- \\| --- \\|<br>\\| lane \\| Source \\|<br>\\| summary \\| check my hand, numb...<br>![空武.jpg](http://localhost:5185/api/storage/media/airvio/runs/upload-088c7665f3bdba06/image/image-088c7665f3bdba06.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC0wODhjNzY2NWYzYmRiYTA2IiwiZXhwaXJlc0F0IjoxNzgzNTE2ODA0MTA2fQ) \\|<br>\\| kgc:readingSummary \\| Source-owned redacted care-plan intake. It carries synthetic or operator-redacted notes only and rejects PHI or credentials. \\| \|<br>\| kgc:readingSummary \| Source-owned redacted care-plan intake. It carries synthetic or operator-redacted notes only and rejects PHI or credentials. \| |
          | kgc:readingSummary | Source-owned redacted care-plan intake. It carries synthetic or operator-redacted notes only and rejects PHI or credentials. |

      outputMimeType: {key: outputMimeType, type: string, value: "text/markdown; charset=utf-8"}
      outputModel: {key: outputModel, type: string, value: "source-backed-card-run"}
      outputSrcDoc:
        key: outputSrcDoc
        type: string
        value: |
          <!doctype html><html><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1"><title>Care Source</title><style>html{color-scheme:dark light}body{margin:0;padding:0;font-family:system-ui,-apple-system,Segoe UI,Roboto,sans-serif;background:rgba(255, 255, 255, 0.95);color:#111827}main{max-width:980px;margin:0 auto;padding:16px}a{color:#3b82f6}pre,code{font-family:ui-monospace,SFMono-Regular,Menlo,Monaco,Consolas,monospace}pre{background:#f8fafc;border:1px solid #e2e8f0;border-radius:8px;padding:12px;overflow:auto;color:#0f172a}code{background:#f8fafc;border:1px solid #e2e8f0;border-radius:6px;padding:1px 4px;color:#0f172a}table{border-collapse:collapse;width:100%}th,td{border:1px solid #e5e7eb;padding:6px 8px;vertical-align:top}blockquote{border-left:3px solid #e5e7eb;margin:0;padding:0 0 0 12px;color:#4b5563}hr{border:0;border-top:1px solid #e5e7eb;margin:16px 0}img,video{max-width:100%;height:auto}</style></head><body><main><section data-kg-rich-media-markdown-srcdoc="1"><h1>Care Source</h1>
          <p>Run-ready card output generated from the selected InputWidget node without a provider call.</p>
          <table>
          <thead>
          <tr>
          <th>Field</th>
          <th>Source-backed value</th>
          </tr>
          </thead>
          <tbody>
          <tr>
          <td>lane</td>
          <td>Source</td>
          </tr>
          <tr>
          <td>summary</td>
          <td>check my hand, numb...&lt;br&gt;<img src="http://localhost:5185/api/storage/media/airvio/runs/upload-088c7665f3bdba06/image/image-088c7665f3bdba06.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC0wODhjNzY2NWYzYmRiYTA2IiwiZXhwaXJlc0F0IjoxNzgzNTE2ODA0MTA2fQ" alt="空武.jpg"></td>
          </tr>
          <tr>
          <td>output</td>
          <td># Care Source&lt;br&gt;Run-ready card output generated from the selected InputWidget node without a provider call.&lt;br&gt;| Field | Source-backed value |&lt;br&gt;| --- | --- |&lt;br&gt;| lane | Source |&lt;br&gt;| summary | check my hand, numb...&lt;br&gt;<img src="http://localhost:5185/api/storage/media/airvio/runs/upload-088c7665f3bdba06/image/image-088c7665f3bdba06.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC0wODhjNzY2NWYzYmRiYTA2IiwiZXhwaXJlc0F0IjoxNzgzNTE2ODA0MTA2fQ" alt="空武.jpg"> |&lt;br&gt;| output | # Care Source&lt;br&gt;Run-ready card output generated from the selected InputWidget node without a provider call.&lt;br&gt;| Field | Source-backed value |&lt;br&gt;| --- | --- |&lt;br&gt;| lane | Source |&lt;br&gt;| summary | check my hand, numb...&lt;br&gt;<img src="http://localhost:5185/api/storage/media/airvio/runs/upload-088c7665f3bdba06/image/image-088c7665f3bdba06.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC0wODhjNzY2NWYzYmRiYTA2IiwiZXhwaXJlc0F0IjoxNzgzNTE2ODA0MTA2fQ" alt="空武.jpg"> |&lt;br&gt;| kgc:readingSummary | Source-owned redacted care-plan intake. It carries synthetic or operator-redacted notes only and rejects PHI or credentials. | |&lt;br&gt;| kgc:readingSummary | Source-owned redacted care-plan intake. It carries synthetic or operator-redacted notes only and rejects PHI or credentials. |</td>
          </tr>
          <tr>
          <td>kgc:readingSummary</td>
          <td>Source-owned redacted care-plan intake. It carries synthetic or operator-redacted notes only and rejects PHI or credentials.</td>
          </tr>
          </tbody>
          </table>
          </section></main></body></html>

      redactedCarePlan: {key: redactedCarePlan, type: string, value: "Synthetic care-plan note: take a morning walk if cleared, track symptoms, prepare questions for the next visit, and ask a clinician about medication uncertainty."}
      summary:
        key: summary
        type: string
        value: |
          check my hand, numb...

          ![空武.jpg](http://localhost:5185/api/storage/media/airvio/runs/upload-088c7665f3bdba06/image/image-088c7665f3bdba06.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC0wODhjNzY2NWYzYmRiYTA2IiwiZXhwaXJlc0F0IjoxNzgzNTE2ODA0MTA2fQ)

      thumbnailUrl: {key: thumbnailUrl, type: string, value: "http://localhost:5185/api/storage/media/airvio/runs/upload-088c7665f3bdba06/image/image-088c7665f3bdba06.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC0wODhjNzY2NWYzYmRiYTA2IiwiZXhwaXJlc0F0IjoxNzgzNTE2ODA0MTA2fQ"}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 0}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "care_normalize"}
      type: {key: type, type: string, value: "ComputeWidget"}
      label: {key: label, type: string, value: "Normalize Source"}
      position: {key: position, type: object, value: {"x":-14.067901234567785,"y":116.40046296296296}}
      handles: {key: handles, type: object, value: {"target":["redactedCarePlan"],"source":["normalizedSummary","safetyBoundary"]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"care_source_signal_in":"care_source_signal"},"out":{"care_task_signal_out":"care_task_signal"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:care_normalize"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 2}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      invocation: {key: invocation, type: string, value: "/source.normalize #frontmatter #no-hardcode @source.frontmatter @source.body"}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Normalization removes stale or unsafe source content at the document source and surfaces missing care-plan fields before any model spend."}
      lane: {key: lane, type: string, value: "Source"}
      normalizedSummary: {key: normalizedSummary, type: string, value: ""}
      safetyBoundary: {key: safetyBoundary, type: string, value: "No diagnosis, dosage change, emergency triage, or PHI persistence."}
      "visual:height": {key: "visual:height", type: number, value: 203}
      "visual:importance": {key: "visual:importance", type: number, value: 20}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 15.65685424949238}
      "visual:width": {key: "visual:width", type: number, value: 360}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 1}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "care_tasks"}
      type: {key: type, type: string, value: "ComputeWidget"}
      label: {key: label, type: string, value: "Care Task Cards"}
      position: {key: position, type: object, value: {"x":409.9320987654322,"y":-150.59953703703704}}
      handles: {key: handles, type: object, value: {"target":["normalizedSummary","language"],"source":["taskCards","teachBackQuestions"]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"care_task_signal_in":"care_task_signal"},"out":{"care_task_signal_out":"care_task_signal"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:care_tasks"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 3}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 2}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      invocation: {key: invocation, type: string, value: "/memory.seed /prd-tad.create #ttv #vcc @source.body @operator"}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Minimum viable task-card generation for patient engagement: explain, confirm understanding, and prepare caregiver follow-up."}
      lane: {key: lane, type: string, value: "Ideation"}
      taskCards: {key: taskCards, type: string, value: ""}
      teachBackQuestions: {key: teachBackQuestions, type: string, value: ""}
      "visual:importance": {key: "visual:importance", type: number, value: 20}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 15.65685424949238}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 2}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "care_probe"}
      type: {key: type, type: string, value: "ComputeWidget"}
      label: {key: label, type: string, value: "Probe Tree Branches"}
      position: {key: position, type: object, value: {"x":833.9320987654322,"y":-150.59953703703704}}
      handles: {key: handles, type: object, value: {"target":["taskCards","teachBackQuestions"],"source":["probeOptions","checkpointPolicy"]}}
      checkpointPolicy: {key: checkpointPolicy, type: string, value: "Markdown graph store is the only persistent checkpoint source; no native checkpointer datastore."}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"care_task_signal_in":"care_task_signal"},"out":{"care_task_signal_out":"care_task_signal"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:care_probe"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 2}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      invocation: {key: invocation, type: string, value: "/mcp.capabilities #mcp #runtime-ready @mcp-gateway @runtime-proof"}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Probe-tree branching asks the next best care-plan clarification, persists the selected path as type: probe markdown, and writes resolved exemplars to local memory."}
      lane: {key: lane, type: string, value: "Probe"}
      probeOptions: {key: probeOptions, type: array, value: []}
      probeTools: {key: probeTools, type: array, value: ["knowgrph.probe.generate","knowgrph.probe.select","knowgrph.probe.evolve"]}
      "visual:importance": {key: "visual:importance", type: number, value: 20}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 15.65685424949238}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 3}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "care_harness"}
      type: {key: type, type: string, value: "ComputeWidget"}
      label: {key: label, type: string, value: "Harness Contract"}
      position: {key: position, type: object, value: {"x":1257.9320987654323,"y":-150.59953703703704}}
      handles: {key: handles, type: object, value: {"target":["taskCards","probeOptions"],"source":["manifest","costLog","blockedReasons"]}}
      blockedReasons: {key: blockedReasons, type: array, value: ["clinical_decision_without_clinician","phi_upload_without_redaction","missing_operator_approval_for_live_call"]}
      costLog: {key: costLog, type: object, value: {"model":"local-dry-run","prompt_tokens":0,"completion_tokens":0,"cache_hits":0,"estimated_cost_usd":0}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"care_task_signal_in":"care_task_signal"},"out":{"care_proof_signal_out":"care_proof_signal"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:care_harness"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 2}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      invocation: {key: invocation, type: string, value: "/harness.define /mcp.capabilities /cost.audit #harness #token-economics @local-harness @cost-log @mcp-gateway"}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Typed local harness manifest with one-iteration bounds, safety fallback, approval gates, and zero-cost dry-run ledger."}
      lane: {key: lane, type: string, value: "Harness"}
      manifest: {key: manifest, type: string, value: ""}
      "visual:importance": {key: "visual:importance", type: number, value: 20}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 15.65685424949238}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 4}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "care_canvas"}
      type: {key: type, type: string, value: "RichMediaPanel"}
      label: {key: label, type: string, value: "Patient Coach Panel"}
      position: {key: position, type: object, value: {"x":-113.94238535767022,"y":-682.3836865764334}}
      handles: {key: handles, type: object, value: {"target":["manifest","taskCards"],"source":["outputSrcDoc","runtimeProof"]}}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"care_proof_signal_in":"care_proof_signal"},"out":{"care_proof_signal_out":"care_proof_signal"}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "richMediaPanel"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 2}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      invocation: {key: invocation, type: string, value: "/canvas.project #canvas #runtime-ready @canvas @runtime-proof"}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Semantic HTML Rich Media panel for care-agent proof surfaces. It uses article, header, section, heading, paragraph, and list elements instead of generic containers."}
      lane: {key: lane, type: string, value: "Canvas"}
      output:
        key: output
        type: textarea
        value: |
          # Care Source

          Run-ready card output generated from the selected InputWidget node without a provider call.

          | Field | Source-backed value |
          | --- | --- |
          | lane | Source |
          | summary | check my hand, numb...<br>![空武.jpg](http://localhost:5185/api/storage/media/airvio/runs/upload-088c7665f3bdba06/image/image-088c7665f3bdba06.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC0wODhjNzY2NWYzYmRiYTA2IiwiZXhwaXJlc0F0IjoxNzgzNTE2ODA0MTA2fQ) |
          | output | # Care Source<br>Run-ready card output generated from the selected InputWidget node without a provider call.<br>\| Field \| Source-backed value \|<br>\| --- \| --- \|<br>\| lane \| Source \|<br>\| summary \| check my hand, numb...<br>![空武.jpg](http://localhost:5185/api/storage/media/airvio/runs/upload-088c7665f3bdba06/image/image-088c7665f3bdba06.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC0wODhjNzY2NWYzYmRiYTA2IiwiZXhwaXJlc0F0IjoxNzgzNTE2ODA0MTA2fQ) \|<br>\| output \| # Care Source<br>Run-ready card output generated from the selected InputWidget node without a provider call.<br>\\| Field \\| Source-backed value \\|<br>\\| --- \\| --- \\|<br>\\| lane \\| Source \\|<br>\\| summary \\| check my hand, numb...<br>![空武.jpg](http://localhost:5185/api/storage/media/airvio/runs/upload-088c7665f3bdba06/image/image-088c7665f3bdba06.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC0wODhjNzY2NWYzYmRiYTA2IiwiZXhwaXJlc0F0IjoxNzgzNTE2ODA0MTA2fQ) \\|<br>\\| kgc:readingSummary \\| Source-owned redacted care-plan intake. It carries synthetic or operator-redacted notes only and rejects PHI or credentials. \\| \|<br>\| kgc:readingSummary \| Source-owned redacted care-plan intake. It carries synthetic or operator-redacted notes only and rejects PHI or credentials. \| |
          | kgc:readingSummary | Source-owned redacted care-plan intake. It carries synthetic or operator-redacted notes only and rejects PHI or credentials. |

      outputMimeType: {key: outputMimeType, type: string, value: "text/markdown; charset=utf-8"}
      outputModel: {key: outputModel, type: string, value: "source-backed-card-run"}
      outputSrcDoc:
        key: outputSrcDoc
        type: textarea
        value: |
          <!doctype html><html><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1"><title>Care Source</title><style>html{color-scheme:dark light}body{margin:0;padding:0;font-family:system-ui,-apple-system,Segoe UI,Roboto,sans-serif;background:rgba(255, 255, 255, 0.95);color:#111827}main{max-width:980px;margin:0 auto;padding:16px}a{color:#3b82f6}pre,code{font-family:ui-monospace,SFMono-Regular,Menlo,Monaco,Consolas,monospace}pre{background:#f8fafc;border:1px solid #e2e8f0;border-radius:8px;padding:12px;overflow:auto;color:#0f172a}code{background:#f8fafc;border:1px solid #e2e8f0;border-radius:6px;padding:1px 4px;color:#0f172a}table{border-collapse:collapse;width:100%}th,td{border:1px solid #e5e7eb;padding:6px 8px;vertical-align:top}blockquote{border-left:3px solid #e5e7eb;margin:0;padding:0 0 0 12px;color:#4b5563}hr{border:0;border-top:1px solid #e5e7eb;margin:16px 0}img,video{max-width:100%;height:auto}</style></head><body><main><section data-kg-rich-media-markdown-srcdoc="1"><h1>Care Source</h1>
          <p>Run-ready card output generated from the selected InputWidget node without a provider call.</p>
          <table>
          <thead>
          <tr>
          <th>Field</th>
          <th>Source-backed value</th>
          </tr>
          </thead>
          <tbody>
          <tr>
          <td>lane</td>
          <td>Source</td>
          </tr>
          <tr>
          <td>summary</td>
          <td>check my hand, numb...&lt;br&gt;<img src="http://localhost:5185/api/storage/media/airvio/runs/upload-088c7665f3bdba06/image/image-088c7665f3bdba06.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC0wODhjNzY2NWYzYmRiYTA2IiwiZXhwaXJlc0F0IjoxNzgzNTE2ODA0MTA2fQ" alt="空武.jpg"></td>
          </tr>
          <tr>
          <td>output</td>
          <td># Care Source&lt;br&gt;Run-ready card output generated from the selected InputWidget node without a provider call.&lt;br&gt;| Field | Source-backed value |&lt;br&gt;| --- | --- |&lt;br&gt;| lane | Source |&lt;br&gt;| summary | check my hand, numb...&lt;br&gt;<img src="http://localhost:5185/api/storage/media/airvio/runs/upload-088c7665f3bdba06/image/image-088c7665f3bdba06.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC0wODhjNzY2NWYzYmRiYTA2IiwiZXhwaXJlc0F0IjoxNzgzNTE2ODA0MTA2fQ" alt="空武.jpg"> |&lt;br&gt;| output | # Care Source&lt;br&gt;Run-ready card output generated from the selected InputWidget node without a provider call.&lt;br&gt;| Field | Source-backed value |&lt;br&gt;| --- | --- |&lt;br&gt;| lane | Source |&lt;br&gt;| summary | check my hand, numb...&lt;br&gt;<img src="http://localhost:5185/api/storage/media/airvio/runs/upload-088c7665f3bdba06/image/image-088c7665f3bdba06.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC0wODhjNzY2NWYzYmRiYTA2IiwiZXhwaXJlc0F0IjoxNzgzNTE2ODA0MTA2fQ" alt="空武.jpg"> |&lt;br&gt;| kgc:readingSummary | Source-owned redacted care-plan intake. It carries synthetic or operator-redacted notes only and rejects PHI or credentials. | |&lt;br&gt;| kgc:readingSummary | Source-owned redacted care-plan intake. It carries synthetic or operator-redacted notes only and rejects PHI or credentials. |</td>
          </tr>
          <tr>
          <td>kgc:readingSummary</td>
          <td>Source-owned redacted care-plan intake. It carries synthetic or operator-redacted notes only and rejects PHI or credentials.</td>
          </tr>
          </tbody>
          </table>
          </section></main></body></html>

      richMediaActiveTab: {key: richMediaActiveTab, type: string, value: "text"}
      runtimeProof: {key: runtimeProof, type: string, value: ""}
      "visual:height": {key: "visual:height", type: number, value: 324}
      "visual:importance": {key: "visual:importance", type: number, value: 20}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 15.65685424949238}
      "visual:width": {key: "visual:width", type: number, value: 576}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 5}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "care_validation"}
      type: {key: type, type: string, value: "ReviewWidget"}
      label: {key: label, type: string, value: "Validation Gate"}
      position: {key: position, type: object, value: {"x":1595.7829194413932,"y":-661.3772091354265}}
      handles: {key: handles, type: object, value: {"target":["runtimeProof","costLog"],"source":["validationStatus","deployBoundary"]}}
      deployBoundary: {key: deployBoundary, type: string, value: "Dev-only; no Prod mirror or Cloudflare deploy without explicit operator instruction."}
      "flow:portTypes": {key: "flow:portTypes", type: object, value: {"in":{"care_proof_signal_in":"care_proof_signal"},"out":{}}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:care_validation"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 1}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      invocation: {key: invocation, type: string, value: "/validation.run /deploy.guard #vcc #dev-only #approval-gate @runtime-proof @dev-only @operator"}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Validation gate requires parse, route, schema, cost, safety, approval, and deploy-boundary proof before runtime-ready status."}
      lane: {key: lane, type: string, value: "Validation"}
      validationStatus: {key: validationStatus, type: string, value: "pending"}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 6}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "care_source-media-panel"}
      type: {key: type, type: string, value: "RichMediaPanel"}
      label: {key: label, type: string, value: "空武.jpg"}
      position: {key: position, type: object, value: {"x":-779.2079874414642,"y":-119.87324393358875}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "richMediaPanel"}
      "flow:widgetTypeId": {key: "flow:widgetTypeId", type: string, value: "default"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 1}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 1}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      image: {key: image, type: string, value: "http://localhost:5185/api/storage/media/airvio/runs/upload-088c7665f3bdba06/image/image-088c7665f3bdba06.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC0wODhjNzY2NWYzYmRiYTA2IiwiZXhwaXJlc0F0IjoxNzgzNTE2ODA0MTA2fQ"}
      imageUrl: {key: imageUrl, type: text, value: "http://localhost:5185/api/storage/media/airvio/runs/upload-088c7665f3bdba06/image/image-088c7665f3bdba06.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC0wODhjNzY2NWYzYmRiYTA2IiwiZXhwaXJlc0F0IjoxNzgzNTE2ODA0MTA2fQ"}
      media: {key: media, type: string, value: "http://localhost:5185/api/storage/media/airvio/runs/upload-088c7665f3bdba06/image/image-088c7665f3bdba06.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC0wODhjNzY2NWYzYmRiYTA2IiwiZXhwaXJlc0F0IjoxNzgzNTE2ODA0MTA2fQ"}
      media_kind: {key: media_kind, type: string, value: "image"}
      media_url: {key: media_url, type: string, value: "http://localhost:5185/api/storage/media/airvio/runs/upload-088c7665f3bdba06/image/image-088c7665f3bdba06.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC0wODhjNzY2NWYzYmRiYTA2IiwiZXhwaXJlc0F0IjoxNzgzNTE2ODA0MTA2fQ"}
      mediaKind: {key: mediaKind, type: string, value: "image"}
      mediaSource: {key: mediaSource, type: string, value: "storyboard-card-media-drop"}
      mediaSourceKey: {key: mediaSourceKey, type: string, value: "sha256:088c7665f3bdba063c925453157c5694d4db12f5c8b34e872bc7a1960a821216"}
      mediaUrl: {key: mediaUrl, type: string, value: "http://localhost:5185/api/storage/media/airvio/runs/upload-088c7665f3bdba06/image/image-088c7665f3bdba06.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC0wODhjNzY2NWYzYmRiYTA2IiwiZXhwaXJlc0F0IjoxNzgzNTE2ODA0MTA2fQ"}
      output: {key: output, type: textarea, value: ""}
      outputSrcDoc: {key: outputSrcDoc, type: textarea, value: ""}
      richMediaActiveTab: {key: richMediaActiveTab, type: string, value: "image"}
      storyboardCanvasRichMediaPanel: {key: storyboardCanvasRichMediaPanel, type: boolean, value: true}
      storyboardCardMediaSourceKind: {key: storyboardCardMediaSourceKind, type: string, value: "image"}
      storyboardCardMediaTargetId: {key: storyboardCardMediaTargetId, type: string, value: "care_source"}
      thumbnailUrl: {key: thumbnailUrl, type: string, value: "http://localhost:5185/api/storage/media/airvio/runs/upload-088c7665f3bdba06/image/image-088c7665f3bdba06.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC0wODhjNzY2NWYzYmRiYTA2IiwiZXhwaXJlc0F0IjoxNzgzNTE2ODA0MTA2fQ"}
      "visual:importance": {key: "visual:importance", type: number, value: 16}
      "visual:nodeSize": {key: "visual:nodeSize", type: number, value: 14}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 0}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
  edges:
    - {"id":"edge_source_normalize","source":"care_source","sourceHandle":"care_source_signal_out","target":"care_normalize","targetHandle":"care_source_signal_in","type":"care_source_signal"}
    - {"id":"edge_normalize_tasks","source":"care_normalize","sourceHandle":"care_task_signal_out","target":"care_tasks","targetHandle":"care_task_signal_in","type":"care_task_signal"}
    - {"id":"edge_tasks_probe","source":"care_tasks","sourceHandle":"care_task_signal_out","target":"care_probe","targetHandle":"care_task_signal_in","type":"care_task_signal"}
    - {"id":"edge_probe_harness","source":"care_probe","sourceHandle":"care_task_signal_out","target":"care_harness","targetHandle":"care_task_signal_in","type":"care_task_signal"}
    - {"id":"edge_harness_canvas","source":"care_harness","sourceHandle":"care_proof_signal_out","target":"care_canvas","targetHandle":"care_proof_signal_in","type":"care_proof_signal"}
    - {"id":"edge_canvas_validation","source":"care_canvas","sourceHandle":"care_proof_signal_out","target":"care_validation","targetHandle":"care_proof_signal_in","type":"care_proof_signal"}
    - {"id":"e1","source":"care_source-media-panel","sourceHandle":"imageUrl","target":"care_source","targetHandle":"mediaUrl","label":"linksTo"}
    - {"id":"e2","source":"care_source","sourceHandle":"redactedCarePlan","target":"care_tasks","targetHandle":"normalizedSummary","label":"linksTo"}
strybldr_storyboard:
  version: '1'
  runId: care-agent-demo
  createdAtMs: '1783468800000'
  notes: Neutral care-agent payload for local-first patient engagement. Use synthetic or redacted source fields before any live provider call.
  workflow:
    stages:
      - Source
      - Ideation
      - Probe
      - Harness
      - Canvas
      - Safety
      - Cost
      - Validation
      - Publish
    publish:
      id: care-agent-local-publish-packet
      label: Local publish packet
      policy: Write local packet fields only; do not claim Prod, Cloudflare, provider IDs, patient outcomes, or live evidence without explicit operator approval and returned proof.
  sources:
    - sourceUnitId: care-agent-demo-source
      workspacePath: docs/knowgrph-care-agent-demo.md
      relativePath: knowgrph-care-agent-demo.md
      originalName: Care agent demo source
      mediaKind: doc
      mimeHint: text/markdown
      byteSize: '0'
      textHash: care-agent-demo
      mediaUrl: ''
  elements:
    - id: care-source-card
      sourceUnitId: care-agent-demo-source
      label: Care source
      confidence: 1
      sourceBox: null
      evidenceKind: source-metadata
      provider: knowgrph
      lane: Source
      order: 1
      prompt: 'Run /source.normalize #frontmatter #no-hardcode @source.frontmatter @source.body.'
      action: Keep source notes synthetic or redacted; reject PHI, credentials, and provider-owned secrets.
      summary: Source intake owns the care-plan context and safety boundary before any agent step runs.
    - id: care-ideation-card
      sourceUnitId: care-agent-demo-source
      label: Care-plan ideation
      confidence: 1
      sourceBox: null
      evidenceKind: agentic-os-invocation
      provider: knowgrph
      lane: Ideation
      order: 2
      prompt: 'Run /memory.seed /prd-tad.create #ttv #vcc #foss @source.body @operator.'
      action: Produce the smallest patient-engagement workflow with clear time-to-value and VCC checks.
      summary: Ideation turns redacted care notes into task cards, teach-back prompts, and caregiver handoff scope.
    - id: care-harness-card
      sourceUnitId: care-agent-demo-source
      label: Care harness
      confidence: 1
      sourceBox: null
      evidenceKind: runtime-plan
      provider: knowgrph-local-care-dry-run
      lane: Harness
      order: 3
      prompt: 'Run /harness.define /mcp.capabilities /cost.audit #harness #token-economics @local-harness @cost-log @mcp-gateway.'
      action: Define typed input, output, fallback, cost log, max iteration, and approval gates.
      summary: Harness definition blocks unsafe clinical, PHI, paid, mutating, and deployment paths by default.
    - id: care-probe-card
      sourceUnitId: care-agent-demo-source
      label: Probe-tree branching
      confidence: 1
      sourceBox: null
      evidenceKind: probe-tree-runtime
      provider: knowgrph-local-probe-tree
      lane: Probe
      order: 4
      prompt: Run knowgrph.probe.generate, select one option, then evolve after resolution.
      action: 'Persist user-selected clarification paths as type: probe markdown nodes with branches-to edges.'
      summary: Probe-tree runtime turns vague care-plan intake into a bounded branch path and local memory exemplar.
    - id: care-canvas-card
      sourceUnitId: care-agent-demo-source
      label: Canvas projection
      confidence: 1
      sourceBox: null
      evidenceKind: canvas-proof-plan
      provider: knowgrph
      lane: Canvas
      order: 5
      prompt: 'Run /canvas.project #canvas #runtime-ready @canvas @runtime-proof.'
      action: Project source-backed cards and semantic HTML panel through existing Canvas owners.
      summary: Canvas projection uses Storyboard and Rich Media surfaces without renderer forks or dashboard-only state.
    - id: care-safety-card
      sourceUnitId: care-agent-demo-source
      label: Safety gate
      confidence: 1
      sourceBox: null
      evidenceKind: safety-boundary
      provider: knowgrph
      lane: Safety
      order: 6
      prompt: Check clinical decision, emergency, medication-dose, conflicting-instruction, and PHI upload gates.
      action: Route high-risk requests to clinician or emergency guidance and stop the agent loop.
      summary: Safety gate keeps the demo as a coach and explanation aid, not a medical decision system.
    - id: care-cost-card
      sourceUnitId: care-agent-demo-source
      label: Cost audit
      confidence: 1
      sourceBox: null
      evidenceKind: cost-ledger
      provider: knowgrph-local-care-dry-run
      lane: Cost
      order: 7
      prompt: 'Run /cost.audit #token-economics #tco #foss @cost-log @operator.'
      action: Keep local proof zero-cost and compare any proposed live dependency against FOSS or existing-owner alternatives.
      summary: Cost audit reports token, cache, TCO, and budget fields before any paid call can run.
    - id: care-validation-card
      sourceUnitId: care-agent-demo-source
      label: Validation
      confidence: 1
      sourceBox: null
      evidenceKind: runtime-review
      provider: knowgrph
      lane: Validation
      order: 8
      prompt: 'Run /validation.run #vcc #no-hardcode @runtime-proof @dev-only.'
      action: Require focused parse, route, schema, cost, safety, approval, and deploy-boundary evidence.
      summary: Validation can promote the doc only after surfaced proof; prose alone keeps it spec-complete.
    - id: care-publish-card
      sourceUnitId: care-agent-demo-source
      label: Publish gate
      confidence: 1
      sourceBox: null
      evidenceKind: runtime-publish
      provider: knowgrph
      lane: Publish
      order: 9
      prompt: 'Run /deploy.guard #dev-only #approval-gate @operator @dev-only.'
      action: Keep publish scope local-only until the operator explicitly authorizes Prod or Cloudflare.
      summary: Publish gate records local packet readiness and blocks mirror or deploy mutation by default.
  cards:
    - nodeId: care_source
      mediaKind: image
      mediaUrl: http://localhost:5185/api/storage/media/airvio/runs/upload-088c7665f3bdba06/image/image-088c7665f3bdba06.jpg?kg_media_token=eyJydW5JZCI6InVwbG9hZC0wODhjNzY2NWYzYmRiYTA2IiwiZXhwaXJlc0F0IjoxNzgzNTE2ODA0MTA2fQ
---

# Knowgrph Care Agent Demo

This is a `/prd-tad.create` minimum viable care-agent seed for multilingual patient engagement. It uses `/source.normalize`, `/memory.seed`, `/harness.define`, `/cost.audit`, `/canvas.project`, `/runtime-ready.check`, `/validation.run`, and `/deploy.guard` with existing `#` semantic filters and `@` bindings. /memory.seed #frontmatter #ttv #vcc @source.frontmatter @source.body

The demo is intentionally neutral and local-first. It explains a redacted care plan, prepares task cards, asks teach-back questions, and creates a caregiver handoff. It does not diagnose, prescribe, alter medication instructions, upload PHI, or claim live provider output. Runtime IDs, generated media, provider evidence, Prod mirror status, and Cloudflare deployment fields remain blank until real proof exists and the operator approves the relevant gate.

## Care-Agent Flow

| Stage | Invocation | Output | Gate |
|---|---|---|---|
| Source | `/source.normalize #frontmatter #no-hardcode @source.frontmatter @source.body` | Redacted source summary and missing-field list | Reject PHI, credentials, and stale hardcodes |
| Ideation | `/memory.seed /prd-tad.create #ttv #vcc #foss @source.body @operator` | Minimum viable patient-engagement journey | Keep scope small and ROI-positive |
| Probe tree | `knowgrph.probe.generate` → `knowgrph.probe.select` → `knowgrph.probe.evolve` | Candidate clarification questions, selected branch node, and memory exemplar | Markdown graph store stays SSOT; local model adapter is host-owned |
| Harness | `/harness.define /mcp.capabilities #harness @local-harness @mcp-gateway` | Typed input, output, fallback, bounds, and capability list | Fail before spend when schema or approval is missing |
| Cost | `/cost.audit #token-economics #tco @cost-log @operator` | Token, cache, TCO, and budget ledger | Local dry-run reports exact zero |
| Canvas | `/canvas.project #canvas @canvas @runtime-proof` | Storyboard cards and semantic Rich Media panel | Existing shared Canvas owners only |
| Validation | `/validation.run #vcc #runtime-ready @runtime-proof @dev-only` | Focused proof or spec-complete gap | No prose-only runtime-ready promotion |
| Deploy guard | `/deploy.guard #dev-only #approval-gate @operator @dev-only` | Local-only status | No Prod or Cloudflare mutation |

## MVP Value

| Persona | Job | First value | Time-to-value target |
|---|---|---|---|
| Patient | Understand the next care-plan steps | Plain-language task cards and teach-back prompts | Under 3 minutes after redacted note entry |
| Caregiver | Know what to support and when to escalate | Handoff checklist and clinician-question list | Under 5 minutes |
| Solo builder | Prove a care-agent harness without cloud spend | Local Storyboard and validation packet | Same working session |

## Harness Contract

```yaml
care_agent_local_harness:
  source: "@source.frontmatter + @source.body"
  normalize: "/source.normalize #frontmatter #no-hardcode @source.frontmatter @source.body"
  ideation: "/memory.seed /prd-tad.create #ttv #vcc #foss @source.body @operator"
  probe_generate: "knowgrph.probe.generate thread_root_id=care-agent-demo current_node_id=care_source k=3 recall_top_k=0 token_budget=1200"
  probe_select: "knowgrph.probe.select writes a fresh type: probe markdown node, branches-to edge, checkpoint metadata, and local-zero cost_log"
  probe_evolve: "knowgrph.probe.evolve scores the resolved path, reports incomplete parents, writes a scoped memory exemplar, and returns local-zero cost_log"
  probe_mutation_semantics: "probe.select and probe.evolve are non-idempotent process tools; host retry behavior must not duplicate branches or silently rewrite scores"
  harness: "/harness.define /mcp.capabilities #harness @local-harness @mcp-gateway"
  cost: "/cost.audit #token-economics #tco @cost-log @operator"
  canvas: "/canvas.project #canvas #runtime-ready @canvas @runtime-proof"
  validation: "/validation.run #vcc #no-hardcode @runtime-proof @dev-only"
  deploy_guard: "/deploy.guard #dev-only #approval-gate @operator @dev-only"
  default_result: "local care-agent packet; paid_call_count remains 0"
  live_result: "blank until @operator approves @approval-gate and returned evidence exists"
```

## Safety Boundaries

| Risk | Required behavior |
|---|---|
| Emergency symptom or red flag | Stop coaching and route to emergency or clinician guidance. |
| Diagnosis or medication-dose request | Explain that the agent cannot decide and prepare clinician questions. |
| Conflicting source instructions | Preserve the conflict and ask for clinician clarification. |
| Raw PHI or credential input | Reject or redact before persistence, model calls, or sharing. |
| Live provider, browser-auth, Prod, or Cloudflare action | Require explicit `@operator` approval and `@approval-gate` evidence. |

## Use

1. From a clean local canvas, run `npm run demo:care-agent -- --port <free-port>`.
2. Confirm Canvas View reports `2D Renderer: Storyboard`.
3. Replace the synthetic care-plan note with operator-redacted source content only.
4. Run `/source.normalize #frontmatter #no-hardcode @source.frontmatter @source.body`.
5. Run `knowgrph.probe.generate` with `thread_root_id=care-agent-demo`, `current_node_id=care_source`, `recall_top_k=0`, `token_budget=1200`, and the redacted context; optionally configure `KNOWGRPH_PROBE_TREE_MODEL` for Ollama-backed local generation.
6. Run `knowgrph.probe.select` for the user-selected option, then run `knowgrph.probe.evolve` after the branch resolves; keep the parent checkpoint materialized in `data/probe-tree`, require local-zero `cost_log` in both responses, and treat any returned incomplete-path status as a validation blocker.
7. Run `/harness.define /cost.audit #harness #token-economics @local-harness @cost-log`.
8. Run `/canvas.project #canvas @canvas @runtime-proof` and review the Storyboard plus Rich Media panel.
9. Run `/validation.run #vcc @runtime-proof @dev-only`.
10. Keep `/deploy.guard #dev-only @dev-only` active unless the operator explicitly authorizes Prod or Cloudflare.

## Acceptance Checklist

- [x] Frontmatter parses from byte zero without repair fallback.
- [x] Clean-canvas demo mode loads this sibling docs source through `VITE_KNOWGRPH_RUN_READY_DEMO=care-agent`.
- [x] Source content is synthetic or operator-redacted.
- [x] `/`, `#`, and `@` tokens match the Agentic OS dictionaries.
- [x] Probe-tree tools are registered in local MCP and `probe.generate` does not mutate graph state.
- [x] `probe.generate` enforces `token_budget` before local model invocation.
- [x] `probe.generate` honors `recall_top_k=0` against a seeded memory store.
- [x] `probe.select` writes one fresh `type: probe` markdown node with a `branches-to` edge under `data/probe-tree`.
- [x] `probe.select` output parses through frontmatter-flow for existing Canvas/sync projection.
- [x] `probe.select` returns a local-zero `cost_log`.
- [x] `probe.evolve` writes one scoped memory exemplar without adding a second checkpoint datastore.
- [x] `probe.evolve` scores the complete traversed path or reports missing parent checkpoints.
- [x] `probe.evolve` returns a local-zero `cost_log`.
- [x] Probe markdown parsing preserves semantic hyphen and dot frontmatter keys.
- [x] `probe.select` and `probe.evolve` are advertised as non-idempotent process tools.
- [x] Harness fields include schemas, fallback, max iteration, circuit breaker, and cost log.
- [x] Local dry-run cost fields remain exact zero.
- [x] Storyboard and Rich Media projection use existing shared Canvas owners.
- [x] Rich Media HTML uses semantic elements and no generic container markup.
- [x] Safety gate blocks clinical decisions, PHI upload, and medication-dose changes.
- [x] Runtime-ready status is backed by focused proof.
- [x] Publish scope remains `local-only` unless the operator explicitly authorizes Prod or Cloudflare.

## Guardrails

- Do not hardcode patient identifiers, PHI, source URLs, provider IDs, credentials, generated media, or runtime proof into repo code or tests.
- Do not add downstream aliases, compatibility remaps, duplicate registries, or renderer forks for care-agent routing.
- Do not backfill runtime-ready claims from prose, screenshots, or stale local state.
- Do not deploy this demo to Prod or Cloudflare from this document alone.
- Keep frontmatter as the source-owned graph and body prose as the human workflow.
w.
