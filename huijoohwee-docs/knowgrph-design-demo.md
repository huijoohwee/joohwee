---
title: "Knowgrph · Design Renderer Demo — Floating Design Panel (Layers + DOM)"
graphId: "md:knowgrph-design-demo-v1"
doc_type: "Design Demo — Phase 0+1+2 E2E Functional Contract"
date: "2026-05-14"
lang: en-US

kgCanvasSurfaceMode: "2d"
kgCanvasRenderMode: "2d"
kgCanvas2dRenderer: "design"
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

# Knowgrph · Design Renderer Demo

This document is a minimal, reproducible **E2E functional** demo for the Canvas **2D Renderer: Design** editor surface (Phase **0 + 1 + 2**).

It mirrors the style of [knowgrph-video-demo.md](./knowgrph-video-demo.md) frontmatter (explicit `kg*` settings), but uses a simpler graph so you can quickly validate:

- Design renderer is selectable and stable.
- A first-class **Design** floating-panel view exists (not hidden behind “More”).
- Design view contains sub-tabs: **Layers**, **Inspector**, **DOM Tree**, **DOM Inspect** (DOM tabs are webpage-backed only).
- A minimal Design HUD/status appears on-canvas (selection count + hint).
- Tool mode: **Select/Pan** (UI + shortcuts).
- Undo/Redo: **Cmd/Ctrl+Z** and **Shift+Cmd/Ctrl+Z**.
- Inspector edits: numeric **x/y/w/h** with mixed-state handling and single-commit Apply.

---

## Editor Workspace (Frontmatter)

| Setting | Value | Purpose |
|---|---|---|
| Surface Mode | `2d` | Flat surface |
| Render Mode | `2d` | 2D pipeline |
| 2D Renderer | `design` | SVG Design renderer surface |
| Semantic Mode | `document` | Markdown-derived graph |
| Frontmatter Mode | `enabled` | Enables seeding via `index.mermaid` |
| Multi-Dim Table | `disabled` | Keep demo minimal |
| Structure Lock | `false` | Allow structure re-derivation |

---

## Phase 0+1+2 E2E (What You Should See)

### Floating panel header

- A **Design** button (Palette icon) is present alongside existing primary views (Props / Interaction / Chat / Geo / Renderer).
- Clicking **Design** opens a Design panel.
- Design panel header contains:
  - **Select** + **Pan** tool toggles (and tool mode is reflected in gesture behavior).
  - **Undo** / **Redo** buttons (enabled/disabled based on history).
  - `Snap:On/Off` indicator (schema-driven).

### Design panel body

- Sub-tabs exist inside the Design panel:
  - **Layers**: shows graph nodes as a layer list; supports show/hide and ordering controls.
  - **Inspector**: numeric geometry edits for selected frames (x/y/w/h) with mixed-state support.
  - **DOM Tree**: available only when the document produces a webpage-backed layout graph.
  - **DOM Inspect**: available only when the document produces a webpage-backed layout graph.

### Design canvas HUD

- When the Design renderer is active, a small HUD appears at top-left with:
  - `Design`
  - `{N} selected`
  - a hint to open the Design panel

---

## How to Run the Demo (Manual, E2E)

1. Open this document in Knowgrph.
2. Set Canvas View Mode to **2D**.
3. In the Eye dropdown (Canvas View Mode), choose **2D Renderer → Design**.
4. Open the floating panel and click **Design** (Palette icon).
5. Use **Layers**:
   - Select a node; validate the on-canvas HUD updates `{N} selected`.
   - Toggle visibility; validate the frame hides/shows.
   - Move a layer up/down; validate order changes (and is undoable).
6. Use **Tools**:
   - Toggle **Pan** (or press `H`); validate frame drag/resize/select is disabled and pan/zoom remains usable.
   - Toggle **Select** (or press `V`); validate selection/resize/drag returns.
7. Use **Inspector**:
   - Select 1 frame → set X/Y/W/H → **Apply**.
   - Select multiple frames with different values → fields show `—` placeholder; set just `W` and Apply → all selected frames get the same width.
8. Use **Undo/Redo**:
   - `Cmd/Ctrl+Z` undo and `Shift+Cmd/Ctrl+Z` redo across: move, resize, inspector apply, layer visibility/order.

Notes:
- Design panels are gated and should remain inactive unless:
  - Workspace view is `canvas`
  - Render mode is `2d`
  - 2D renderer is `design`
  - Geospatial mode is disabled

---

## Demo Graph Seed (Frontmatter-driven)

This seed graph exists only to generate a few frames you can select/move/resize in Design renderer.

```yaml
index:
  mermaid: |
    %%{init: {"theme":"base"}}%%
    flowchart LR
      A["Design Panel\n(Palette icon)"] --> B["Layers tab\n(Visibility + order)"]
      A --> G["Inspector tab\n(x/y/w/h + Apply)"]
      A --> T["Tools\n(Select/Pan + V/H)"]
      A --> U["Undo/Redo\n(Cmd/Ctrl+Z)"]
      A --> C["DOM Tree tab\n(webpage-backed only)"]
      A --> D["DOM Inspect\n(webpage-backed only)"]
      B --> E["Select nodes\n(HUD count updates)"]
      E --> F["Arrange / Resize\n(no churn)"]
      F --> U
      G --> U
```

---

## Demo Notes (Why this matters)

- Phase 0 establishes a single coherent Design surface (no duplicated entry points).
- Phase 1 adds minimal editor controls (tools + undo/redo) without introducing per-move history spam.
- Phase 2 adds Inspector numeric geometry editing with mixed-state support and single-commit Apply.
- This UI avoids duplicate entry points (Design tooling is not split between overflow menus and hidden views).
- The Design panel remains a **view switch only** and must not mutate graph topology, layout caches, or overlay geometry beyond its own UI.
