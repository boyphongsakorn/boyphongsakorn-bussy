# Graph Report - boyphongsakorn-bussy  (2026-09-30)

## Corpus Check
- Corpus is ~2,496 words - fits in a single context window. You may not need a graph.

## Summary
- 63 nodes · 55 edges · 12 communities (7 shown, 5 thin omitted)
- Extraction: 93% EXTRACTED · 7% INFERRED · 0% AMBIGUOUS · INFERRED: 4 edges (avg confidence: 0.85)
- Token cost: 0 input · 0 output

## Community Hubs (Navigation)
- JS Compiler Options
- Package Dependency Graph
- Svelte Vite Docs
- App Entry Components
- Dev Dependencies
- Runtime Dependencies
- NPM Scripts
- TS Config Extends
- Event Schedule Helpers
- CheckJs Rationale

## God Nodes (most connected - your core abstractions)
1. `compilerOptions` - 13 edges
2. `scripts` - 4 edges
3. `Svelte` - 4 edges
4. `@sveltejs/vite-plugin-svelte` - 2 edges
5. `vite` - 2 edges
6. `Vite` - 2 edges
7. `main.js module script` - 2 edges
8. `getoutoldevents` - 2 edges
9. `moduleResolution` - 1 edges
10. `target` - 1 edges

## Surprising Connections (you probably didn't know these)
- `Svelte logo asset` --conceptually_related_to--> `Svelte`  [INFERRED]
  src/assets/svelte.png → README.md
- `Vite` --conceptually_related_to--> `main.js module script`  [INFERRED]
  README.md → index.html

## Import Cycles
- None detected.

## Hyperedges (group relationships)
- **Schedule display flow** — test_event_schedule, test_getoutoldevents, test_getthaiformat [EXTRACTED 1.00]

## Communities (12 total, 5 thin omitted)

### Community 0 - "JS Compiler Options"
Cohesion: 0.13
Nodes (14): compilerOptions, baseUrl, checkJs, esModuleInterop, forceConsistentCasingInFileNames, importsNotUsedAsValues, isolatedModules, module (+6 more)

### Community 1 - "Package Dependency Graph"
Cohesion: 0.17
Nodes (11): name, private, type, version, svelte, svelte-avatar, @sveltejs/vite-plugin-svelte, sveltestrap (+3 more)

### Community 2 - "Svelte Vite Docs"
Cohesion: 0.29
Nodes (7): App entry div, main.js module script, HMR state preservation, Svelte, SvelteKit, Vite, Svelte logo asset

### Community 4 - "Dev Dependencies"
Cohesion: 0.40
Nodes (5): devDependencies, svelte, @sveltejs/vite-plugin-svelte, @tsconfig/svelte, vite

### Community 5 - "Runtime Dependencies"
Cohesion: 0.50
Nodes (4): dependencies, svelte-avatar, sveltestrap, @sveltestrap/sveltestrap

### Community 6 - "NPM Scripts"
Cohesion: 0.50
Nodes (4): scripts, build, dev, preview

### Community 8 - "Event Schedule Helpers"
Cohesion: 0.67
Nodes (3): Event schedule list, getoutoldevents, getthaiformat

## Knowledge Gaps
- **42 isolated node(s):** `moduleResolution`, `target`, `module`, `importsNotUsedAsValues`, `isolatedModules` (+37 more)
  These have ≤1 connection - possible missing edges or undocumented components. (Counts symbols only; 47 node(s) total have ≤1 connection when file, concept and rationale nodes are included.)
- **5 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `devDependencies` connect `Dev Dependencies` to `Package Dependency Graph`?**
  _High betweenness centrality (0.048) - this node is a cross-community bridge._
- **Why does `scripts` connect `NPM Scripts` to `Package Dependency Graph`?**
  _High betweenness centrality (0.036) - this node is a cross-community bridge._
- **Are the 2 inferred relationships involving `Svelte` (e.g. with `HMR state preservation` and `Svelte logo asset`) actually correct?**
  _`Svelte` has 2 INFERRED edges - model-reasoned connections that need verification._
- **What connects `moduleResolution`, `target`, `module` to the rest of the system?**
  _42 weakly-connected nodes found - possible documentation gaps or missing edges._
- **Should `JS Compiler Options` be split into smaller, more focused modules?**
  _Cohesion score 0.13333333333333333 - nodes in this community are weakly interconnected._