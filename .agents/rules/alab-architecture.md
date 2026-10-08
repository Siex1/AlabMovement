---
trigger: always_on
description: Core system architecture, non-partisan mandate, and governance rules for ALAB Movement.
---

# ALAB Movement — System Blueprint & Architecture Rules

Source blueprint: `docs/ALAB_Movement_System_Blueprint.md`

## 1. Core Principles & Mandate
- **Non-Partisan Platform**: Dedicated exclusively to youth civic participation and organizational management. No electioneering, campaign targeting, or political profiling.
- **Single Source of Truth**: PHP Laravel backend manages all authentication, authorization (RBAC), membership lifecycles, and financial transactions. (FastAPI is strictly an optional isolated secondary service for analytics).
- **Separation of Authority**: Technical administration (SysAdmin) is strictly separated from organizational governance. System Administrators cannot silently alter finance or governance records.
- **No Self-Approval**: Approvers (e.g. Chair, Treasurer) cannot approve their own submissions or transactions.

## 2. Technical Stack
- **Backend**: PHP Laravel (running on PHP 8.2+ with MySQL/MariaDB).
- **Frontend**: Blade templates, responsive Bootstrap 5, Alpine.js / Livewire, adhering to Apple-style fluid design (`apple-design` skill).
- **Data Privacy**: Philippine Data Privacy Act (RA 10173) compliance, purposeful data collection, audit logging with token/password redaction.

## 3. Implementation Order
Develop systematically following the Phase-by-Phase Development Roadmap:
1. Phase 0: Discovery & Governance
2. Phase 1: Foundation & Security (Laravel setup, DB migrations, RBAC, base layouts)
3. Phase 2: Public Landing Page & CMS (Apple-design fluid UI, public pages)
4. Phase 3: Registration, Authentication & Member Onboarding
5. Phase 4: System Administration & Audit Logging
6. Phase 5: Officer & Committee Workspaces
7. Phase 6: Events, Projects & Volunteer Tracking (QR check-in)
8. Phase 7: Finance & Transparency
9. Phase 8: Documents, Certificates & Notifications
10. Phase 9: Optional Python/FastAPI Integrations
11. Phase 10: QA, Security Hardening & Production Launch
