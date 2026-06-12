# Setup & configuration guide

This file documents everything that needs to be updated before using this CRM with real client data.

---

## 1. Required before first use

### Adviser names and login credentials

Open `index.html` and find the `USERS` array (search for `const USERS=`). Update with your real adviser names and set secure PINs:

```js
const USERS=[
  {id:'admin',      name:'Administrator', role:'admin',    pin:'CHANGE_ME'},
  {id:'adviser1',   name:'Your Name',     role:'adviser',  adviser:'Your Name',  pin:'CHANGE_ME'},
  {id:'adviser2',   name:'Adviser Two',   role:'adviser',  adviser:'Adviser Two',pin:'CHANGE_ME'},
];
```

Also update the `ADV` array (search for `const ADV=`) and the adviser filter dropdown in the HTML (search for `All advisers`).

### Firm name

Search for `Nexus IFA` and `Nexus Independent Financial Advisers` and replace with your firm name throughout.

### FCA number

Search for `[000000]` and replace with your actual FCA registration number.

### Firm address

Search for `[Practice address]` and replace with your registered address. This appears in printed client reports.

---

## 2. Recommended before going live with real data

### Change the storage key

To avoid conflicts if you've previously used the demo version, update the storage key in `index.html`:

```js
const SK='nexus_crm_v1';  // change to e.g. 'your_firm_crm_v1'
```

### Clear demo data

On first load with the new storage key, the app seeds 100 demo clients. To remove these:

1. Log in as Administrator
2. Go to **Export → Full database backup** and download a copy
3. Open browser DevTools → Application → Local Storage
4. Delete the `nexus_crm_v1` key
5. Reload — the app will seed fresh demo data
6. Or: modify `buildDb()` to start with empty arrays if you want a clean slate

### Review default PINs

All demo accounts use `1234`. Change every PIN before sharing access.

---

## 3. GitHub Pages deployment

The CRM works as a static file on GitHub Pages with no configuration.

**Important:** The HTML source code is publicly visible on GitHub. This is fine for the code, but means:
- Never commit files containing real client data
- Never commit your production PINs to the repo
- Consider making the repository **private** (requires GitHub Pro for Pages on private repos, or use Netlify/Cloudflare Pages which support private repos on free tiers)

**Recommended approach:** Keep the repo private and deploy via Cloudflare Pages (free, supports private repos).

---

## 4. Moving to a real database (future)

Currently all data lives in `localStorage` — per-browser, per-device. For shared multi-user access:

The two functions to replace are:
- `sDb()` — currently `localStorage.setItem(SK, JSON.stringify(db))`
- `lDb()` — currently `localStorage.getItem(SK)` then `JSON.parse()`

Replace these with API calls to a backend. Recommended options:
- **Supabase** (free tier, EU hosting available, Postgres)
- **PocketBase** (self-hosted, single binary)
- **Cloudflare D1** (serverless SQLite, very cheap)

The entire database is already one JSON object (`db`), so the migration is straightforward.

---

## 5. HappyScribe / AI transcript integration (planned)

When ready to integrate review transcript processing:

1. HappyScribe API endpoint: `https://www.happyscribe.com/api/v1/`
2. Transcripts can be fetched as JSON after completion
3. Send transcript text to Claude API with client context
4. Parse returned JSON into pending approvals (`db.pa`) for adviser review

The pending approvals workflow already exists — transcript-derived updates would flow through the same adviser approval screen as client portal submissions.

---

## 6. Browser notifications (planned)

To enable browser notifications for overdue reviews, pending approvals, and upcoming tasks:

```js
// Request permission on login
Notification.requestPermission();

// Send notification
new Notification('Nexus IFA', { body: 'You have 3 overdue reviews', icon: '/icon.png' });
```

Add calls into `updB()` where badge counts are calculated. Notifications only fire while the browser tab is open — for background notifications, a service worker and push API are required (needs HTTPS hosting).
