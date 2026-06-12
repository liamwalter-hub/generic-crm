# Nexus IFA — Practice Management CRM

A single-file browser-based CRM for independent financial advisers. Runs entirely in the browser with no backend required — data is stored in `localStorage`.

## Quick start

1. Open `index.html` in any modern browser
2. Log in with any adviser account (default PIN: `1234`)
3. Data is saved automatically in your browser's local storage

For a shared/hosted version, see [SETUP.md](SETUP.md).

## Features

- **Client management** — profiles, fact find, goals, risk profiling, compliance
- **Review management** — calendar, scheduling, checklists, overdue tracking
- **Policies & investments** — portfolio tracking, provider management
- **Cash flow modelling** — projections, stress testing (2008-style), household mode
- **Fees & ledger** — ongoing charges, fee ledger, exports
- **Tasks** — per-client and practice-wide task management
- **Households** — linked client records, combined projections
- **Client portal** — client-facing login with approval workflow
- **Pending approvals** — adviser inbox for client-submitted changes
- **Export** — CSV exports for clients, policies, reviews, fees, tasks
- **Audit trail** — full activity log

## Hosting on GitHub Pages

1. Push this repository to GitHub
2. Go to **Settings → Pages**
3. Set source to `main` branch, `/ (root)`
4. Your CRM will be live at `https://[username].github.io/[repo-name]`

> **Note:** GitHub Pages serves the file publicly. The app requires a login, but the source code is visible. Do not commit real client data or production PINs to the repository.

## Technology

Plain HTML, CSS and JavaScript. No frameworks, no dependencies, no build step. Everything is in `index.html`.

Data is stored in `localStorage` under the key `nexus_crm_v1`. This is per-browser and per-device — for shared multi-user access with persistent data, a backend database is required (see [SETUP.md](SETUP.md)).

## Licence

Private — not for redistribution.
