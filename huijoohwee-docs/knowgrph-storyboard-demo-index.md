---
title: "Knowgrph Storyboard Demo"
kgCanvasSurfaceMode: "2d"
kgCanvasRenderMode: "2d"
kgCanvas2dRenderer: "storyboard"
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
flow:
  direction: {key: direction, type: string, value: "LR"}
  edgeType: {key: edgeType, type: string, value: "smoothstep"}
  balancedViewportPreset: {key: balancedViewportPreset, type: string, value: "widgetFrontmatter"}
  computed: {key: computed, type: boolean, value: true}
  snapToGrid: {key: snapToGrid, type: boolean, value: true}
  nodes:
    - id: {key: id, type: string, value: "STORY_ROOT"}
      type: {key: type, type: string, value: "Story"}
      label: {key: label, type: string, value: "Creative Review Storyboard"}
      position: {key: position, type: object, value: {x: -960, y: 0}}
      stage: {key: stage, type: string, value: "Planning"}
      summary: {key: summary, type: string, value: "Native in-repo storyboard demo for the 2D Storyboard renderer."}
      slugline: {key: slugline, type: string, value: "Story Spine - Review Narrative"}
      action: {key: action, type: string, value: "Root story node groups all review scenes and preserves one native graph source for storyboard projection."}
      owner: {key: owner, type: string, value: "Production"}
      priority: {key: priority, type: string, value: "P0"}
      tags: {key: tags, type: array, value: ["storyboard", "demo", "launch"]}
      style: {key: style, type: string, value: "Knowgrph Native"}
    - id: {key: id, type: string, value: "SCENE_01"}
      type: {key: type, type: string, value: "Scene"}
      label: {key: label, type: string, value: "Cold Open"}
      position: {key: position, type: object, value: {x: -640, y: 720}}
      stage: {key: stage, type: string, value: "Draft"}
      frame: {key: frame, type: number, value: 1}
      location: {key: location, type: string, value: "Conference Room"}
      timeOfDay: {key: timeOfDay, type: string, value: "Monday"}
      summary: {key: summary, type: string, value: "Open on the user pain point before the product is shown."}
      action: {key: action, type: string, value: "Designer and client review printed boards on the table while markup accumulates across the surface."}
      dialogue: {key: dialogue, type: string, value: "CLIENT: \"Just a few small changes.\""}
      prompt: {key: prompt, type: string, value: "A designer and client sit at a conference table with printed storyboard boards, marked-up notes, pens, and calm office lighting."}
      style: {key: style, type: string, value: "Doodle"}
      references: {key: references, type: array, value: ["https://images.unsplash.com/photo-1517048676732-d65bc937f952?auto=format&fit=crop&w=1200&q=80", "https://images.unsplash.com/photo-1520607162513-77705c0f0d4a?auto=format&fit=crop&w=1200&q=80"]}
      owner: {key: owner, type: string, value: "Director"}
      priority: {key: priority, type: string, value: "P0"}
      tags: {key: tags, type: array, value: ["hook", "problem", "wide"]}
      image: {key: image, type: string, value: "https://images.unsplash.com/photo-1492691527719-9d1e07e534b4?auto=format&fit=crop&w=1200&q=80"}
      order: {key: order, type: number, value: 10}
      url: {key: url, type: string, value: "https://airvio.co/knowgrph"}
    - id: {key: id, type: string, value: "SHOT_01A"}
      type: {key: type, type: string, value: "Shot"}
      label: {key: label, type: string, value: "Friction Montage"}
      position: {key: position, type: object, value: {x: -320, y: 480}}
      stage: {key: stage, type: string, value: "Draft"}
      frame: {key: frame, type: number, value: 2}
      slugline: {key: slugline, type: string, value: "Review Notes - Print Markup Pass"}
      summary: {key: summary, type: string, value: "Quick cuts show duplicate tools, scattered notes, and timeline drift."}
      action: {key: action, type: string, value: "Printouts, sticky notes, and disconnected tools stack up faster than the team can reconcile them."}
      dialogue: {key: dialogue, type: string, value: "DESIGNER: \"We fixed that in the canvas, but the board is already stale.\""}
      prompt: {key: prompt, type: string, value: "Fast montage of sticky notes, printouts, browser windows, and duplicated timeline updates spreading across a worktable."}
      style: {key: style, type: string, value: "Paper Cut"}
      references: {key: references, type: array, value: ["https://images.unsplash.com/photo-1516321318423-f06f85e504b3?auto=format&fit=crop&w=1200&q=80", "https://images.unsplash.com/photo-1455390582262-044cdead277a?auto=format&fit=crop&w=1200&q=80"]}
      owner: {key: owner, type: string, value: "Editor"}
      priority: {key: priority, type: string, value: "P1"}
      tags: {key: tags, type: array, value: ["closeup", "workflow", "pain"]}
      imageUrl: {key: imageUrl, type: string, value: "https://images.unsplash.com/photo-1516321318423-f06f85e504b3?auto=format&fit=crop&w=1200&q=80"}
      order: {key: order, type: number, value: 20}
    - id: {key: id, type: string, value: "SCENE_02"}
      type: {key: type, type: string, value: "Scene"}
      label: {key: label, type: string, value: "Graph-to-Storyboard Reveal"}
      position: {key: position, type: object, value: {x: 0, y: 240}}
      stage: {key: stage, type: string, value: "Review"}
      frame: {key: frame, type: number, value: 3}
      location: {key: location, type: string, value: "Workspace Canvas"}
      timeOfDay: {key: timeOfDay, type: string, value: "Live Sync"}
      summary: {key: summary, type: string, value: "The graph reorganizes into storyboard lanes without a second authoring system."}
      action: {key: action, type: string, value: "The same source graph snaps into a native storyboard board while lane chips, counts, and card media stay in sync."}
      dialogue: {key: dialogue, type: string, value: "PM: \"Same graph, same markdown, better review surface.\""}
      prompt: {key: prompt, type: string, value: "Product interface transitions from graph nodes into a storyboard board with compact lanes, consistent chips, and native media cards."}
      style: {key: style, type: string, value: "Product UI"}
      references: {key: references, type: array, value: ["https://images.unsplash.com/photo-1558655146-d09347e92766?auto=format&fit=crop&w=1200&q=80", "https://images.unsplash.com/photo-1461749280684-dccba630e2f6?auto=format&fit=crop&w=1200&q=80"]}
      owner: {key: owner, type: string, value: "Product"}
      priority: {key: priority, type: string, value: "P0"}
      tags: {key: tags, type: array, value: ["reveal", "kanban", "native"]}
      image: {key: image, type: string, value: "https://images.unsplash.com/photo-1558655146-d09347e92766?auto=format&fit=crop&w=1200&q=80"}
      order: {key: order, type: number, value: 30}
    - id: {key: id, type: string, value: "SHOT_02A"}
      type: {key: type, type: string, value: "Shot"}
      label: {key: label, type: string, value: "Lane Focus"}
      position: {key: position, type: object, value: {x: 320, y: 0}}
      stage: {key: stage, type: string, value: "Review"}
      frame: {key: frame, type: number, value: 4}
      slugline: {key: slugline, type: string, value: "Selection Sync - Active Source Node"}
      summary: {key: summary, type: string, value: "Clicking a card highlights the source node and keeps graph/story alignment visible."}
      action: {key: action, type: string, value: "A selected storyboard card drives the active graph selection while the lane remains compact and readable."}
      dialogue: {key: dialogue, type: string, value: "REVIEWER: \"Click the board, inspect the node, keep the source honest.\""}
      prompt: {key: prompt, type: string, value: "Storyboard card selection highlights a connected source node in a graph editor, showing one unified system."}
      style: {key: style, type: string, value: "Diagram Hybrid"}
      references: {key: references, type: array, value: ["https://images.unsplash.com/photo-1461749280684-dccba630e2f6?auto=format&fit=crop&w=1200&q=80"]}
      owner: {key: owner, type: string, value: "Product"}
      priority: {key: priority, type: string, value: "P1"}
      tags: {key: tags, type: array, value: ["selection", "lane", "sync"]}
      imageUrl: {key: imageUrl, type: string, value: "https://images.unsplash.com/photo-1461749280684-dccba630e2f6?auto=format&fit=crop&w=1200&q=80"}
      order: {key: order, type: number, value: 40}
    - id: {key: id, type: string, value: "SCENE_03"}
      type: {key: type, type: string, value: "Frame"}
      label: {key: label, type: string, value: "Media-Rich Variant"}
      position: {key: position, type: object, value: {x: 0, y: -720}}
      stage: {key: stage, type: string, value: "Approved"}
      frame: {key: frame, type: number, value: 5}
      location: {key: location, type: string, value: "Publishing Surface"}
      timeOfDay: {key: timeOfDay, type: string, value: "Final Review"}
      summary: {key: summary, type: string, value: "Approved card carries poster art, tags, owner, and publish link in one native board card."}
      action: {key: action, type: string, value: "The approved frame combines preview video, review metadata, references, and outgoing brief links in a compact native card."}
      dialogue: {key: dialogue, type: string, value: "MARKETING: \"This one is approved. Ship the brief with the source attached.\""}
      prompt: {key: prompt, type: string, value: "Final approved product storyboard frame with poster art, compact metadata chips, and a linked launch brief."}
      style: {key: style, type: string, value: "Launch Polish"}
      references: {key: references, type: array, value: ["https://images.unsplash.com/photo-1516321497487-e288fb19713f?auto=format&fit=crop&w=1200&q=80", "https://images.unsplash.com/photo-1558655146-d09347e92766?auto=format&fit=crop&w=1200&q=80"]}
      owner: {key: owner, type: string, value: "Marketing"}
      priority: {key: priority, type: string, value: "P0"}
      tags: {key: tags, type: array, value: ["media", "approved", "publish"]}
      videoUrl: {key: videoUrl, type: string, value: "https://interactive-examples.mdn.mozilla.net/media/cc0-videos/flower.mp4"}
      order: {key: order, type: number, value: 50}
      href: {key: href, type: string, value: "https://airvio.co/knowgrph"}
    - id: {key: id, type: string, value: "SCENE_04"}
      type: {key: type, type: string, value: "Panel"}
      label: {key: label, type: string, value: "CTA End Card"}
      position: {key: position, type: object, value: {x: 320, y: -960}}
      stage: {key: stage, type: string, value: "Approved"}
      frame: {key: frame, type: number, value: 6}
      slugline: {key: slugline, type: string, value: "End Card - Workspace Native Delivery"}
      summary: {key: summary, type: string, value: "End card closes on a clear call to action for workspace-native production planning."}
      action: {key: action, type: string, value: "End card lands on a decisive launch message that ties storyboard review back to the shared Knowgrph workspace."}
      dialogue: {key: dialogue, type: string, value: "NARRATOR: \"Plan, review, and ship from the same native graph workspace.\""}
      prompt: {key: prompt, type: string, value: "Clean final end card with bold product message, warm accent color, and confident launch composition."}
      style: {key: style, type: string, value: "Brand Card"}
      references: {key: references, type: array, value: ["https://images.unsplash.com/photo-1522542550221-31fd19575a2d?auto=format&fit=crop&w=1200&q=80"]}
      owner: {key: owner, type: string, value: "Growth"}
      priority: {key: priority, type: string, value: "P1"}
      tags: {key: tags, type: array, value: ["cta", "endcard", "publish"]}
      image: {key: image, type: string, value: "https://images.unsplash.com/photo-1522542550221-31fd19575a2d?auto=format&fit=crop&w=1200&q=80"}
      order: {key: order, type: number, value: 60}
  edges:
    - {id: "edge:story:scene_01", source: "STORY_ROOT", target: "SCENE_01"}
    - {id: "edge:story:shot_01a", source: "SCENE_01", target: "SHOT_01A"}
    - {id: "edge:story:scene_02", source: "STORY_ROOT", target: "SCENE_02"}
    - {id: "edge:story:shot_02a", source: "SCENE_02", target: "SHOT_02A"}
    - {id: "edge:story:scene_03", source: "STORY_ROOT", target: "SCENE_03"}
    - {id: "edge:story:scene_04", source: "STORY_ROOT", target: "SCENE_04"}
---
# Knowgrph Storyboard Demo

Use this document to validate the native `2D Renderer: Storyboard` surface.

## Typed Fixture Contract

- This file is an approved typed validation fixture for storyboard ingest -> parse -> render coverage.
- The opening YAML frontmatter block remains the first-block machine SSOT for renderer activation and graph-backed storyboard data.
- Normalized `{key, type, value}` envelopes in `flow.nodes[*]` are intentional here so the typed E2E path stays exercised during regression and manual validation.
- This document is not the canonical plain-YAML authoring example; canonical authored storyboard docs should still prefer plain YAML for frontmatter and related schema-bearing blocks.
- Parser warning, repair, or fallback behavior is recovery-only; malformed YAML frontmatter still remains invalid source that must be fixed upstream.

## Related Docs

- [Storyboard Demo Index](./knowgrph-storyboard-demo-index.md)
- [Storyboard Product UI Demo](./knowgrph-storyboard-product-ui-demo.md)
- [Storyboard Neutral Schema Contract Demo](./knowgrph-storyboard-neutral-schema-contract-demo.md)

## Validation Goals

- Confirm the renderer activates from frontmatter via `kgCanvas2dRenderer: "storyboard"`.
- Confirm `2D Renderer: Storyboard` owns both display variants: `Card` remains the default card presentation, and `Widget` reuses the same shared renderer utilities with widget-only UI differences.
- Confirm Storyboard `Cards`, `Widgets`, and `Rich Media Panels` render from the same source graph, semantic key, pan/drag/zoom contract, and edge model without a Flow Editor renderer fork.
- Confirm the storyboard surface is repo-owned and native to Knowgrph, not copied from Boords or any vendor storyboard runtime.
- Confirm existing graph nodes project into storyboard lanes through canonical fields such as `stage`, `status`, `lane`, `phase`, or `track`, without creating a second authoring schema.
- Confirm scene-like node types such as `Scene`, `Shot`, `Frame`, `Panel`, `Beat`, and `Story` are recognized as storyboard-friendly inputs while structural/root-only nodes stay secondary or are filtered when richer cards exist.
- `#EF4444:Confirm` the board reuses shared semantic-key infrastructure and does not introduce parallel identity assembly, stale local caches, or per-renderer duplicate graph derivation.
- Confirm storyboard cards reuse shared chip/theme primitives for lane status, tags, and metadata instead of **`bg#FEF08A:bespoke`** demo-only UI shells.
- Confirm card ordering follows explicit node properties like `order`, `sequence`, `sceneOrder`, `shotOrder`, `index`, or `rank` before falling back to stable source order.
- Confirm storyboard cards project native frame/index badges from properties such as `frame`, `frameNumber`, `sceneNumber`, `shotNumber`, or `panelNumber`.
- Confirm storyboard cards build slugline text from `slugline` directly or from `location` + `timeOfDay` when explicit slugline text is absent.
- Confirm storyboard cards surface native `Action` and `Dialogue` sections from graph/frontmatter fields instead of demo-only text formatting.
- Confirm storyboard, workspace Viewer kanban, and Workflow Manager kanban surface shared paragraph-style card content from canonical text fields instead of drifting per-surface card bodies.
- Confirm storyboard, workspace Viewer kanban, and Workflow Manager kanban allow double-click inline editing on shared card title/body text, committing back to the root markdown-table or graph-node source instead of local card state.
- Confirm storyboard cards surface a native `Visual Brief` block from shared properties such as `prompt`, `imagePrompt`, and `style`.
- Confirm storyboard cards surface a compact native `Reference Pack` from shared reference arrays such as `references` or `referenceUrls`.
- Confirm image, video, and link properties such as `image`, `imageUrl`, `videoUrl`, `media_url`, `src`, `url`, or `href` render as native media-rich storyboard cards without placeholder fixtures.
- Confirm clicking a storyboard card selects the source node in the active graph store instead of creating a parallel storyboard-only selection state.
- Confirm the storyboard surface stays source-backed during inline edits: card text commits directly to graph/frontmatter-owned fields with no storyboard-local persistence layer or parallel markdown format.
- Confirm the shared Viewer `Properties` panel now owns add, duplicate, rename, and delete column CRUD end-to-end so Layout / Properties / Filter / Sort / Group state does not drift after a property mutation.
- Confirm the storyboard renderer bypasses minimap-only D3 assumptions and does not inherit incompatible minimap behavior from unrelated 2D surfaces.
- Confirm the board keeps lane/card density compact, uses horizontal lane scrolling, and avoids oversized helper chrome or copied vendor interaction patterns.

## Native Contract

- Frontmatter remains the single authoring owner.
- `flow.nodes[*]` remains the canonical node source.
- Storyboard derives view-only lane/card presentation from node labels, types, and properties.
- Lane grouping prefers `stage`, then other shared lane-like fields.
- Card content prefers `label`, `summary`-like fields, tags, owner, priority, and media/link URLs already present on the node.
- Storyboard detail blocks also reuse shared graph properties for frame numbering, slugline, action, dialogue, prompt, style, and references.
- `Card` is the default Storyboard Display variant; `Widget` is the same Storyboard renderer surface with widget-form UI, not a separate Flow Editor renderer.
- Rich Media Panels remain first-class Storyboard surfaces for image, video, HTML/srcdoc, audio, and generated output nodes.

## Authoring Notes

- Use stable scene-like ids such as `SCENE_01`, `SHOT_01A`, or `PANEL_04`.
- Prefer `stage` for lane grouping when authoring storyboard demos because it reads cleanly as `Draft`, `Review`, and `Approved`.
- Prefer `order` for deterministic left-to-right narrative sequencing inside each lane.
- Prefer shared graph properties like `summary`, `owner`, `priority`, `tags`, `url`, `href`, `image`, `imageUrl`, `videoUrl`, `media_url`, `frame`, `slugline`, `location`, `timeOfDay`, `action`, `dialogue`, `prompt`, `style`, and `references` instead of renderer-local custom keys.
- Prefer canonical text properties such as `summary`, `description`, `content`, `text`, `note`, `notes`, `action`, `dialogue`, and `prompt` when authoring card body copy so storyboard and kanban surfaces project the same paragraph content.
- Keep storyboard content enhancement-first: edit the graph/frontmatter source, then let the renderer project the board.

## Expected Lanes

- `Draft` should contain `SCENE_01` and `SHOT_01A`.
- `Review` should contain `SCENE_02` and `SHOT_02A`.
- `Approved` should contain `SCENE_03` and `SCENE_04`.

## Expected Card Signals

- `SCENE_01` should show frame `1`, a generated slugline from `Conference Room - Monday`, an `Action` block, a `Dialogue` block, a Doodle-style `Visual Brief`, a two-item `Reference Pack`, and an external brief link.
- `SHOT_01A` should show frame `2`, explicit slugline text, workflow-pain tags, a style chip, and reference thumbnails while staying ordered after `SCENE_01`.
- `SCENE_02` should validate graph-to-storyboard projection language: native board, shared kanban visual language, no copied vendor shell, plus a product-UI visual brief.
- `SHOT_02A` should validate card-click selection sync back to the graph node and keep a compact selection-focused storyboard card body.
- `SCENE_03` should validate video preview support for approved media-rich cards together with references, style, owner, priority, and launch brief metadata.
- `SCENE_04` should validate approved CTA card rendering with compact chips, explicit end-card dialogue, and a brand-card visual brief.

## Demo Intent

- The cold open proves storyboard cards can represent narrative setup.
- The reveal proves current graph data can become a storyboard board without a second system.
- The approved cards prove media-rich review planning can stay inside the same Markdown + graph authoring pipeline.
- The overall demo proves the new storyboard-specific card sections remain graph-derived, kanban-shaped, and fully native in-repo.
