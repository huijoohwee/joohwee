---
title: "Knowgrph MiroMind Deep Research Strytree Demo - Dynamic Structured Response Dataflow"
graphId: "md:knowgrph-miromind-deep-research-strytree-demo"
doc_type: "MiroMind Deep Research Strytree Demo"
date: "2026-06-05"
lang: "en-US"
schema: "kgc-computing-flow/v1"
implementation_contract:
  - "docs/documents/knowgrph-chat-ai-markdown-pipeline-document.md"
  - "docs/documents/knowgrph-strytree-prd-tad.md"
source_documents:
  - "docs/knowgrph-strytree-demo.md"
  - "docs/knowgrph-research-agent-demo.md"
demo_status: "dev-source capability demo; no Prod or Cloudflare deploy claim"
deployed_api_claim: false
live_route_validation_required_before_claim: true
copyhardcode_forbid: true
validation_input_forbid_hardcode_in_repo: true

storytree_product: "strytree"
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
kgFloatingPanelView: "eventModeling"
kgStrybldrStoryboard: true
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

miromind_deep_research_demo:
  schema_version: "knowgrph-miromind-deep-research-strytree/v1"
  provider_id: "miromind"
  provider_label: "MiroMind API"
  request_mode: "mcp-style structured response"
  task_level: "deep_research"
  active_graph_mutated: false
  output_authority: "frontmatter source -> inline compute -> connected Rich Media Panel render field"
  source_policy: "Use source docs as capability references; do not copy external reports, share URLs, provider payloads, prompts, or page text into repo code."
  input_surfaces:
    - "FloatingPanel Chat"
    - "Markdown YAML frontmatter"
    - "Storyboard renderer"
    - "FlowDiagramSource"
  outputs:
    markdown_flow: "flow.nodes + flow.edges"
    gitgraph: "flow_diagrams.value.gitgraph"
    gantt: "flow_diagrams.value.gantt"
    storytree_edges: "strybldr-storyboard.storytree.nodes[].parentNodeId"
    forkcompare_edges: "strybldr-storyboard.storytree.candidateRuns[].parentNodeId"
    rich_media: "structured_response_panel.outputSrcDoc"

storytree_edge_flow_alignment:
  key: storytree_edge_flow_alignment
  type: object
  value:
    source_demo: "docs/knowgrph-strytree-demo.md"
    edge_authority: "storytree.nodes[].parentNodeId plus candidateRuns[].parentNodeId"
    graph_edges: ["rootBranch", "parent_node_id", "candidateRun", "candidateOption", "candidateScorecard"]
    card_flow_policy: "Cards expose lineage data; Strybldr derives visible connectors from active graph edges."
    static_edge_backfill_forbid: true

universal_structured_response_demo:
  key: universal_structured_response_demo
  type: object
  value:
    response_shape:
      key: response_shape
      type: mcp_structured_response
      value:
        root: "response.structuredContent"
        records: [widgets, cards, panels, media, nodes, edges]
        render_fields: [output, imageUrl, audioUrl, videoUrl, outputSrcDoc]
    neutrality_policy:
      key: neutrality_policy
      type: string
      value: "Structured content carries data only; renderer-specific UI instructions, static panel backfill, provider share URLs, and project-specific aliases are forbidden."
    dataflow_path:
      key: dataflow_path
      type: string
      value: "FloatingPanel Chat -> response.structuredContent -> Markdown flow frontmatter -> inline compute -> RichMediaPanel.outputSrcDoc"

flow_diagrams:
  key: flow_diagrams
  type: object
  value:
    gitgraph:
      key: gitgraph
      type: mermaid_gitgraph
      floatingPanelView: "gitGraph"
      floatingPanelOpen: true
      bottomPanelTab: "gitGraph"
      bottomPanelOpen: true
      title: "Strytree deep-research GitGraph branches"
      render_on: [storyboard, flow_editor]
      value: |-
        gitGraph
          commit id:"storytree_source"
          branch source_scout
          checkout source_scout
          commit id:"prototype_contract_review"
          checkout main
          branch miromind_research
          checkout miromind_research
          commit id:"structured_tool_result"
          commit id:"evidence_pack"
          checkout main
          branch strybldr_artifact
          checkout strybldr_artifact
          commit id:"storytree_snapshot"
          commit id:"fork_compare"
          checkout main
          merge source_scout
          merge miromind_research
          merge strybldr_artifact
          commit id:"review_gate"
    gantt:
      key: gantt
      type: mermaid_gantt
      floatingPanelView: "gantt"
      floatingPanelOpen: true
      bottomPanelTab: "gantt"
      bottomPanelOpen: true
      title: "Strytree deep-research Gantt critical path"
      render_on: [storyboard, flow_editor, document_view, timeline_view]
      value: |-
        gantt
          title computing flow: miromind-deep-research-strytree
          dateFormat YYYY-MM-DD
          section Intake
          Storytree source review :done, storytree_source, 2026-06-05, 1d
          section Parallel structured work
          Source scout :source_scout, after storytree_source, 2d
          MiroMind structured result :crit, structured_tool_result, after storytree_source, 2d
          Strybldr storyboard artifact :strybldr_artifact, after storytree_source, 2d
          ForkCompare scoring :fork_compare, after strybldr_artifact, 1d
          section Review
          Review gate :crit, review_gate, after structured_tool_result, 1d
          Rich Media Panels :panel_outputs, after review_gate, 1d
    miromind_architecture:
      key: miromind_architecture
      type: mermaid_architecture
      floatingPanelView: "architecture"
      floatingPanelOpen: true
      bottomPanelTab: "architecture"
      bottomPanelOpen: true
      forbidPlatform: ["vercel", "aws"]
      value: |-
        architecture-beta
          group operator(cloud)[Operator]
          group cloudflare(cloud)[Cloudflare Control Plane]
          group providers(cloud)[Default provider BytePlus plus Stripe]
          service canvas(internet)[Canvas UI airvio.co knowgrph] in cloudflare
          service miromind(server)[Miromind Research Agent] in cloudflare
          service gateway(server)[Cloudflare AI Gateway] in cloudflare
          service d1(database)[D1 Thesis and Evidence Store] in cloudflare
          service byteplus(server)[BytePlus agnes and seed] in providers
          canvas:R --> L:miromind
          miromind:R --> L:gateway
          gateway:R --> L:byteplus
          miromind:B --> T:d1
    miromind_event_model:
      key: miromind_event_model
      type: mermaid_eventmodeling
      floatingPanelView: "eventModeling"
      floatingPanelOpen: true
      bottomPanelTab: "eventModeling"
      bottomPanelOpen: true
      value: |-
        eventmodeling
        tf 01 ui StoryTreeSourceReview
        tf 02 cmd StartMiromindResearch
        tf 03 evt RunManifestCreated
        tf 04 pcr MiromindResearchAgent
        tf 05 cmd CrawlStructuredEvidence
        tf 06 evt EvidencePackReady
        tf 07 cmd CompileStoryTreeSnapshot
        tf 08 evt StoryTreeSnapshotReady
        tf 09 cmd RequestForkCompare
        tf 10 evt ForkCompareScored
        tf 11 cmd PersistToD1
        tf 12 evt PersistedToD1
        tf 13 ui ReplayStoryTreeFromCache
    miromind_pipeline_flowchart:
      key: miromind_pipeline_flowchart
      type: mermaid_flowchart
      floatingPanelView: "flowchart"
      floatingPanelOpen: true
      bottomPanelTab: "flowchart"
      bottomPanelOpen: true
      value: |-
        flowchart LR
          storytree_source["StoryTree Source\n(reference review)"]
          miromind_research["Miromind Research\n(structured tool result · evidence pack)"]
          strybldr_artifact["Strybldr Artifact\n(snapshot · fork compare)"]
          review_gate{"Review Gate\n(human approval)"}
          panel_outputs["Rich Media Panels\n(text · chart · claim)"]
          storytree_source -->|"source_ref_signal"| miromind_research
          miromind_research -->|"parallel"| strybldr_artifact
          strybldr_artifact -->|"merge"| review_gate
          review_gate -->|"approved"| panel_outputs

flow:
  direction: {key: direction, type: string, value: "LR"}
  edgeType: {key: edgeType, type: string, value: "smoothstep"}
  balancedViewportPreset: {key: balancedViewportPreset, type: string, value: "widgetFrontmatter"}
  computed: {key: computed, type: boolean, value: true}
  snapToGrid: {key: snapToGrid, type: boolean, value: true}
  nodes:
    - id: {key: id, type: string, value: "structured_response_source"}
      type: {key: type, type: string, value: "StructuredResponseSource"}
      label: {key: label, type: string, value: "MCP structured response source"}
      position: {key: position, type: object, value: {"x":-360,"y":0}}
      handles: {key: handles, type: object, value: {"source":["structuredContentJson"]}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:structured_response_source"}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "source"}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Headless MiroMind-style structured content is kept as data before Markdown flow projection."}
      structuredContentJson:
        key: structuredContentJson
        type: string
        value: |-
          {
            "cards": [
              {
                "id": "storytree-source-review",
                "label": "Strytree source review",
                "lane": "Storytree",
                "parentNodeId": null,
                "output": "Review the Strytree demo contract, parent-derived card edges, protected unlocks, candidate comparison, credit ledger, and provider-safe generation boundaries."
              },
              {
                "id": "structured-research-branch",
                "label": "Structured research branch",
                "lane": "Storytree",
                "parentNodeId": "storytree-source-review",
                "output": "Convert the research-agent capability into neutral response.structuredContent records with no provider page copy."
              },
              {
                "id": "forkcompare-card-flow",
                "label": "ForkCompare card flow",
                "lane": "ForkCompare",
                "parentNodeId": "structured-research-branch",
                "output": "Compare bounded candidate continuations as private scorecards before publishing one durable child branch."
              },
              {
                "id": "review-gated-panel-output",
                "label": "Review-gated Rich Media output",
                "lane": "Storytree",
                "parentNodeId": "forkcompare-card-flow",
                "output": "Only connected compute output feeds the Rich Media Panel; static panel authority stays empty."
              }
            ],
            "panels": [
              {
                "id": "panel-text-brief",
                "label": "Research brief panel",
                "kind": "html"
              }
            ],
            "edges": [
              {
                "source": "storytree-source-review.output",
                "target": "structured-research-branch.output",
                "label": "parent_node_id"
              },
              {
                "source": "structured-research-branch.output",
                "target": "forkcompare-card-flow.output",
                "label": "candidateRun"
              },
              {
                "source": "forkcompare-card-flow.output",
                "target": "review-gated-panel-output.output",
                "label": "candidateOption"
              },
              {
                "source": "review-gated-panel-output.output",
                "target": "panel-text-brief.outputSrcDoc",
                "label": "computed srcdoc"
              }
            ]
          }
    - id: {key: id, type: string, value: "structured_response_compute"}
      type: {key: type, type: string, value: "TextGeneration"}
      label: {key: label, type: string, value: "Structured response inline compute"}
      position: {key: position, type: object, value: {"x":40,"y":0}}
      handles: {key: handles, type: object, value: {"target":["structuredContentJson"],"source":["outputSrcDoc"]}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "textGeneration"}
      "flow:widgetTypeId": {key: "flow:widgetTypeId", type: string, value: "default"}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "compute"}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Inline compute turns structured content into live Rich Media HTML from connected input."}
      outputSrcDoc: {key: outputSrcDoc, type: string, value: ""}
      compute:
        key: compute
        type: javascript
        value: |-
          inputs => {
            const first = value => Array.isArray(value) ? value.find(item => item != null && item !== "") : value;
            const raw = String(first(inputs.structuredContentJson) || "").trim();
            const escape = value => String(value || "").replace(/[&<>"']/g, ch => ch === "&" ? "&amp;" : ch === "<" ? "&lt;" : ch === ">" ? "&gt;" : ch === '"' ? "&quot;" : "&#39;");
            let parsed = null;
            try { parsed = raw ? JSON.parse(raw) : null; } catch { parsed = null; }
            const cards = parsed && Array.isArray(parsed.cards) ? parsed.cards : [];
            const panels = parsed && Array.isArray(parsed.panels) ? parsed.panels : [];
            const edges = parsed && Array.isArray(parsed.edges) ? parsed.edges : [];
            const cardItems = cards.map(card => "<li><strong>" + escape(card.label || card.id) + "</strong>: " + escape(card.output || "") + "</li>").join("");
            const panelItems = panels.map(panel => "<li>" + escape(panel.label || panel.id) + " -> " + escape(panel.kind || "html") + "</li>").join("");
            const parentEdgeItems = cards.filter(card => card.parentNodeId).map(card => "<li>" + escape(card.parentNodeId) + " -> " + escape(card.id) + " (parentNodeId)</li>");
            const explicitEdgeItems = edges.map(edge => "<li>" + escape(edge.source || "") + " -> " + escape(edge.target || "") + " (" + escape(edge.label || "edge") + ")</li>");
            const edgeItems = explicitEdgeItems.concat(parentEdgeItems).join("");
            const output = "Structured response cards: " + cards.length + ". Card edges: " + (edges.length + parentEdgeItems.length) + ". Rich Media targets: " + panels.length + ".";
            return {
              output,
              outputSrcDoc: "<main data-kg-mcp-structured-response=\\"1\\"><h1>Strytree deep research structured response</h1><p>" + escape(output) + "</p><section><h2>Cards</h2><ul>" + (cardItems || "<li>none</li>") + "</ul></section><section><h2>Card edge flow</h2><ul>" + (edgeItems || "<li>none</li>") + "</ul></section><section><h2>Rich Media targets</h2><ul>" + (panelItems || "<li>none</li>") + "</ul></section><pre data-kg-structured-source=\\"1\\">" + escape(raw) + "</pre></main>"
            };
          }
    - id: {key: id, type: string, value: "structured_response_panel"}
      type: {key: type, type: string, value: "RichMediaPanel"}
      label: {key: label, type: string, value: "Computed Rich Media Panel"}
      position: {key: position, type: object, value: {"x":440,"y":0}}
      handles: {key: handles, type: object, value: {"target":["outputSrcDoc"],"source":["outputSrcDoc"]}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "richMediaPanel"}
      "kgc:nodeType": {key: "kgc:nodeType", type: string, value: "rich_media_panel"}
      "kgc:readingSummary": {key: "kgc:readingSummary", type: string, value: "Panel output is connected from inline compute; local static render fallback is intentionally empty."}
      richMediaActiveTab: {key: richMediaActiveTab, type: string, value: "html"}
      media_interactive: {key: media_interactive, type: boolean, value: true}
      outputSrcDoc: {key: outputSrcDoc, type: string, value: ""}
  edges:
    - id: {key: id, type: string, value: "structured_response_source_to_compute"}
      source: {key: source, type: string, value: "structured_response_source"}
      sourceHandle: {key: sourceHandle, type: string, value: "structuredContentJson"}
      target: {key: target, type: string, value: "structured_response_compute"}
      targetHandle: {key: targetHandle, type: string, value: "structuredContentJson"}
      label: {key: label, type: string, value: "structured content"}
      animated: {key: animated, type: boolean, value: true}
    - id: {key: id, type: string, value: "structured_response_compute_to_panel"}
      source: {key: source, type: string, value: "structured_response_compute"}
      sourceHandle: {key: sourceHandle, type: string, value: "outputSrcDoc"}
      target: {key: target, type: string, value: "structured_response_panel"}
      targetHandle: {key: targetHandle, type: string, value: "outputSrcDoc"}
      label: {key: label, type: string, value: "computed srcdoc"}
      animated: {key: animated, type: boolean, value: true}
  subgraphs:
    - {id: sg-structured-response, kind: subgraph, label: "Structured Response Dataflow", memberNodeIds: [structured_response_source, structured_response_compute, structured_response_panel], parentId: null}
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

# Knowgrph MiroMind Deep Research Strytree Demo

This demo combines the Strytree source validation shape with the research-agent
review-first capability shape. It keeps the machine contract in frontmatter:
renderer intent, typed GitGraph and Gantt diagram sources, a neutral structured
response source, inline compute, and a connected Rich Media Panel render target.

## Validation Surface

| Surface | Contract |
|---|---|
| FloatingPanel Chat | A provider response can arrive as `response.structuredContent` data rather than UI prose. |
| Markdown frontmatter | `flow_diagrams`, `flow.nodes`, and `flow.edges` are the source of truth. |
| Storyboard renderer | `storytree_product: "strytree"` and `kgCanvas2dRenderer: "storyboard"` select the storytree surface. |
| Dynamic panels | GitGraph, Gantt, and structured response panels derive `outputSrcDoc` from inline compute. |
| Review gate | The document makes no live API, Prod, or Cloudflare deploy claim. |

## Expected Dataflow

The authored data enters as Markdown frontmatter. The parser derives diagram
source nodes for GitGraph and Gantt, then connects each source through a safe
compute node into a Rich Media Panel. The structured response sample follows the
same pattern explicitly: source data feeds `structured_response_compute`, and
that compute node feeds `structured_response_panel.outputSrcDoc`.

## Runnable Strybldr Card Edge Seed

This seed mirrors the Strytree demo's edge authority: story cards carry
`parentNodeId`, ForkCompare runs carry their `parentNodeId`, and Strybldr derives
visible connectors from the active graph instead of trusting static edge copies.

```json strybldr-storyboard
{
  "version": 1,
  "runId": "miromind-strytree-deep-research-card-flow",
  "createdAtMs": 1780668300000,
  "notes": "Dev-only validation input for MiroMind-style structured research rendered through Strybldr card edges. It uses original demo data and derives edges from parentNodeId.",
  "sources": [
    {
      "sourceUnitId": "miromind-strytree-source-doc",
      "workspacePath": "docs/knowgrph-strytree-demo.md",
      "relativePath": "knowgrph-strytree-demo.md",
      "originalName": "Knowgrph Strytree demo source",
      "mediaKind": "doc",
      "mimeHint": "text/markdown",
      "byteSize": 0,
      "textHash": "miromind-strytree-source",
      "mediaUrl": "docs/knowgrph-strytree-demo.md"
    },
    {
      "sourceUnitId": "miromind-research-agent-source-doc",
      "workspacePath": "docs/knowgrph-research-agent-demo.md",
      "relativePath": "knowgrph-research-agent-demo.md",
      "originalName": "Knowgrph research-agent demo source",
      "mediaKind": "doc",
      "mimeHint": "text/markdown",
      "byteSize": 0,
      "textHash": "miromind-research-agent-source",
      "mediaUrl": "docs/knowgrph-research-agent-demo.md"
    }
  ],
  "elements": [
    {
      "id": "miromind-element-structured-result",
      "sourceUnitId": "miromind-research-agent-source-doc",
      "label": "Structured result envelope",
      "confidence": 1,
      "sourceBox": null,
      "evidenceKind": "source-metadata",
      "provider": "fallback",
      "order": 1,
      "summary": "The response shape is response.structuredContent with neutral records, frontmatter metadata, and render fields.",
      "action": "Keep metadata in frontmatter and graph records in cards, panels, widgets, nodes, and edges.",
      "prompt": "Produce a headless structured response that can be stored as Markdown and rendered by Strybldr."
    },
    {
      "id": "miromind-element-parent-edge-flow",
      "sourceUnitId": "miromind-strytree-source-doc",
      "label": "Parent-derived card edge flow",
      "confidence": 0.98,
      "sourceBox": null,
      "evidenceKind": "user-edit",
      "provider": "fallback",
      "order": 2,
      "summary": "Storytree cards derive visible connectors from parentNodeId and candidate run parent references.",
      "action": "Do not emit duplicate static card-edge fixtures when parent lineage can be read from source data.",
      "prompt": "Render source review, structured branch, candidate comparison, and review gate as connected cards."
    },
    {
      "id": "miromind-element-compute-panel",
      "sourceUnitId": "miromind-strytree-source-doc",
      "label": "Compute-backed Rich Media Panel",
      "confidence": 0.97,
      "sourceBox": null,
      "evidenceKind": "user-edit",
      "provider": "fallback",
      "order": 3,
      "summary": "Panel srcdoc is generated from upstream card data through inline compute.",
      "action": "Leave authored panel render fields empty and consume connected compute output.",
      "prompt": "Summarize card lineage and candidate scorecards into a dynamic Rich Media Panel."
    }
  ],
  "storytree": {
    "storyId": "miromind_strytree_deep_research_flow",
    "title": "MiroMind Strytree Research Flow",
    "synopsis": "A review-gated research card flow where each card connector is derived from parentNodeId lineage.",
    "tokenBalance": 96,
    "activeBranchCount": 5,
    "totalLikes": 233,
    "generationCostCredits": 6,
    "unlockCurrency": "credits",
    "nodes": [
      {
        "nodeId": "miromind_strytree_source_review",
        "parentNodeId": null,
        "title": "Strytree Source Review",
        "synopsis": "Read the runnable Strytree demo as the authority for card lanes, parent-derived edges, and ForkCompare fan-out.",
        "prompt": "Map Strytree source behavior into a neutral structured research card.",
        "authorName": "Knowgrph demo",
        "status": "hot",
        "duration": "00:12",
        "ageDays": 0,
        "isFreeWindow": true,
        "isProtected": false,
        "unlockPriceCredits": 0,
        "likes": 72,
        "impressions": 420,
        "paidUnlocks": 0,
        "ownAssetIds": ["asset_source_contract", "asset_parent_edges"]
      },
      {
        "nodeId": "miromind_structured_response_branch",
        "parentNodeId": "miromind_strytree_source_review",
        "title": "Structured Response Branch",
        "synopsis": "Package research output as response.structuredContent with portable frontmatter and neutral cards.",
        "prompt": "Convert the research result into renderer-neutral structuredContent records.",
        "authorName": "Knowgrph demo",
        "status": "active",
        "duration": "00:14",
        "ageDays": 0,
        "isFreeWindow": true,
        "isProtected": false,
        "unlockPriceCredits": 0,
        "likes": 48,
        "impressions": 310,
        "paidUnlocks": 0,
        "ownAssetIds": ["asset_structured_content"]
      },
      {
        "nodeId": "miromind_gitgraph_gantt_branch",
        "parentNodeId": "miromind_structured_response_branch",
        "title": "GitGraph And Gantt Branch",
        "synopsis": "Preserve diagram sources as typed flow_diagrams data while compute derives panel srcdoc.",
        "prompt": "Keep GitGraph and Gantt as frontmatter data sources with dynamic panel rendering.",
        "authorName": "Knowgrph demo",
        "status": "active",
        "duration": "00:13",
        "ageDays": 1,
        "isFreeWindow": true,
        "isProtected": false,
        "unlockPriceCredits": 0,
        "likes": 39,
        "impressions": 250,
        "paidUnlocks": 0,
        "ownAssetIds": ["asset_flow_diagrams"]
      },
      {
        "nodeId": "miromind_forkcompare_review",
        "parentNodeId": "miromind_structured_response_branch",
        "title": "ForkCompare Review",
        "synopsis": "Compare candidate continuations without publishing until review chooses one durable child branch.",
        "prompt": "Create private candidate scorecards with cost, continuity, fallback, and publish eligibility.",
        "authorName": "Knowgrph demo",
        "status": "active",
        "duration": "00:15",
        "ageDays": 1,
        "isFreeWindow": false,
        "isProtected": true,
        "unlockPriceCredits": 5,
        "likes": 34,
        "impressions": 220,
        "paidUnlocks": 4,
        "ownAssetIds": ["asset_candidate_scorecards"]
      },
      {
        "nodeId": "miromind_rich_media_review_gate",
        "parentNodeId": "miromind_forkcompare_review",
        "title": "Rich Media Review Gate",
        "synopsis": "Review connected compute output before claiming any live API, production route, or Cloudflare deploy.",
        "prompt": "Render the final panel from connected card data and keep deploy claims false.",
        "authorName": "Knowgrph demo",
        "status": "hot",
        "duration": "00:11",
        "ageDays": 2,
        "isFreeWindow": true,
        "isProtected": false,
        "unlockPriceCredits": 0,
        "likes": 27,
        "impressions": 180,
        "paidUnlocks": 0,
        "ownAssetIds": ["asset_rich_media_panel"]
      },
      {
        "nodeId": "miromind_static_panel_backfill_rejected",
        "parentNodeId": "miromind_rich_media_review_gate",
        "title": "Static Panel Backfill Rejected",
        "synopsis": "A dropped branch records why copied panel srcdoc and provider page payloads are not accepted.",
        "prompt": "Keep this branch audit-only so static fallback authority never replaces connected compute.",
        "authorName": "Knowgrph demo",
        "status": "dropped",
        "duration": "00:08",
        "ageDays": 2,
        "isFreeWindow": false,
        "isProtected": true,
        "unlockPriceCredits": 0,
        "likes": 13,
        "impressions": 90,
        "paidUnlocks": 0,
        "ownAssetIds": ["asset_audit_guard"]
      }
    ],
    "candidateRuns": [
      {
        "candidateRunId": "miromind_compare_review_outputs",
        "parentNodeId": "miromind_forkcompare_review",
        "status": "completed",
        "maxCandidates": 3,
        "quotedCostCredits": 18,
        "scorecardMode": "cost_continuity",
        "candidates": [
          {
            "candidateId": "miromind_candidate_inline_compute",
            "title": "Inline Compute Summary",
            "synopsis": "Use connected card output to generate an inspectable Rich Media Panel summary.",
            "prompt": "Summarize card lineage, edge labels, and review gates into dynamic HTML.",
            "provider": "local-harness",
            "status": "succeeded",
            "creditCost": 6,
            "elapsedMs": 32000,
            "fallbackStatus": "none",
            "moderationStatus": "approved",
            "inheritedAssetCount": 5,
            "continuityScore": 0.9,
            "publishEligible": true,
            "selected": true,
            "notes": "Best match for compute-backed panel authority."
          },
          {
            "candidateId": "miromind_candidate_diagram_focus",
            "title": "Diagram Source Focus",
            "synopsis": "Prioritize GitGraph and Gantt sources before Rich Media panel composition.",
            "prompt": "Route flow_diagrams into compute nodes before rendering panels.",
            "provider": "local-harness",
            "status": "succeeded",
            "creditCost": 6,
            "elapsedMs": 41000,
            "fallbackStatus": "none",
            "moderationStatus": "approved",
            "inheritedAssetCount": 4,
            "continuityScore": 0.82,
            "publishEligible": true,
            "selected": false,
            "notes": "Useful when diagram fidelity is the priority."
          },
          {
            "candidateId": "miromind_candidate_static_backfill",
            "title": "Static Backfill Rejection",
            "synopsis": "Reject a candidate that would paste final panel srcdoc instead of deriving it.",
            "prompt": "Document the rejection of static panel authority.",
            "provider": "local-harness",
            "status": "rejected",
            "creditCost": 6,
            "elapsedMs": 27000,
            "fallbackStatus": "fallback-preview",
            "moderationStatus": "approved",
            "inheritedAssetCount": 3,
            "continuityScore": 0.44,
            "publishEligible": false,
            "selected": false,
            "notes": "Kept private as an audit card."
          }
        ]
      }
    ]
  }
}
```

## No Static Panel Authority

Rich Media Panel render fields are intentionally empty in authored frontmatter.
Connected compute output is the render authority. Static fallback text, copied
provider report URLs, and demo-specific backfill nodes are not part of this
contract.

## Local Validation

```bash
FLOW_DIAGRAM_SAMPLE_PATHS="../huijoohwee/docs/knowgrph-miromind-deep-research-strytree-demo.md" npm --prefix ../knowgrph/canvas run test:ci:unit -- markdown.frontmatterFlowGraph.fidelity.publishedFlowDiagramDocs.dynamicPanels
```
