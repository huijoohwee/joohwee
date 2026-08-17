---

title: "Knowgrph MissAlpha Dashboard Demo"
graphId: "md:knowgrph-missalph-dashboard-demo"
doc_type: "Dashboard Renderer Demo"
date: "2026-06-05"
lang: "en-US"
schema: "kgc-dashboard-flow/v1"
template_status: "publish-side reusable demo; no Prod or Cloudflare deploy claim"
deployed_api_claim: false
live_route_validation_required_before_claim: true
sourceKind: "published-markdown-frontmatter"
kgCanvasSurfaceMode: "2d"
kgCanvasRenderMode: "2d"
kgCanvas2dRenderer: "dashboard"
kgDocumentSemanticMode: "document"
kgFrontmatterModeEnabled: true
kgMultiDimTableModeEnabled: false
kgDocumentStructureBaselineLock: false
kgWorkflowManagerModeEnabled: false
kgSharedRendererContract:
  version: "shared-renderer-contract/v1"
  semanticIdentity: "buildScopedGraphSemanticKey"
  cardPreview: "CardMediaPreview + CardMarkdownPreview"
  widgetCard: "canvas:widgetCard"
  richMediaPanel: "RichMediaPanel"
  storyboardDisplay: "2D Renderer: Storyboard Card (default) and Widget variants"
  storyboardSurfaces: ["Cards", "Widgets", "Rich Media Panels"]
  edgeModel: "active graph edges from the selected source graph"
  timelineSurface: "TimelineTransportControls + shared bottom-panel surface"
  rendererPolicy: "frontmatter and source payloads own data; renderers project view state only"
dashboard_pipeline:
  renderer_contract: "2D Renderer: Dashboard"
  graph_owner: "frontmatter flow graph"
  render_owner: "DashboardCanvas"
  charting_owner: "d3"
  view_control_path: "Toolbar -> Canvas View Mode -> Display Controls -> Grid"
  validation_markers:
    - "data-kg-dashboard-canvas=1"
    - "data-kg-dashboard-grid-enabled toggles with shared Grid control"
  non_goals:
    - "no copied third-party dashboard markup"
    - "no fixed chart screenshot"
    - "no fixture backfill"
socket_types:
  SignalFlow: {color: "#14b8a6", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [SignalFlow]}
  ProcessLink: {color: "#14b8a6", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [ProcessLink]}
  RiskLink: {color: "#14b8a6", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [RiskLink]}
  OutputLink: {color: "#14b8a6", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [OutputLink]}
  MediaLink: {color: "#14b8a6", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [MediaLink]}
  ValidationLink: {color: "#14b8a6", edgeWidthPx: 2, handleStrokeWidthPx: 2, accepts: [ValidationLink]}
flow:
  balancedViewportPreset: {key: "balancedViewportPreset", type: string, value: "widgetFrontmatter"}
  direction: {key: direction, type: string, value: "LR"}
  edgeType: {key: edgeType, type: string, value: "smoothstep"}
  computed: {key: computed, type: boolean, value: false}
  snapToGrid: {key: snapToGrid, type: boolean, value: true}
  gridSize: {key: gridSize, type: number, value: 24}
  nodes:
    - id: {key: id, type: string, value: "source_brief"}
      type: {key: type, type: string, value: "DashboardInput"}
      label: {key: label, type: string, value: "Source Brief"}
      position: {x: 80, y: 110}
      input_query: {key: input_query, type: string, value: "Find missing-alpha signals across active research notes"}
      source_signal_count: {key: source_signal_count, type: number, value: 42}
      source_confidence: {key: source_confidence, type: number, value: 71}
      freshness_score: {key: freshness_score, type: number, value: 92}
      properties:
        dashboardRole: "input"
        cadence: "daily"
    - id: {key: id, type: string, value: "flow_positioning"}
      type: {key: type, type: string, value: "DashboardSignal"}
      label: {key: label, type: string, value: "Flow Positioning"}
      position: {x: 360, y: 60}
      process_method: {key: process_method, type: string, value: "cross-source flow normalization"}
      flow_momentum: {key: flow_momentum, type: number, value: 74}
      participation_gap: {key: participation_gap, type: number, value: 18}
      confidence: {key: confidence, type: number, value: 67}
      properties:
        dashboardRole: "process"
        signal_family: "flow"
    - id: {key: id, type: string, value: "skew_diagnostics"}
      type: {key: type, type: string, value: "DashboardSignal"}
      label: {key: label, type: string, value: "Skew Diagnostics"}
      position: {x: 360, y: 250}
      process_method: {key: process_method, type: string, value: "option-skew contrast"}
      skew_gap: {key: skew_gap, type: number, value: 6.4}
      signal_noise: {key: signal_noise, type: number, value: 31}
      conviction_score: {key: conviction_score, type: number, value: 69}
      properties:
        dashboardRole: "process"
        signal_family: "skew"
    - id: {key: id, type: string, value: "catalyst_filter"}
      type: {key: type, type: string, value: "DashboardProcess"}
      label: {key: label, type: string, value: "Catalyst Filter"}
      position: {x: 640, y: 60}
      process_method: {key: process_method, type: string, value: "calendar and event relevance filter"}
      macro_sensitivity: {key: macro_sensitivity, type: number, value: 62}
      event_alignment: {key: event_alignment, type: number, value: 79}
      reprice_window_days: {key: reprice_window_days, type: number, value: 12}
      properties:
        dashboardRole: "process"
        cadence: "weekly"
    - id: {key: id, type: string, value: "risk_guardrail"}
      type: {key: type, type: string, value: "DashboardRisk"}
      label: {key: label, type: string, value: "Risk Guardrail"}
      position: {x: 640, y: 250}
      process_method: {key: process_method, type: string, value: "drawdown and liquidity check"}
      drawdown_risk: {key: drawdown_risk, type: number, value: 28}
      hedge_cost: {key: hedge_cost, type: number, value: 16}
      liquidity_risk: {key: liquidity_risk, type: number, value: 21}
      properties:
        dashboardRole: "process"
        signal_family: "risk"
    - id: {key: id, type: string, value: "thesis_output"}
      type: {key: type, type: string, value: "DashboardOutput"}
      label: {key: label, type: string, value: "Thesis Output"}
      position: {x: 930, y: 70}
      output: {key: output, type: string, value: "Prioritize asymmetric setup notes with positive flow and bounded risk"}
      output_score: {key: output_score, type: number, value: 81}
      alpha_conviction: {key: alpha_conviction, type: number, value: 76}
      review_priority: {key: review_priority, type: number, value: 88}
      properties:
        dashboardRole: "output"
        artifact_type: "summary"
    - id: {key: id, type: string, value: "media_snapshot"}
      type: {key: type, type: string, value: "DashboardMedia"}
      label: {key: label, type: string, value: "Media Snapshot"}
      position: {x: 930, y: 250}
      mediaUrl: {key: mediaUrl, type: string, value: "https://example.invalid/knowgrph/missalph-dashboard-preview"}
      preview_score: {key: preview_score, type: number, value: 69}
      html_preview_available: {key: html_preview_available, type: boolean, value: true}
      properties:
        dashboardRole: "media"
        artifact_type: "preview"
    - id: {key: id, type: string, value: "validation_gate"}
      type: {key: type, type: string, value: "DashboardValidation"}
      label: {key: label, type: string, value: "Validation Gate"}
      position: {x: 1190, y: 160}
      output: {key: output, type: string, value: "Renderer proof requires parsed graph, Dashboard canvas, and Grid state marker"}
      validation_score: {key: validation_score, type: number, value: 88}
      freshness_score: {key: freshness_score, type: number, value: 92}
      drift_risk: {key: drift_risk, type: number, value: 13}
      properties:
        dashboardRole: "output"
        validation_scope: "local app"
  edges:
    - id: {key: id, type: string, value: "edge_source_to_flow"}
      source: {key: source, type: string, value: "source_brief"}
      target: {key: target, type: string, value: "flow_positioning"}
      label: {key: label, type: string, value: "flow signal"}
      type: {key: type, type: string, value: "SignalFlow"}
    - id: {key: id, type: string, value: "edge_source_to_skew"}
      source: {key: source, type: string, value: "source_brief"}
      target: {key: target, type: string, value: "skew_diagnostics"}
      label: {key: label, type: string, value: "skew signal"}
      type: {key: type, type: string, value: "SignalFlow"}
    - id: {key: id, type: string, value: "edge_flow_to_catalyst"}
      source: {key: source, type: string, value: "flow_positioning"}
      target: {key: target, type: string, value: "catalyst_filter"}
      label: {key: label, type: string, value: "candidate filter"}
      type: {key: type, type: string, value: "ProcessLink"}
    - id: {key: id, type: string, value: "edge_skew_to_risk"}
      source: {key: source, type: string, value: "skew_diagnostics"}
      target: {key: target, type: string, value: "risk_guardrail"}
      label: {key: label, type: string, value: "risk contrast"}
      type: {key: type, type: string, value: "RiskLink"}
    - id: {key: id, type: string, value: "edge_catalyst_to_thesis"}
      source: {key: source, type: string, value: "catalyst_filter"}
      target: {key: target, type: string, value: "thesis_output"}
      label: {key: label, type: string, value: "rank output"}
      type: {key: type, type: string, value: "OutputLink"}
    - id: {key: id, type: string, value: "edge_risk_to_thesis"}
      source: {key: source, type: string, value: "risk_guardrail"}
      target: {key: target, type: string, value: "thesis_output"}
      label: {key: label, type: string, value: "guardrail"}
      type: {key: type, type: string, value: "RiskLink"}
    - id: {key: id, type: string, value: "edge_thesis_to_media"}
      source: {key: source, type: string, value: "thesis_output"}
      target: {key: target, type: string, value: "media_snapshot"}
      label: {key: label, type: string, value: "preview artifact"}
      type: {key: type, type: string, value: "MediaLink"}
    - id: {key: id, type: string, value: "edge_media_to_validation"}
      source: {key: source, type: string, value: "media_snapshot"}
      target: {key: target, type: string, value: "validation_gate"}
      label: {key: label, type: string, value: "visual proof"}
      type: {key: type, type: string, value: "ValidationLink"}
    - id: {key: id, type: string, value: "edge_thesis_to_validation"}
      source: {key: source, type: string, value: "thesis_output"}
      target: {key: target, type: string, value: "validation_gate"}
      label: {key: label, type: string, value: "semantic proof"}
      type: {key: type, type: string, value: "ValidationLink"}
validation_checklist:
  - "Open Source Files and select knowgrph-missalph-dashboard-demo.md"
  - "Confirm Canvas View Mode resolves to 2D Renderer: Dashboard"
  - "Toggle Display Controls -> Grid and confirm dashboard grid marker changes"
  - "Confirm metrics derive 8 nodes, 9 edges, node type distribution, relationship type distribution, numeric fields, and semantic buckets"
modelSelection:
  selectionModel: "projected-data"            # renderers project these typed option groups as dropdowns; they do not branch on them
  scope: "local-overrides-global"             # a node-local options.model overrides the matching group's global default
  groups:
    text:
      global: "agnes-2.0-flash"               # group-global default; override per node via options.model
      options:
        - "agnes-2.0-flash"
        - "seed-2-0-mini-260215"
        - "seed-2-0-lite-260228"
        - "seed-2-0-pro-260328"
        - "seed-1-8-251228"
    image:
      global: "seedream-4-0-250828"
      options:
        - "seedream-4-0-250828"
        - "seedream-4-5-251128"
        - "seedream-5-0-260128"
    video:
      global: "seedance-1-0-pro-fast-251015"
      options:
        - "seedance-1-0-pro-fast-251015"
        - "seedance-1-5-pro-251215"
        - "dreamina-seedance-2-0-fast-260128"
        - "dreamina-seedance-2-0-260128"
kgParserRoutingContract:
  version: "knowgrph-parser-routing/v1"
  parserLogic: "opening frontmatter and authored source payloads are SSOT; parsers materialize graphData without renderer-local aliases"
  routingKeys:
    surface: "kgCanvasSurfaceMode"
    renderMode: "kgCanvasRenderMode"
    renderer: "kgCanvas2dRenderer"
    semanticMode: "kgDocumentSemanticMode"
    frontmatterMode: "kgFrontmatterModeEnabled"
    flowGraph: "flow"
    flowNodes: "flow.nodes"
    flowEdges: "flow.edges"
    mermaidBlocks: "flow_diagrams"
    strybldrStoryboard: "kgStrybldrStoryboard"
  diagramKinds:
    - "mermaid_flowchart"
    - "mermaid_gitgraph"
    - "mermaid_architecture"
    - "mermaid_eventmodeling"
    - "mermaid_gantt"
    - "frontmatter_flow"
    - "strybldr_storyboard"
  surfaces:
    - "2D Renderer: Storyboard"
    - "2D Renderer: Storyboard"
    - "BottomPanel/FloatingPanel Mermaid panels"
  edgePolicy: "explicit graphData.edges, flow.edges, workflow.edges, and diagram edges are source-owned SSOT; renderers project visible connectors only"
  forkPolicy: "fork, branch, candidate, and publish metadata remain authored source fields and surface through parsed graph edges without downstream remapping"
---
# Knowgrph MissAlpha Dashboard Demo

This demo is frontmatter-first. It is intended to exercise the local E2E path: published Markdown source file -> typed frontmatter flow parse -> active GraphData -> 2D Dashboard renderer -> shared Grid display control.

It intentionally avoids copied external dashboard markup, fixed chart screenshots, body-side graph mirrors, and backfilled fixture data. The visible dashboard should be derived from the graph in the YAML frontmatter above.
