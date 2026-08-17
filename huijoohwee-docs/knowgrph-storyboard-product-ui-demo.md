---
title: Knowgrph Storyboard Product UI Demo
schema: "kgc-computing-flow/v1"
kgCanvasSurfaceMode: "2d"
kgCanvasRenderMode: "2d"
kgCanvas2dRenderer: "storyboard"
kgDocumentSemanticMode: "document"
kgFrontmatterModeEnabled: true
kgWorkflowManagerModeEnabled: true
kgAutoSaveEnabled: true
kgAutoSaveDebounceMs: 1500
kgAutoSaveOn: ["nodeEdit", "runComplete", "approval", "assetReady"]
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
flow:
  direction: {key: direction, type: string, value: "LR"}
  edgeType: {key: edgeType, type: string, value: "smoothstep"}
  balancedViewportPreset: {key: balancedViewportPreset, type: string, value: "widgetFrontmatter"}
  computed: {key: computed, type: boolean, value: false}
  snapToGrid: {key: snapToGrid, type: boolean, value: true}
  nodes:
    - id: {key: id, type: string, value: "STEP_03"}
      type: {key: type, type: string, value: "Frame"}
      label: {key: label, type: string, value: "Selection Sync"}
      position: {key: position, type: object, value: {"x":0,"y":-480}}
      artDirection: {key: artDirection, type: string, value: "Native storyboard card with selection emphasis, compact chips, and linked source context."}
      category: {key: category, type: string, value: "In Review"}
      context: {key: context, type: string, value: "Storyboard Surface"}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:STEP_03"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      imageUrl: {key: imageUrl, type: string, value: "https://images.unsplash.com/photo-1461749280684-dccba630e2f6?auto=format&fit=crop&w=1200&q=80"}
      instructions: {key: instructions, type: string, value: "Verify the active card selects the matching graph node and preserves a neutral, project-agnostic handoff."}
      lane: {key: lane, type: string, value: "In Review"}
      order: {key: order, type: number, value: 3}
      ordinal: {key: ordinal, type: number, value: 3}
      owner: {key: owner, type: string, value: "Product"}
      preset: {key: preset, type: string, value: "Native Board"}
      priority: {key: priority, type: string, value: "P0"}
      refs: {key: refs, type: array, value: ["https://images.unsplash.com/photo-1461749280684-dccba630e2f6?auto=format&fit=crop&w=1200&q=80"]}
      state: {key: state, type: string, value: "Selected"}
      summary: {key: summary, type: string, value: "Selecting a card keeps the source node and the review board aligned."}
      tags: {key: tags, type: array, value: ["selection","sync","board"]}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 2}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 1}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
      voiceOver: {key: voiceOver, type: string, value: "System: \"Selection sync confirms one board and one source of truth.\""}
    - id: {key: id, type: string, value: "STEP_01"}
      type: {key: type, type: string, value: "Panel"}
      label: {key: label, type: string, value: "Intake Triage"}
      position: {key: position, type: object, value: {"x":0,"y":-240}}
      assets: {key: assets, type: array, value: ["https://images.unsplash.com/photo-1516321165247-4aa89a48be28?auto=format&fit=crop&w=1200&q=80","https://images.unsplash.com/photo-1498050108023-c5249f4df085?auto=format&fit=crop&w=1200&q=80"]}
      brief: {key: brief, type: string, value: "Product review inbox with compact cards, screenshots, and a clear canonical intake path."}
      context: {key: context, type: string, value: "Review Inbox"}
      documentUrl: {key: documentUrl, type: string, value: "https://airvio.co/knowgrph"}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:STEP_01"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      group: {key: group, type: string, value: "Backlog"}
      image: {key: image, type: string, value: "https://images.unsplash.com/photo-1516321165247-4aa89a48be28?auto=format&fit=crop&w=1200&q=80"}
      lane: {key: lane, type: string, value: "Backlog"}
      narration: {key: narration, type: string, value: "Reviewer: \"Keep the ask scoped, readable, and source-owned.\""}
      order: {key: order, type: number, value: 4}
      owner: {key: owner, type: string, value: "Review"}
      priority: {key: priority, type: string, value: "P0"}
      state: {key: state, type: string, value: "New Request"}
      step: {key: step, type: number, value: 1}
      summary: {key: summary, type: string, value: "A new review request lands with screenshots, notes, and a target artifact."}
      tags: {key: tags, type: array, value: ["intake","backlog","scope"]}
      task: {key: task, type: string, value: "Consolidate incoming comments into one neutral intake card without duplicating state across tools."}
      theme: {key: theme, type: string, value: "Workspace UI"}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 1}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 1}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "STEP_04"}
      type: {key: type, type: string, value: "Panel"}
      label: {key: label, type: string, value: "Delivery Handoff"}
      position: {key: position, type: object, value: {"x":0,"y":0}}
      assetRefs: {key: assetRefs, type: array, value: ["https://images.unsplash.com/photo-1516321497487-e288fb19713f?auto=format&fit=crop&w=1200&q=80","https://images.unsplash.com/photo-1522542550221-31fd19575a2d?auto=format&fit=crop&w=1200&q=80"]}
      brief: {key: brief, type: string, value: "Final product handoff card with review summary, references, and linked implementation context."}
      briefUrl: {key: briefUrl, type: string, value: "https://airvio.co/knowgrph"}
      bucket: {key: bucket, type: string, value: "In Review"}
      context: {key: context, type: string, value: "Delivery Surface"}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:STEP_04"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      lane: {key: lane, type: string, value: "In Review"}
      order: {key: order, type: number, value: 1}
      owner: {key: owner, type: string, value: "Delivery"}
      priority: {key: priority, type: string, value: "P0"}
      quote: {key: quote, type: string, value: "Lead: \"Approved. Deliver the brief with source, refs, and neutral wording.\""}
      state: {key: state, type: string, value: "Ready"}
      summary: {key: summary, type: string, value: "The approved board card carries its brief, references, and source link into delivery."}
      tags: {key: tags, type: array, value: ["approved","handoff","delivery"]}
      task: {key: task, type: string, value: "Hand off one approved card with clear references and no project-specific assumptions baked into the structure."}
      theme: {key: theme, type: string, value: "Delivery Kit"}
      videoUrl: {key: videoUrl, type: string, value: "https://interactive-examples.mdn.mozilla.net/media/cc0-videos/flower.mp4"}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 2}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 2}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "STEP_02"}
      type: {key: type, type: string, value: "Shot"}
      label: {key: label, type: string, value: "Comment Merge"}
      position: {key: position, type: object, value: {"x":0,"y":240}}
      context: {key: context, type: string, value: "Active Canvas"}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:STEP_02"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      group: {key: group, type: string, value: "In Review"}
      imageUrl: {key: imageUrl, type: string, value: "https://images.unsplash.com/photo-1558655146-d09347e92766?auto=format&fit=crop&w=1200&q=80"}
      lane: {key: lane, type: string, value: "In Review"}
      order: {key: order, type: number, value: 1}
      owner: {key: owner, type: string, value: "Design"}
      priority: {key: priority, type: string, value: "P1"}
      referenceLinks: {key: referenceLinks, type: array, value: ["https://images.unsplash.com/photo-1558655146-d09347e92766?auto=format&fit=crop&w=1200&q=80","https://images.unsplash.com/photo-1461749280684-dccba630e2f6?auto=format&fit=crop&w=1200&q=80"]}
      sequenceNumber: {key: sequenceNumber, type: number, value: 2}
      speakerLine: {key: speakerLine, type: string, value: "Designer: \"One board, one review path, no stale side copy.\""}
      state: {key: state, type: string, value: "Consolidating"}
      summary: {key: summary, type: string, value: "Related comments, screenshots, and references merge into one review surface."}
      tags: {key: tags, type: array, value: ["merge","comments","canvas"]}
      variant: {key: variant, type: string, value: "Comment Density"}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 1}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
      visualBrief: {key: visualBrief, type: string, value: "Product canvas with annotation chips, grouped comments, and a compact review lane."}
      workflow: {key: workflow, type: string, value: "Merge overlapping requests before implementation so the board reflects one coherent ask."}
    - id: {key: id, type: string, value: "BOARD_ROOT"}
      type: {key: type, type: string, value: "Story"}
      label: {key: label, type: string, value: "Product Review Flow"}
      position: {key: position, type: object, value: {"x":0,"y":480}}
      "flow:widgetFormId": {key: "flow:widgetFormId", type: string, value: "fm:BOARD_ROOT"}
      "frontmatter:primitive": {key: "frontmatter:primitive", type: string, value: "node"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      group: {key: group, type: string, value: "Planning"}
      lane: {key: lane, type: string, value: "Planning"}
      order: {key: order, type: number, value: 5}
      summary: {key: summary, type: string, value: "Neutral product UI storyboard demo for review, sync, and delivery."}
      tags: {key: tags, type: array, value: ["storyboard","product-ui","review"]}
      task: {key: task, type: string, value: "Keep review artifacts, comments, and source state in one native graph-derived board."}
      theme: {key: theme, type: string, value: "Neutral UI"}
      "visual:xIndex": {key: "visual:xIndex", type: number, value: 0}
      "visual:yIndex": {key: "visual:yIndex", type: number, value: 0}
      "visual:zIndex": {key: "visual:zIndex", type: number, value: 0}
    - id: {key: id, type: string, value: "anchor:md:knowgrph-storyboard-product-ui-demo:demo-intent"}
      type: {key: type, type: string, value: "Anchor"}
      label: {key: label, type: string, value: "demo-intent"}
      anchorId: {key: anchorId, type: string, value: "demo-intent"}
      chunk_text: {key: chunk_text, type: string, value: "demo-intent"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      kind: {key: kind, type: string, value: "heading"}
      labels: {key: labels, type: array, value: ["Anchor"]}
    - id: {key: id, type: string, value: "anchor:md:knowgrph-storyboard-product-ui-demo:expected-card-signals"}
      type: {key: type, type: string, value: "Anchor"}
      label: {key: label, type: string, value: "expected-card-signals"}
      anchorId: {key: anchorId, type: string, value: "expected-card-signals"}
      chunk_text: {key: chunk_text, type: string, value: "expected-card-signals"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      kind: {key: kind, type: string, value: "heading"}
      labels: {key: labels, type: array, value: ["Anchor"]}
    - id: {key: id, type: string, value: "anchor:md:knowgrph-storyboard-product-ui-demo:expected-lanes"}
      type: {key: type, type: string, value: "Anchor"}
      label: {key: label, type: string, value: "expected-lanes"}
      anchorId: {key: anchorId, type: string, value: "expected-lanes"}
      chunk_text: {key: chunk_text, type: string, value: "expected-lanes"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      kind: {key: kind, type: string, value: "heading"}
      labels: {key: labels, type: array, value: ["Anchor"]}
    - id: {key: id, type: string, value: "anchor:md:knowgrph-storyboard-product-ui-demo:knowgrph-storyboard-product-ui-demo"}
      type: {key: type, type: string, value: "Anchor"}
      label: {key: label, type: string, value: "knowgrph-storyboard-product-ui-demo"}
      anchorId: {key: anchorId, type: string, value: "knowgrph-storyboard-product-ui-demo"}
      chunk_text: {key: chunk_text, type: string, value: "knowgrph-storyboard-product-ui-demo"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      kind: {key: kind, type: string, value: "heading"}
      labels: {key: labels, type: array, value: ["Anchor"]}
    - id: {key: id, type: string, value: "anchor:md:knowgrph-storyboard-product-ui-demo:related-docs"}
      type: {key: type, type: string, value: "Anchor"}
      label: {key: label, type: string, value: "related-docs"}
      anchorId: {key: anchorId, type: string, value: "related-docs"}
      chunk_text: {key: chunk_text, type: string, value: "related-docs"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      kind: {key: kind, type: string, value: "heading"}
      labels: {key: labels, type: array, value: ["Anchor"]}
    - id: {key: id, type: string, value: "anchor:md:knowgrph-storyboard-product-ui-demo:typed-fixture-contract"}
      type: {key: type, type: string, value: "Anchor"}
      label: {key: label, type: string, value: "typed-fixture-contract"}
      anchorId: {key: anchorId, type: string, value: "typed-fixture-contract"}
      chunk_text: {key: chunk_text, type: string, value: "typed-fixture-contract"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      kind: {key: kind, type: string, value: "heading"}
      labels: {key: labels, type: array, value: ["Anchor"]}
    - id: {key: id, type: string, value: "anchor:md:knowgrph-storyboard-product-ui-demo:validation-goals"}
      type: {key: type, type: string, value: "Anchor"}
      label: {key: label, type: string, value: "validation-goals"}
      anchorId: {key: anchorId, type: string, value: "validation-goals"}
      chunk_text: {key: chunk_text, type: string, value: "validation-goals"}
      "graph:degree": {key: "graph:degree", type: number, value: 0}
      "graph:inDegree": {key: "graph:inDegree", type: number, value: 0}
      "graph:outDegree": {key: "graph:outDegree", type: number, value: 0}
      "graph:structuralDegree": {key: "graph:structuralDegree", type: number, value: 0}
      kind: {key: kind, type: string, value: "heading"}
      labels: {key: labels, type: array, value: ["Anchor"]}
  edges:
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

# Knowgrph Storyboard Product UI Demo

Use this document to validate a neutral, project-agnostic storyboard workflow for product UI review.

This fixture uses normalized `{key, type, value}` envelopes inside `flow.nodes[*]` so ingestion, parsing, and storyboard rendering all exercise the typed E2E contract instead of relying on plain-YAML-only alias parsing.

## Typed Fixture Contract

- This file is an approved typed validation fixture for neutral storyboard workflow and alias-envelope coverage.
- The opening YAML frontmatter block remains the first-block machine SSOT for renderer activation and graph-backed storyboard data.
- Normalized `{key, type, value}` envelopes in `flow.nodes[*]` are intentional here so typed ingest -> parse -> render behavior stays validated.
- This document is not the canonical plain-YAML authoring example; canonical authored storyboard docs should still prefer plain YAML for frontmatter and related schema-bearing blocks.
- Parser warning, repair, or fallback behavior is recovery-only; malformed YAML frontmatter still remains invalid source that must be fixed upstream.

## Related Docs

- [Storyboard Demo Index](./knowgrph-storyboard-demo-index.md)
- [Storyboard Demo](./knowgrph-storyboard-demo.md)
- [Storyboard Neutral Schema Contract Demo](./knowgrph-storyboard-neutral-schema-contract-demo.md)

## Validation Goals

- Confirm the storyboard renderer activates from frontmatter through `kgCanvas2dRenderer: "storyboard"`.
- Confirm Storyboard Display `Card` and `Widget` are UI variants of `2D Renderer: Storyboard`, with shared source graph, edge, pan, drag, zoom, and Rich Media Panel behavior.
- Confirm `Cards`, `Widgets`, and `Rich Media Panels` stay visually balanced and source-backed during selection, inline edit, and media preview flows.
- Confirm the runtime supports neutral alias fields such as `group`, `bucket`, `category`, `step`, `sequenceNumber`, `ordinal`, `position`, `task`, `workflow`, `instructions`, `narration`, `speakerLine`, `voiceOver`, `brief`, `visualBrief`, `artDirection`, `theme`, `variant`, `preset`, `assets`, `assetRefs`, `refs`, `referenceLinks`, `documentUrl`, and `briefUrl`.
- Confirm alias-backed cards still render the same native sections: frame badge, slugline, `Summary`, `Action`, `Dialogue`, `Visual Brief`, `Reference Pack`, tags, metadata, and source link.
- Confirm `context` + `state` compose slugline text when no explicit `slugline` is authored.
- Confirm `group`, `bucket`, and `category` all drive native lane grouping without introducing renderer-specific schema forks.
- Confirm selection-focused review cards remain compact and readable while still selecting the source node in the active graph store.
- Confirm the product UI review flow stays universal and neutral: no project-locked field names, no file-specific assumptions, no copied vendor shells.

## Expected Lanes

- `Backlog` should contain `STEP_01`.
- `In Review` should contain `STEP_02` and `STEP_03`.
- `Approved` should contain `STEP_04`.

## Expected Card Signals

- `STEP_01` should validate `group`, `step`, `task`, `narration`, `brief`, `theme`, `assets`, and `documentUrl`.
- `STEP_02` should validate `sequenceNumber`, `workflow`, `speakerLine`, `visualBrief`, `variant`, and `referenceLinks`.
- `STEP_03` should validate `category`, `ordinal`, `instructions`, `voiceOver`, `artDirection`, and `preset`.
- `STEP_04` should validate `bucket`, `position`, `quote`, `brief`, `assetRefs`, `briefUrl`, and video-backed approved delivery cards.

## Demo Intent

- The first card proves neutral intake can stay source-owned.
- The second and third cards prove active review can remain graph-derived and selection-synced.
- The final card proves approved delivery can stay compact, referenced, and project-agnostic.
