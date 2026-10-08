# Graph Report - AlabMovement  (2026-10-09)

## Corpus Check
- 5 files · ~5,012 words
- Verdict: corpus is large enough that graph structure adds value.
- Unclassified: 2 file(s) not represented in the graph (top: .example 1, (none) 1)

## Summary
- 37 nodes · 34 edges · 4 communities (3 shown, 1 thin omitted)
- Extraction: 100% EXTRACTED · 0% INFERRED · 0% AMBIGUOUS
- Token cost: 0 input · 0 output

## Graph Freshness
- Built from commit: `d477e167`
- Run `git rev-parse HEAD` and compare to check if the graph is stale.
- Run `graphify update .` after code changes (no API cost).

## Community Hubs (Navigation)
- Two-Way Branching & Environment Workflow
- 2. Daily Workflow Guide
- Apple Design
- autonomous-execution.md

## God Nodes (most connected - your core abstractions)
1. `Apple Design` - 21 edges
2. `2. Daily Workflow Guide` - 5 edges
3. `Two-Way Branching & Environment Workflow` - 4 edges
4. `Alab Movement` - 3 edges
5. `Autonomous Mode & Auto-Execution` - 1 edges
6. `Initial Response` - 1 edges
7. `The Core Idea` - 1 edges
8. `1. Response — kill latency` - 1 edges
9. `2. Direct manipulation — 1:1 tracking` - 1 edges
10. `3. Interruptibility — the single most important principle` - 1 edges

## Surprising Connections (you probably didn't know these)
- None detected - all connections are within the same source files.

## Communities (4 total, 1 thin omitted)

### Community 0 - "Two-Way Branching & Environment Workflow"
Cohesion: 0.25
Nodes (6): 1. Branch Roles, 3. Golden Rules, Two-Way Branching & Environment Workflow, Alab Movement, Environment & Database Setup, Repository Structure

### Community 1 - "2. Daily Workflow Guide"
Cohesion: 0.40
Nodes (5): 2. Daily Workflow Guide, Step 1: Work on the `testing` branch, Step 2: Test against the testing database, Step 3: Promote tested changes to `production`, Step 4: Return to the `testing` branch

### Community 2 - "Apple Design"
Cohesion: 0.09
Nodes (21): 10. Gesture design details (the "feel" checklist), 11. Frame-level smoothness, 12. Materials & depth — translucency conveys hierarchy, 13. Multimodal feedback — motion + sound + haptics, 14. Reduced motion & accessibility, 15. Typography — optical sizing, tracking, leading, 16. Design foundations — the eight principles, 17. Process (+13 more)

## Knowledge Gaps
- **29 isolated node(s):** `Autonomous Mode & Auto-Execution`, `Initial Response`, `The Core Idea`, `1. Response — kill latency`, `2. Direct manipulation — 1:1 tracking` (+24 more)
  These have ≤1 connection - possible missing edges or undocumented components. (Counts symbols only; 31 node(s) total have ≤1 connection when file, concept and rationale nodes are included.)
- **1 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `Two-Way Branching & Environment Workflow` connect `Two-Way Branching & Environment Workflow` to `2. Daily Workflow Guide`?**
  _High betweenness centrality (0.073) - this node is a cross-community bridge._
- **What connects `Autonomous Mode & Auto-Execution`, `Initial Response`, `The Core Idea` to the rest of the system?**
  _29 weakly-connected nodes found - possible documentation gaps or missing edges._
- **Should `Apple Design` be split into smaller, more focused modules?**
  _Cohesion score 0.09090909090909091 - nodes in this community are weakly interconnected._
- **Why does `2. Daily Workflow Guide` connect `2. Daily Workflow Guide` to `Two-Way Branching & Environment Workflow`?**
  _High betweenness centrality (0.060) - this node is a cross-community bridge._