# Changelog

## v1.0.0 — Initial GitHub release

### Core CRM
- Client management with full profile, fact find, goals, risk profiling, compliance
- Lead pipeline with conversion workflow
- Review calendar with scheduling, checklists, overdue tracking
- Household management with linked client records
- Policy and investment tracking
- Cash flow modelling with 2008-style stress test (real historical returns)
- Fee management and fee ledger
- Task management (per-client and practice-wide)
- Communications log
- Document management
- Audit trail

### Reporting & export
- CSV export for clients, policies, reviews, fees, tasks
- Per-client PDF report
- Cash flow PDF with scenarios
- Full JSON database backup (admin only)

### Client portal
- Separate client login (email + 4-digit PIN)
- Client view: dashboard, policies, reviews, fees, documents, goals, personal details, fact find
- Client-submitted changes routed to adviser approval inbox
- Adviser "view as client" preview on client profile

### Access control
- Admin and adviser roles
- Per-adviser data filtering
- Audit trail of all actions

### Infrastructure
- Single HTML file, no dependencies
- localStorage persistence
- Dark mode support
