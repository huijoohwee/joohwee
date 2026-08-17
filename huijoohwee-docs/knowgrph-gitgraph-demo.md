---
title: "Knowgrph GitGraph Demo - YAML Mermaid Frontmatter Pipeline"
graphId: "md:knowgrph-gitgraph-demo"
doc_type: "GitGraph Demo"
date: "2026-06-03"
lang: "en-US"
schema: "kgc-computing-flow/v1"

implementation_contract: "../knowgrph/docs/documents/knowgrph-yaml-mermaid-gitgraph-frontmatter-prd-tad.md"
source_truth:
  - "../knowgrph/grph-shared/src/markdown/mermaidInput.ts"
  - "../knowgrph/canvas/src/lib/parsers/markdownJsonLd.impl.ts"
  - "../knowgrph/canvas/src/lib/mermaid/mermaidGitGraph.ts"
  - "../knowgrph/canvas/src/components/MermaidGitGraphCanvas.tsx"
demo_status: "local published-doc demo; no Cloudflare deploy claim"
deployed_api_claim: false
live_route_validation_required_before_claim: true

kgCanvasSurfaceMode: "2d"
kgCanvasRenderMode: "2d"
kgCanvas2dRenderer: "gitGraph"
kgDocumentSemanticMode: "document"
kgFrontmatterModeEnabled: true
kgMultiDimTableModeEnabled: false
kgDocumentStructureBaselineLock: false
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

mermaid: |
  ---
  config:
    theme: base
    logLevel: info
  ---
  gitGraph:
    commit id:"source_md" tag:"md"
    branch ingestion
    checkout ingestion
    commit id:"frontmatter_yaml"
    commit id:"mermaid_payload" type:HIGHLIGHT
    checkout main
    merge ingestion id:"ingest_ready" tag:"ingested"
    branch parsing
    checkout parsing
    commit id:"diagram_kind"
    commit id:"mermaid_diagram" tag:"gitgraph"
    commit id:"no_flow_topology" type:REVERSE
    checkout main
    merge validation id:"e2e_proof" tag:"demo"
    branch rendering
    checkout rendering
    commit id:"renderer_id"
    commit id:"svg_cache"
    commit id:"gitgraph_surface" type:HIGHLIGHT
    checkout main
    merge rendering id:"render_ready" tag:"rendered"
    branch validation
    checkout validation
    commit id:"focused_tests"
    commit id:"browser_smoke"
    checkout main
    merge validation id:"e2e_proof" tag:"demo"
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

# Knowgrph GitGraph Demo

This document is a runnable frontmatter demo for **Toolbar -> Canvas View Mode -> 2D Renderer: GitGraph**.

It demonstrates the Dev-source pipeline described by the implementation contract:

| Stage | Frontmatter signal | Expected Knowgrph behavior |
|---|---|---|
| Ingestion | `kgCanvas2dRenderer: "gitGraph"` and top-level `mermaid: |` | The Markdown loader keeps the source text and selects the canonical GitGraph renderer. |
| Parsing | `gitGraph:` after a Mermaid config header | The shared Mermaid detector tags the payload as `diagramKind: "gitgraph"`. |
| Isolation | GitGraph commands such as `commit`, `branch`, `checkout`, and `merge` | The Flowchart parser does not emit `MermaidNode` or Flow topology from GitGraph syntax. |
| Rendering | Preserved frontmatter Mermaid code | `MermaidGitGraphCanvas` resolves the GitGraph slice and renders it through the shared Mermaid SVG cache. |

## How To Run

1. Open this Markdown file in Knowgrph.
2. Keep Canvas View Mode on `2D`.
3. Select **2D Renderer: GitGraph** from the Canvas View Mode menu.
4. Confirm the Git history diagram renders from the frontmatter Mermaid block.

## Expected Diagram

The GitGraph should show `main` receiving merges from four branches:

| Branch | Pipeline stage | Highlight |
|---|---|---|
| `ingestion` | YAML and Mermaid source capture | `mermaid_payload` is highlighted. |
| `parsing` | Diagram-kind detection and topology isolation | `no_flow_topology` is marked reverse. |
| `rendering` | Renderer id, SVG cache, and GitGraph surface | `gitgraph_surface` is highlighted. |
| `validation` | Focused tests and browser smoke | `e2e_proof` is tagged as the demo merge. |

## Contract Notes

- The Mermaid source is the top-level frontmatter `mermaid` value.
- The renderer id is the canonical `gitGraph` value, not a downstream alias fixture.
- GitGraph stays diagram-native; this file does not ask Knowgrph to convert GitGraph commits into Flow nodes.
- This file is a local published-doc artifact only. It does not claim a Prod mirror sync or Cloudflare deployment.
