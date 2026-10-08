# Graph Report - AlabMovement  (2026-10-09)

## Corpus Check
- 8 files · ~9,502 words
- Verdict: corpus is large enough that graph structure adds value.
- Unclassified: 2 file(s) not represented in the graph (top: .example 1, (none) 1)

## Summary
- 107 nodes · 102 edges · 10 communities (9 shown, 1 thin omitted)
- Extraction: 100% EXTRACTED · 0% INFERRED · 0% AMBIGUOUS
- Token cost: 0 input · 0 output

## Graph Freshness
- Built from commit: `1f15ea8f`
- Run `git rev-parse HEAD` and compare to check if the graph is stale.
- Run `graphify update .` after code changes (no API cost).

## Community Hubs (Navigation)
- 2. Daily Workflow Guide
- ALAB Movement — Organization Management System
- Apple Design
- autonomous-execution.md
- 10. Phase-by-phase development roadmap
- 7. Functional modules
- 3. Roles and authority
- ALAB Movement — Phase-by-Phase Roadmap Progress
- ALAB Movement — System Blueprint & Architecture Rules
- 6. Registration, authentication, and membership lifecycle

## God Nodes (most connected - your core abstractions)
1. `Apple Design` - 21 edges
2. `ALAB Movement — Organization Management System` - 17 edges
3. `7. Functional modules` - 13 edges
4. `10. Phase-by-phase development roadmap` - 13 edges
5. `3. Roles and authority` - 11 edges
6. `2. Daily Workflow Guide` - 5 edges
7. `ALAB Movement — System Blueprint & Architecture Rules` - 4 edges
8. `Two-Way Branching & Environment Workflow` - 4 edges
9. `6. Registration, authentication, and membership lifecycle` - 4 edges
10. `Alab Movement` - 3 edges

## Surprising Connections (you probably didn't know these)
- None detected - all connections are within the same source files.

## Communities (10 total, 1 thin omitted)

### Community 0 - "2. Daily Workflow Guide"
Cohesion: 0.15
Nodes (11): 1. Branch Roles, 2. Daily Workflow Guide, 3. Golden Rules, Step 1: Work on the `testing` branch, Step 2: Test against the testing database, Step 3: Promote tested changes to `production`, Step 4: Return to the `testing` branch, Two-Way Branching & Environment Workflow (+3 more)

### Community 1 - "ALAB Movement — Organization Management System"
Cohesion: 0.12
Nodes (17): 11. MVP priorities, 12. Screen inventory, 13. Non-functional requirements, 14. Suggested future features, 15. Example acceptance tests, 16. Decisions to confirm before coding, 1. Project overview, 2. Recommended technology architecture (+9 more)

### Community 2 - "Apple Design"
Cohesion: 0.09
Nodes (21): 10. Gesture design details (the "feel" checklist), 11. Frame-level smoothness, 12. Materials & depth — translucency conveys hierarchy, 13. Multimodal feedback — motion + sound + haptics, 14. Reduced motion & accessibility, 15. Typography — optical sizing, tracking, leading, 16. Design foundations — the eight principles, 17. Process (+13 more)

### Community 4 - "10. Phase-by-phase development roadmap"
Cohesion: 0.15
Nodes (13): 10. Phase-by-phase development roadmap, Phase 0 — Discovery and governance (1–2 weeks), Phase 10 — QA, privacy, deployment, and launch (2–3 weeks), Phase 11 — Post-launch improvements (ongoing), Phase 1 — Foundation and security (1–2 weeks), Phase 2 — Public landing page and CMS (2 weeks), Phase 3 — Registration, login, and member onboarding (2–3 weeks), Phase 4 — System administration (2 weeks) (+5 more)

### Community 5 - "7. Functional modules"
Cohesion: 0.15
Nodes (13): 7.10 Reports and dashboards, 7.11 Audit logs and accountability, 7.12 Monitoring, maintenance, and disaster recovery, 7.1 Public content management (CMS), 7.2 Membership management, 7.3 Organization structure & committees, 7.4 Events and attendance, 7.5 Projects and volunteer management (+5 more)

### Community 6 - "3. Roles and authority"
Cohesion: 0.18
Nodes (11): 3.10 Optional future roles, 3.1 System administrator (technical), 3.2 Chairperson, 3.3 Vice Chairperson, 3.4 Secretary, 3.5 Treasurer, 3.6 Press Relations Officer, 3.7 Public Relations Officer (+3 more)

### Community 7 - "ALAB Movement — Phase-by-Phase Roadmap Progress"
Cohesion: 0.29
Nodes (5): ALAB Movement — Phase-by-Phase Roadmap Progress, Phase 0 — Discovery and Governance, Phase 1 — Foundation and Security, Phase Details, Progress Overview

### Community 8 - "ALAB Movement — System Blueprint & Architecture Rules"
Cohesion: 0.40
Nodes (4): 1. Core Principles & Mandate, 2. Technical Stack, 3. Implementation Order, ALAB Movement — System Blueprint & Architecture Rules

### Community 9 - "6. Registration, authentication, and membership lifecycle"
Cohesion: 0.50
Nodes (4): 6. Registration, authentication, and membership lifecycle, Registration fields (minimum), Registration workflow, Security

## Knowledge Gaps
- **86 isolated node(s):** `1. Core Principles & Mandate`, `2. Technical Stack`, `3. Implementation Order`, `Autonomous Mode & Auto-Execution`, `Initial Response` (+81 more)
  These have ≤1 connection - possible missing edges or undocumented components. (Counts symbols only; 89 node(s) total have ≤1 connection when file, concept and rationale nodes are included.)
- **1 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `ALAB Movement — Organization Management System` connect `ALAB Movement — Organization Management System` to `10. Phase-by-phase development roadmap`, `7. Functional modules`, `3. Roles and authority`, `ALAB Movement — Phase-by-Phase Roadmap Progress`, `6. Registration, authentication, and membership lifecycle`?**
  _High betweenness centrality (0.318) - this node is a cross-community bridge._
- **What connects `1. Core Principles & Mandate`, `2. Technical Stack`, `3. Implementation Order` to the rest of the system?**
  _86 weakly-connected nodes found - possible documentation gaps or missing edges._
- **Should `ALAB Movement — Organization Management System` be split into smaller, more focused modules?**
  _Cohesion score 0.11764705882352941 - nodes in this community are weakly interconnected._
- **Why does `7. Functional modules` connect `7. Functional modules` to `ALAB Movement — Organization Management System`?**
  _High betweenness centrality (0.124) - this node is a cross-community bridge._
- **Should `Apple Design` be split into smaller, more focused modules?**
  _Cohesion score 0.09090909090909091 - nodes in this community are weakly interconnected._
- **Why does `10. Phase-by-phase development roadmap` connect `10. Phase-by-phase development roadmap` to `ALAB Movement — Organization Management System`?**
  _High betweenness centrality (0.124) - this node is a cross-community bridge._