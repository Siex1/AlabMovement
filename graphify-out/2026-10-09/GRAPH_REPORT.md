# Graph Report - AlabMovement  (2026-10-08)

## Corpus Check
- 4 files · ~1,533 words
- Verdict: corpus is large enough that graph structure adds value.
- Unclassified: 2 file(s) not represented in the graph (top: .example 1, (none) 1)

## Summary
- 15 nodes · 13 edges · 4 communities (3 shown, 1 thin omitted)
- Extraction: 100% EXTRACTED · 0% INFERRED · 0% AMBIGUOUS
- Token cost: 0 input · 0 output

## Graph Freshness
- Built from commit: `3a0a1d01`
- Run `git rev-parse HEAD` and compare to check if the graph is stale.
- Run `graphify update .` after code changes (no API cost).

## Community Hubs (Navigation)
- Alab Movement
- 2. Daily Workflow Guide
- Two-Way Branching & Environment Workflow
- autonomous-execution.md

## God Nodes (most connected - your core abstractions)
1. `2. Daily Workflow Guide` - 5 edges
2. `Two-Way Branching & Environment Workflow` - 4 edges
3. `Alab Movement` - 3 edges
4. `Autonomous Mode & Auto-Execution` - 1 edges
5. `1. Branch Roles` - 1 edges
6. `Step 1: Work on the `testing` branch` - 1 edges
7. `Step 2: Test against the testing database` - 1 edges
8. `Step 3: Promote tested changes to `production`` - 1 edges
9. `Step 4: Return to the `testing` branch` - 1 edges
10. `3. Golden Rules` - 1 edges

## Surprising Connections (you probably didn't know these)
- None detected - all connections are within the same source files.

## Communities (4 total, 1 thin omitted)

### Community 0 - "Alab Movement"
Cohesion: 0.40
Nodes (3): Alab Movement, Environment & Database Setup, Repository Structure

### Community 1 - "2. Daily Workflow Guide"
Cohesion: 0.40
Nodes (5): 2. Daily Workflow Guide, Step 1: Work on the `testing` branch, Step 2: Test against the testing database, Step 3: Promote tested changes to `production`, Step 4: Return to the `testing` branch

### Community 2 - "Two-Way Branching & Environment Workflow"
Cohesion: 0.67
Nodes (3): 1. Branch Roles, 3. Golden Rules, Two-Way Branching & Environment Workflow

## Knowledge Gaps
- **9 isolated node(s):** `Autonomous Mode & Auto-Execution`, `1. Branch Roles`, `Step 1: Work on the `testing` branch`, `Step 2: Test against the testing database`, `Step 3: Promote tested changes to `production`` (+4 more)
  These have ≤1 connection - possible missing edges or undocumented components. (Counts symbols only; 10 node(s) total have ≤1 connection when file, concept and rationale nodes are included.)
- **1 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `Two-Way Branching & Environment Workflow` connect `Two-Way Branching & Environment Workflow` to `Alab Movement`, `2. Daily Workflow Guide`?**
  _High betweenness centrality (0.505) - this node is a cross-community bridge._
- **What connects `Autonomous Mode & Auto-Execution`, `1. Branch Roles`, `Step 1: Work on the `testing` branch` to the rest of the system?**
  _9 weakly-connected nodes found - possible documentation gaps or missing edges._
- **Why does `2. Daily Workflow Guide` connect `2. Daily Workflow Guide` to `Two-Way Branching & Environment Workflow`?**
  _High betweenness centrality (0.418) - this node is a cross-community bridge._