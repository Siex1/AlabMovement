# ALAB Movement — Organization Management System

**Document:** System Architecture, Features, and Phase-by-Phase Development Blueprint  
**Version:** 1.0 | **Date:** October 2026  
**Organization:** ALAB Movement — proposed non-partisan, youth-led civic organization platform  
**Facebook reference:** https://www.facebook.com/alabmovement  

> This is a proposed system design, not a statement of ALAB Movement's existing policies or Facebook content. Confirm organizational titles, eligibility, privacy notices, and approval processes with the leadership before implementation.

## 1. Project overview

Build a secure web-based platform for ALAB Movement to manage membership, leadership, activities, volunteer work, communications, finances, and public engagement. The platform must remain non-partisan: no party/candidate endorsements, political profiling, or campaign targeting.

### Goals
- Provide a public website describing the organization and its initiatives.
- Accept and review membership applications.
- Coordinate members, committees, events, volunteers, and community projects.
- Keep official records, meeting minutes, announcements, and reports.
- Track donations and expenses transparently, with appropriate approval controls.
- Separate technical administration from organizational decision-making.
- Preserve security, privacy, accountability, and auditability.

### Scope boundaries
- The platform is for organization management and civic participation, **not** electioneering or voter persuasion.
- Membership and volunteer data should be collected only when necessary and with appropriate notice/consent or other valid legal basis.
- Public transparency reports must not expose private member or donor information.

## 2. Recommended technology architecture

| Layer | Recommendation | Purpose |
|---|---|---|
| Web backend | PHP Laravel | Primary application, authentication, business rules, admin/member portal |
| Web frontend | Laravel Blade + Bootstrap 5 + Alpine.js (or Livewire) | Accessible responsive interface; keep initial build simple |
| Database | MySQL 8 / MariaDB (supported Laravel version) | Transactional organizational data |
| Local development | XAMPP (Apache + PHP + database) | Local development only; verify Laravel/PHP version compatibility |
| Python service | FastAPI | Optional isolated analytics, document processing, or future AI-assisted features |
| API integration | REST/JSON over HTTPS | Laravel communicates with FastAPI using service credentials |
| Background jobs | Laravel queues + scheduler | Email, reminders, report generation, maintenance |
| Cache/queue (optional) | Redis | Production caching and jobs at scale |
| Storage | Laravel private storage / S3-compatible object storage | Documents, photos, receipts; access-controlled |
| Email | SMTP or transactional email provider | Verification, password reset, invitations, notices |
| Deployment | Linux + Nginx/Apache + PHP-FPM + HTTPS | Production hosting; do not expose XAMPP publicly |
| Source control | Git + GitHub | Branches, reviews, release tags |

**Architecture decision:** Laravel is the **single source of truth** for accounts, permissions, membership, and finances. FastAPI is an optional internal service, not a second login system. Begin with Laravel only; add FastAPI when a specific Python-only requirement is approved.

```text
Visitor / Guest / Member / Officer / System Admin
                    |
               HTTPS Web
                    |
         Laravel Web Application
        /       |       |       \
   Auth/RBAC  Modules  Jobs   API Client
        |       |       |         |
        +-------+-------+     FastAPI (optional)
                |
           MySQL Database
                |
        Private File Storage
```

## 3. Roles and authority

### 3.1 System administrator (technical)
- Manage accounts, activation/deactivation, role assignments, access requests.
- View immutable audit trails and security events (with controlled access).
- Monitor application health, errors, failed logins, storage, queue jobs, and uptime.
- Configure backups, restore testing, patches, integrations, and system settings.
- Manage incident response and emergency access.
- **Cannot silently approve their own finance transactions or change governance records.** Technical privilege does not equal organizational authority.

### 3.2 Chairperson
- Oversee strategic plans, programs, official announcements, and organizational reports.
- Approve proposals, major events, and expenditures according to policy.
- View leadership dashboards and committee performance.

### 3.3 Vice Chairperson
- Assist chairperson; supervise assigned programs and committees.
- Act as delegated approver only when delegation is documented and time-limited.

### 3.4 Secretary
- Manage meetings, agendas, minutes, resolutions, attendance, official records, and membership documentation.
- Publish approved minutes and maintain document version history.

### 3.5 Treasurer
- Record budgets, funding sources, donations, reimbursements, receipts, and expenses.
- Prepare financial statements and reconcile transactions.
- Submit expenses for independent approval; cannot approve own submissions.

### 3.6 Press Relations Officer
- Draft press releases, media kits, public statements, and media inquiries.
- Route external statements through a publication approval workflow.

### 3.7 Public Relations Officer
- Manage public inquiries, community partnerships, outreach, volunteer recruitment, and event promotions.
- Coordinate public-facing campaigns that are non-partisan.

**Note:** Press Relations and Public Relations have overlapping functions. Keep them separate if the organization needs two officers; otherwise combine under a Communications committee with distinct permissions.

### 3.8 Member
- Manage own profile and consent preferences.
- Browse approved internal announcements, events, projects, and volunteer opportunities.
- Register for activities, submit participation reports, access permitted files, and request certificates.
- Submit proposals or feedback where enabled.

### 3.9 Guest / public visitor
- Browse public pages, announcements, public events, programs, and published transparency reports.
- Submit inquiries, join event waitlists, and apply for membership.
- No access to internal membership lists, financial source records, or private documents.

### 3.10 Optional future roles
- Membership Officer, Committee Lead, Event Coordinator, Volunteer Coordinator, Content Editor, Auditor (read-only), and Data Privacy Officer.
- Prefer **permissions** over creating many fixed roles; a user may hold multiple positions with scoped access.

## 4. Access-control matrix (initial policy)

Legend: **M** = manage; **A** = approve; **C** = create/edit within scope; **V** = view authorized data; **—** = no access.

| Feature | Sys Admin | Chair | Vice Chair | Secretary | Treasurer | Press | Public Relations | Member | Guest |
|---|---|---|---|---|---|---|---|---|---|
| System accounts & security | M | V* | — | — | — | — | — | — | — |
| Membership applications | Technical only | A | A* | C | — | — | C* | Own | Apply |
| Meetings & minutes | Technical only | A/V | V | M | V | V* | V* | V* | — |
| Event/program proposals | Technical only | A | A* | C | Budget V | C | C | C | — |
| Public announcements | Technical only | A | A* | C | — | C | C | V | V |
| Financial transactions | Technical only | A** | A** | — | C | — | — | — | — |
| Financial summaries | Technical only | V | V | V* | M | — | — | V* | Published only |
| Audit/security logs | M | V* | — | — | — | — | — | — | — |

`*` Subject to approved scope and delegation. `**` No self-approval, and follow documented approval thresholds. Technical-only means maintenance access, not authority to decide or alter organizational records. Implement row-level policies and committee scoping, not only menu hiding.

## 5. Public website and landing page

### Main navigation
- Home
- About ALAB Movement (mission, vision, values, history, officers)
- Programs & Advocacy (non-partisan initiatives)
- Events & Activities
- News & Announcements
- Volunteer / Join Us
- Transparency & Impact
- Contact / FAQ
- Login / Register

### Home page sections
1. Hero banner with organization mission and calls to **Join**, **Volunteer**, and **Explore Programs**.
2. About the organization and non-partisan commitment.
3. Featured activities and upcoming events.
4. Community impact indicators (verified and dated).
5. News, announcements, and photo gallery with media consent.
6. Partnership/contact form.
7. Footer with policies, social links, and official contact details.

## 6. Registration, authentication, and membership lifecycle

### Registration fields (minimum)
- Full name, email, password, optional phone, general location (e.g., city/municipality), optional interests, required policy acknowledgment.
- Additional eligibility fields only when organizational policy requires them; avoid collecting government IDs by default.
- If minors can join, implement age-appropriate consent/guardian processes before launch.

### Registration workflow
```text
Visitor registers
    -> email verification
    -> membership application created (Pending)
    -> Secretary/Membership Officer reviews
    -> Approve / Request More Info / Reject (with reason)
    -> approved applicant becomes Member
    -> member receives onboarding notification
    -> optional committee assignment
```

### Security
- Laravel authentication with secure password hashing and email verification.
- Rate limiting, CSRF protection, session regeneration, secure cookies, logout everywhere.
- MFA required for system admins and finance approvers; recommended for all officers.
- Password reset tokens with expiration; no plaintext password storage.
- Permission checks on every backend route and resource.
- Track consent/policy version, timestamp, and withdrawal preferences.

## 7. Functional modules

### 7.1 Public content management (CMS)
- Pages, articles, program profiles, banners, galleries, scheduled publishing.
- Draft -> Review -> Approved -> Published -> Archived workflow.
- Media usage permission records and alt text.

### 7.2 Membership management
- Applications, member directory (restricted), status, renewal (if needed), committees, skills/interests, membership history.
- Deactivate/leave/appeal process; export own data subject to policy.

### 7.3 Organization structure & committees
- Positions, terms of office, appointments, committees, delegations, organizational chart, role history.
- Support multiple roles per user and start/end dates.

### 7.4 Events and attendance
- Event proposals, schedules, venues, capacity, registration, waitlists, check-in QR, attendance, volunteer hours, feedback.
- Public events can allow guests; private events require membership.

### 7.5 Projects and volunteer management
- Project proposals, objectives, budgets, milestones, tasks, volunteer assignments, activity logs, outcomes, evidence/photos.
- Dashboard for project completion and impact reporting.

### 7.6 Meetings and governance
- Meeting calendar, agenda, invitations, minutes, motions, resolutions, attendance, action items, approvals, document versioning.
- Optional voting for internal governance only, with eligibility rules and auditable results; not for political campaigns.

### 7.7 Communications
- Internal announcements, officer bulletins, member inbox, email notifications, inquiry ticketing, contact requests.
- Press releases and public statements require approval before publishing.
- Avoid bulk political persuasion or member profiling.

### 7.8 Finance and transparency
- Chart of accounts/categories, budgets, donations, income, expenses, reimbursement requests, attachments/receipts.
- Submit -> Treasurer review -> Independent approval -> Paid/Recorded -> Reconciled.
- Maintain append-only transaction history, corrections via reversing entries, monthly summary reports.
- Publish only aggregated approved figures; protect donor identities and financial details.
- Do not collect payment-card details directly; use a compliant payment provider if online payments are added.

### 7.9 Documents and certificates
- Private document repository, folders, access scopes, versions, retention, downloadable participation certificates with verification codes.
- Scan uploaded files for malware; restrict types and sizes.

### 7.10 Reports and dashboards
- System admin: accounts, access events, failed jobs, backup health, security incidents.
- Leadership: member growth, active projects, event turnout, volunteer hours, approvals pending.
- Treasurer: budget vs actual, income/expenses, unreconciled entries.
- Member: registered events, participation hours, assigned tasks, certificates.
- Public: published impact metrics and approved transparency reports.

### 7.11 Audit logs and accountability
Record: timestamp (UTC), actor ID, role at action time, event/action, affected record type/ID, outcome, request/correlation ID, IP/device metadata where justified, and redacted before/after changes.

**Log events:** login/logout, failed login, account/role changes, membership decisions, approvals, publication changes, finance modifications, document access where justified, exports, backup/restore, configuration changes.

**Controls:** append-only storage, strict read access, retention policy, tamper detection, sensitive-field redaction, audit review, and separation from editable business records. Never log passwords, session tokens, or secret keys.

### 7.12 Monitoring, maintenance, and disaster recovery
- Health checks, exception tracking, application logs, job failures, disk/storage capacity, database status, uptime alerts.
- Regular security updates and dependency scanning; change/release log.
- Encrypted automated backups, off-site copies, least-privilege backup credentials, documented restoration tests.
- Define recovery time and recovery point targets before production.
- Hardware lifecycle applies only if ALAB operates its own physical devices/servers; otherwise track hosting and organizational devices.

## 8. Proposed database schema

**Identity and authorization**
- `users` (id, name, email, password_hash, status, email_verified_at, timestamps)
- `roles` (id, name, description)
- `permissions` (id, key, description)
- `model_has_roles`, `role_has_permissions` (or equivalent Laravel authorization tables)
- `officer_terms` (user_id, position, committee_id, starts_at, ends_at, appointed_by)
- `consent_records` (user_id, policy_version, consent_type, recorded_at, withdrawn_at)

**Membership**
- `membership_applications` (user_id, status, reviewed_by, reviewed_at, decision_reason)
- `member_profiles` (user_id, municipality, interests, joined_at, membership_status)
- `committees`, `committee_members`

**Content and communication**
- `pages`, `posts`, `media_assets`, `publication_approvals`
- `announcements`, `notifications`, `contact_inquiries`

**Programs and governance**
- `projects`, `project_tasks`, `project_volunteers`, `project_updates`
- `events`, `event_registrations`, `attendance`, `volunteer_hour_entries`
- `meetings`, `meeting_attendees`, `meeting_minutes`, `resolutions`, `action_items`

**Finance**
- `budgets`, `budget_lines`, `donations`, `expenses`, `expense_approvals`, `financial_ledger_entries`, `receipts`, `reconciliations`

**Security and operations**
- `audit_logs`, `security_incidents`, `system_alerts`, `backup_runs`, `integration_jobs`, `file_access_logs`

**Implementation notes:** Use foreign keys, unique constraints, indexes, timestamps, status enums or lookup tables, soft deletes only where justified, and migrations/seeders. Never use soft delete as a substitute for legally required permanent deletion or financial history retention. Define retention per data category.

## 9. Suggested Laravel project structure

```text
alab-movement/
├── app/
│   ├── Http/Controllers/
│   │   ├── Public/
│   │   ├── Auth/
│   │   ├── Admin/
│   │   ├── Officers/
│   │   └── Members/
│   ├── Http/Requests/
│   ├── Models/
│   ├── Policies/
│   ├── Services/
│   │   ├── Membership/
│   │   ├── Events/
│   │   ├── Finance/
│   │   ├── Publishing/
│   │   └── Audit/
│   ├── Jobs/
│   ├── Notifications/
│   └── Events/
├── bootstrap/
├── config/
├── database/
│   ├── migrations/
│   ├── seeders/
│   └── factories/
├── public/
├── resources/
│   ├── views/{public,auth,admin,officers,members,components}/
│   ├── css/
│   └── js/
├── routes/{web.php,api.php,console.php}/
├── storage/app/private/
├── tests/{Feature,Unit}/
├── docs/
├── .env.example
└── composer.json

# Separate optional Python service (not inside Laravel public/)
fastapi-service/
├── app/{main.py,api,services,schemas,core}/
├── tests/
├── requirements.txt
└── .env.example
```

Use version control for migrations, never commit `.env` secrets, and avoid putting application logic into Blade templates.

## 10. Phase-by-phase development roadmap

### Phase 0 — Discovery and governance (1–2 weeks)
**Deliverables:** requirements, approved organization roles, policies, data inventory, sitemap, wireframes, acceptance criteria.
- [ ] Interview Chairperson, Secretary, Treasurer, Press/Public Relations.
- [ ] Confirm membership eligibility, officer appointments, finance thresholds, content approvals.
- [ ] Identify data privacy responsibilities, consent and retention requirements.
- [ ] Confirm public-facing brand assets and content from authorized ALAB representatives.
- [ ] Prioritize MVP vs later releases.
**Exit criterion:** leadership signs off on requirements and access matrix.

### Phase 1 — Foundation and security (1–2 weeks)
**Deliverables:** working Laravel repository, XAMPP local environment, migrations, design system, CI basics.
- [ ] Set up Laravel, database, `.env.example`, Git branching and deployment environments.
- [ ] Implement common layout, navigation, validation, errors, responsive design.
- [ ] Configure roles/permissions, security headers, logging, and test framework.
- [ ] Establish coding conventions and backup strategy.
**Exit criterion:** clean install from README and passing smoke tests.

### Phase 2 — Public landing page and CMS (2 weeks)
**Deliverables:** public website and draft/approve/publish workflow.
- [ ] Build Home, About, Programs, Events, News, Join, Contact, Privacy pages.
- [ ] Add accessible mobile layouts and image optimization.
- [ ] Build controlled content publishing and media permissions.
**Exit criterion:** guest can navigate and submit an inquiry; only authorized editors publish.

### Phase 3 — Registration, login, and member onboarding (2–3 weeks)
**Deliverables:** authentication, email verification, membership approval, member dashboard.
- [ ] Register/login/reset/logout, verification, throttling, MFA for privileged accounts.
- [ ] Membership review with decision reasons and notifications.
- [ ] Profile, consent, membership status, onboarding.
- [ ] Backend authorization and audit events.
**Exit criterion:** a guest can apply and become a member only after authorized approval.

### Phase 4 — System administration (2 weeks)
**Deliverables:** account management, permission assignments, audit viewer, operational dashboard.
- [ ] User CRUD/deactivation, role assignment with approval controls.
- [ ] Audit log filters/export with restricted access.
- [ ] Failed-login alerts, uptime/queue checks, backup status and restore test.
- [ ] Incident register and maintenance records.
**Exit criterion:** admin actions are attributable and security alerts are testable.

### Phase 5 — Officer and committee workspaces (2–3 weeks)
**Deliverables:** role-specific dashboards and governance records.
- [ ] Chair/Vice Chair approval queue and program overview.
- [ ] Secretary minutes, agendas, resolutions, membership records.
- [ ] Press/Public Relations editorial workflow and inquiry queue.
- [ ] Officer terms, committees, delegations.
**Exit criterion:** each officer sees only authorized records and actions.

### Phase 6 — Events, projects, and volunteering (3 weeks)
**Deliverables:** event management, registrations, QR attendance, tasks, volunteer hours.
- [ ] Event approval and publication, capacity and waitlist rules.
- [ ] QR check-in with replay protection and manual fallback.
- [ ] Project milestones, assignments, volunteer logs, outcome reports.
**Exit criterion:** event-to-attendance-to-impact workflow works end to end.

### Phase 7 — Finance and transparency (3 weeks)
**Deliverables:** controlled expense workflow, budget reporting, public summaries.
- [ ] Budgets, income/expenses, receipts, independent approvals.
- [ ] Ledger corrections, reconciliation, exports, monthly financial summaries.
- [ ] Privacy-safe public transparency page.
**Exit criterion:** self-approval is blocked and reports reconcile with ledger records.

### Phase 8 — Documents, certificates, and notifications (2 weeks)
**Deliverables:** private repository, certificates, email alerts, reminders.
- [ ] Scoped document permissions and versioning.
- [ ] Certificates with verifiable codes (do not expose private profile data).
- [ ] Scheduled reminders, notification preferences, delivery logs.
**Exit criterion:** files cannot be downloaded without authorization.

### Phase 9 — Optional FastAPI integrations (2–3 weeks)
**Deliverables:** one justified Python-powered service, API contract, observability.
- [ ] Choose a real use case: document extraction, report summarization, or statistical analytics.
- [ ] Define authenticated service-to-service endpoints and strict input validation.
- [ ] Keep authorization and official data writes in Laravel.
- [ ] Add retries, timeouts, error handling, rate limits, and service tests.
**Exit criterion:** service can fail safely without breaking registration or finance.

### Phase 10 — QA, privacy, deployment, and launch (2–3 weeks)
**Deliverables:** tested production release, operating manual, admin training, rollback plan.
- [ ] Unit, feature, integration, authorization, accessibility, and mobile tests.
- [ ] Test IDOR, CSRF, XSS, file uploads, role escalation, and approval bypasses.
- [ ] Run backup restore drill, dependency scan, and incident simulation.
- [ ] Deploy with HTTPS, production secrets, queue workers, cron, monitoring.
- [ ] Train officers and conduct user acceptance testing.
**Exit criterion:** documented sign-off, no critical security defects, successful recovery drill.

### Phase 11 — Post-launch improvements (ongoing)
- [ ] Gather user feedback and review metrics monthly.
- [ ] Add partnerships, chapter/branch support, surveys, member skill matching.
- [ ] Improve reporting, accessibility, and performance based on evidence.
- [ ] Review security patches, permissions, and data retention regularly.

**Estimated timeline:** Approximately 20–27 weeks for the full sequential scope, excluding significant staffing/content delays. A smaller MVP (Phases 0–4 plus basic events) can be targeted first; estimates are planning assumptions, not commitments.

## 11. MVP priorities

**Must-have for first launch:** public website, register/login, verified membership approval, member dashboard, officer accounts, RBAC, CMS approvals, basic events, audit logs, backups, privacy notice, secure deployment.

**Next release:** committees, volunteer tracking, governance documents, communications, finance approvals, transparency reports.

**Later:** FastAPI analytics, certificate verification, partnership portal, chapter management, advanced reporting, integrations.

## 12. Screen inventory

| ID | Screen | Audience |
|---|---|---|
| P-01 | Public Home / Landing | Guest |
| P-02 | About / Mission / Leadership | Guest |
| P-03 | Programs / Events / News | Guest |
| P-04 | Join / Contact / Privacy | Guest |
| A-01 | Register / Verify Email / Login | All |
| A-02 | Membership Application Status | Applicant |
| M-01 | Member Dashboard / Profile | Member |
| M-02 | Event Registration / QR Pass | Member |
| M-03 | Volunteer Tasks / Hours | Member |
| O-01 | Chairperson Dashboard / Approvals | Chair |
| O-02 | Vice Chairperson Workspace | Vice Chair |
| O-03 | Secretary Records / Minutes | Secretary |
| O-04 | Treasurer Ledger / Budgets | Treasurer |
| O-05 | Press Editorial / Releases | Press |
| O-06 | PR Inquiries / Partnerships | PR |
| S-01 | System Dashboard / Health | System Admin |
| S-02 | Users / Roles / Permissions | System Admin |
| S-03 | Audit Logs / Security Incidents | System Admin |
| S-04 | Backups / Settings / Integrations | System Admin |
| G-01 | Projects / Events Management | Authorized officers |
| G-02 | Reports / Transparency | Authorized roles / public summary |

## 13. Non-functional requirements

- **Security:** least privilege, MFA for sensitive roles, encrypted transit, encrypted backups, no public database access.
- **Privacy:** Philippine Data Privacy Act (RA 10173) considerations, purpose limitation, data minimization, appropriate notices, access/correction requests, retention and deletion rules.
- **Accessibility:** target WCAG 2.2 AA where feasible; keyboard support, readable contrast, form errors.
- **Reliability:** automated backups, health monitoring, restore drills, incident response.
- **Performance:** paginated lists, indexed queries, background jobs for heavy tasks.
- **Maintainability:** modular services, migrations, tests, API documentation, code reviews.
- **Non-partisanship:** editorial guidelines, conflict-of-interest declarations, neutral public communications, no candidate/party promotion through the platform.

## 14. Suggested future features

1. **Chapter/municipality management:** chapters with scoped coordinators and local projects.
2. **Partnership portal:** partner applications, memoranda, contact history, approval records.
3. **Member skills matching:** opt-in skills and volunteer opportunity matching.
4. **Community needs intake:** residents submit non-sensitive community project suggestions.
5. **Surveys and consultations:** transparent, consent-based feedback without political profiling.
6. **Impact dashboard:** outcomes and volunteer hours with evidence and review status.
7. **Conflict-of-interest register:** disclosures and recusal workflow for approvals.
8. **Safeguarding and incident reporting:** confidential reports, limited reviewers, escalation policy.
9. **Offline attendance import:** CSV or local capture for low-connectivity events with deduplication.
10. **Multilingual content:** English and Filipino language options.

## 15. Example acceptance tests

- Guest cannot access `/admin` or another member's private profile.
- System admin cannot approve their own finance expense.
- Treasurer cannot both submit and independently approve the same payment.
- Unverified registrant cannot become an active member automatically.
- Member cannot alter recorded volunteer hours after officer approval without a logged correction.
- Public content cannot publish without authorized approval.
- Audit log records sensitive changes without storing passwords or tokens.
- Backup restoration produces a usable database in a separate test environment.
- Deactivated officer immediately loses officer privileges, including active sessions where feasible.
- FastAPI outage does not interrupt login or membership processing.

## 16. Decisions to confirm before coding

1. Are members limited to a particular age range, area, or residency status?
2. Who approves membership: Secretary, Chairperson, Membership Officer, or a committee?
3. Are Press Relations and Public Relations separate positions?
4. Does the organization need chapters/municipal branches from day one?
5. Who can approve expenses, and at what monetary thresholds?
6. Which documents, announcements, and financial reports are public?
7. Can guests register for public events without becoming members?
8. Will the organization collect donations online, or only record offline funds?
9. Is FastAPI needed for a confirmed feature, or should it be deferred?
10. Who is responsible for privacy, data retention, and safeguarding reports?

---

**Recommended build order:** Requirements -> Laravel foundation -> Public website -> Authentication/membership -> System administration -> Officer workflows -> Events/volunteering -> Finance -> Documents/notifications -> Optional FastAPI -> Testing/launch.
